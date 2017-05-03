---
title: How to fix error 0x80004005 - Cannot enable developer mode in Windows 10
date: 2017-04-26T10:00:00+00:00
author: wiseindy
comments: true
layout: post
header:
  image: /assets/images/featured/featured-developer-full.jpg
  teaser: /assets/images/featured/featured-developer.jpg
categories:
  - IT
tags:
  - windows 10
  - developer
  - developer mode
  - shell
  - bash shell
  - subsystem
  - guide
  - linux
  - ubuntu
  - UseWUServer
  - regedit
  - error 0x80004005
  - 0x80004005
  - Guides
---

"Developer mode package failed to install. Error code 0x80004005". A few people, including me, faced issues when trying to enable developer mode in Windows 10. This guide will show you how to fix it.

<!--more-->
## Why this happens?

After quite some digging and research online, I found that this problem is related to WSUS (Windows Server Update Services). If you're in an environment where your PC gets updates from WSUS, you can face this problem. Luckily, it's a straightforward fix.

## Step 1:

Click **Start** and type `regedit`. Open it.

![Click start and search for regedit](/assets/images/posts/2017-04-26-windows-10-developer-mode-fix-error-0x80004005-001.png "Click start and search for regedit")

Navigate to `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU` in **regedit**

![Navigate to key in regedit](/assets/images/posts/2017-04-26-windows-10-developer-mode-fix-error-0x80004005-002.png "Navigate to key in regedit")

Double click **UseWUServer** and set the value to **0**

![Set UseWUServer to 0](/assets/images/posts/2017-04-26-windows-10-developer-mode-fix-error-0x80004005-003.png "Set UseWUServer to 0")

## Step 2:

Restart your PC. Now try to enable developer mode again. This time you will not see the error 0x80004005 and it should be enabled successfully.

(header image source: [sf.co.ua](http://sf.co.ua/id169202))
