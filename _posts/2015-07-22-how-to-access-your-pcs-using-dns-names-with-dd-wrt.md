---
id: 915
title: How to access your PCs using DNS names with DD-WRT
date: 2015-07-22T02:53:06+00:00
author: wiseindy
layout: post
guid: http://wiseindy.com/?p=915
permalink: /it/how-to-access-your-pcs-using-dns-names-with-dd-wrt/
image: /wp-content/uploads/2015/07/how-to-access-your-pcs-using-dns-names-with-dd-wrt.jpg
categories:
  - Guides
  - IT
  - Networking
tags:
  - cmd
  - connection-specific DNS Suffix
  - dd-wrt
  - ddwrt
  - dhcp
  - dns
  - DNS resolution
  - dns suffix
  - domain
  - fqdn
  - hostname
  - ip
  - ip address
  - ipconfig
  - ipv4
  - ipv6
  - LAN domain
  - local
  - networking
  - release
  - renew
  - resolve
---
Pretty sure you must've noticed it

Most of us must've faced this problem, especially in our home networks. You must've noticed that when you're trying reach one machine from another using it's IP address, it works perfectly. However when you try to reach it using its hostname/DNS name like <code>wiseindy-pc</code>, it is extremely unreliable and rarely works.

<!--more-->

And if you've got the opportunity to work with corporate networks, you'll notice that this is not the case there. Communicating with machines via hostnames is as reliable as communicating via their individual IP addresses in a corporate environment.

Is it because companies have "bigger" and "better" hardware? And your home router sucks? Well, not really.
<h3>So, what IS the problem?</h3>
The problem is pretty straightforward actually. The devices on your network don't really know whom they should ask to resolve the hostname.

To translate a hostname to an IP address, the machine will need to know the "Fully Qualified Domain Name" or "FQDN" in short.

FQDN for a particular machine looks something like this: <code>hostname.dnz.zone</code> / <code>hostname.domain.com</code> / <code>hostname.domain.whatever</code>. A home environment (in almost all cases) is not a domain environment, i.e., the computers are not connected to a central domain unlike most companies. This  <code>domain.com</code> part in the FQDN called the "DNS Zone".

Let us assume that machine we are trying to connect is called <code>wiseindy-pc</code> and its IP address is <code>192.168.1.120</code>.

So on your home network, you have the <code>hostname</code> part, e.g. <code>wiseindy-pc</code>. But the machine has no idea about the <code>domain.com</code> part (since there IS no domain). Hence it has no way to convert <code>wiseindy-pc</code> to <code>192.168.1.120</code>.

Ok, so that explains why it doesn't work. But, in some rare cases (probably when the planets align) it actually does work, even on a network without a DNS zone. How is that possible?

Well, as it turns out, if a DNS zone is not defined for the network, your device tries ANOTHER way to figure out the IP address before abandoning the resolving process altogether. It tries to find out the hostname -&gt; IP address mapping on its own using a technique called "DNS broadcast". The problem with this is that not all machines/devices are configured to answer to this DNS broadcasr, or are actually configured to deliberately not answer such a request.

To fix this you need to configure a "DNS Suffix" for your network.
<h3>So how do I get this "DNS Suffix" thing?</h3>
If you open up command prompt and type <code>ipconfig</code>, you'll notice that the <strong>Connection-specific DNS Suffix</strong> is blank.

<a href="http://wiseindy.com/wp-content/uploads/2015/07/how-to-access-your-pcs-using-dns-names-with-dd-wrt-03.png"><img class="alignnone size-full wp-image-926" src="http://wiseindy.com/wp-content/uploads/2015/07/how-to-access-your-pcs-using-dns-names-with-dd-wrt-03.png" alt="How to access your PCs using DNS names with DD-WRT" width="540" height="94" /></a>

It's extremely simple to do this on a router which has the <a href="https://en.wikipedia.org/wiki/DD-WRT" target="_blank">DD-WRT</a> firmware installed. In case you don't have a router with DD-WRT, <a href="http://wiseindy.com/it/installing-dd-wrt-on-tp-link-tl-wdr3600-n600/" target="_blank">here's my guide</a> to install DD-WRT on one.

