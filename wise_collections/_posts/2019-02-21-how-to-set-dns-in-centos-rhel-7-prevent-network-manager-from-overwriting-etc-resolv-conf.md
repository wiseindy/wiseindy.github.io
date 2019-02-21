---
title: How to set DNS in CentOS/RHEL 7 & prevent NetworkManager from overwriting /etc/resolv.conf?
date: 2019-02-21T15:03:00+00:00
author: wiseindy
comments: true
layout: single
header:
  image: /assets/images/featured/featured-dnslinux.jpg
  teaser: /assets/images/featured/featured-dnslinux.jpg
categories:
  - Linux
tags:
  - dns
  - resolv.conf
  - nameservers
  - centos
  - centos 7
  - redhat
  - rhel
  - rhel 7
  - redhat 7
  - linux
  - guides
---

This guide shows you how to set custom DNS entries for CentOS 7 / RedHat 7 and ensure that the settings are persistent even after a reboot.

<!--more-->

# What you need

* A CentOS 7 or a Red Hat Enterprise Linux (RHEL) 7 server
* A couple of minutes

# Overview

In CentOS and Red Hat Enterprise Linux (RHEL) 7, any custom DNS entries are stored in the file `/etc/resolv.conf`. However, if we simply go ahead and add our nameservers to this file, we'll notice that after a reboot or a restart of the network.service, the file is overwritten by NetworkManager.

In this guide, we will first configure NetworkManager to **not overwrite** this file. Then, we will go ahead and actually add our custom nameservers to `/etc/resolv.conf`.

# Step 1

The NetworkManager configuration is located here: `/etc/NetworkManager/NetworkManager.conf`
Open this file using `vim` or your favorite text editor.

Search for the `[main]` section in this file. It should look something like this:

```
...
[main]
#plugins=ifcfg-rh,ibft
...
```

Add `dns=none` just after the `[main]` tag like this:

```
...
[main]
dns=none
#plugins=ifcfg-rh,ibft
...
```

Go ahead and save the file.

# Step 2

Let's restart the `NetworkManager.service` service so that it picks up the changes we made to the configuration.

```
sudo systemctl restart NetworkManager.service
```

Note that the service name `NetworkManager.service` is **case-sensitive**.

# Step 3

Now, let's add our nameservers to `/etc/resolv.conf`

Open this file in you favorite text editor and specify the name servers as follows:

```
# Generated by NetworkManager
nameserver 8.8.8.8
nameserver 8.8.4.4
```

That's it! You're done. The nameservers added to `/etc/resolv.conf` will now persist even after a reboot. NetworkManager will not longer overwrite this file.

---

Photo by Steve Johnson on Unsplash

<a style="background-color:black;color:white;text-decoration:none;padding:4px 6px;font-family:-apple-system, BlinkMacSystemFont, &quot;San Francisco&quot;, &quot;Helvetica Neue&quot;, Helvetica, Ubuntu, Roboto, Noto, &quot;Segoe UI&quot;, Arial, sans-serif;font-size:12px;font-weight:bold;line-height:1.2;display:inline-block;border-radius:3px" href="https://unsplash.com/@steve_j?utm_medium=referral&amp;utm_campaign=photographer-credit&amp;utm_content=creditBadge" target="_blank" rel="noopener noreferrer" title="Download free do whatever you want high-resolution photos from Steve Johnson"><span style="display:inline-block;padding:2px 3px"><svg xmlns="http://www.w3.org/2000/svg" style="height:12px;width:auto;position:relative;vertical-align:middle;top:-2px;fill:white" viewBox="0 0 32 32"><title>unsplash-logo</title><path d="M10 9V0h12v9H10zm12 5h10v18H0V14h10v9h12v-9z"></path></svg></span><span style="display:inline-block;padding:2px 3px">Steve Johnson</span></a>