---
id: 827
title: How to add MS SQL server as an ODBC data source?
date: 2015-06-17T05:29:51+00:00
author: wiseindy
comments: true
layout: single
guid: https://wiseindy.com/?p=827
header:
  image: /wp-content/uploads/2015/06/how-to-add-odbc-data-source_microsoft_sql_server.jpg
  teaser: /assets/images/featured/featured-odbc.jpg
redirect_from: "/it/how-to-add-ms-sql-server-as-an-odbc-data-source/"
categories:
  - Windows
tags:
  - connection
  - database
  - database connection
  - microsoft
  - ms sql
  - mssql
  - odbc
  - sql
  - sql server
  - Guides
---
<a target="_blank" href="https://en.wikipedia.org/wiki/Open_Database_Connectivity" target="_blank">ODBC</a> stands for <a target="_blank" href="https://en.wikipedia.org/wiki/Open_Database_Connectivity" target="_blank">Open Database Connectivity</a>. It is an API that allows you to access database systems. This connection was developed with an aim to make it independent of database systems and operating systems.

<!--more-->

In this quick guide, we will see how a connection can be established to a Microsoft SQL server on your network.
<h3>What you need:</h3>
<ul>
	<li>A Microsoft SQL Server (MS SQL) on the network.
<ul>
	<li>In this case, we will be connection to a server running Microsoft SQL Server 2005.</li>
</ul>
</li>
	<li>A normal PC on the network.
<ul>
	<li>In this example, I'll be using a workstation running Windows 7.</li>
</ul>
</li>
</ul>
<h3>Step 1:</h3>
Click the <strong>Start</strong> button. Either navigate to <strong>Administrative Tools &gt; Data Sources (ODBC)</strong> or simply search for <strong>ODBC</strong>.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/06/how-to-add-odbc-data-source_02.png"><img class="alignnone wp-image-829 size-medium" src="https://wiseindy.com/wp-content/uploads/2015/06/how-to-add-odbc-data-source_02.png" alt="how-to-add-odbc-data-source_02" /></a>  <a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/06/how-to-add-odbc-data-source_01.png"><img class="alignnone wp-image-828 size-medium" src="https://wiseindy.com/wp-content/uploads/2015/06/how-to-add-odbc-data-source_01.png" alt="How to add ODBC data source - Microsoft SQL Server" /></a>
<h3>Step 2:</h3>
In the <strong>ODBC Data Source Administrator</strong> window, click <strong>Add</strong>.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/06/how-to-add-odbc-data-source_03.png"><img class="alignnone size-full wp-image-830" src="https://wiseindy.com/wp-content/uploads/2015/06/how-to-add-odbc-data-source_03.png" alt="how-to-add-odbc-data-source_03" /></a>
<h3>Step 3:</h3>
Since we are going to be connecting to MS SQL Server 2005, select <strong>SQL server</strong> in the <strong>Create New Data Source</strong> window. Click <strong>Next</strong>.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/06/how-to-add-odbc-data-source_04.png"><img class="alignnone size-full wp-image-831" src="https://wiseindy.com/wp-content/uploads/2015/06/how-to-add-odbc-data-source_04.png" alt="how-to-add-odbc-data-source_04" /></a>

<div class="row">
  <div class="col-12">
    {% include adsense-post-content.html %}
  </div>
</div>

<h3>Step 4:</h3>
Type a <strong>Name</strong> for your data source. Next, enter the <strong>Server</strong> hostname or IP address. Click <strong>Next</strong>.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/06/how-to-add-odbc-data-source_05.png"><img class="alignnone size-full wp-image-832" src="https://wiseindy.com/wp-content/uploads/2015/06/how-to-add-odbc-data-source_05.png" alt="how-to-add-odbc-data-source_05" /></a>
<h3>Step 5:</h3>
Select <strong>With SQL Server authentication using a login ID and password entered by the user.</strong>

Enter the <strong>Login ID</strong> and <strong>Password</strong> for your SQL server. Click <strong>Next</strong>.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/06/how-to-add-odbc-data-source_06.png"><img class="alignnone size-full wp-image-833" src="https://wiseindy.com/wp-content/uploads/2015/06/how-to-add-odbc-data-source_06.png" alt="how-to-add-odbc-data-source_06" /></a>
<h3>Step 6:</h3>
Leave all settings as default and click <strong>Next</strong>.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/06/how-to-add-odbc-data-source_07.png"><img class="alignnone size-full wp-image-834" src="https://wiseindy.com/wp-content/uploads/2015/06/how-to-add-odbc-data-source_07.png" alt="how-to-add-odbc-data-source_07" /></a>
<h3>Step 7:</h3>
Leave all settings as default and click <strong>Finish</strong>.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/06/how-to-add-odbc-data-source_08.png"><img class="alignnone size-full wp-image-835" src="https://wiseindy.com/wp-content/uploads/2015/06/how-to-add-odbc-data-source_08.png" alt="how-to-add-odbc-data-source_08" /></a>
<h3>Step 8:</h3>
A window will pop up asking you whether you want to test the connection or not. Click <strong>Test Data Source... </strong>If all goes well, you should see a <strong>TESTS COMPLETED SUCCESSFULLY!</strong> message. Click <strong>OK</strong>.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/06/how-to-add-odbc-data-source_09.png"><img class="alignnone size-full wp-image-836" src="https://wiseindy.com/wp-content/uploads/2015/06/how-to-add-odbc-data-source_09.png" alt="how-to-add-odbc-data-source_09" /></a>

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/06/how-to-add-odbc-data-source_10.png"><img class="alignnone size-full wp-image-837" src="https://wiseindy.com/wp-content/uploads/2015/06/how-to-add-odbc-data-source_10.png" alt="how-to-add-odbc-data-source_10" /></a>
<h3>Step 10:</h3>
Your new ODBC data source has been successfully added. Now you can use this data source in different applications to connect and access data from your SQL server.

<a target="_blank" href="https://wiseindy.com/wp-content/uploads/2015/06/how-to-add-odbc-data-source_11.png"><img class="alignnone size-full wp-image-838" src="https://wiseindy.com/wp-content/uploads/2015/06/how-to-add-odbc-data-source_11.png" alt="how-to-add-odbc-data-source_11" /></a>
<h3>Further reading</h3>
<a target="_blank" href="https://msdn.microsoft.com/en-us/library/ms811006.aspx" target="_blank">https://msdn.microsoft.com/en-us/library/ms811006.aspx</a>

(header image source: <a target="_blank" href="https://www.thebigdatainsightgroup.com/site/topics/relational%20database" target="_blank">thebigdatainsightgroup.com</a>)
