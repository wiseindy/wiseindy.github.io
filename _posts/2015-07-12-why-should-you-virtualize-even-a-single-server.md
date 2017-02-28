---
id: 868
title: Why should you virtualize even a single server?
date: 2015-07-12T11:04:55+00:00
author: wiseindy
layout: post
guid: http://wiseindy.com/?p=868
permalink: /blog/why-should-you-virtualize-even-a-single-server/
image: /wp-content/uploads/2015/07/why-should-you-virtualize-even-a-single-server.jpg
featured: /wp-content/uploads/2015/07/why-should-you-virtualize-even-a-single-server-featured.jpg
categories:
  - Blog
  - IT
tags:
  - abstraction
  - advantages
  - citrix
  - cons
  - encapsulation
  - esxi
  - esxi 6.0
  - hyper-v
  - hypervisor
  - microsoft
  - pros
  - server
  - vcenter
  - virtual
  - virtual machine
  - virtualization
  - virtualizing
  - vm
  - vmware
  - vsphere
  - windows
  - windows server
  - xenserver
---
I believe the default mindset these days should be always virtualized. It doesn't matter if you are looking to implement a single server or several. Of course, there may be outlier cases where virtualization cannot be applied (special case hardware, huge computer clusters, etc.). While providing business requirements or planning a new project, start with the "always virtualized" mindset and work from there.

<!--more-->
<h3>Hardware abstraction simplifies things</h3>
The key point that comes to mind when considering virtualization is hardware abstraction. When you virtualize, you are adding a layer between baremetal and the operating system. In a practical sense, this is what virtualization is.

If you are familiar with programming languages, you should be aware of the concept of <a target="_blank" href="https://en.wikipedia.org/wiki/Encapsulation_(computer_programming)" target="_blank">encapsulation</a>. Virtualization works in a similar way by encapsulating the underlying server hardware and presenting a standardized hardware base to operating systems. This hardware abstraction and the resulting stability alone are reason enough to go virtual.

This will greatly enhance the future-proofing of the infrastructure, make backups significantly easier and more versatile. You'll effectively have a baremetal backup that you can restore to any other host and it also opens doors for effective clustering and migrations.
<h3>Backups &amp; snapshots make life easier</h3>
Virtual machines are extremely easy to backup and restore compared to their physical counterparts. Due to abstraction of storage and memory, we can <a target="_blank" href="https://en.wikipedia.org/wiki/Snapshot_(computer_storage)" target="_blank">snapshot</a> the current state of a machine at any point of time. This is basically taking an image of the running system and storing it in a file.

These features allow you to take a system snapshot before carrying out any activities that may risk the stability of the system. For e.g., installing new software, changing configurations, installing updates &amp; patching, etc. Snapshots can assist you in extremely rapid rollbacks should anything go wrong. This seemingly minor feature can lead to big peace of mind and overall system reliability.  It also makes testing of features and rolling back or repeated testing very easy in non-production environments.

<div class="row">
  <div class="col-12">
    {% include adsense-post-content.html %}
  </div>
</div>

Compare this with a physical machine. You're unable to do any of this with such ease and speed. Some may say there's Windows System Restore, but we all know it rarely works when you need it to. Windows System Restore is not an operating system agnostic backup unlike snapshots. In addition, it's not guaranteed to bring your OS back to the state it was in when you took the snapshot. Also, restoring a VM snapshot will get rid of any viruses or malware you picked up. This is definitely not the case with System Restore.

However, an important point to keep in mind is that that snapshots <a target="_blank" href="http://wiseindy.com/it/virtual-machines-snapshots-arent-backups/" target="_blank">are not backups</a>. You should always have a solid disaster recovery plan in place.
<h3>Do more with less</h3>
This one is fairly obvious. Virtualization enables you to run multiple machines on a single physical server. Instead of dedicating individual physical boxes for multiple requirements, virtualization enables you to consolidate multiple workloads onto a single physical box thereby maximizing efficiency and bringing down costs.

Virtualization allows you to prepare for any future expansions even though you may think you do not need it at that time.
<h3>Virtual machines are files</h3>
Any hardware upgrades or migrations between physical machines are rife with uncertainity and have the potential to cause odd problems requiring days or weeks to fix. In worst cases, a system rebuild needs to be done.

Virtual machines bypass most of these issues. VMs are simply files, at least when not actively running. You can safely and rapidly migrate between physical hosts without any regard to the underlying hardware. These tasks that would be otherwise risky can become trivial with a virtual environment.
<h3>The options</h3>
At the end of the day, IT is about reducing risk, mitigating disasters and maximizing stability and flexibility. Virtualization standardizes your environment, hence making it more flexible, stable and easy to manage. The major enterprise virtualization products (Microsoft Hyper-V, VMware vSphere, Citrix XenServer, KVM) are available, at least in some form, for free.

Virtualization, at zero cost, provides you all the above listed benefits. There are no measureable downsides and if offers a huge potential benefit in the areas of safety, stability, flexibility and future-proofing of your environment. This leaves us with a the conculsion that virtualization in today's day and age is a no-brainer and should be used as a "default" strategy in every possible environment.

(header image source: <a target="_blank" href="http://vyle-art.com/portfolio/tronlegacy/" target="_blank">vyle-art.com</a>)
