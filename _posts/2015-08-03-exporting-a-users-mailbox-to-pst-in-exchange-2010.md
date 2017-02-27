---
id: 947
title: 'How to export a user&#8217;s mailbox to .pst in Exchange 2010'
date: 2015-08-03T02:01:39+00:00
author: wiseindy
layout: post
guid: http://wiseindy.com/?p=947
permalink: /it/exporting-a-users-mailbox-to-pst-in-exchange-2010/
image: /wp-content/uploads/2015/08/Mailbox.jpg
categories:
  - Exchange
  - Guides
  - IT
  - Powershell
tags:
  - emc
  - exchange
  - exchange 2010
  - exchange management shell
  - export
  - mailbox
  - mailboxexportrequest
  - microsoft
  - microsoft exchange
  - powershell
  - pst
---
A mailbox export request is a process of exporting mailbox or archive data to a <code>.pst</code> file. It's very simple to do with Exchange Management Shell.

<!--more-->

The first thing you need to know is that <a href="https://msdn.microsoft.com/en-us/library/cc505910.aspx" target="_blank">Exchange Management <strong>Shell</strong></a> is not the same as <a href="https://msdn.microsoft.com/en-us/library/cc505909.aspx" target="_blank">Exchange Management <strong>Console</strong></a>. As the name suggests, the <strong>Shell</strong> is a Powershell based command-line interface to manage Exchange.
<h3>Before you begin</h3>
<ol>
	<li>The first thing to keep in mind that you can <strong>only export to a UNC path.</strong></li>
	<li><strong>Exchange Trusted Subsystem</strong> security group needs to have <strong>modify</strong> NTFS permissions on the destination folder.</li>
</ol>
<h3>Let's export</h3>
To export, simply fire up the <strong>Exchange Management Shell</strong> and use the <code>New-MailboxExportRequest</code> cmdlet. Lets assume that the user whose mailbox we are exporting is called "John Doe" and his username is "johndoe"
<pre>New-MailboxExportRequest -Mailbox johndoe -FilePath "\\server\folder\file.pst"</pre>
You can start many export requests at the same time. They will be added to the queue.

<strong>Note</strong>: You may get an error as follows:
<pre>The term "New-MailboxExportRequest" is not recognized.</pre>
This may happen because of missing roles. In order to resolve this issue, grant the account performing the export request the ‘Import Export Mailbox’ role assignment.
<pre>New-ManagementRoleAssignment –Role “Mailbox Import Export” –User "DOMAIN\USER"</pre>
Restart your powershell session and try again.
<h3>See the export status</h3>
To see the status while it is exporting, use this cmdlet:
<pre>Get-MailboxExportRequest</pre>
You can use various formatting options:
<pre>Get-MailboxExportRequest | Format-List</pre>
<pre>Get-MailboxExportRequest | Format-Wide -Property Mailbox</pre>
<pre>Get-MailboxExportRequest | Format-Table</pre>
<pre>Get-MailboxExportRequest | Format-Table -Wrap</pre>
<pre>Get-MailboxExportRequest | Format-Table -Property Mailbox, Status</pre>
<h3>Clear completed export requests</h3>
Completed mailbox export requests aren't cleared automatically. You can remove fully or partially completed mailbox export requests by using the following cmdlets.

This will remove the export request <strong>only</strong> for the user "John Doe".
<pre>Remove-MailboxExportRequest -Identity "John Doe\MailboxExport"</pre>
This will remove <strong>all</strong> completed export requests.
<pre>Get-MailboxExportRequest -Status Completed | Remove-MailboxExportRequest</pre>
To read more about exporting mailboxes, you can check out <a href="https://technet.microsoft.com/en-us/library/ff459227(v=exchg.141).aspx" target="_blank">this TechNet article</a> by Microsoft.

(header image source: <a href="http://www.wallpaperscastle.com/free-mood-desktop-wallpaper-11761.html" target="_blank">wallpaperscastle.com</a>)