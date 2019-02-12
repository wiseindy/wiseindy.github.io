---
id: 849
title: How to import .CSV as external contacts in Exchange?
date: 2015-06-22T09:00:59+00:00
author: wiseindy
comments: true
layout: single
guid: https://wiseindy.com/?p=849
header:
  image: /wp-content/uploads/2015/06/import-csv-contacts-exchange.jpeg
  teaser: /assets/images/featured/featured-csv.jpg
redirect_from: "/it/how-to-import-csv-as-external-contacts-in-exchange/"
categories:
  - Windows
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
  - Guides
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

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/06/import-csv-contacts-exchange_01.png"><img class="alignnone size-full wp-image-850" src="https://wiseindy.com/wp-content/uploads/2015/06/import-csv-contacts-exchange_01.png" alt="import-csv-contacts-exchange_01" /></a>

Save it as <strong>contacts.csv</strong>. For the purpose of this guide, I have saved it to <strong>D:\contacts.csv</strong>

Also, make sure you have the Organizational Units (OUs) created in your Active Directory before proceeding. If not, you will get an error in <strong>Step 3</strong>.

<div class="row">
  <div class="col-12">
    {% include adsense-post-content.html %}
  </div>
</div>

<h3>Step 2:</h3>
Launch <strong>Exchange Management Shell</strong>.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/06/import-csv-contacts-exchange_02.png"><img class="alignnone size-full wp-image-851" src="https://wiseindy.com/wp-content/uploads/2015/06/import-csv-contacts-exchange_02.png" alt="import-csv-contacts-exchange_02" /></a>

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/06/import-csv-contacts-exchange_03.png"><img class="alignnone size-full wp-image-852" src="https://wiseindy.com/wp-content/uploads/2015/06/import-csv-contacts-exchange_03.png" alt="import-csv-contacts-exchange_03" /></a>
<h3>Step 3:</h3>
Once it launches, type the following code:
<code>Import-Csv D:\contacts.csv | ForEach-Object { New-MailContact -Name $_."Name" -ExternalEmailAddress $_."Email" -FirstNa
me $_."FirstName" -OrganizationalUnit $_."Oupath" -Alias $_."Alias" }</code>

Hit <strong>Enter</strong> and you are done!

(header image source: <a target="_blank" href="https://www.freecodesource.com/wallpapers/wallpaper/Microsoft-Office-Logo/" target="_blank">freecodesource.com</a>)
