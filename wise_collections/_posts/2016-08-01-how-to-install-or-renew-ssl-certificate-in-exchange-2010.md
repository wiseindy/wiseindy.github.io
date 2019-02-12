---
id: 1025
title: How to install or renew SSL certificate in Exchange 2010
date: 2016-08-01T08:00:08+00:00
author: wiseindy
comments: true
layout: single
guid: https://wiseindy.com/?p=1025
dsq_thread_id:
  - "5585733524"
header:
  image: /wp-content/uploads/2015/08/how-to-install-ssl-certificate-in-exchange-2010.jpg
  teaser: /assets/images/featured/featured-sslexchange.jpg
redirect_from: "/it/how-to-install-or-renew-ssl-certificate-in-exchange-2010/"
categories:
  - Windows
tags:
  - certificate
  - csr
  - digicert
  - exchange
  - exchange 2010
  - exchange 2013
  - exchange management shell
  - godaddy
  - microsoft
  - microsoft exchange
  - request
  - signing
  - ssl
  - trusted
  - Guides
---
You will need to create and assign a new SSL certificate if you're putting up a new Exchange server into production or renewing it for an existing server. The steps are fairly straightforward, however it may seem daunting and completely foreign for new users who aren't familiar with certificates.

<!--more-->

This guide will show you how to create a CSR (Certificate Signing Request) using your Exchange server and subsequently generating a new SSL cert and installing it.

Here's a brief overview of what we will be doing in this guide:
<ol>
 	<li>Create a certificate signing request (CSR) in Exchange.</li>
 	<li>Buy a new certificate from one of many SSL providers (GoDaddy in this case - process should be similar for other providers).</li>
 	<li>Use the CSR to create a new certificate on GoDaddy and download it</li>
 	<li>Install this in our Exchange server.</li>
</ol>
<h3>What you need:</h3>
<ul>
 	<li>Microsoft Exchange Server
<ul>
 	<li>In this guide, we are using Microsoft Exchange 2010.</li>
</ul>
</li>
 	<li>A commercial Certificate Authority such as <a target="_blank" href="https://www.digicert.com/" target="_blank">DigiCert</a>, <a target="_blank" href="https://www.godaddy.com/" target="_blank">GoDaddy</a>, etc.
<ul>
 	<li>In this guide, we are using Godaddy.</li>
</ul>
</li>
</ul>
<h3>Step 1:</h3>
The first step is to generate a Certificate Signing Request. This is a requisite for generating your SSL certificate.

Open up your <strong>Exchange Management Console</strong>

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/08/how-to-install-ssl-certificate-in-exchange-2010-01.png"><img class="alignnone size-full wp-image-1028" src="https://wiseindy.com/wp-content/uploads/2015/08/how-to-install-ssl-certificate-in-exchange-2010-01.png" alt="how-to-install-ssl-certificate-in-exchange-2010-01" /></a>
<h3>Step 2:</h3>
Navigate to <strong>Server Configuration &gt; Select your server</strong> (from the Server Configuration list)<strong> &gt; Exchange Certificates</strong> tab and click on <strong>New Exchange Certificate</strong>.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/08/how-to-install-ssl-certificate-in-exchange-2010-02.png"><img class="alignnone size-full wp-image-1029" src="https://wiseindy.com/wp-content/uploads/2015/08/how-to-install-ssl-certificate-in-exchange-2010-02.png" alt="how-to-install-ssl-certificate-in-exchange-2010-02" /></a>
<h3>Step 3:</h3>
In the <strong>New Exchange Certificate</strong> Wizard, enter a name for your certificate. It can be anything you want. Click <strong>Next</strong>.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2016/08/how-to-install-ssl-certificate-in-exchange-2010-03_01.png"><img class="alignnone size-full wp-image-1228" src="https://wiseindy.com/wp-content/uploads/2016/08/how-to-install-ssl-certificate-in-exchange-2010-03_01.png" alt="how-to-install-ssl-certificate-in-exchange-2010-03_01" /></a>
<h3>Step 3:</h3>
If you want to apply the certificate to <strong>all</strong> your sub domains, check <strong>Enable wildcard certificate</strong>. In my case, I wish to apply this certificate to 2 subdomains (not all), so I leave it unchecked.

