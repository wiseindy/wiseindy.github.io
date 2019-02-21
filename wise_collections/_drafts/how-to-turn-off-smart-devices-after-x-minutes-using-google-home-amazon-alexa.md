---
title: How to turn off smart devices after X minutes using Google Home, Amazon Alexa?
date: 2019-02-18T12:00:00+00:00
author: wiseindy
comments: true
layout: single
header:
  image: /assets/images/featured/featured-googlehome.jpg
  teaser: /assets/images/featured/featured-googlehome.jpg
categories:
  - Linux
tags:
  - google
  - google assistant
  - google home
  - guide
  - linux
  - amazon
  - amazon alexa
  - siri
  - automation
  - home automation
  - IoT
  - IFTTT
  - guides
---

Did you ever wish your Google Home or Amazon Alexa could turn off/on the fan, heater, lights or any other device in your home after, say, 30 minutes?

Google Home has a sleep timer for music, but not for other smart devices. Turns out, with a little bit of programming, you can set up a system where your home assistant will switch a device off/on after a set period of time.

**This guide will also work with the Google Assistant in your smartphone.** You don't *need* to have a home assistant device.

<!--more-->

{: .notice}
Please note that some of the links on this page are affiliate links to services that I personally use and have validated them before recommending to you. **At no additional cost to you**, I will earn a commission if you click through and make a purchase.

# What you need

