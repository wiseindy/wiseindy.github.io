---
id: 877
title: 'Virtual Machines: Snapshots aren&#8217;t backups'
date: 2015-08-23T06:50:33+00:00
author: wiseindy
layout: post
guid: http://wiseindy.com/?p=877
permalink: /it/virtual-machines-snapshots-arent-backups/
image: /wp-content/uploads/2015/08/virtual-machines-snapshots-are-not-backups.jpg
categories:
  - IT
---
Backups, Snapshots and Archives. They are three different things, however they're frequently confused to be the same. Does the advent of virtualization mean traditional backups can be replaced by new data protection methods such as snapshots?

<!--more-->
<h3>Backups</h3>
Backing up is the process of making an additional copy of data that can be easily restored if the primary data becomes lost or unusable. Backups can be copied to external media, like portable hard drives and tape, or remote storage, like a NAS, SAN, or server at another site.

Backups offers a solid solution should a major hardware or site disaster occur. Although traditional backups don’t necessarily provide the flexibility or efficiency of other methods, they offer a better long-term solution for data retention especially where backup policies dictate redundant backup copies in geographically dispersed locations.
<h3>Archives</h3>
Archives are different. Imagine you back your SQL databases up to simple *.bak files on the same drive as the database, you haven't created a backup, but rather you've created an archive. An archive is a copy of your data as it exists at a point in time that doesn't meet all of the requirements to be a true backup. Assume that your SQL server crashes. You will not be able to restore your database from the archives. You'll have to first rebuild your entire server and configure it exactly as it was before and then restore from archive. Not ideal.

However, archives can be very useful for quick restores and solving minor issues, but only backups truly protect your data. A backup must be able to survive a total failure of the source, not just a single hard drive failure.
<h3>Snapshots</h3>
Snapshots are point-in-time copies of the data. As the name indicates, they're "snapshots" of the entire data set taken at a specific time. Snapshots are not backups. A snapshot file is only a change log of the original virtual disk. Snapshots are sometimes marketed as valid “backup solutions”. This is an incorrect and dangerous assumption.

<div class="row">
  <div class="col-12">
    {% include adsense-post-content.html %}
  </div>
</div>

Snapshots <strong>are not complete copies of the original virtual machine disk files</strong>. Taking a snapshot does not create a complete copy of the original vm disk file, rather it only copies the changes that were made since the previous snapshot. Every snapshot needs the base disk and the previous snapshot file to be fucntional. At any point of time, to access a snapshot, you should have full access to the snapshot chain before it. If the base disks are deleted, the snapshot files are useless.

While there are benefits of using snapshots for development or testing purposes on non-production systems, they should not be considered as valid data protection or backups of your virtual machines.

A good data protection strategy combines a number of aspects that can include all of the above features.

While snapshots aren't true backups, they do provide a lot of value. Short-term snapshots are great for dealing with user errors and some data corruption scenarios. More importantly, they are very fast (data can be reverted or restored in seconds). They're extremely space-efficient and in many cases, restores can be performed very quickly. Snapshots reduce the amount of labor needed to manage an environment and are generally good enough for daily use. The issue is simply that they can't be relied upon in a major disaster, and any true backup strategy must go beyond snapshots.

(header image source: <a target="_blank" href="http://www.wallpaperlayer.com/vintage-camera-wallpaper-704.html" target="_blank">wallpaperlayer.com</a>)