Open up a browser and navigate to your router homepage. After logging in, click on the <strong>Services</strong> tab.

<a href="http://wiseindy.com/wp-content/uploads/2015/07/how-to-access-your-pcs-using-dns-names-with-dd-wrt-001.png"><img class="alignnone size-full wp-image-924" src="http://wiseindy.com/wp-content/uploads/2015/07/how-to-access-your-pcs-using-dns-names-with-dd-wrt-001.png" alt="How to access your PCs using DNS names with DD-WRT" width="921" height="482" /></a>
<ul>
	<li>For “Used Domain” select “LAN &amp; WLAN” from the dropdown.</li>
	<li>For "LAN domain", pick whatever you like. It should be of the form <code>domain.com</code> or <code>sub.domain.com</code>, etc.
<ul>
	<li>For my home network, I picked  <code>wise.lan</code></li>
	<li>You can pick whatever you want.
<ul>
	<li>The one exception to that rule, is that if you use <code>.local</code>, while your windows machines will probably do just fine, your Linux machines will adhere to the mDNS (<a href="http://tools.ietf.org/html/draft-lynn-dnsext-site-mdns-01" target="_blank">Multicast DNS</a>) standard and will again ignore the DNS server.</li>
</ul>
</li>
</ul>
</li>
</ul>
<img class="alignnone size-full wp-image-925" src="http://wiseindy.com/wp-content/uploads/2015/07/how-to-access-your-pcs-using-dns-names-with-dd-wrt-02.png" alt="How to access your PCs using DNS names with DD-WRT" width="916" height="307" />

Scroll down, click <strong>Save</strong>. Then hit <strong>Apply</strong>.

To get the new settings on your PC, you'll need to refresh the IP configuration. Open up a Command Prompt window and type the following commands one after the other:

<code>ipconfig /release</code>
<code>ipconfig /renew</code>

<a href="http://wiseindy.com/wp-content/uploads/2015/07/how-to-access-your-pcs-using-dns-names-with-dd-wrt-05.png"><img class="alignnone size-full wp-image-927" src="http://wiseindy.com/wp-content/uploads/2015/07/how-to-access-your-pcs-using-dns-names-with-dd-wrt-05.png" alt="How to access your PCs using DNS names with DD-WRT" width="305" height="39" /></a>

<a href="http://wiseindy.com/wp-content/uploads/2015/07/how-to-access-your-pcs-using-dns-names-with-dd-wrt-06.png"><img class="alignnone size-full wp-image-928" src="http://wiseindy.com/wp-content/uploads/2015/07/how-to-access-your-pcs-using-dns-names-with-dd-wrt-06.png" alt="How to access your PCs using DNS names with DD-WRT" width="289" height="39" /></a>

Type <code>ipconfig</code>. You should see that a DNS suffix is now defined.

<a href="http://wiseindy.com/wp-content/uploads/2015/07/how-to-access-your-pcs-using-dns-names-with-dd-wrt-4.png"><img class="alignnone size-full wp-image-929" src="http://wiseindy.com/wp-content/uploads/2015/07/how-to-access-your-pcs-using-dns-names-with-dd-wrt-4.png" alt="How to access your PCs using DNS names with DD-WRT" width="540" height="94" /></a>

Now, since you have a DNS suffix, the resulting FQDN for this machine will be <code>wiseindy-pc.wise.lan</code>. The hostname can now be resolved to its IP address easily.

Repeat this <code>ipconfig /release</code> and <code>ipconfig /renew</code> on at least one more machine and try pinging <code>wiseindy-pc</code> using only the hostname. You should see that the client has automatically understood that the full name of the device you’re pinging is <code>wiseindy-pc.wise.lan</code> (<code>hostname.dns.zone</code>), and was able to translate (resolve) the FQDN to an IP.

(header image source: <a href="http://www.goodfon.su/wallpaper/dns-d-n-s-oskolki-tuman.html" target="_blank">goodfon.su</a>)