* A linux web server with shell access and PHP support. [Don't have a server?](#dont-have-a-server)
  > You can use Python or any other language, however, this guide uses PHP
* A website domain pointing to this web server
* An [IFTTT](https://ifttt.com){:target="_blank"} account
* A Google Home / Google Home Mini / Amazon Alexa / Smartphone with Google Assistant

{: .notice--info}
**Just a heads up!** The requirements may seem a bit overwhelming especially if you are new to programming or Linux. However, do not let that discourage you. It is an opportunity to learn.<br><br>
The best way to learn something is to undertake a project or task that covers technologies you do not yet know. This way, you learn "while on the job". In my opinion and personal experience, you gain a deeper understanding while tinkering with stuff and trying to get it working rather than following rigid instructions.

## Don't have a server?

If you need a Linux server, you can quickly sign up on [DigitalOcean](https://m.do.co/c/6944f7f84907){:target="_blank"} and fire up a test server. [DigitalOcean](https://m.do.co/c/6944f7f84907){:target="_blank"} is a great platform that helps you quickly and cheaply deploy servers in the cloud. I use their VMs to host most of my sites.

[Create a DigitalOcean account and receive $100 in credit](https://m.do.co/c/6944f7f84907){:target="_blank"}

<a href="https://m.do.co/c/6944f7f84907" class="btn btn--info btn--x-large" target="_blank">Create a Linux VM on DigitalOcean</a>

# The Automation Logic

We are going to utilize [IFTTT](https://ifttt.com){:target="_blank"} to link Google Assistant, the smart device and our web server. Here is a brief overview how this is going to work.

* Google Assistant receives a command from us which goes like *"Hey Google, turn off the bedroom lights after 30 minutes."*
* [IFTTT](https://ifttt.com){:target="_blank"} processes this string and retrieves the variable "30" from the string.
* [IFTTT](https://ifttt.com){:target="_blank"} then passes this variable to a PHP script on our web server via a POST request.
* The PHP script saves the current timestamp in a file (*CURRENT_TIME*). Then, it adds "30 minutes" to the current time and saves the resulting timestamp in a different file (*FUTURE_TIME*).
* The PHP script also triggers an applet in [IFTTT](https://ifttt.com){:target="_blank"} that turns on the lights.
* The Linux server has a cron job running every minute that checks to see if *CURRENT_TIME* > *FUTURE_TIME*. If yes, then the script makes a POST request to [IFTTT](https://ifttt.com){:target="_blank"} which triggers an applet to turn the lights off. It also removes the *CURRENT_TIME* and *FUTURE_TIME* files.

{: .notice--warning}
**Note**: There could be a better way of achieving the same result. My code may not be efficient, but it gets the job done. If you have a better approach, please feel free to let me know in the comments. My scripts were meant to be "quick fixes" written on a lazy weekend rather than being production-ready :)

# Part 1

## Installation and configuration of OpenVPN server

### Step 1.1:

First, update your package lists and then install the `openvpn` and `easy-rsa` package.

```shell
sudo apt-get update
sudo apt-get install openvpn easy-rsa
```

### Step 1.2:

From now onwards, all the steps below have to be run as `root`. So, go ahead and login as root.

```shell
su
```

### Step 1.3:

Lets extract the sample VPN server configuration file to this location: `/etc/openvpn`

```shell
gunzip -c /usr/share/doc/openvpn/examples/sample-config-files/server.conf.gz > /etc/openvpn/server.conf
```

_Note: `gunzip` is a utility that uncompresses a `gzip` file. `gz` or `.Z` is the extension for `gzip` files._

### Step 1.4:

Still as root, open this file.

I prefer `vim` to open files on ubuntu. If you prefer `nano` instead, you can use that too.

```shell
vi /etc/openvpn/server.conf
```

### Step 1.5:

Now, we have to modify a few lines in this file.

Search for a section that looks like this

```shell
# Diffie hellman parameters.
# Generate your own with:
#   openssl dhparam -out dh1024.pem 1024
# Substitute 2048 for 1024 if you are using
# 2048 bit keys.
dh dh1024.pem
```

Change `dh1024.pem` to `dh2048.pem`. This doubles the RSA key length when we generate the server and client keys later in the guide.

### Step 1.6:

Find and uncomment the line below. To uncomment, simply remove the semicolon `;` in front of the line.

Before:

```shell
# If enabled, this directive will configure
# all clients to redirect their default
# network gateway through the VPN, causing
# all IP traffic such as web browsing and
# and DNS lookups to go through the VPN
# (The OpenVPN server machine may need to NAT
# or bridge the TUN/TAP interface to the internet
# in order for this to work properly).
;push "redirect-gateway def1 bypass-dhcp"
```

After:

```shell
# If enabled, this directive will configure
# all clients to redirect their default
# network gateway through the VPN, causing
# all IP traffic such as web browsing and
# and DNS lookups to go through the VPN
# (The OpenVPN server machine may need to NAT
# or bridge the TUN/TAP interface to the internet
# in order for this to work properly).
push "redirect-gateway def1 bypass-dhcp"
```

This makes sure that the OpenVPN server will pass the client device's web traffic to its destination.

### Step 1.7:

Still in the same file, find and uncomment the following two lines. To uncomment, simply remove the semicolon `;` in front of the two lines.

Before:

```shell
# Certain Windows-specific network settings
# can be pushed to clients, such as DNS
# or WINS server addresses.  CAVEAT:
# http://openvpn.net/faq.html#dhcpcaveats
# The addresses below refer to the public
# DNS servers provided by opendns.com.
;push "dhcp-option DNS 208.67.222.222"
;push "dhcp-option DNS 208.67.220.220"
```

After:

```shell
# Certain Windows-specific network settings
# can be pushed to clients, such as DNS
# or WINS server addresses.  CAVEAT:
# http://openvpn.net/faq.html#dhcpcaveats
# The addresses below refer to the public
# DNS servers provided by opendns.com.
push "dhcp-option DNS 208.67.222.222"
push "dhcp-option DNS 208.67.220.220"
```

The two IP addresses above belong to OpenDNS and will be used to lookup DNS request where possible. You can use any DNS service of your choice. Here we have used OpenDNS, and hence their IP addresses are listed in the file.

### Step 1.8:

This is the last thing to change in the file. Look for this section below and uncomment the two lines by removing the semicolons `;`

Before:

```shell
# You can uncomment this out on
# non-Windows systems.
;user nobody
;group nogroup
```

After:

```shell
# You can uncomment this out on
# non-Windows systems.
user nobody
group nogroup
```

Save and close the file.

### Step 1.9:

#### Packet Forwarding

We need to now enable an option that allows the server to forward traffic from client devices out to the Internet. If this is not done, the client traffic will stop at the server. To enable packet forwarding, run this command.

```shell
echo 1 > /proc/sys/net/ipv4/ip_forward
```

This setting is not yet permanent and will not survive a reboot. To make it permanent, we need to edit the `sysctl.conf` file.

```shell
vi /etc/sysctl.conf
```

In this file, find and uncomment the following line. To uncomment, remove the `#` in front of the line.

Before:

```shell
# Uncomment the next line to enable packet forwarding for IPv4
#net.ipv4.ip_forward=1
```

After:

```shell
# Uncomment the next line to enable packet forwarding for IPv4
net.ipv4.ip_forward=1
```

Save the file and exit.

### Step 1.10:

#### Set up firewall rules in the Uncomplicated Firewall (ufw)

We will be using OpenVPN over UDP, so the firewall must allow UDP traffic over port **1194**.

Still as root, enter the following command:

```shell
ufw allow 1194/udp
```

Open the firewall's (ufw) primary configuration file. We habe to set the firewall forwarding policy.

```shell
vi /etc/default/ufw
```

Search for the string `DEFAULT_FORWARD_POLICY="DROP"` in this file. Change the `DROP` to `ACCEPT`.

Before:

```shell
DEFAULT_FORWARD_POLICY="DROP"
```

After:

```shell
DEFAULT_FORWARD_POLICY="ACCEPT"
```

Save the file and exit.

### Step 1.11:

There's one more step before we can move on to the next section.

We need to add add additional firewall rules.

Open this file

```shell
vi /etc/ufw/before.rules
```

We will be adding rules for NAT (network address translation) and IP masquerading of connected devices.

Modify this file to look like this.

Before:

```shell
#
# rules.before
#
# Rules that should be run before the ufw command line added rules. Custom
# rules should be added to one of these chains:
#   ufw-before-input
#   ufw-before-output
#   ufw-before-forward
#

# Don't delete these required lines, otherwise there will be errors
*filter
```

After:

```shell
#
# rules.before
#
# Rules that should be run before the ufw command line added rules. Custom
# rules should be added to one of these chains:
#   ufw-before-input
#   ufw-before-output
#   ufw-before-forward
#

#################################
# START OPENVPN RULES
# NAT table rules
*nat
:POSTROUTING ACCEPT [0:0] 
# Allow traffic from OpenVPN client to eth0
-A POSTROUTING -s 10.8.0.0/8 -o eth0 -j MASQUERADE
COMMIT
# END OPENVPN RULES
#################################

# Don't delete these required lines, otherwise there will be errors
*filter
```

Once you've added the section, enable the firewall (ufw).

```shell
ufw enable
```

<div class="row">
  <div class="col-12">
    {% include adsense-post-content.html %}
  </div>
</div>

# Part 2

## Creating a Certificate Authority and Server-Side Certificate and Key

Okay, so we have installed and configured OpenVPN and the firewall settings in the above section. Now, let's go ahead and create certificates and keys for our new OpenVPN server.

#### Creating a certificate authority (CA)

### Step 2.1:

Make sure you're still logged in as root.

Copy the Easy-RSA generation scripts to `/etc/openvpn`

```shell
cp -r /usr/share/easy-rsa/ /etc/openvpn
```

### Step 2.2:

Now, create a directory to store our keys.

```shell
mkdir /etc/openvpn/easy-rsa/keys
```

### Step 2.3:

Now we will edit the `vars` file and add in some default values for a person or a business. The information that is entered into this file will be copied to the certificates and keys and will help us in identifying them later.

You can put in any values you like. Here is an example.

```shell
export KEY_COUNTRY="CA"
export KEY_PROVINCE="ON"
export KEY_CITY="Toronto"
export KEY_ORG="Wiseindy"
export KEY_EMAIL="wiseindy@example.com"
export KEY_OU="WiseOU"
```

There is one more line to edit in this file before you close it. We need to set the default filename for the server key and certificate. In this tutorial we've used the name `server` for simplicity. If you're using a different name, please make sure you replace `server` with your custom name in the commands.

```shell
export KEY_NAME="server"
```

Save and close the file.

### Step 2.4:

The next step is to generate the Diffie-Hellman parameters.

```shell
openssl dhparam -out /etc/openvpn/dh2048.pem 2048
```

### Step 2.5:

Now, navigate to the `easy-rsa` directory.

```shell
cd /etc/openvpn/easy-rsa
```

### Step 2.6:

Once you're in the `easy-rsa` directory, run the following command to initialize the PKI (Public Key Infrastructure).

```shell
. ./vars
```

Note the `.` (dot) and ` ` (space) in front of `./vars`.

The above command will output the following:

```shell
NOTE: If you run ./clean-all, I will be doing a rm -rf on /etc/openvpn/easy-rsa/keys
```

You can ignore this warning message since we haven't yet generated anything.

### Step 2.7:

Let's clear the working directory of any example keys and start fresh.

```shell
./clean-all
```

### Step 2.8:

We are all set to create our certificate authority now. When you run the following command, it will ask you to confirm the values you had entered in the `vars` file in step 2.6. Hit enter to confirm the values.

```shell
./build-ca
```

#### Generate a Certificate and Key for the Server

### Step 2.9:

Well, we now have a certificate authority (CA) set up. Let's build our server key now.

```shell
./build-key-server server
```

_Note: Note that I've used the name **server** in the above command. This is because I've set `export KEY_NAME="server"` in the `vars` file (step 2.6). If you've used a different name, make sure you modify the command accordingly_

When you run this command, you'll see a similar output as the previous step. You can hit enter to confirm them. However, this time you will see two additional prompts.

```shell
Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:
```

Both of the should be left blank. Hit Enter to continue.

When it prompts you to sign the certificate and commit, type `y` for both the prompts and hit enter.

```shell
Sign the certificate? [y/n]  y
1 out of 1 certificate requests certified, commit? [y/n]  y
```

Now you should see the following output. This means that all is good so far.

```shell
Write out database with 1 new entries
Data Base Updated
```

### Step 2.10

#### Move the Server Certificates and Keys

Well, we've now generated the server CA, keys and certificate. Let's copy these over to the correct location `/etc/openvpn/`.

```shell
cp /etc/openvpn/easy-rsa/keys/{server.crt,server.key,ca.crt} /etc/openvpn
```

### Step 2.11

Well, guess what? Our OpenVPN server is ready now. Let's start it.

```shell
service openvpn start
```

# Part 3

## Generate Certificates and Keys for your devices

In the previous section, we created the key and certificate for our server. We are going to do that for our devices now.

We will build one for a client device called `myphone`. You can name your client device anything. Just make sure to substitute the name in the commands that follow.

### Step 3.1:

You should still be root and still working from this directory `/etc/openvpn/easy-rsa`.

```shell
./build-key myphone
```

Like in the previous steps, you'll be asked to confirm the Distinguised Name variables. Hit enter to accept the defaults.

### Step 3.2:

Now copy the sample client configuration file to the `easy-rsa/keys` directory. This file will be used as a template. We will be editing this template file for each of our devices.

```shell
cp /usr/share/doc/openvpn/examples/sample-config-files/client.conf /etc/openvpn/easy-rsa/keys/myphone.ovpn
```

You can repeat this section (steps 3.1 and 3.2) for each client device. Just make sure you use a different name for each of your devices (in this case we've used `myphone`)

# Part 4

## Create a Unified OpenVPN Profile for each of your devices

Now that you have created keys and certificates for your device `myphone`, let's create one unified `.ovpn` file which will contain all this information.

### Step 4.1:

From the `/etc/openvpn/easy-rsa` directory, copy the following files to your computer (the one you're reading this article on). We will be editing these in a text editor (Notepad, TextEdit, etc.).

```shell
myphone.crt
myphone.key
myphone.ovpn
ca.crt
```

### Step 4.2

Open the `myphone.ovpn` file in a text editor like Notepad (Windows) or TextEdit (macOS) or whatever you prefere, really.

Add your server's IP address to the this section in the beginning of the file. Replace `my-server-1` with your server's IP address.

Before:

```shell
# The hostname/IP and port of the server.
# You can have multiple remote entries
# to load balance between the servers.
remote my-server-1 1194
```

After:

```shell
# The hostname/IP and port of the server.
# You can have multiple remote entries
# to load balance between the servers.
remote 142.189.11.1 1194
```

### Step 4.3

In the same file, scroll down and uncomment this section (This doesn't apply to Windows, so you can skip it if you're going to use thie VPN profile on a Windows machine).

Before:

```shell
# Downgrade privileges after initialization (non-Windows only)
;user nobody
;group nogroup
```
  
After:

```shell
# Downgrade privileges after initialization (non-Windows only)
user nobody
group nogroup
```

### Step 4.4:

Scroll further down and this time you'll **comment** a few lines instead of uncommenting. We do this because we are directly including the `.crt` and `.key` files within this `.ovpn` file.

Before:

```shell
# SSL/TLS parms.
# . . .
ca ca.crt
cert client.crt
key client.key
```

After:

```shell
# SSL/TLS parms.
# . . .
#ca ca.crt
#cert client.crt
#key client.key
```

### Step 4.5:

At the end of the file, add this text to block outside DNS

```shell
# Prevent DNS leak
block-outside-dns
```

### Step 4.6:

Now, at the end of the file, we will be copying and pasting the contents of `ca.crt`, `myphone.crt`, and `myphone.key` files.

Open the `.crt` and `.key` files in a text editor and copy-paste the content as shown below

This is how we will be doing it.

```shell
<ca>
  (insert ca.crt here)
</ca>

<cert>
  (insert myphone.crt here)
</cert>

<key>
  (insert myphone.key here)
</key>
```

Once you're done copy-pasting the content, the end of your `.ovpn` file should look like this:

```shell
<ca>
-----BEGIN CERTIFICATE-----
. . .
-----END CERTIFICATE-----
</ca>
  
<cert>
Certificate:
. . .
-----END CERTIFICATE-----
. . .
-----END CERTIFICATE-----
</cert>
  
<key>
-----BEGIN PRIVATE KEY-----
. . .
-----END PRIVATE KEY-----
</key>
```

Save the changes and close the file.

### Step 4.7:

#### Windows
If you're using Windows, install the official [OpenVPN client from here](https://openvpn.net/index.php/open-source/downloads.html).
After installation, paste your `myphone.ovpn` file here `C:\Program Files\OpenVPN\config\`.

To connect to your VPN server, right-click the OpenVPN client in the taskbar and click **Connect**.

![Connect to OpenVPN](/assets/images/posts/2017-04-27-install-openvpn-ubuntu-1404-001.png "Connect to OpenVPN")

To verify if you're connected, go to [Google](https://google.com) and type `What is my IP`. If it returns the IP address of your OpenVPN server, all is well and your VPN is working as expected.

#### macOS
For macOS, install [Tunnelblick](https://tunnelblick.net/downloads.html) and import your `.ovpn` profile.
**Note:** If you get an error and Tunnelblick is unable to connect, remove the following text from your `.ovpn` profile.

```shell
# Prevent DNS leak
block-outside-dns
```

#### Android
For Android, download the [OpenVPN Connect app from the Google Play Store](https://play.google.com/store/apps/details?id=net.openvpn.openvpn&hl=en). Import your `.ovpn` profile and you're all set!

#### iOS
For iPhone and iPad, download the [OpenVPN Connect app from the Apple App Store](https://itunes.apple.com/us/app/openvpn-connect/id590379981?mt=8). Import your `.ovpn` profile and you're all set!

Guess what? You're done.

I recommened you create separate `.ovpn` files for each of your devices instead of using the same key & certificate for everything.

**To create `.ovpn` profiles for more devices, [repeat steps from part 3 onwards](#part-3).**

Photo by Ben Kolde on Unsplash

<a style="background-color:black;color:white;text-decoration:none;padding:4px 6px;font-family:-apple-system, BlinkMacSystemFont, &quot;San Francisco&quot;, &quot;Helvetica Neue&quot;, Helvetica, Ubuntu, Roboto, Noto, &quot;Segoe UI&quot;, Arial, sans-serif;font-size:12px;font-weight:bold;line-height:1.2;display:inline-block;border-radius:3px" href="https://unsplash.com/@benkolde?utm_medium=referral&amp;utm_campaign=photographer-credit&amp;utm_content=creditBadge" target="_blank" rel="noopener noreferrer" title="Download free do whatever you want high-resolution photos from Ben Kolde"><span style="display:inline-block;padding:2px 3px"><svg xmlns="http://www.w3.org/2000/svg" style="height:12px;width:auto;position:relative;vertical-align:middle;top:-2px;fill:white" viewBox="0 0 32 32"><title>unsplash-logo</title><path d="M10 9V0h12v9H10zm12 5h10v18H0V14h10v9h12v-9z"></path></svg></span><span style="display:inline-block;padding:2px 3px">Ben Kolde</span></a>