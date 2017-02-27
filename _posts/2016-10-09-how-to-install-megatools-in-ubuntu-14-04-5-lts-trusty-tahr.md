---
id: 1232
title: How to install megatools in Ubuntu 14.04.5 LTS (Trusty Tahr)
date: 2016-10-09T05:43:44+00:00
author: wiseindy
layout: post
guid: https://wiseindy.com/?p=1232
permalink: /it/how-to-install-megatools-in-ubuntu-14-04-5-lts-trusty-tahr/
dsq_thread_id:
  - "5585733554"
image: /wp-content/uploads/2016/10/how-to-install-megatools-in-ubuntu-14-04-5-lts-trusty-tahr.jpg
categories:
  - Guides
  - IT
tags:
  - "14.04"
  - download
  - guide
  - linux
  - mega
  - mega.nz
  - megacopy
  - megadf
  - megadl
  - megafs
  - megaget
  - megals
  - megamkdir
  - megaput
  - megareg
  - megarm
  - megastream
  - megatools
  - ubuntu
  - ubuntu 14.04
---
Megatools is a great collection of command line utilities that allow you to interact with your <a target="_blank" href="https://mega.nz">mega.nz</a> account directly from the command line. You can directly download using the cli on your Ubuntu machine. They are a great set of tools, however, installing them does get confusing for a new Linux user. This guide will show you how to install it and set it up in no time.

<!--more-->
<h3>What you need:</h3>
<ul>
 	<li>SSH or terminal access to an Ubuntu 14.04 server.</li>
 	<li>An internet connection (duh).</li>
</ul>
<h3>Step 1:</h3>
First you need to find out what's the latest version of megatools available.

To find out the latest version, simply visit any one of the links below and see what's the latest version number:
<ul>
 	<li><a target="_blank" href="https://megatools.megous.com/">https://megatools.megous.com/</a></li>
 	<li><a target="_blank" href="https://github.com/megous/megatools">https://github.com/megous/megatools</a></li>
</ul>
At the time of writing this article (9 October 2016), the latest version was <code>1.9.97</code>. If it is different in your case, simply replace <code>1.9.97</code> with your version in all the commands below.
<h3>Step 2:</h3>
Open your Ubuntu terminal (or SSH to it) and type in the following commands one after the other.
``` shell
sudo apt-get update
```
Run this command to download the package lists from the repositories and "update" them to get information on the newest versions of packages and their dependencies.
``` shell
sudo apt-get install libtool libglib2.0-dev gobject-introspection libgmp3-dev nettle-dev asciidoc glib-networking openssl libcurl4-openssl-dev libssl-dev
```
This installs all the dependencies that you may need to compile megatools from source.
``` shell
wget http://megatools.megous.com/builds/megatools-1.9.97.tar.gz
```
<code>wget</code> is used to download the latest megatools. Replace <code>1.9.97</code> with the latest version is available.
``` shell
zcat megatools-1.9.97.tar.gz > megatools-1.9.97.tar
tar -xf megatools-1.9.97.tar
```
Use <code>zcat</code> to decompress the downloaded file and <code>tar -xf</code> to extract the contents to a folder.
``` shell
cd megatools-1.9.97/
./configure
make
sudo make install
```
Finally, run the above commands to compile megatools and install it in your system.

<div class="row">
  <div class="col-12">
    {% include adsense-post-content.html %}
  </div>
</div>

<h3>Step 3:</h3>
If all went well, you should now have megatools installed on your system.

To download from a <a target="_blank" href="https://mega.nz">mega.nz</a> link, simply type <code>megadl '&lt;link&gt;'</code> and the download will start.

Here's an example:
``` shell
megadl 'https://mega.nz/#G!IK9KLpRS8J1h82Kpa0kWJkPwDh!2adB'
```
For syntax of other commands, type
``` shell
man megatools
```
That's it. You're done!