<img class="alignnone size-full wp-image-1032" src="https://wiseindy.com/wp-content/uploads/2015/08/how-to-install-ssl-certificate-in-exchange-2010-04-alt-0.png" alt="how-to-install-ssl-certificate-in-exchange-2010-04-alt-0" />
<h3>Step 4:</h3>
On the next page, you'll need to provide your Exchange Server configuration. Select whatever is applicable for <strong>each section</strong>.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/08/how-to-install-ssl-certificate-in-exchange-2010-04-alt-1.png"><img class="alignnone size-full wp-image-1033" src="https://wiseindy.com/wp-content/uploads/2015/08/how-to-install-ssl-certificate-in-exchange-2010-04-alt-1.png" alt="how-to-install-ssl-certificate-in-exchange-2010-04-alt-1" /></a>

In my case, OWA (Outlook Web App/Access) is being accessed from the web. This is why I enable the second option "Outlook Web App is on the Internet" in the below image. The URL should be automatically populated.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/08/how-to-install-ssl-certificate-in-exchange-2010-04-alt-2.png"><img class="alignnone size-full wp-image-1034" src="https://wiseindy.com/wp-content/uploads/2015/08/how-to-install-ssl-certificate-in-exchange-2010-04-alt-2.png" alt="how-to-install-ssl-certificate-in-exchange-2010-04-alt-2" /></a>

Go through each of the sections below and verify if everything you need is selected. In my case, I didn't need to change anything other than the Outlook Web App part in the above step. I left everything else as it is.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/08/how-to-install-ssl-certificate-in-exchange-2010-04-alt-3.png"><img class="alignnone size-full wp-image-1035" src="https://wiseindy.com/wp-content/uploads/2015/08/how-to-install-ssl-certificate-in-exchange-2010-04-alt-3.png" alt="how-to-install-ssl-certificate-in-exchange-2010-04-alt-3" /></a>

Some more pics to help you cross-verify your info.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/08/how-to-install-ssl-certificate-in-exchange-2010-04-alt-4.png"><img class="alignnone size-full wp-image-1036" src="https://wiseindy.com/wp-content/uploads/2015/08/how-to-install-ssl-certificate-in-exchange-2010-04-alt-4.png" alt="how-to-install-ssl-certificate-in-exchange-2010-04-alt-4" /></a>

