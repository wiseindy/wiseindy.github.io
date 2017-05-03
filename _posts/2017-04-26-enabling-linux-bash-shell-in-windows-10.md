---
title: Enabling Linux Bash Shell in Windows 10
date: 2017-04-26T05:43:44+00:00
author: wiseindy
comments: true
layout: post
header:
  image: /assets/images/featured/featured-bash-full.jpg
  teaser: /assets/images/featured/featured-bash.jpg
categories:
  - IT
tags:
  - windows 10
  - bash
  - shell
  - bash shell
  - subsystem
  - guide
  - linux
  - ubuntu
  - ubuntu 14.04
  - Guides
---

Windows 10 (the new Anniversary update, specifically) has a new feature called "Windows Subsystem for Linux". It's basically a full-fledged Ubuntu based bash shell running directly under Windows. Pretty cool, eh? This guide will show you how exactly to enable it.

<!--more-->
## What you need:

* A PC running 64-bit of Windows 10 Anniversary Update build 14393 or later (Step 1 shows you how to check your Windows 10 version).
* And as always, an internet connection.

## Step 1:

First, let's find out whether your Windows 10 is build 14393 or later.

To do this, simply open **Settings**

![Search for Settings in the Start menu](/assets/images/posts/2017-04-26-enabling-linux-bash-shell-in-windows-10-001.png "Search for Settings in the Start menu")

Click on **System**

![Select System](/assets/images/posts/2017-04-26-enabling-linux-bash-shell-in-windows-10-002.png "Select System")

Scroll to the end and click on **About**.
Here you'll see your **OS Build** number. This should be equal to or higher than **14393**. Also, verify if your Windows 10 installation is 64 bit.

If your build number is less than **14393**, check for updates.

![Click on About](/assets/images/posts/2017-04-26-enabling-linux-bash-shell-in-windows-10-003.png "Click on About")

## Step 2:

The next step is to enable **Developer Mode** in Windows 10.

Open **Settings** again. Select **Update & security**.

![Select Update & security in Settings](/assets/images/posts/2017-04-26-enabling-linux-bash-shell-in-windows-10-004.png "Select Update & security in Settings")

Click on **For developers** and enable **Developer mode**. If it asks you to restart the PC, go ahead and restart.

![Enable developer mode in Windows 10](/assets/images/posts/2017-04-26-enabling-linux-bash-shell-in-windows-10-005.png "Select For developers and enable developer mode")

**Note:** [If you get an error message **Developer mode package failed to install. Error code 0x80004005** while trying to enable developer mode, please click here to see how to fix it](/it/windows-10-developer-mode-fix-error-0x80004005/)

## Step 3:

Now, let's enable **Windows Subsystem for Linux**. Click the **Start** button and search for **Turn Windows features on or off**.

![Search for Turn Windows features on or off](/assets/images/posts/2017-04-26-enabling-linux-bash-shell-in-windows-10-006.png "Search for Turn Windows features on or off")

Check **Windows Subsystem for Linux (Beta)** to enable it and click **OK**

![Enable Windows Subsystem for Linux (Beta)](/assets/images/posts/2017-04-26-enabling-linux-bash-shell-in-windows-10-007.png "Enable Windows Subsystem for Linux (Beta)")

Restart your PC when it prompts you to.

<div class="row">
  <div class="col-12">
    {% include adsense-post-content.html %}
  </div>
</div>

## Step 4:

After you've rebooted your PC, open a command prompt window (click the Start button and type `cmd`).

Type `bash` and hit enter.

Since this is the first time you're running `bash`, you'll be asked whether you want to install it. Type `y` and hit enter to proceed.

![Installing bash via command prompt](/assets/images/posts/2017-04-26-enabling-linux-bash-shell-in-windows-10-008.png "Installing bash via command prompt")

After the installation is complete, you will be asked to create a new UNIX username and password. This user account is for the new Ubuntu environment and in no way related to your Windows account.

Well, that's all there is. You should have a bash prompt now and can run linux commands.

## Step 5:

To start `bash` you can use two ways:

* Simply open any command prompt window and type `bash`. It will start the Ubuntu command line environment.
* Click the Start button and search for **bash**. Open **Bash on Ubuntu for Windows**.

![Launching Bash on Ubuntu for Windows](/assets/images/posts/2017-04-26-enabling-linux-bash-shell-in-windows-10-008.png "Search for Bash on Ubuntu for Windows")

That's it!

**Note:** While in the Ubuntu environment, you can access your Windows drives under `/mnt/`. All Windows drives will be listed under this. You can `cd` to any directory and work with the files.

(header image source: [wall.alphacoders.com](https://wall.alphacoders.com/big.php?i=520207))
