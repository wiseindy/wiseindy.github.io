---
id: 849
title: How to import .CSV as external contacts in Exchange?
date: 2015-06-22T09:00:59+00:00
author: wiseindy
layout: post
guid: http://wiseindy.com/?p=849
permalink: /it/how-to-import-csv-as-external-contacts-in-exchange/
image: /wp-content/uploads/2015/06/import-csv-contacts-exchange.jpeg
categories:
  - Guides
  - IT
  - Powershell
tags:
  - cmdlet
  - contacts
  - csv
  - email
  - emails
  - exchange
  - exchange 2010
  - exchange 2013
  - import-csv
  - microsoft
  - microsoft exchange
  - new-mailcontact
  - outlook
  - powershell
  - windows
  - windows server
  - windows server 2008 r2
---
<h3>What you need:</h3>
<ul>
	<li>Microsoft Exchange Server
<ul>
	<li>In this guide ,we are using Microsoft Exchange 2010.</li>
</ul>
</li>
	<li>A specially formatted <strong>.CSV</strong> file.
<ul>
	<li>This is illustrated below.</li>
</ul>
</li>
</ul>
<!--more-->
<h3>Step 1:</h3>
Create a <strong>.CSV</strong> file with this format:

<a href="http://wiseindy.com/wp-content/uploads/2015/06/import-csv-contacts-exchange_01.png"><img class="alignnone size-full wp-image-850" src="http://wiseindy.com/wp-content/uploads/2015/06/import-csv-contacts-exchange_01.png" alt="import-csv-contacts-exchange_01" width="755" height="122" /></a>

Save it as <strong>contacts.csv</strong>. For the purpose of this guide, I have saved it to <strong>D:\contacts.csv</strong>

Also, make sure you have the Organizational Units (OUs) created in your Active Directory before proceeding. If not, you will get an error in <strong>Step 3</strong>.
<h3>Step 2:</h3>
Launch <strong>Exchange Management Shell</strong>.

<a href="http://wiseindy.com/wp-content/uploads/2015/06/import-csv-contacts-exchange_02.png"><img class="alignnone size-full wp-image-851" src="http://wiseindy.com/wp-content/uploads/2015/06/import-csv-contacts-exchange_02.png" alt="import-csv-contacts-exchange_02" width="405" height="464" /></a>

<a href="http://wiseindy.com/wp-content/uploads/2015/06/import-csv-contacts-exchange_03.png"><img class="alignnone size-full wp-image-852" src="http://wiseindy.com/wp-content/uploads/2015/06/import-csv-contacts-exchange_03.png" alt="import-csv-contacts-exchange_03" width="772" height="431" /></a>
<h3>Step 3:</h3>
Once it launches, type the following code:
<code>Import-Csv D:\contacts.csv | ForEach-Object { New-MailContact -Name $_."Name" -ExternalEmailAddress $_."Email" -FirstNa
me $_."FirstName" -OrganizationalUnit $_."Oupath" -Alias $_."Alias" }</code>

Hit <strong>Enter</strong> and you are done!

(header image source: <a href="http://www.freecodesource.com/wallpapers/wallpaper/Microsoft-Office-Logo/" target="_blank">freecodesource.com</a>)