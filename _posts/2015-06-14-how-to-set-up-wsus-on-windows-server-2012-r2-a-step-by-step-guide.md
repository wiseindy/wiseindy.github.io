---
id: 381
title: 'How to set up WSUS on Windows Server 2012 R2 &#8211; A Step-by-Step Guide'
date: 2015-06-14T08:21:40+00:00
author: wiseindy
layout: post
guid: https://wiseindy.wordpress.com/?p=381
permalink: /it/how-to-set-up-wsus-on-windows-server-2012-r2-a-step-by-step-guide/
dsq_thread_id:
  - "5585733469"
image: /wp-content/uploads/2015/06/windows-server-update-services.jpg
categories:
  - Guides
  - IT
tags:
  - guide
  - server
  - windows
  - windows server 2012 r2
  - windows server update services
  - windows update for business
  - wsus
  - wub
---
Windows Server Update Services (WSUS) is a free patch management tool by Microsoft. It allows sysadmins to centrally push Microsoft product updates to computers that are running Windows on their network.

This guide will help you set up your very own WSUS server on Windows Server 2012 R2.

<!--more-->
<h3>Why WSUS?</h3>
How do Windows computers usually update? In a non-WSUS environment (generally all home environments), each PC independently connects to Microsoft Update to get its patches and MS product updates.

This may not be always preferred in a corporate environment. Instead of each workstation manually connecting to Microsoft Update, testing updates and then deploying updates using traditional methods, administrators can use WSUS to download updates centrally to an internal server. Once updates are authorised in WSUS, they’re also deployed internally and reporting tools keep administrators informed of patch progress. This is a very efficient way of working, allowing administrators full control of which updates are deployed to workstations.

In Windows Server 2012 and 2012 R2, WSUS is integrated with the operating system as a server role. In previous versions of Windows Server (2003, 2008, 2008 R2), you had to separately install WSUS 3.0.
<blockquote>Also, seems like Microsoft will be moving away from WSUS to an entirely new product called Windows Update for Business (WUB). <a target="_blank" href="http://blogs.windows.com/bloggingwindows/2015/05/04/announcing-windows-update-for-business/" target="_blank">You can read more about it here.</a></blockquote>
Ok, so now, let's see how we can set up WSUS on Windows Server 2012 R2
<h3>What you need:</h3>
<ol>
	<li>A machine with Windows Server 2012 R2 installed</li>
	<li>Internet connection</li>
	<li>20 minutes (not including download times)</li>
</ol>
I started with a fresh install of Windows Server 2012 R2 on a VM and connected it to my domain.
<h3>Step 1:</h3>
On your Windows Server 2012 R2 machine, launch <strong>Server Manager</strong> as shown below.

You can either launch it using the icon in the taskbar or you can click the <strong>Start</strong> button and just search for "server manager".

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_1.png"><img class="alignnone wp-image-382 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_1.png" alt="Click on the Server Manager icon on the taskbar to launch Server Manager" /></a>
<h3>Step 2:</h3>
Once <strong>Server Manager</strong> is open, select <strong>Add roles and features</strong>.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_2.png"><img class="alignnone wp-image-383 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_2.png" alt="Server Manager window" /></a>
<h3>Step 3:</h3>
In the <strong>Add Roles and Features Wizard</strong>, click next on the <strong>Before You Begin</strong> page. You can optionally select to <strong>Skip</strong> <strong>this page by default</strong> for the future.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_3.png"><img class="alignnone wp-image-542 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_3.png" alt="wsus_server_2012_wiseindy_3" /></a>
<h3>Step 4:</h3>
Select <strong>Role-based or feature-based installation</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_4.png"><img class="alignnone wp-image-543 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_4.png" alt="wsus_server_2012_wiseindy_4" /></a>
<h3>Step 5:</h3>
Select your server from the server pool. If you're not using Hyper-V, you will see only one server, i.e., your soon-to-be WSUS server.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_5.png"><img class="alignnone wp-image-544 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_5.png" alt="wsus_server_2012_wiseindy_5" /></a>
<h3>Step 6:</h3>
In the <strong>Server Roles</strong> list, scroll down and select <strong>Windows Server Update Services</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_6.png"><img class="alignnone wp-image-545 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_6.png" alt="wsus_server_2012_wiseindy_6" /></a>
<h3>Step 7:</h3>
A window will pop up showing you the features that are required for WSUS which will be enabled. Click <strong>Add Features</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_7.png"><img class="alignnone wp-image-546 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_7.png" alt="wsus_server_2012_wiseindy_7" /></a>
<h3>Step 8:</h3>
You will notice that <strong>IIS</strong> has been automatically selected. Leave everything as default and click <strong>Next</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_8.png"><img class="alignnone wp-image-547 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_8.png" alt="wsus_server_2012_wiseindy_8" /></a>
<h3>Step 9:</h3>
On the <strong>Features</strong> screen, leave the default selections and click <strong>Next</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_9.png"><img class="alignnone wp-image-548 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_9.png" alt="wsus_server_2012_wiseindy_9" /></a>

