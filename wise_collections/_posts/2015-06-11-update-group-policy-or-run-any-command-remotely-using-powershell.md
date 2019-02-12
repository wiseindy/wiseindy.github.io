---
id: 625
title: Update group policy (or run any command) remotely using Powershell
date: 2015-06-11T10:34:55+00:00
author: wiseindy
comments: true
layout: single
guid: https://wiseindy.com/?p=625
header:
  image: /wp-content/uploads/2015/06/poweshell.jpg
  teaser: /assets/images/featured/featured-powershell.jpg
redirect_from: "/it/update-group-policy-or-run-any-command-remotely-using-powershell/"
categories:
  - Windows
tags:
  - gpupdate
  - group policy
  - powershell
  - pstools
  - Guides
---
<p style="text-align: left;">This script allows you to run any command remotely using Powershell on your network. I usually use this to update group policy configurations on all PCs on my network remotely.</p>
<!--more-->
<blockquote>Note: In <strong>Windows Server 2012</strong> &amp; <strong>Windows Server 2012 R2</strong>, you can run the <code>Invoke-GPUpdate</code> PowerShell cmdlet ro refresh group policy on any <strong>Windows 8</strong> computers on your network. <a target="_blank" href="https://technet.microsoft.com/en-us/library/jj134201.aspx" target="_blank">More information here</a>.</blockquote>
<h3>What you will need:</h3>
<ul>
	<li>PsTools
<ul>
	<li>Download PsTools from here:
<a target="_blank" href="https://technet.microsoft.com/en-us/sysinternals/bb896649.aspx">https://technet.microsoft.com/en-us/sysinternals/bb896649.aspx</a></li>
</ul>
</li>
	<li>Domain admin permissions</li>
	<li>This small script
<ul>
	<li><code>PsExec.exe \\* -s cmd /C echo N | gpupdate /force</code></li>
</ul>
</li>
</ul>

<div class="row">
  <div class="col-12">
    {% include adsense-post-content.html %}
  </div>
</div>

<h3>What this script does:</h3>
<ul>
	<li>Remotely runs <code>gpupdate /force</code> on all workstations</li>
	<li>Selects "N" if it asks to logoff user</li>
</ul>
When you run it, you'll see some output like:
<code>Starting cmd on PC1-USRNAME... on PC1-USRNAME...
cmd exited on PC1-USRNAME with error code 0.</code>

"<code>error code 0</code>" means it has completed successfully without any errors.
<h3>Additional syntax:</h3>
<ul>
	<li>To run this script only on a specific computer, e.g., <code>PC1-USRNAME</code>,
replace "<code>\\*</code>" with "<code>\\PC1-USRNAME</code>" as shown below:
<code>PsExec.exe \\PC1-USRNAME -s cmd /C echo N | gpupdate /force</code></li>
	<li>To force a logoff after updating the group policy settings, use this:
<code>PsExec.exe \\* -s cmd /C echo Y | gpupdate /force</code></li>
	<li>To run any other command remotely, simply use the following syntax:
<code>PsExec.exe \\* -s cmd /C</code></li>
	<li>For example, to create a directory in all workstations, simply run:
<code>PsExec.exe \\* -s cmd /C mkdir C:\test</code></li>
</ul>
(header image source: <a target="_blank" href="https://interfaceit.com">interfaceit.com</a>)
