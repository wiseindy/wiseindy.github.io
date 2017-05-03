---
id: 707
title: 'Convert a physical machine to a virtual machine (P2V) using VMware vCenter Converter Standalone &#8211; A Step-by-Step Guide'
date: 2015-06-16T10:20:37+00:00
author: wiseindy
comments: true
layout: post
guid: http://wiseindy.com/?p=707
dsq_thread_id:
  - "5585733521"
header:
  image: /wp-content/uploads/2015/06/convert-physical-machine-to-virtual-machine-using-vmware-vcenter-converter.jpg
  teaser: /assets/images/featured/featured-p2v.jpg
categories:
  - IT
tags:
  - bare metal
  - esxi
  - esxi 6.0
  - hypervisor
  - migration
  - p2v
  - physical
  - vcenter
  - vcenter converter
  - virtual
  - virtual machine
  - virtualization
  - vm
  - vmware
  - vsphere
  - windows server
  - Guides
---
In this guide, I will walk you through a step-by-step procedure to convert my physical, bare-metal Windows Server 2003 to a virtual machine. We will be doing a remote hot cloning, i.e., virtualizing a powered on physical machine.

I'll also show you some errors that I ran into during this process and how I fixed them.

<!--more-->
<h3>Why P2V?</h3>
P2V means "Physical to Virtual". This conversion copies over the operating system, applications and data from an existing physical server a new virtual server.

Virtualization allows you to dramatically reduce your server room requirements by phasing out legacy hardware. Virtual machines are hardware agnostic and make a sysadmin's life easier. They make backups &amp; disaster recovery easier &amp; more reliable. In case of any hardware failure, you can quickly get the VM up and running on a different piece of hardware with zero or negligible downtime. Also, reduced power consumption, less datacentre space, less hardware to maintain and repair – all reduce costs.

So, let's get started.
<h3>What you need:</h3>
<ul>
	<li><strong>A physical machine that you want to convert to virtual (P2V conversion).</strong>
<ul>
	<li>I have a physical (bare-metal) Windows Server 2003 that I want to virtualize.</li>
</ul>
</li>
	<li><strong>VMware virtual infrastructure</strong>
<ul>
	<li>I have a VMware vSphere Hypervisor (ESXi 6.0) installed on a machine. It's free of cost.
You can download it for free from here:
<a target="_blank" href="https://my.vmware.com/web/vmware/evalcenter?p=free-esxi6" target="_blank">https://my.vmware.com/web/vmware/evalcenter?p=free-esxi6
</a>(You will need to register for a free VMware account first)</li>
	<li>At the time of writing this article, the latest version of VMware vSphere Hypervisor (ESXi) is <strong><strong>6.0</strong></strong></li>
</ul>
</li>
	<li><strong>VMware vCenter Converter Standalone</strong>
<ul>
	<li>VMware vCenter Converter Standalone is a free product to convert virtual and physical machines to VMware virtual machines.
You can download it for free here:
<a target="_blank" href="https://my.vmware.com/web/vmware/info/slug/infrastructure_operations_management/vmware_vcenter_converter_standalone/6_0" target="_blank">https://my.vmware.com/web/vmware/info/slug/infrastructure_operations_management/vmware_vcenter_converter_standalone/6_0</a></li>
	<li>At the time of writing this article, the latest version of VMware vCenter Converter Standalone is <strong>6.0</strong></li>
</ul>
</li>
</ul>
<h3>Additional resources (optional):</h3>
<blockquote>Download VMware's official user's guide for VMware vCenter Converter Standalone here:
<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_vcenter_converter_standalone_p2v_convsa_60_guide.pdf" target="_blank">VMware vCenter Converter Standalone User's Guide.pdf</a>

Mirror: <a target="_blank" href="http://www.vmware.com/pdf/convsa_60_guide.pdf">VMware official</a></blockquote>
<h3>Some points to keep in mind</h3>
<ul>
	<li>P2V has a downtime of a few minutes at best. So do inform your users before making the switch.</li>
	<li>You <strong>should</strong> use synchronization (all this is explained in detail during <strong>Step 9</strong>).
<ul>
	<li>Important services must be stopped before synchronizing.</li>
	<li>Synchronization will take place at the <strong>end</strong> of your conversion process.</li>
	<li>Use scheduled synchronization.</li>
	<li>Make sure you <strong>do not</strong> select <strong>Perform final synchronization</strong> at <strong>Step 9</strong>.</li>
	<li>Your downtime should be roughly the duration of the synchronization.</li>