<div class="row">
  <div class="col-12">
    {% include adsense-post-content.html %}
  </div>
</div>

<h3>Step 10:</h3>
On the <strong>Web Server Role (IIS)</strong> page, click <strong>Next</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_10.png"><img class="alignnone wp-image-549 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_10.png" alt="wsus_server_2012_wiseindy_10" /></a>
<h3>Step 11:</h3>
Leave all selections as default on the <strong>Role Services </strong>page and click <strong>Next</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_11.png"><img class="alignnone wp-image-550 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_11.png" alt="wsus_server_2012_wiseindy_11" /></a>
<h3>Step 12:</h3>
Click <strong>Next</strong> on this screen

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_12.png"><img class="alignnone wp-image-551 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_12.png" alt="wsus_server_2012_wiseindy_12" /></a>
<h3>Step 13:</h3>
On the <strong>Role Services</strong> page, make sure <strong>WID Database</strong> and <strong>WSUS</strong> <strong>Services</strong> are selected (They should be selected by default). Click <strong>Next</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_13.png"><img class="alignnone wp-image-552 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_13.png" alt="wsus_server_2012_wiseindy_13" /></a>
<h3>Step 14:</h3>
This page will allow you to set the destination directory for the downloaded updates. Tick the <strong>checkbox</strong> for <strong>Store updates in the following location</strong>.

Enter the path here. It can either be a local or a remote path.
Keep in mind that WSUS will take up considerable amount of storage as time goes on. It is not unusual to find update folders of sizes greater than 100 GB.

Choose your destination accordingly.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_14.png"><img class="alignnone wp-image-553 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_14.png" alt="wsus_server_2012_wiseindy_14" /></a>
<h3>Step 15:</h3>
On the <strong>Confirmation</strong> screen, check the <strong>Restart the destination server automatically if required</strong> option if you wish to do so, otherwise you can leave it unchecked.

Click <strong>Install</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_15.png"><img class="alignnone wp-image-554 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_15.png" alt="wsus_server_2012_wiseindy_15" /></a>
<h3>Step 16:</h3>
Sit back and grab a coffee. This will take about 5-10 minutes.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_16.png"><img class="alignnone wp-image-555 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_16.png" alt="wsus_server_2012_wiseindy_16" /></a>
<h3>Step 17:</h3>
Once its installed, hit <b>Close</b>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_17.png"><img class="alignnone wp-image-556 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_17.png" alt="wsus_server_2012_wiseindy_17" /></a>
<h3>Step 18:</h3>
Search for <strong>WSUS</strong> or <strong>Windows Server Update Services</strong> and launch it

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_18.png"><img class="alignnone wp-image-557 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_18.png" alt="wsus_server_2012_wiseindy_18" /></a>
<h3>Step 19:</h3>
Since it's the first time you're opening it, it'll take a while to set up. Wait for it to complete and then hit <strong>Close</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_19.png"><img class="alignnone wp-image-558 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_19.png" alt="wsus_server_2012_wiseindy_19" /></a>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_20.png"><img class="alignnone wp-image-559 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_20.png" alt="wsus_server_2012_wiseindy_20" /></a>
<h3>Step 20:</h3>
You will now see a wizard that will walk you through a series of steps to configure your installation.

