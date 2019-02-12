---
id: 886
title: Installing DD-WRT on TP-Link TL-WDR3600 N600
date: 2015-07-16T04:46:04+00:00
author: wiseindy
comments: true
layout: single
guid: https://wiseindy.com/?p=886
enclosure:
  - |
    https://wiseindy.com/wp-content/uploads/2015/07/installing-dd-wrt-on-tp-link-tl-wdr3600-n600-05.webm
    281109
    video/webm
    
dsq_thread_id:
  - "5585733411"
header:
  image: /wp-content/uploads/2015/07/installing-dd-wrt-on-tp-link-tl-wdr3600-n600-header.jpg
  teaser: /assets/images/featured/featured-installddwrt.jpg
redirect_from: "/it/installing-dd-wrt-on-tp-link-tl-wdr3600-n600/"
categories:
  - Networking
tags:
  - custom firmware
  - dd-wrt
  - ddwrt
  - firmware
  - guide
  - IT
  - n600
  - network
  - networking
  - router
  - tlwdr3600
  - tp-link
  - wdr3600
  - wl-wdr3600
  - Guides
---
<a target="_blank" href="https://en.wikipedia.org/wiki/DD-WRT" target="_blank">DD-WRT</a> is a third-party firmware project that is designed to replace the original firmware for commercial wireless routers and wireless access points. It is a Linux-based firmware and is a solid alternative to the original firmware in your router.

<!--more-->
<h3>Why would I do this?</h3>
The <a target="_blank" href="http://www.tp-link.com/en/products/details/cat-9_TL-WDR3600.html" target="_blank">TP-Link TL-WDR3600 N600</a> is a pretty good budget Gigabit router for homes. I've been using it for a few years now and I like almost everything about this except the fact that there's no inherent VPN or QoS functionality. Not a deal breaker, but it would be great to extend the capabilities of the device for no additonal cost. There's also the fact that I'm a networking enthusiast and this is a good opportunity to learn.
<h3>What you need:</h3>
<ul>
	<li>A <a target="_blank" href="http://www.tp-link.com/en/products/details/cat-9_TL-WDR3600.html" target="_blank">TP-Link TL-WDR3600 N600</a> router.
<ul>
	<li>You could use any other DD-WRT supported routers as well. Check out the <a target="_blank" href="http://www.dd-wrt.com/site/support/router-database" target="_blank">DD-WRT website</a> to see if your router is supported.</li>
</ul>
</li>
	<li>A PC connected to your router with an ethernet cable (duh).</li>
</ul>
<h3>Step 1:</h3>
Head to the <a target="_blank" href="http://www.dd-wrt.com/site/support/router-database" target="_blank">DD-WRT website</a> and search for your router. Mine is <a target="_blank" href="http://www.tp-link.com/en/products/details/cat-9_TL-WDR3600.html" target="_blank">TP-Link TL-WDR3600</a>, hence I pick that one from the search results.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/07/installing-dd-wrt-on-tp-link-tl-wdr3600-n600-01.png"><img class="alignnone size-full wp-image-887" src="https://wiseindy.com/wp-content/uploads/2015/07/installing-dd-wrt-on-tp-link-tl-wdr3600-n600-01.png" alt="DD-WRT database search" /></a>

If your router is supported by DD-WRT, you will see a bunch of firmwares which you can download.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/07/installing-dd-wrt-on-tp-link-tl-wdr3600-n600-02.png"><img class="alignnone wp-image-889 size-full" src="https://wiseindy.com/wp-content/uploads/2015/07/installing-dd-wrt-on-tp-link-tl-wdr3600-n600-02.png" alt="Installing DD-WRT on TP-Link TL-WDR3600 N600" /></a>

In this case, we see 3 firmwares.
<ul>
	<li><code>factory-to-ddwrt.bin</code>
<ul>
	<li>Use this if you're flashing from <strong>stock</strong> firmware to <strong>DD-WRT</strong> firmware. This is what we will be doing.</li>
</ul>
</li>
	<li><code>wdr3600v1_webrevert.rar</code>
<ul>
	<li>Use this if you already have <strong>DD-WRT</strong> installed and you want to go back to <strong>stock</strong> firmware.</li>
</ul>
</li>
	<li><code>tl-wdr3600-webflash.bin</code>
<ul>
	<li>Use this if you currently have <strong>DD-WRT</strong> installed and you want to upgrade to a newer version of <strong>DD-WRT</strong>.</li>
