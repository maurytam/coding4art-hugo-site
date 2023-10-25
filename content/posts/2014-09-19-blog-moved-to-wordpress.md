---
title: Blog moved to WordPress
author: mtammacco
type: post
date: 2014-09-18T22:10:09+00:00
url: /archive/2014/09/19/blog-moved-to-wordpress.aspx
categories:
  - Troubleshooting
tags:
  - SubText
  - WordPress

---
It’s long time I don’t write anything on this blog, I was very busy in recent times, but now the time has come and I intend to regain the time lost.

When I came back to this blog, the first thing I noticed were the look & feel and the software engine on which it was based, SubText, a very old bog software, but still widely used, so I decided to move it to another platform, possibly in step with times, and my choice was WordPress.

Now this blog is based on WordPress engine <span style="color: #444444; font-family: 'Open Sans', 'Helvetica Neue', sans-serif; font-size: 15px; line-height: 24px;">t</span><span style="color: #444444; line-height: 24px;">he most popular online publishing platform, currently powering more than 20% of the web.</span>

<span style="color: #444444;"><span style="line-height: 24px;">Here are the necessary steps (and troubleshooting) to move an entire blog content based on SubText to WordPress:</span></span>

<span style="color: #444444;"><span style="line-height: 24px;"><b>STEP 1: Subtext &#8211; Export your blog content</b></span></span>

<span style="color: #444444;"><span style="line-height: 24px;">This is a “one choice” step, because SubText exports its content only in BlogML format, based on XML, and creates an XML file with all your posts, your categories and son forth. To accomplish this, logon to SubText as administrator, go to “Options > Import/Export” and click on the Save button. The check “embed attachment” must remain unchecked otherwise WordPress won’t be able to import the file.</span></span>

<span style="color: #444444;"><span style="line-height: 24px;">The file’s content is base64 encoded, so I was recommended to convert it as normal text. Don’t worry, fortunately there always are other people who had before the same problem as you had. Not that writing a very little program that convert the file’s content from base64 encode to normal text is a particularly difficult task, but if things are already done it’s better! So if you surf <a href="http://garfoot.com/blog/2010/08/importing-blogml-into-wordpress/">here</a> you can copy and past the code, compile it, run it, and have the file correctly converted.</span></span>

<b style="color: #444444; line-height: 24px;">STEP 2: WordPress &#8211; configure the permalink structure</b><span style="color: #444444;"><br /> </span>

<span style="color: #444444;"><span style="line-height: 24px;">This step is strongly recommended if you don’t want that the structure of all URL’s doesn’t change compared to the URL’s structure of the SubText blog.so as not to lose the Google indexing of your blog. Then the URL’s structure of the WordPress based blog must remain the same.</span></span>

<span style="color: #444444;"><span style="line-height: 24px;">To accomplish this, you need to change the permalink structure in WordPress. After you login as administrator, go to “Settings > Permalink” and check “Custom structure”, then typing this URL structure:</span></span>

> **<span style="letter-spacing: 0px; font-family: Courier;">/archive/%year%/%monthnum%/%day%/%postname%.aspx</span>**

This is exactly the URL’s structure used by SubText. Note the “ASPX” suffix, even if WordPress isn’t an ASP .NET application.

This picture may helps:

<img loading="lazy" src="http://coding4art.com/wp-content/uploads/2014/09/Schermata1.png" alt="Schermata 2014-09-18 alle 22.59.53.png" width="857" height="160" /> 

<b style="color: #444444; line-height: 24px;">STEP 3: WordPress &#8211; import your blog using the BlogML WordPress plugin importer.</b>

This plugin is built in into WordPress installation, so it’s nothing to download and install. Just click to “Tools > Import” and then choose BlogMl importer, upload the file XML generated at step 1 and click the button “Upload file and import”<b style="color: #444444; line-height: 24px;"><br /> </b>

<img loading="lazy" src="http://coding4art.com/wp-content/uploads/2014/09/Schermata-2014-09-18-alle-23.10.10.png" alt="Schermata 2014-09-18 alle 23.10.10.png" width="668" height="235" /> 

Just a few seconds and your blog is imported in WordPress and is up and running!

<b style="color: #444444; line-height: 24px;">STEP 4: WordPress &#8211; troubleshooting.</b>

1) The BlogML Importer plugin doesn’t import blog categories correctly. They have been imported with the ID they had in SqlServer SubText repository in place of description. You must correct them manually.

2) The RSS Feed wasn’t generated correctly; the procedure ended with a XML parsing error, as shown in this picture:

<img loading="lazy" src="http://coding4art.com/wp-content/uploads/2014/09/Schermata-2014-09-18-alle-23.34.06.png" alt="Schermata 2014-09-18 alle 23.34.06.png" width="596" height="125" /> 

and it seems to be related to some whitespace or blank lines into the various *.php files of the WordPress installation, or with custom permalinks that break RSS feed, like they said [here][1]

This problem was quite difficult to resolve and it took several time and Google searching.

Initially I founded this [WordPress Fix plugin][2], I tried it but it fixed anything, on the contrary it said that my RSS feed was working well and that all was fine!

After an hour of Google searching, I found the solution in this [Peter Krzyzek’s post][3], and I can never be grateful enough to the author for having solved this problem.

These are the steps you have to do:

&#8211; Download this: <http://wejn.org/stuff/wejnswpwhitespacefix.php> (this is a php file)

&#8211; Copy this file in the ROOT folder of your WordPress installation

&#8211; Edit the index.php file in the ROOT folder and add the followings:

<span style="background-color: #f7f7f9;"><span style="color: #dd1144; font-family: Monaco, Menlo, Consolas, 'Courier New', monospace;"><span style="line-height: 18px; white-space: nowrap;">include(“wejnswpwhitespacefix.php&#8221;);</span></span></span>

after the first line, e.g. just after the **<?php** line

&#8211; Reload the page and….BOOM….IT WORKED!!!!!!

I don’t know anything about php, I’m a .Net developer, and without that post I will never solve this problem.

Thank you Peter!

 [1]: https://wordpress.org/support/topic/custom-permalinks-break-rss-feeds
 [2]: https://wordpress.org/plugins/fix-rss-feed/
 [3]: http://www.piotrkrzyzek.com/wordpress-remove-blank-line-from-rss-feed-wordpress-error-on-line-2-at-column-6-xml-declaration-allowed-only-at-the-start-of-the-document/