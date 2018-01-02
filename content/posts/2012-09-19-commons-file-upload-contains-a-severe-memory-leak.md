---
status: publish
published: true
title: Commons File Upload contains a severe memory leak
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img class=\"alignleft  wp-image-2284\" title=\"commons-file-upload\" src=\"http://blog.novoj.net/binary/2012/09/commons-file-upload.png\"
  alt=\"\" width=\"180\" height=\"60\" />Do you use <a href=\"http://commons.apache.org/fileupload/\"
  target=\"_blank\">Commons File Upload</a> library in your application? Do you use <a
  href=\"http://commons.apache.org/fileupload/apidocs/org/apache/commons/fileupload/disk/DiskFileItemFactory.html\"
  target=\"_blank\">DiskFileItemFactory</a> for storing big files to a temporary disk
  storage? Do you use <a href=\"http://commons.apache.org/io/api-release/org/apache/commons/io/FileCleaningTracker.html\"
  target=\"_blank\">FileCleaningTracker</a> to get rid of unused temporary files as
  it is recommended in documentation?\r\n\r\nIf so you probably have a memory leak
  in your application you don't know about.\r\n\r\n"
wordpress_id: 2283
wordpress_url: http://blog.novoj.net/?p=2283
date: '2012-09-19 21:12:10 +0200'
date_gmt: '2012-09-19 20:12:10 +0200'
categories:
- Programování
- Java
- Web
tags: []
comments:
- id: 93538
  author: Craig Doremus
  author_email: cdoremus@gmail.com
  author_url: http://
  date: '2012-09-21 17:12:27 +0200'
  date_gmt: '2012-09-21 16:12:27 +0200'
  content: Thank you for submitting a bug report and patch to Apache. I've read too
    many blog posts reporting bugs, but not following through the way you did.
---
<p><img class="alignleft  wp-image-2284" title="commons-file-upload" src="http://blog.novoj.net/binary/2012/09/commons-file-upload.png" alt="" width="180" height="60" />Do you use <a href="http://commons.apache.org/fileupload/" target="_blank">Commons File Upload</a> library in your application? Do you use <a href="http://commons.apache.org/fileupload/apidocs/org/apache/commons/fileupload/disk/DiskFileItemFactory.html" target="_blank">DiskFileItemFactory</a> for storing big files to a temporary disk storage? Do you use <a href="http://commons.apache.org/io/api-release/org/apache/commons/io/FileCleaningTracker.html" target="_blank">FileCleaningTracker</a> to get rid of unused temporary files as it is recommended in documentation?</p>
<p>If so you probably have a memory leak in your application you don't know about.</p>
<p><a id="more"></a><a id="more-2283"></a></p>
<p>Stored files are meant to be cleared when there is no reference to the FileItem instance created by this library. Or at least this is stated in the documentation:</p>
<p><em>"Such temporary files are deleted automatically, if they are no longer used (more precisely, if the corresponding instance of <strong>java.io.File</strong> is garbage collected. This is done silently by the <strong>org.apache.commons.io.FileCleaner</strong> class, which starts a reaper thread."</em></p>
<p>Whole logic is written in a very clever way excluding a little bug in DiskFileItemFactory class on this spot:</p>
<p>[source lang="java"]<br />
public FileItem createItem(String fieldName, String contentType,<br />
            boolean isFormField, String fileName) {<br />
   DiskFileItem result = new DiskFileItem(fieldName, contentType,<br />
                isFormField, fileName, sizeThreshold, repository);<br />
   FileCleaningTracker tracker = getFileCleaningTracker();<br />
   if (tracker != null) {<br />
      tracker.track(result.getTempFile(), this);<br />
   }<br />
   return result;<br />
}<br />
[/source]</p>
<p>On the place where tracker registers new file to track instance of <strong>this</strong> is passed there as a "marker" reference. This obviously means DiskFileItemFactory that is usually kept as a long living instance in the application. This marker is then propagated to this place:</p>
<p>[source lang="java"]<br />
private static final class Tracker extends PhantomReference {<br />
   private final String path;<br />
   private final FileDeleteStrategy deleteStrategy;</p>
<p>   Tracker(String path, FileDeleteStrategy deleteStrategy, Object marker, ReferenceQueue queue) {<br />
      super(marker, queue);<br />
      this.path = path;<br />
      this.deleteStrategy = (deleteStrategy == null ? FileDeleteStrategy.NORMAL : deleteStrategy);<br />
   }</p>
<p>   public boolean delete() {<br />
      return deleteStrategy.deleteQuietly(new File(path));<br />
   }<br />
}<br />
[/source]</p>
<p>And is used as a reference of the PhantomReference. This reference is then monitored for garbage collection instead FileItem instance as it should be according to documentation. Because DiskFileItemFactory is long living thing trackers in FileCleaningTracker only get collected and <a href="http://java.dzone.com/articles/finalization-and-phantom" target="_blank">NEVER get cleaned</a>!</p>
<p>We found this issue when experiencing OutOfMemory problems on our server that was undergoing a penetration test that tried to upload huge amount of files through open web form. Using <a href="http://www.eclipse.org/mat/" target="_blank">Eclipse MAT</a> we found out that there are more than 350 thousands of tracker objects inside FileCleaningTracker that are not cleared even after original requests and sessions were all dropped.</p>
<p>Please vote for <a href="https://issues.apache.org/jira/browse/FILEUPLOAD-189" target="_blank">this issue</a> if you want to see it resolved.</p>
<p>Meanwhile you can build your own version of the Commons File Upload with <a href="https://issues.apache.org/jira/secure/attachment/12545785/FILEUPLOAD-189.patch" target="_blank">this patch</a>.</p>
