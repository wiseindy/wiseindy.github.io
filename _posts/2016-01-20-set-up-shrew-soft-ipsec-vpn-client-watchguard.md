---
id: 1060
title: How to set up Shrew Soft IPSec VPN Client for WatchGuard
date: 2016-01-20T06:36:14+00:00
author: wiseindy
comments: true
layout: post
guid: http://wiseindy.com/?p=1060
permalink: /it/set-up-shrew-soft-ipsec-vpn-client-watchguard/
header:
  image: /wp-content/uploads/2016/01/header-set-up-shrew-soft-ipsec-vpn-client-watchguard.jps_.jpg
  teaser: /images/featured/featured-shrew.jpg
categories:
  - Firewall
  - IT
  - Networking
tags:
  - firebox
  - firewall
  - ipsec
  - m300
  - network
  - networking
  - shrew
  - shrew soft
  - vpn
  - watchguard
  - xtm
---
This guide will show you how to enable Mobile VPN with IPSec for WatchGuard Firebox M300. It's a pretty straightfoward process, however it took me quite a while to figure out initially. Hope this guide makes it easier for you.

<!--more-->

It will also show you how to install and configure the <a target="_blank" href="https://www.shrew.net/download/vpn" target="_blank">Shrew Soft IPSec VPN Client</a>. In my opinion, you are better off using this client than the <a target="_blank" href="http://www.watchguard.com/help/docs/wsm/xtm_11/en-US/index.html#en-US/mvpn/client/mvpn-ipsec_client_about_c.html%3FTocPath%3DMobile%2520VPN%2520with%2520IPSec%7CAbout%2520the%2520IPSec%2520Mobile%2520VPN%25C2%25A0Client%7C_____0" target="_blank">WatchGuard IPSec Mobile VPN Monitor</a>. Old versions of this WatchGuard IPSec Mobile VPN Monitor were free, but they do not work on Windows 10. The new version of the IPSec client needs a paid subscription license. Unless you want to go this route, I would suggest using the Shrew Soft IPSec VPN Client. It's free and you can <a target="_blank" href="https://www.shrew.net/download/vpn" target="_blank">download</a> it from their <a target="_blank" href="https://www.shrew.net/download/vpn" target="_blank">official website</a>.

<strong>Note:</strong> While this guide was created for Firebox M300, it should work with other WatchGuard XTM devices as well.
<h3>What do you need:</h3>
<ul>
	<li>An environment where a WatchGuard firewall is installed and running.</li>
	<li>Administrative access to the firewall (of course).</li>
</ul>
So let's being shall we?
<h3>Step 1</h3>
Fire up your browser and navigate to the web interface of your firewall? If your firewall's IP address is <code>192.168.1.1</code>, then type <code>https://192.168.1.1:8080</code> in the URL bar.

After logging in, go to <strong>VPN</strong> &gt; <strong>Mobile VPN with IPSec</strong>.

Click on <strong>Add</strong> to add a new group.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-01.png" rel="attachment wp-att-1087"><img class="alignnone size-full wp-image-1087" src="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-01.png" alt="set-up-shrew-soft-ipsec-vpn-client-watchguard-01" /></a>
<h3>Step 2:</h3>
Select the <strong>General</strong> tab. Type in a <strong>Name</strong> and select Authentication Server as <strong>Firebox-DB</strong>. You can also set it to authenticate it with your domain, but for this tutorial we will use the firewall as the authentication server.

Next, enter the <strong>passphrase</strong> and enter your firewall's external IP address. This is the IP address that you use to connect to your firewall from the Internet.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-02.png" rel="attachment wp-att-1062"><img class="alignnone size-full wp-image-1062" src="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-02.png" alt="set-up-shrew-soft-ipsec-vpn-client-watchguard-02" /></a>
<h3>Step 3:</h3>
Select the <strong>IPSec Tunnel</strong> tab. Make the following changes as shown in the image below.
<ul>
	<li>Select <strong>Use the passphrase of the end user profile as the pre-shared key</strong>.</li>
	<li>Under <strong>Phase 1</strong><strong> Settings</strong>, select <strong>Authentication</strong> as <strong>SHA1</strong> and <strong>Encryption</strong> as <strong>3DES</strong>.</li>
	<li>Under <strong>Phase 2</strong><strong> Settings</strong>, seelct <strong>PFS</strong> and choose <strong>Diffie-Hellman Group 1</strong>.</li>