</ul>
</li>
</ul>
<h3>Step 1:</h3>
Download <strong>VMware vCenter Converter Standalone</strong> from here:
<a target="_blank" href="https://my.vmware.com/web/vmware/info/slug/infrastructure_operations_management/vmware_vcenter_converter_standalone/6_0">https://my.vmware.com/web/vmware/info/slug/infrastructure_operations_management/vmware_vcenter_converter_standalone/6_0</a>

Install this on any workstation which is connected to your network. It doesn't necessarily need to be installed <em>on </em>the machine you are migrating. The converter can be installed on any PC connected to the network.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_0.png"><img class="alignnone size-full wp-image-713" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_0.png" alt="vmware_physical_to_virtual_p2v_0" width="79" height="111" /></a>

Once installed, launch it.
<h3>Step 2:</h3>
Select <strong>Convert machine</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_01.png"><img class="alignnone wp-image-714 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_01.png" alt="vmware_physical_to_virtual_p2v_01" /></a>
<h3>Step 3:</h3>
In our scenario, we will be migrating a powered-on physical machine (hot cloning), so select <strong>Powered-on machine</strong> from the <strong>Select source type</strong> dropdown.

Since the <strong>VMWare vCenter Converter Standalone</strong> is installed on a different machine than the one we are migrating, select <strong>A remote machine</strong>. As shown below, enter the <strong>IP address or name</strong> for your physical server. Enter the <strong>User name</strong> &amp; <strong>Password</strong> to connect to this physical server.

Username is in the form of <strong>domain\username</strong> (You can even use <strong>username@domain</strong>). Use an account which has full administrator privileges on the remote machine.

Since our physical machine is Windows Server 2003, select<strong> OS Family</strong> as <strong>Windows</strong> from the dropdown. Click <strong>Next</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_02.png"><img class="alignnone wp-image-715 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_02.png" alt="vmware_physical_to_virtual_p2v_02" /></a>
<h3>Step 4:</h3>
VMware vCenter Converter Standalone will need to install an agent in your physical server temporarily. It will do so automatically. Once the migration is successful, you can specify to automatically remove this agent.

In the dialog box that pops up, select <strong>Automatically uninstall the files when import suceeds</strong>.

Click <strong>Yes.</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_03-.png"><img class="alignnone size-full wp-image-769" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_03-.png" alt="vmware_physical_to_virtual_p2v_03" /></a>

Wait for it to deploy the agent.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_04-.png"><img class="alignnone size-full wp-image-770" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_04-.png" alt="vmware_physical_to_virtual_p2v_04" /></a>

<div class="row">
  <div class="col-12">
    {% include adsense-post-content.html %}
  </div>
</div>

<h3>Step 5:</h3>
<blockquote>If you do not get an error, you can skip to <strong>Step 6</strong>.</blockquote>
At this point, you may or may get an error. It can be something like:
<code>Error 1219: Multiple connections to a server or shared resource by the same user, using more than one user name, are not allowed. [...]</code>

Or, you might also get an error like this:

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_05.png"><img class="alignnone wp-image-718 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_05.png" alt="vmware_physical_to_virtual_p2v_05" /></a>

It is an easy fix.
<ul>
	<li><strong>Disconnect all network drives</strong> to this server from your current PC.
<ul>
	<li>Open My Computer / This PC and check for any mapped network drives to this server. If you find any, disconnect them.</li>
</ul>
</li>
	<li>Log in to the physical server and disconnect any remote drives. (Run the command below in a command prompt window)
<ul>
	<li><code>net use \\&lt;remote_hostname&gt; * /delete</code></li>
</ul>
</li>
	<li>Close any applications that are connected to this server.</li>
	<li>Close all Windows Explorer windows showing files from this server</li>
	<li>Close all Microsoft Management Console (MMC) snap-ins in the server you are trying to convert.</li>
</ul>
Once you do the above, carry out steps <strong>2 to 5</strong> once again. If you still get an error, reboot your PC (the one that has the VMware vCenter Converter Standalone installed).

More information on this error and similar errors here: <a target="_blank" href="http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&amp;cmd=displayKC&amp;externalId=1001344" target="_blank">http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&amp;cmd=displayKC&amp;externalId=1001344</a>
<h3>Step 6:</h3>
VMware vCenter Converter Standalone has now successfully connected to your physical server. Next step is to communicate with your VMware set up.