If you use POP/IMAP, check the appropriate check boxes or leave them unchecked (as in my case since I don't use it).

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/08/how-to-install-ssl-certificate-in-exchange-2010-04-alt-5.png"><img class="alignnone size-full wp-image-1037" src="https://wiseindy.com/wp-content/uploads/2015/08/how-to-install-ssl-certificate-in-exchange-2010-04-alt-5.png" alt="how-to-install-ssl-certificate-in-exchange-2010-04-alt-5" /></a>

Click Next.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/08/how-to-install-ssl-certificate-in-exchange-2010-04-alt-6.png"><img class="alignnone size-full wp-image-1038" src="https://wiseindy.com/wp-content/uploads/2015/08/how-to-install-ssl-certificate-in-exchange-2010-04-alt-6.png" alt="how-to-install-ssl-certificate-in-exchange-2010-04-alt-6" /></a>
<h3>Step 5:</h3>
On this page, enter the details of your organization. Everything should be self-explanatory. At the bottom it asks you to specify the location of the <strong>Certificate Request File Path</strong> also known as a <strong>Certificate Signing Request</strong> or <strong>CSR</strong> in short.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/08/how-to-install-ssl-certificate-in-exchange-2010-05.png"><img class="alignnone size-full wp-image-1039" src="https://wiseindy.com/wp-content/uploads/2015/08/how-to-install-ssl-certificate-in-exchange-2010-05.png" alt="how-to-install-ssl-certificate-in-exchange-2010-05" /></a>

Specify the location and click <strong>Save</strong>.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/08/how-to-install-ssl-certificate-in-exchange-2010-06.png"><img class="alignnone size-full wp-image-1040" src="https://wiseindy.com/wp-content/uploads/2015/08/how-to-install-ssl-certificate-in-exchange-2010-06.png" alt="how-to-install-ssl-certificate-in-exchange-2010-06" /></a>

Verify the information and click <strong>New</strong>.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/08/how-to-install-ssl-certificate-in-exchange-2010-07.png"><img class="alignnone size-full wp-image-1041" src="https://wiseindy.com/wp-content/uploads/2015/08/how-to-install-ssl-certificate-in-exchange-2010-07.png" alt="how-to-install-ssl-certificate-in-exchange-2010-07" /></a>

<div class="row">
  <div class="col-12">
    {% include adsense-post-content.html %}
  </div>
</div>

<h3>Step 6:</h3>
If all goes well, which it should, you will find that your CSR is generated and saved it in the location you specified. It's basically a text file with a <code>.req</code> extension. We will need this file in a while.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/08/how-to-install-ssl-certificate-in-exchange-2010-08.png"><img class="alignnone size-full wp-image-1042" src="https://wiseindy.com/wp-content/uploads/2015/08/how-to-install-ssl-certificate-in-exchange-2010-08.png" alt="how-to-install-ssl-certificate-in-exchange-2010-08" /></a> <a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/08/how-to-install-ssl-certificate-in-exchange-2010-09.png"><img class="alignnone size-full wp-image-1043" src="https://wiseindy.com/wp-content/uploads/2015/08/how-to-install-ssl-certificate-in-exchange-2010-09.png" alt="how-to-install-ssl-certificate-in-exchange-2010-09" /></a>
<h3>Step 7:</h3>
Log in to your SSL provider and buy an SSL certificate if you haven't bought one already.

Make sure you buy a <strong>Unified Communications Certificate</strong> <strong>(UCC)</strong> (also known as a <strong>Multiple Domain SSL</strong> or <strong>SAN</strong> certificate). A <strong>UCC/SAN</strong> certificate will allow you to secure multiple domains. You need this for Microsoft Exchange. More information here: <a target="_blank" href="https://www.godaddy.com/help/what-is-a-multiple-domain-ucc-ssl-certificate-3908">https://www.godaddy.com/help/what-is-a-multiple-domain-ucc-ssl-certificate-3908</a>

In this tutorial, I'm using GoDaddy, but the steps should be more or less the same for other providers.
<h3>Step 8:</h3>
After you buy your SSL certificate, you'll have to provide it your CSR that was generated in <strong>Step 6</strong>.

In my case, I'm <em>renewing</em> my certificate instead of purchasing a new one, so some screens may be different for you. If you're renewing your certificate, you'll have to <strong>re-key</strong> your certificate. Again, that means you have to provide your <strong>CSR</strong> from step 6.

Login to your SSL provider. Open your CSR (.req) file with notepad. Copy everything and paste it wherever your SSL provider asks you to.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2016/08/how-to-install-ssl-certificate-in-exchange-2010-18.png"><img class="alignnone size-full wp-image-1212" src="https://wiseindy.com/wp-content/uploads/2016/08/how-to-install-ssl-certificate-in-exchange-2010-18.png" alt="how-to-install-ssl-certificate-in-exchange-2010-18" /></a>
<h3>Step 9:</h3>
Once you provide your CSR, you'll have to wait for a bit till your domain and other details are verified. You may even need to prove your domain ownership. In case you have to, then your SSL provider will give you the steps to do so.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2016/08/how-to-install-ssl-certificate-in-exchange-2010-10.png"><img class="alignnone size-full wp-image-1211" src="https://wiseindy.com/wp-content/uploads/2016/08/how-to-install-ssl-certificate-in-exchange-2010-10.png" alt="how-to-install-ssl-certificate-in-exchange-2010-10" /></a>
<h3>Step 10:</h3>
Once your certificate is ready, click the <strong>Download</strong> button.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2016/08/how-to-install-ssl-certificate-in-exchange-2010-11_1.png"><img class="alignnone size-full wp-image-1214" src="https://wiseindy.com/wp-content/uploads/2016/08/how-to-install-ssl-certificate-in-exchange-2010-11_1.png" alt="how-to-install-ssl-certificate-in-exchange-2010-11_1" /></a>

From the server type drop down, select <strong>Exchange</strong> and click <strong>Download File</strong>. It will be a zip with two files. Extract it and copy this over to your Exchange server.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2016/08/how-to-install-ssl-certificate-in-exchange-2010-12.png"><img class="alignnone size-full wp-image-1215" src="https://wiseindy.com/wp-content/uploads/2016/08/how-to-install-ssl-certificate-in-exchange-2010-12.png" alt="how-to-install-ssl-certificate-in-exchange-2010-12" /></a>
<h3>Step 11:</h3>
Go to your Exchange server. Right-click your certificate in Exchange Management Console and select <strong>Complete Pending Request...</strong>

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2016/08/how-to-install-ssl-certificate-in-exchange-2010-19_0.png"><img class="alignnone size-full wp-image-1223" src="https://wiseindy.com/wp-content/uploads/2016/08/how-to-install-ssl-certificate-in-exchange-2010-19_0.png" alt="how-to-install-ssl-certificate-in-exchange-2010-19_0" /></a>
<h3>Step 12:</h3>
Click the <strong>Browse</strong> button in the window that pops up.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2016/08/how-to-install-ssl-certificate-in-exchange-2010-14.png"><img class="alignnone size-full wp-image-1218" src="https://wiseindy.com/wp-content/uploads/2016/08/how-to-install-ssl-certificate-in-exchange-2010-14.png" alt="how-to-install-ssl-certificate-in-exchange-2010-14" /></a>

In the Browse window, select <strong>All Files(*.*)</strong> and then choose your certificate file that you received from your SSL provider (GoDaddy).

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2016/08/how-to-install-ssl-certificate-in-exchange-2010-15.png"><img class="alignnone size-full wp-image-1219" src="https://wiseindy.com/wp-content/uploads/2016/08/how-to-install-ssl-certificate-in-exchange-2010-15.png" alt="how-to-install-ssl-certificate-in-exchange-2010-15" /></a>

Click <strong>Complete</strong>.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2016/08/how-to-install-ssl-certificate-in-exchange-2010-16.png"><img class="alignnone size-full wp-image-1220" src="https://wiseindy.com/wp-content/uploads/2016/08/how-to-install-ssl-certificate-in-exchange-2010-16.png" alt="how-to-install-ssl-certificate-in-exchange-2010-16" /></a>

If everything goes well, you'll see the following screen. Click <strong>Finish.</strong>

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2016/08/how-to-install-ssl-certificate-in-exchange-2010-17.png"><img class="alignnone size-full wp-image-1221" src="https://wiseindy.com/wp-content/uploads/2016/08/how-to-install-ssl-certificate-in-exchange-2010-17.png" alt="how-to-install-ssl-certificate-in-exchange-2010-17" /></a>
<h3>Step 13:</h3>
The new Exchange certificate should have a little blue tick on the icon now. The only thing remaining now is to assign Exchange services to this certificate. That's easily done. Right click the certificate and choose <strong>Assign Services to Certificate...</strong>

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2016/08/how-to-install-ssl-certificate-in-exchange-2010-19_2.png"><img class="alignnone size-full wp-image-1224" src="https://wiseindy.com/wp-content/uploads/2016/08/how-to-install-ssl-certificate-in-exchange-2010-19_2.png" alt="how-to-install-ssl-certificate-in-exchange-2010-19_2" /></a>

Step 14:

In the window that pops up, select your server and click <strong>Next</strong>.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2016/08/how-to-install-ssl-certificate-in-exchange-2010-20.png"><img class="alignnone size-full wp-image-1225" src="https://wiseindy.com/wp-content/uploads/2016/08/how-to-install-ssl-certificate-in-exchange-2010-20.png" alt="how-to-install-ssl-certificate-in-exchange-2010-20" /></a>

Select all appropriate services for this certificate. Click <strong>Next</strong>.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2016/08/how-to-install-ssl-certificate-in-exchange-2010-21.png"><img class="alignnone size-full wp-image-1226" src="https://wiseindy.com/wp-content/uploads/2016/08/how-to-install-ssl-certificate-in-exchange-2010-21.png" alt="how-to-install-ssl-certificate-in-exchange-2010-21" /></a>

If you have some services already assigned to a different certificate, Exchange will ask you to confirm if you want to overwrite it with the new one. In my case, I do want to replace it, so I click <strong>Yes</strong>.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2016/08/how-to-install-ssl-certificate-in-exchange-2010-22.png"><img class="alignnone size-full wp-image-1227" src="https://wiseindy.com/wp-content/uploads/2016/08/how-to-install-ssl-certificate-in-exchange-2010-22.png" alt="how-to-install-ssl-certificate-in-exchange-2010-22" /></a>

Guess what? That's it! You've successfully installed a new SSL certificate for your Microsoft Exchange server.

&nbsp;

(header image source: <a target="_blank" href="http://www.animalhi.com/Insects/spiders/rust_locker_room_spider_webs_lock_2560x1440_wallpaper_12182" target="_blank">animalhi.com</a>)