</ul>
</li>
</ul>
<h3>Step 2:</h3>
<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/07/installing-dd-wrt-on-tp-link-tl-wdr3600-n600-003.png"><img class="alignnone size-full wp-image-895" src="https://wiseindy.com/wp-content/uploads/2015/07/installing-dd-wrt-on-tp-link-tl-wdr3600-n600-003.png" alt="Installing DD-WRT on TP-Link TL-WDR3600 N600" /></a>

Once the <code>factory-to-ddwrt.bin</code> file is downloaded, head to your router's web interface and log in.

Open up your browser and type your router's IP address. By default, it should be <code>192.168.1.1</code> or <code>192.168.0.1</code>. If your network uses a different private IP range, then enter the appropriate router address.

[video width="842" height="444" webm="https://wiseindy.com/wp-content/uploads/2015/07/installing-dd-wrt-on-tp-link-tl-wdr3600-n600-05.webm" loop="true" autoplay="true" preload="auto"][/video]
<h3>Step 3:</h3>
From the left sidebar, navigate to <strong>System Tools</strong> &gt; <strong>Firmware Upgrade</strong>

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/07/installing-dd-wrt-on-tp-link-tl-wdr3600-n600-08.png"><img class="alignnone size-full wp-image-904" src="https://wiseindy.com/wp-content/uploads/2015/07/installing-dd-wrt-on-tp-link-tl-wdr3600-n600-08.png" alt="Installing DD-WRT on TP-Link TL-WDR3600 N600" /></a>

Select <strong>Browse...</strong> and pick the <code>factory-to-ddwrt.bin</code> file downloaded in the previous steps. Then click <strong>Upgrade</strong>.

The firmware upgrade process will take about 2-3 minutes. Hang tight.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/07/installing-dd-wrt-on-tp-link-tl-wdr3600-n600-09.png"><img class="alignnone size-full wp-image-905" src="https://wiseindy.com/wp-content/uploads/2015/07/installing-dd-wrt-on-tp-link-tl-wdr3600-n600-09.png" alt="Installing DD-WRT on TP-Link TL-WDR3600 N600" /></a>

Once the upgrade is done, you should see another progress bar like this informing you that the router is restarting.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/07/installing-dd-wrt-on-tp-link-tl-wdr3600-n600-10.png"><img class="alignnone size-full wp-image-906" src="https://wiseindy.com/wp-content/uploads/2015/07/installing-dd-wrt-on-tp-link-tl-wdr3600-n600-10.png" alt="Installing DD-WRT on TP-Link TL-WDR3600 N600" /></a>

<div class="row">
  <div class="col-12">
    {% include adsense-post-content.html %}
  </div>
</div>

<h3>Step 4:</h3>
If all goes well, which it should and will, you should see the new DD-WRT router page.
<blockquote>One thing to note here. If your router was configured to use a different IP range, for example <code>10.15.15.x</code>, then you'll need to manually go to <code>192.168.1.1</code> to see this page.

This is the new firmware's default IP range. You'll need to reconfigure it if you want to work on a different range.</blockquote>
On this page, enter a <strong>username</strong> and <strong>password</strong> and click <strong>Change Password</strong>.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/07/installing-dd-wrt-on-tp-link-tl-wdr3600-n600-11.png"><img class="alignnone size-full wp-image-907" src="https://wiseindy.com/wp-content/uploads/2015/07/installing-dd-wrt-on-tp-link-tl-wdr3600-n600-11.png" alt="Installing DD-WRT on TP-Link TL-WDR3600 N600" /></a>

Now you will be inside the router configuration page.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/07/installing-dd-wrt-on-tp-link-tl-wdr3600-n600-12.png"><img class="alignnone size-full wp-image-909" src="https://wiseindy.com/wp-content/uploads/2015/07/installing-dd-wrt-on-tp-link-tl-wdr3600-n600-12.png" alt="Installing DD-WRT on TP-Link TL-WDR3600 N600" /></a>

Your router just gained a whole lot of features that are available only in high end ones. For free. And in less than 10 minutes. That isn't so bad, is it? Have fun configuring!

Now that you've got DD-WRT powered up, see how you can configure DD-WRT to <a target="_blank" href="https://wiseindy.com/it/how-to-access-your-pcs-using-dns-names-with-dd-wrt/" target="_blank">access computers using hostnames on your home network</a>

(header image source: <a target="_blank" href="http://www.freeimageslive.co.uk/image/view/3929/_original" target="_blank">freeimageslive.co.uk</a>)