Before starting, make sure of the following:
<ul>
	<li>Confirm whether the PCs on your network can communicate with this server.</li>
	<li>Your WSUS server should be able to communicate with Microsoft Update (Make sure your firewall isn't blocking it)</li>
	<li>If your environment uses a proxy, make sure you have the proxy server credentials before continuing.</li>
</ul>
If all seems well, click <strong>Next</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_21.png"><img class="alignnone wp-image-560 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_21.png" alt="wsus_server_2012_wiseindy_21" /></a>
<h3>Step 21:</h3>
If you would like to join the <strong>Microsoft Update Improvement Program</strong>, check the box. Otherwise uncheck it. Click<strong> Next</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_22.png"><img class="alignnone wp-image-561 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_22.png" alt="wsus_server_2012_wiseindy_22" /></a>
<h3>Step 22:</h3>
If you want to synch updates directly from Microsoft Update (the most likely scenario in your case since you're reading this guide), enable the first option and click <strong>Next</strong>.

If you have already have a WSUS server in your environment and want your new WSUS to synch updates from that instead of Microsoft Update, enable the second option.
<ul>
	<li>Enter the server name and port number (For WSUS on Windows Servere 2012 R2, the default port is 8530)</li>
	<li>Enable/disable SSL based on your environment</li>
	<li>Decide whether it is going to be a replica server or not and click <strong>Next</strong></li>
</ul>
<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_23.png"><img class="alignnone wp-image-562 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_23.png" alt="wsus_server_2012_wiseindy_23" /></a>
<h3>Step 23:</h3>
If you use a proxy server, enter the details here, otherwise leave the checkbox unchecked and click <strong>Next</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_24.png"><img class="alignnone wp-image-563 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_24.png" alt="wsus_server_2012_wiseindy_24" /></a>
<h3>Step 24:</h3>
Your server will now need to connect to Microsoft Update and find out information about all available updates.

Click <strong>Start Connecting</strong>. This might take upto 20 minutes or more depending upon your connection.

Once it's done, hit <strong>Next</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_25.png"><img class="alignnone wp-image-564 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_25.png" alt="wsus_server_2012_wiseindy_25" /></a>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_26.png"><img class="alignnone wp-image-565 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_26.png" alt="wsus_server_2012_wiseindy_26" /></a>
<h3>Step 25:</h3>
Choose which all languages do you need updates for and click <strong>Next</strong>. You can always modify this later.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_27.png"><img class="alignnone wp-image-566 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_27.png" alt="wsus_server_2012_wiseindy_27" /></a>
<h3>Step 26:</h3>
The <strong>Choose Products</strong> screen will allow you to subscribe for updates for different Microsoft products.

After selecting your products, click <strong>Next</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_28.png"><img class="alignnone wp-image-567 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_28.png" alt="wsus_server_2012_wiseindy_28" /></a>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_29.png"><img class="alignnone wp-image-568 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_29.png" alt="wsus_server_2012_wiseindy_29" /></a>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_30.png"><img class="alignnone wp-image-569 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_30.png" alt="wsus_server_2012_wiseindy_30" /></a>
<h3>Step 27:</h3>
Here you can choose what type of updates you want to subscribe to. Do you want just critical &amp; security updates? Or do you want everything? This is where you can specify that.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_31.png"><img class="alignnone wp-image-570 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_31.png" alt="wsus_server_2012_wiseindy_31" /></a>
<h3>Step 28:</h3>
Configure your sync schedule for updates here. The synchronization process involves downloading updates from Microsoft Update or another WSUS server. WSUS determines if any new updates have been made available since the last time you synchronized. If this is the first time you are synchronizing the WSUS server, all of the updates are made available for approval.

I chose to automatically sync my server with Microsoft Update daily at 2 AM.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_32.png"><img class="alignnone wp-image-571 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_32.png" alt="wsus_server_2012_wiseindy_32" /></a>
<h3>Step 29:</h3>
Select <strong>Begin initial synchronization</strong> to sync with Microsoft Update and click <strong>Next</strong> and then <strong>Finish</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_33.png"><img class="alignnone wp-image-572 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_33.png" alt="wsus_server_2012_wiseindy_33" /></a>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_34.png"><img class="alignnone wp-image-573 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_34.png" alt="wsus_server_2012_wiseindy_34" /></a>
<h3>Step 30:</h3>
The <strong>Update Services</strong> console will now launch.

This is going to be the place from where you can control everything.

Right now, under the <strong>To Do</strong> section, you will not see much. Wait for the server to synchronize with Microsoft Update. Once it syncs, you will see information like how many updates are available, how many are approved, etc.

Under the <strong>Overview</strong> section, you can see the <strong>Synchronization Status</strong>.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_35.png"><img class="alignnone wp-image-574 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_35.png" alt="wsus_server_2012_wiseindy_35" /></a>

Synchronization status is now <strong>12%</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_36.png"><img class="alignnone wp-image-575 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_36.png" alt="wsus_server_2012_wiseindy_36" /></a>
<h3>Step 31:</h3>
Synchronization is finally complete. You can now see the number of updates that are available to you under the <strong>To Do</strong> section.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_37.png"><img class="alignnone wp-image-576 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_37.png" alt="wsus_server_2012_wiseindy_37" /></a>

This completes the installation and initial configuration of our WSUS server. However, this server is not going to be much use to you right now. It still isn't pushing any updates to your workstations still.

Lets fix that.
<h3>Step 32:</h3>
We will be using a GPO to register the workstations on our network with our newly created WSUS server.

Fire up your <strong>Group Policy Management</strong> console. Right-click <strong>Group Policy Objects</strong> and create a new GPO.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_38.png"><img class="alignnone wp-image-577 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_38.png" alt="wsus_server_2012_wiseindy_38" /></a>

Give it an easy-to-identify name.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_39.png"><img class="alignnone wp-image-578 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_39.png" alt="wsus_server_2012_wiseindy_39" /></a>

After its created, right-click and choose <strong>Edit</strong>. We will now configure the GPO.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_40.png"><img class="alignnone wp-image-579 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_40.png" alt="wsus_server_2012_wiseindy_40" /></a>
<h3>Step 33:</h3>
Expand <strong>Computer Configuration &gt; </strong><strong>Policies &gt; Administrative Templates &gt; Windows Components &gt; Windows Update</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_41.png"><img class="alignnone wp-image-580 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_41.png" alt="wsus_server_2012_wiseindy_41" /></a>
<h3>Step 34:</h3>
Double-click <strong>Configure Automatic Updates</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_42.png"><img class="alignnone wp-image-581 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_42.png" alt="wsus_server_2012_wiseindy_42" /></a>

Select <strong>Enabled</strong>

Under <strong>Options</strong>, choose how would you want your workstations to update. In my case, I prefer the PCs to download the updates and schedule them to be installed at 3 AM daily.

Once you are satisfied with the options, click <strong>OK</strong> to exit the screen.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_43.png"><img class="alignnone wp-image-582 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_43.png" alt="wsus_server_2012_wiseindy_43" /></a>
<h3>Step 35:</h3>
Next, double-click <strong>Enable client-side targeting</strong>.
Configuring this setting will enable the workstations on your network to register directly with your WSUS server (client-side registration).

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_44.png"><img class="alignnone wp-image-583 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_44.png" alt="wsus_server_2012_wiseindy_44" /></a>

Select <strong>Enabled</strong>.
In the <strong>Options</strong> area, type the group name for this computer (Your WSUS server can use this information to group computers into different groups. We will see how this is done further below).

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_45.png"><img class="alignnone wp-image-584 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_45.png" alt="wsus_server_2012_wiseindy_45" /></a>
<h3>Step 36:</h3>
Next, double-click on <strong>Specify intranet Microsoft update service location</strong>.
This is where you will specify your WSUS server's address.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_46.png"><img class="alignnone wp-image-585 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_46.png" alt="wsus_server_2012_wiseindy_46" /></a>

Select <strong>Enabled</strong>.
In the <strong>Options</strong> area, specify your server name in the form of a URL as shown below.

My WSUS server's hostname is <strong>my-wsus-server</strong><strong>. </strong>The default port number for WSUS on Windows Server 2012 R2 is <strong>8530</strong>, so my complete server address is:
<strong>http://my-wsus-server:8530</strong>

Enter the same URL in both the text boxes and click <strong>OK</strong>.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_47.png"><img class="alignnone wp-image-586 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_47.png" alt="wsus_server_2012_wiseindy_47" /></a>
<h3>Step 37:</h3>
Well, the last step is to link the GPO to an OU. Select an OU which has your test computer. Right-click it and select <strong>Link an Existing GPO</strong>.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_48.png"><img class="alignnone wp-image-587 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_48.png" alt="wsus_server_2012_wiseindy_48" /></a>

Choose your newly created GPO and click <strong>OK</strong>.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_49.png"><img class="alignnone size-full wp-image-588" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_49.png" alt="wsus_server_2012_wiseindy_49" /></a>
<h3>Step 38:</h3>
Let's go back to our WSUS server and create a new computer group. By default, under <strong>All Computers</strong>, you'll see a default group called <strong>Unassigned Computers</strong>. Any computer that doesn't belong to a group will appear here.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_50.png"><img class="alignnone size-full wp-image-589" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_50.png" alt="wsus_server_2012_wiseindy_50" /></a>

Right-click <strong>All Computers</strong> and select <strong>Add Computer Group...</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_51.png"><img class="alignnone size-full wp-image-590" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_51.png" alt="wsus_server_2012_wiseindy_51" /></a>

Enter the name of the group. I entered the same group name that I had specified in my GPO <strong>(Step 35)</strong>.

Click <strong>Add</strong>.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_52.png"><img class="alignnone size-full wp-image-591" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_52.png" alt="wsus_server_2012_wiseindy_52" /></a>
<h3>Step 39:</h3>
Now, we can either wait for the GPO to be automatically applied to our test computer or, if you are impatient like me, we can speed things up.

Log into your <strong>test computer</strong>.

Open up <strong>Command Prompt</strong> as <strong>Administrator </strong>and run 3 commands as shown below.
<ul>
	<li><code>gpupdate /force<code></code></code></li>
	<li><code>wuauclt.exe /detectnow<code></code></code></li>
	<li><code>wuauclt.exe /reportnow</code></li>
</ul>
<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_53.png"><img class="alignnone size-full wp-image-592" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_53.png" alt="wsus_server_2012_wiseindy_53" /></a> <a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_54.png"><img class="alignnone size-full wp-image-593" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_54.png" alt="wsus_server_2012_wiseindy_54" /></a>
<h3>Step 40:</h3>
Go back to your WSUS server. Select <strong>All Computers</strong> group.

Hit refresh.

You will see that your <strong>test computer</strong> has appeared in the list.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_55.png"><img class="alignnone size-full wp-image-594" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_55.png" alt="wsus_server_2012_wiseindy_55" /></a>

If you don't see your test computer here, do the following:
<ul>
	<li>Wait for about 5 minutes and hit <strong>Refresh</strong> again. Sometimes it takes a while for the PCs to show up even if you have run the above commands.</li>
	<li>Double-check your GPO settings. Make sure you linked it to the correct OU. The OU should have your <strong>test computer</strong> account and not the user account since its a <em>Computer</em> Configuration policy.</li>
	<li>Run the commands (specified in Step 39) again on your <strong>test computer</strong>. Make sure you run them from an elevated command prompt.</li>
	<li>Reboot your <strong>test </strong><strong>computer</strong>.</li>
</ul>
<h3>Step 41:</h3>
You will notice that even though you have specified the computer to be added to a group <strong>wsus-workstations</strong> in the GPO, the test computer still appears under <strong>Unassigned Computers</strong>.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_56.png"><img class="alignnone size-full wp-image-595" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_56.png" alt="wsus_server_2012_wiseindy_56" /></a>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_57.png"><img class="alignnone size-full wp-image-596" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_57.png" alt="wsus_server_2012_wiseindy_57" /></a>

Well, that's because by default, WSUS ignores the groups and places <strong>all</strong> discovered computers in the <strong>Unassigned Computers</strong> group. You can then manually move it to whichever group you want.

You can change this setting. If you want the computers to automatically add themselves to the group specified in the GPO, do the following.

In your <strong>Update Services</strong> console, select <strong>Options</strong>. Double-click on<strong> Computers</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_58.png"><img class="alignnone size-full wp-image-597" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_58.png" alt="wsus_server_2012_wiseindy_58" /></a>

Choose the <strong>second</strong> option that says <strong>Use Group Policy or registry settings on computers.</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_59.png"><img class="alignnone size-full wp-image-598" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_59.png" alt="wsus_server_2012_wiseindy_59" /></a>

Now any computer that your GPO will apply to, will automatically appear in the group <strong>wsus-computers</strong> instead of <strong>Unassigned Computers</strong>.

You can make different GPOs for machines that you want to be grouped differently.
<h3>Step 42:</h3>
Now, since we have added a test computer, lets see how we can push updates to it.

In your WSUS console, expand the <strong>Updates</strong> tree and select <strong>All Updates</strong>. You will see updates which are needed and that are not yet approve.

You will have to <strong>Approve</strong> them so that they can be pushed out to your test computer.

Select the updates you want to approve using the Shift or Ctrl key.

From the <strong>Actions</strong> sidebar on the right, select <strong>Approve...</strong> (you can also right-click the selected updates and do the same)

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_63.png"><img class="alignnone size-full wp-image-602" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_63.png" alt="wsus_server_2012_wiseindy_63" /></a>

In the window that pops up, right-click <strong>All Computers</strong> and select <strong>Approved for Install</strong>.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_64.png"><img class="alignnone size-full wp-image-603" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_64.png" alt="wsus_server_2012_wiseindy_64" /></a>

You'll notice that the updates haven't been approved for the groups individually. Right-click <strong>All Computers</strong> again and select <b>Apply to Children</b>. This will approve updates for all the children groups under <strong>All Computers</strong>.

Since you have just one test computer right now, we have approved it for all the computers. However, in a production environment you should first approve the updates to a test group (instead of all computers) to see if the updates cause any sorts of problems. Once you are certain the updates don't break anything, you can push it to the critical machines.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_65.png"><img class="alignnone size-full wp-image-604" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_65.png" alt="wsus_server_2012_wiseindy_65" /></a>

Select<strong> OK</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_66.png"><img class="alignnone size-full wp-image-605" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_66.png" alt="wsus_server_2012_wiseindy_66" /></a>

The updates have been approved. Now during the scheduled time (3 AM in our case), these updates will be pushed to out test computer.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_67.png"><img class="alignnone size-full wp-image-606" src="http://wiseindy.com/wp-content/uploads/2015/06/wsus_server_2012_wiseindy_67.png" alt="wsus_server_2012_wiseindy_67" /></a>

That's it! Our WSUS server is now set up.

Hope this guide was useful to you. You can leave your feedback in the comments below.
