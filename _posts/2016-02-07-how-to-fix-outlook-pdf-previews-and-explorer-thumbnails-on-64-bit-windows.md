---
id: 1157
title: How to Fix Outlook PDF Previews and Explorer thumbnails on 64-bit Windows
date: 2016-02-07T03:47:20+00:00
author: wiseindy
layout: post
guid: http://wiseindy.com/?p=1157
permalink: /it/how-to-fix-outlook-pdf-previews-and-explorer-thumbnails-on-64-bit-windows/
dsq_thread_id:
  - "5585733488"
image: /wp-content/uploads/2016/02/how-to-fix-outlook-pdf-previews-and-explorer-thumbnails-on-64-bit-windows.jpg
featured: /images/featured/featured-outlookpreview.jpg
categories:
  - Guides
  - IT
tags:
  - "64"
  - 64 bit
  - acrobat
  - adobe
  - adobe acrobat
  - adobe acrobat reader
  - adobe pdf preview handler for vista
  - adobe reader
  - microsoft outlook
  - outlook
  - pdf
  - pdf handler
  - pdf previewer
  - reader
  - regedit
  - vista
  - windows 10
  - windows 7
  - windows 8
  - windows 8.1
  - x64
---
“This file cannot be previewed because of an error with the following previewer: PDF Preview Handler for Vista”.

You might've seen this pretty common error in Outlook when you cannot preview PDF files in the preview pane. This happens on 64-bit Windows.

Well, it's a pretty easy fix.

<!--more-->

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/02/how-to-fix-outlook-pdf-previews-and-explorer-thumbnails-on-64-bit-windows_02.png" rel="attachment wp-att-1159"><img class="alignnone size-full wp-image-1159" src="http://wiseindy.com/wp-content/uploads/2016/02/how-to-fix-outlook-pdf-previews-and-explorer-thumbnails-on-64-bit-windows_02.png" alt="how-to-fix-outlook-pdf-previews-and-explorer-thumbnails-on-64-bit-windows_02" /></a>
<h2>The manual way to fix this error</h2>
<h3>Step 1:</h3>
Click the <strong>Start</strong> button, type <strong>regedit.exe</strong> and open it.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/02/how-to-fix-outlook-pdf-previews-and-explorer-thumbnails-on-64-bit-windows_01.png" rel="attachment wp-att-1158"><img class="alignnone size-full wp-image-1158" src="http://wiseindy.com/wp-content/uploads/2016/02/how-to-fix-outlook-pdf-previews-and-explorer-thumbnails-on-64-bit-windows_01.png" alt="how-to-fix-outlook-pdf-previews-and-explorer-thumbnails-on-64-bit-windows_01" /></a>
<h3>Step 2:</h3>
Once open, navigate to <span style="color: #339966;"><code>HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Classes\
CLSID\{DC6EFB56-9CFA-464D-8880-44885D7DC193}</code></span>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/02/how-to-fix-outlook-pdf-previews-and-explorer-thumbnails-on-64-bit-windows_03.png" rel="attachment wp-att-1160"><img class="alignnone size-full wp-image-1160" src="http://wiseindy.com/wp-content/uploads/2016/02/how-to-fix-outlook-pdf-previews-and-explorer-thumbnails-on-64-bit-windows_03.png" alt="how-to-fix-outlook-pdf-previews-and-explorer-thumbnails-on-64-bit-windows_03" /></a>
<h3>Step 3:</h3>
Double-click <strong>AppID</strong> in the right column and copy paste this in the Value Data field:<span style="color: #339966;"> <code>{534A1E02-D58F-44f0-B58B-36CBED287C7C}</code></span>

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/02/how-to-fix-outlook-pdf-previews-and-explorer-thumbnails-on-64-bit-windows_04.png" rel="attachment wp-att-1161"><img class="alignnone size-full wp-image-1161" src="http://wiseindy.com/wp-content/uploads/2016/02/how-to-fix-outlook-pdf-previews-and-explorer-thumbnails-on-64-bit-windows_04.png" alt="how-to-fix-outlook-pdf-previews-and-explorer-thumbnails-on-64-bit-windows_04" /></a>

Click <strong>OK</strong> and close regedit. That's it!

<div class="row">
  <div class="col-12">
    {% include adsense-post-content.html %}
  </div>
</div>

<h2>The automatic way to fix this error</h2>
<h3>Step 1:</h3>
Download the Adobe Reader preview handler x64 fixer by <a target="_blank" href="http://www.pretentiousname.com/" target="_blank">Leo Davidson</a>, from this link: <a target="_blank" href="http://www.pretentiousname.com/adobe_pdf_x64_fix/#downl" target="_blank">http://www.pretentiousname.com/adobe_pdf_x64_fix/#downl</a>

You could download either with installer or without. I choose to do the one without the installer.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/02/how-to-fix-outlook-pdf-previews-and-explorer-thumbnails-on-64-bit-windows_05.png" rel="attachment wp-att-1162"><img class="alignnone size-full wp-image-1162" src="http://wiseindy.com/wp-content/uploads/2016/02/how-to-fix-outlook-pdf-previews-and-explorer-thumbnails-on-64-bit-windows_05.png" alt="how-to-fix-outlook-pdf-previews-and-explorer-thumbnails-on-64-bit-windows_05" /></a>
<h3>Step 2:</h3>
Extract the downloaded files. You'll see two folders. Open the one that says <strong>"Fix for x64 Adobe Reader preview handler"</strong>.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/02/how-to-fix-outlook-pdf-previews-and-explorer-thumbnails-on-64-bit-windows_06.png" rel="attachment wp-att-1163"><img class="alignnone size-full wp-image-1163" src="http://wiseindy.com/wp-content/uploads/2016/02/how-to-fix-outlook-pdf-previews-and-explorer-thumbnails-on-64-bit-windows_06.png" alt="how-to-fix-outlook-pdf-previews-and-explorer-thumbnails-on-64-bit-windows_06" /></a>

Run the preview handler fix utility and click <strong>Apply Fix</strong>.

<a target="_blank" href="http://wiseindy.com/wp-content/uploads/2016/02/how-to-fix-outlook-pdf-previews-and-explorer-thumbnails-on-64-bit-windows_07.png" rel="attachment wp-att-1164"><img class="alignnone size-full wp-image-1164" src="http://wiseindy.com/wp-content/uploads/2016/02/how-to-fix-outlook-pdf-previews-and-explorer-thumbnails-on-64-bit-windows_07.png" alt="how-to-fix-outlook-pdf-previews-and-explorer-thumbnails-on-64-bit-windows_07" /></a>

That's it!

(header image source: <a target="_blank" href="http://blog.automart.co.za/wp-content/uploads/2015/01/trying_to_figure_out_car_trouble.jpg" target="_blank">automart.co.za</a>)