</ul>
<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-03.png" rel="attachment wp-att-1063"><img class="alignnone size-full wp-image-1063" src="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-03.png" alt="set-up-shrew-soft-ipsec-vpn-client-watchguard-03" /></a>
<h3>Step 4:</h3>
Select the <strong>Resources</strong> tab. Here under <strong>Allowed Resources</strong> you can specify which IP addresses are allowed to connect through the tunnel. Click <strong>Add</strong> and type in an IP range.

Next, you'll have to specify the <strong>Virtual IP Address Pool</strong>. Whenever a device connects to your tunnel, it will be assigned an IP address from this pool.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-04.png" rel="attachment wp-att-1064"><img class="alignnone size-full wp-image-1064" src="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-04.png" alt="set-up-shrew-soft-ipsec-vpn-client-watchguard-04" /></a>

<div class="row">
  <div class="col-12">
    {% include adsense-post-content.html %}
  </div>
</div>

<h3>Step 5:</h3>
Finally, go the <strong>Advanced</strong> tab and set the <strong>Connect mode</strong> to <strong>Manual</strong> and <strong>Inactivity timeout</strong> to <strong>0 seconds</strong>.

Click <strong>Save</strong>.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-05.png" rel="attachment wp-att-1065"><img class="alignnone size-full wp-image-1065" src="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-05.png" alt="set-up-shrew-soft-ipsec-vpn-client-watchguard-05" /></a>
<h3>Step 6:</h3>
The next step is to create a user which will connect to the tunnel.

In your firewall web interface, navigate to <strong>Authentication</strong> &gt; <strong>Servers</strong>.

Select <strong>Firebox</strong>.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-06.png" rel="attachment wp-att-1066"><img class="alignnone size-full wp-image-1066" src="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-06.png" alt="set-up-shrew-soft-ipsec-vpn-client-watchguard-06" /></a>
<h3>Step 7:</h3>
Under <strong>Firebox Users</strong>, click <strong>Add</strong> to create a new user.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-07.png" rel="attachment wp-att-1067"><img class="alignnone size-full wp-image-1067" src="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-07.png" alt="set-up-shrew-soft-ipsec-vpn-client-watchguard-07" /></a>
<h3>Step 8:</h3>
This part is pretty straight forward. Enter the <strong>Name</strong>, <strong>Description</strong>, <strong>Passphrase </strong>and<strong> timeout</strong> values.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-08.png" rel="attachment wp-att-1068"><img class="alignnone size-full wp-image-1068" src="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-08.png" alt="set-up-shrew-soft-ipsec-vpn-client-watchguard-08" /></a>

Under <strong>Firebox Authentication Groups</strong>, select the <strong>Group</strong> we created previously. In our case, it was <strong>WISEINDY</strong>, so we check that one.

Click <strong>OK</strong>.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-09.png" rel="attachment wp-att-1069"><img class="alignnone size-full wp-image-1069" src="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-09.png" alt="set-up-shrew-soft-ipsec-vpn-client-watchguard-09" /></a>
<h3>Step 9:</h3>
Now, navigate back to <strong>VPN</strong> &gt; <strong>Mobile VPN with IPSec</strong> in the firewall web interface.

Here you can download the configuration settings for your preferred IPSec VPN Client. I prefer the free <a target="_blank" href="https://www.shrew.net/download/vpn" target="_blank">Shrew Soft IPSec VPN Client</a> (click to download the client).

From the <strong>Client</strong> dropdown box, select <strong>Shrew Soft VPN</strong> and click <strong>Generate</strong>. It will generate a <code>.vpn</code> file. Save this on your PC.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-10.png" rel="attachment wp-att-1070"><img class="alignnone size-full wp-image-1070" src="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-10.png" alt="set-up-shrew-soft-ipsec-vpn-client-watchguard-10" /></a>
<h3>Step 10:</h3>
Go ahead and install the Shrew Soft VPN Client on your PC. Once installed, double click the <strong>VPN Access Manager</strong> icon on your desktop to launch it.