I have a VMware vSphere Hypervisor (ESXi 6.0) server set up. I want to convert my physical server to a VM running on this ESXi host.

So, choose <strong>VMware Infrastructure virtual machine</strong> from the <strong>Select destination type</strong> dropdown list. (ESXi is a VMware Infrastructure, i.e., a VMware environment, so that's why we select this).

Enter your ESXi server's IP address under <strong>Server</strong>. Type the <strong>User name</strong> and <strong>Password</strong>. If you want the data traffic to pass through your PC (where the VMware Converter is installed), select the Use proxy mode check box. We don't want this so, leave the <strong>Use proxy mode</strong> button <strong>unchecked</strong>. Click <strong>Next</strong>.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_06.png"><img class="alignnone wp-image-719 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_06.png" alt="vmware_physical_to_virtual_p2v_06" /></a>
<h3>Step 7:</h3>
It has now connected to your ESXi server. Enter the <strong>Name</strong> for your new virtual machine and click <strong>Next</strong>.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_07-.png"><img class="alignnone size-full wp-image-775" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_07-.png" alt="vmware_physical_to_virtual_p2v_07" /></a>
<h3>Step 8:</h3>
On the <strong>Destination Location</strong> page, choose the location for your new VM. In my case, I have only one datastore so I chose that. You can also specify the <strong>Virtual machine version</strong>. I have selected the latest available at thetime of writing this article (version 11). Note that selecting the highest version isn't always the best. Pick a version keeping in mind your existing environment and compatibility requirements. Since this is a test lab, I've picked the highest possible version.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_08-.png"><img class="alignnone size-full wp-image-771" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_08-.png" alt="vmware_physical_to_virtual_p2v_08" /></a>
<h3>Step 9:</h3>
This is where you'll specify the <b>Options </b>for your new VM.

You can change settings for the new drives, CPUs RAM, etc. In this case, I've left everything as default except disk sizes and synchronization options.
<blockquote><strong>Important note:</strong> If you change the drive sizes (<strong>as I've done below to illustrate</strong>), you will not be able to enable <strong>Synchronization</strong>. So, do not change the drive sizes. Leave them as default.</blockquote>
<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_10.png"><img class="alignnone wp-image-723 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_10.png" alt="vmware_physical_to_virtual_p2v_10" /></a>

As you can see above, I've changed the default sizes of C: and D: drive.

<strong>Stop services running on the source machine.</strong>

You can make sure that you do not lose data from services running on the source machine. You can select the services that you want to stop before Converter Standalone synchronizes the data between the source and destination machine. As a result, the services do not generate data while source and destination machines are synchronized (more on synchronization after the jump).

Select <strong>Services &gt; Source services</strong> tab. To stop a service on the source machine before synchronization, highlight a service and select the Stop <strong>check box</strong> to the right.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_10-1.png"><img class="alignnone size-full wp-image-820" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_10-1.png" alt="vmware_physical_to_virtual_p2v_10-1" /></a>

Next, we will specify synchronization options.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_11.png"><img class="alignnone wp-image-724 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_11.png" alt="vmware_physical_to_virtual_p2v_11" /></a>

Here you can set a schedule for synchronization.
<blockquote><strong>What is synchronization?</strong>

When you convert a powered on Windows machine, Converter Standalone copies data from the source machine to the destination machine while the source machine is still running and generating changes. This process is the first transfer of data. You can transfer data for the second time by copying only the changes made during the first transfer of data. This process is called synchronization.</blockquote>
<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_12.png"><img class="alignnone wp-image-725 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_12.png" alt="vmware_physical_to_virtual_p2v_12" /></a>

You can specify post conversion options under the <strong>Post-conversion</strong> tab. Check <strong>Install VMware Tools on the destination virtual machine</strong> and click <strong>Next</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_13.png"><img class="alignnone wp-image-726 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_13.png" alt="vmware_physical_to_virtual_p2v_13" /></a>
<h3>Step 10:</h3>
Review the summary once and make sure everything is OK. Click <strong>Finish</strong>.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_14.png"><img class="alignnone wp-image-727 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_14.png" alt="vmware_physical_to_virtual_p2v_14" /></a>
<h3>Step 11:</h3>
As I had mentioned in <strong>Step 9</strong>, you will get an error if you change the drive sizes and enable synchronization at the same time.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_15.png"><img class="alignnone wp-image-728 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_15.png" alt="vmware_physical_to_virtual_p2v_15" /></a>

To fix this, go <strong>Back</strong> and set the drive sizes to the <strong>default</strong> and click <strong>Next</strong>.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_16.png"><img class="alignnone wp-image-729 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_16.png" alt="vmware_physical_to_virtual_p2v_16" /></a>

Verify the summary and click <strong>Finish</strong>.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_17.png"><img class="alignnone wp-image-730 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_17.png" alt="vmware_physical_to_virtual_p2v_17" /></a>
<h3>Step 12:</h3>
You will see now that the task has been submitted and is now in the <strong>Running</strong> status. This should take a couple of hours.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_18.png"><img class="alignnone wp-image-731 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_18.png" alt="vmware_physical_to_virtual_p2v_18" /></a>
<h3> Step 13:</h3>
Sometimes, after the initial cloning is complete, you may get an error during <strong>Synchronization</strong>. Let us see what could be the reason for this and how it can be fixed.
<blockquote>If you do not get this error, you can skip to <strong>Step 17</strong>.</blockquote>
As you can see below, <strong>Synchronization</strong> has failed at 1% with the error:
<code>FAILED: Unable to create a VSS snapshot of the source volume(s). Error code: 2147754774 (0x80042316)</code>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_20.png"><img class="alignnone wp-image-733 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_20.png" alt="vmware_physical_to_virtual_p2v_20" /></a>

If you select <strong>Jobs</strong> view, you can see the exact process that failed.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_21.png"><img class="alignnone wp-image-734 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_21.png" alt="vmware_physical_to_virtual_p2v_21" /></a>

This error happens because in your physical server, if Volume Shadow Copy Service (VSS) has problems performing a snapshot of disks, which can occur if multiple providers are associated with the operating system. <strong>Steps 14,</strong> <strong>15 &amp; 16</strong> will show you how to fix this.
<blockquote>This can happen if you're running Windows Server 2003. You can read more about it in VMware's knowledgebase article:
<a target="_blank" href="http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&amp;cmd=displayKC&amp;externalId=1035241" target="_blank">http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&amp;cmd=displayKC&amp;externalId=1035241</a>

More: <a target="_blank" href="http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&amp;cmd=displayKC&amp;externalId=1039087" target="_blank">http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&amp;cmd=displayKC&amp;externalId=1039087</a></blockquote>
<h3>Step 14:</h3>
Log into your physical server. Launch <strong>cmd.exe</strong> and type <code>vssadmin list providers </code>and hit Enter.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_22.png"><img class="alignnone wp-image-735 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_22.png" alt="vmware_physical_to_virtual_p2v_22" /></a>

<img class="alignnone wp-image-736 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_23.png" alt="vmware_physical_to_virtual_p2v_23" />

As you can see, there are <b>two providers</b> associated with <strong>VSS</strong>. We will have to remove one. In this case, we will keep the Microsoft provider and remove the StorageCraft one. Note that this can affect your 3rd party backup software (in this case StorageCraft ShadowProtect). After the synchronization is complete, we can add this StorageCraft provider back to VSS. This is illustrated below.
<h3>Step 15:</h3>
To remove the VSS provider, we need to edit the registry. In a <strong>cmd</strong> window, type <code>regedit</code> and hit Enter.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_24.png"><img class="alignnone wp-image-737 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_24.png" alt="vmware_physical_to_virtual_p2v_24" /></a>

Navigate to <code>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\VSS\Providers</code>

Here you'll see the two VSS providers.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_25.png"><img class="alignnone wp-image-738 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_25.png" alt="vmware_physical_to_virtual_p2v_25" /></a>

Select the non-Microsoft VSS provider and <strong>right-click</strong> it. Choose <strong>Export</strong>.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_26.png"><img class="alignnone wp-image-739 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_26.png" alt="vmware_physical_to_virtual_p2v_26" /></a>

Save this registry key in a safe location. Type a filename and make sure the <strong>Selected</strong><strong> branch</strong> radio button is elected. Click <strong>Save</strong>. Do not lose this <strong>.reg</strong> file. Later, you can restore this deleted registry entry by simply double-clicking the <strong>.reg</strong> file.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_27.png"><img class="alignnone wp-image-740 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_27.png" alt="vmware_physical_to_virtual_p2v_27" /></a>

Once you've exported the key successfully, right-click the key again and select <strong>Delete</strong>.
<blockquote>Make sure you've exported the key before deleting it.</blockquote>
<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_28.png"><img class="alignnone wp-image-741 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_28.png" alt="vmware_physical_to_virtual_p2v_28" /></a>

Select <strong>Yes</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_29.png"><img class="alignnone wp-image-742 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_29.png" alt="vmware_physical_to_virtual_p2v_29" /></a>

Once deleted, <strong>reboot</strong> this physical server.
<h3>Step 16:</h3>
Once the physical server reboots, right-click the failed task and select <strong>Synchronize</strong>.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_30.png"><img class="alignnone wp-image-743 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_30.png" alt="vmware_physical_to_virtual_p2v_30" /></a>

If you want to run it immediately or schedule it, then just change the settings under <strong>Advanced options</strong>. Otherwise, click <strong>Next</strong>.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_31.png"><img class="alignnone wp-image-744 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_31.png" alt="vmware_physical_to_virtual_p2v_31" /></a>

Click on <strong>Finish</strong> on the summary screen.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_32.png"><img class="alignnone wp-image-745 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_32.png" alt="vmware_physical_to_virtual_p2v_32" /></a>

The synchronization job will now start running.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_33.png"><img class="alignnone wp-image-746 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_33.png" alt="vmware_physical_to_virtual_p2v_33" /></a>

To view individual tasks, select <strong>Tasks</strong> from the <strong>View by</strong> dropdown.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_34.png"><img class="alignnone wp-image-747 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_34.png" alt="vmware_physical_to_virtual_p2v_34" /></a>

Here you will be able to see the current status of your synchronization task.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_35.png"><img class="alignnone wp-image-748 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_35.png" alt="vmware_physical_to_virtual_p2v_35" /></a>
<h3>Step 17:</h3>
Synchronization is now complete. Your VM should now be ready.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_36.png"><img class="alignnone wp-image-749 size-full" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_36.png" alt="vmware_physical_to_virtual_p2v_36" /></a>
<h3>Step 18:</h3>
Log into your vSphere (ESXi) server.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_41.png"><img class="alignnone size-full wp-image-807" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_41.png" alt="vmware_physical_to_virtual_p2v_41" /></a>

You will see that your new VM has appeared in the list.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_42.png"><img class="alignnone size-full wp-image-808" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_42.png" alt="vmware_physical_to_virtual_p2v_42" /></a>
<h3>Step 19:</h3>
<strong>Do not start the VM yet</strong>. Right-click the VM and choose <strong>Edit Settings...</strong>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_43.png"><img class="alignnone size-full wp-image-809" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_43.png" alt="vmware_physical_to_virtual_p2v_43" /></a>

Under the <strong>Hardware</strong> tab, choose <strong>Network adapter</strong> and <strong>uncheck</strong> the <strong>Connect at power on</strong>. We do not want the VM to be connected to the network when we power it on. This will prevent any conflicts in the network &amp; with the existing physical server.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_44.png"><img class="alignnone size-full wp-image-810" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_44.png" alt="vmware_physical_to_virtual_p2v_44" /></a>
<h3>Step 20:</h3>
Start the VM now. If all goes well, it should boot up.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_45.png"><img class="alignnone size-full wp-image-811" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_45.png" alt="vmware_physical_to_virtual_p2v_45" /></a>

Double-check for any missing drivers and see if everything works as expected. After confirming that everything is functional, you can proceed to power down your physical server when users are not connected to it. Turn off the VM as well, go to it's settings and connect the <strong>network adapter</strong> back (the one that was disabled in <strong>Step 19</strong>). Power on your VM.
<blockquote>Make sure that the physical server is <strong>off</strong> before turning on the VM with network card connected.</blockquote>
Change the IP address of the VM to that of the physical server.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_46.png"><img class="alignnone size-full wp-image-812" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_46.png" alt="vmware_physical_to_virtual_p2v_46" /></a>
<h3>Step 21:</h3>
If you had got an error in <strong>Step 13</strong>, do this step, otherwise skip to <strong>Step 22</strong>.

In your virtual machine, navigate to the location where you saved your exported <strong>.reg</strong> file. Double-click it and click <strong>Yes</strong> when it asks you to add information to the registry.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_47.png"><img class="alignnone size-full wp-image-813" src="http://wiseindy.com/wp-content/uploads/2015/06/vmware_physical_to_virtual_p2v_47.png" alt="vmware_physical_to_virtual_p2v_47" /></a>
<h3>Step 22:</h3>
As a final step, go ahead and test all your applications. You've successfully migrated a physical server to a virtual machine. Good job!

(header image source: <a target="_blank" href="http://www.ismweb.com/optimization-virtualization">ismweb.com</a>)