Select <strong>File</strong> &gt;<strong> Import</strong>.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-11.png" rel="attachment wp-att-1071"><img class="alignnone size-full wp-image-1071" src="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-11.png" alt="set-up-shrew-soft-ipsec-vpn-client-watchguard-11" /></a>

Choose the <code>.vpn</code> file that was downloaded in the previous step. Click <strong>Open</strong>.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-12.png" rel="attachment wp-att-1072"><img class="alignnone size-full wp-image-1072" src="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-12.png" alt="set-up-shrew-soft-ipsec-vpn-client-watchguard-12" /></a>
<h3>Step 11:</h3>
A new connection will be created from the imported settings. Select this connection and click <strong>Connect.</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-13.png" rel="attachment wp-att-1073"><img class="alignnone size-full wp-image-1073" src="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-13.png" alt="set-up-shrew-soft-ipsec-vpn-client-watchguard-13" /></a>

When you click <strong>Connect</strong>, a window will pop up asking you to input credentials to connect to the tunnel.

Enter the <strong>Username</strong> and <strong>Password</strong> that you used to create a user in <strong>Step 8</strong>.

Click <strong>Connect</strong>.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-14.png" rel="attachment wp-att-1074"><img class="alignnone size-full wp-image-1074" src="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-14.png" alt="set-up-shrew-soft-ipsec-vpn-client-watchguard-14" /></a>

If the connection is successful, you'll see a <strong>tunnel enabled</strong> message in the window.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-15.png" rel="attachment wp-att-1075"><img class="alignnone size-full wp-image-1075" src="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-15.png" alt="set-up-shrew-soft-ipsec-vpn-client-watchguard-15" /></a>

That's all. You have sucessfully set up and configured IPSec VPN for your WatchGuard XTM device.
<h3>Additional information:</h3>
In case someone needs it, here are my configuration settings that were imported into the Shrew Soft VPN client. You don't need to change anything here. The correct settings should automatically be configured when this file was generated by your firewall. I've only put up this screenshots in case someone is facing any issues and would like to double-check or compare his settings.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-16.png" rel="attachment wp-att-1076"><img class="alignnone size-full wp-image-1076" src="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-16.png" alt="set-up-shrew-soft-ipsec-vpn-client-watchguard-16" /></a> <a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-17.png" rel="attachment wp-att-1077"><img class="alignnone size-full wp-image-1077" src="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-17.png" alt="set-up-shrew-soft-ipsec-vpn-client-watchguard-17" /></a> <a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-18.png" rel="attachment wp-att-1078"><img class="alignnone size-full wp-image-1078" src="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-18.png" alt="set-up-shrew-soft-ipsec-vpn-client-watchguard-18" /></a> <a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-19.png" rel="attachment wp-att-1079"><img class="alignnone size-full wp-image-1079" src="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-19.png" alt="set-up-shrew-soft-ipsec-vpn-client-watchguard-19" /></a> <a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-20.png" rel="attachment wp-att-1080"><img class="alignnone size-full wp-image-1080" src="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-20.png" alt="set-up-shrew-soft-ipsec-vpn-client-watchguard-20" /></a> <a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-21.png" rel="attachment wp-att-1081"><img class="alignnone size-full wp-image-1081" src="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-21.png" alt="set-up-shrew-soft-ipsec-vpn-client-watchguard-21" /></a> <a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-22.png" rel="attachment wp-att-1082"><img class="alignnone size-full wp-image-1082" src="http://wiseindy.com/wp-content/uploads/2016/01/set-up-shrew-soft-ipsec-vpn-client-watchguard-22.png" alt="set-up-shrew-soft-ipsec-vpn-client-watchguard-22" /></a>

(header image source: <a target="_blank" href="https://www.sciencenews.org/sites/default/files/main/articles/note_shrew_001.jpg" target="_blank">sciencenews.org</a>)
