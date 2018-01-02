---
status: publish
published: true
title: Mock FTP server - další perla do sbírky automatického testování
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Předevčírem se v mé RSS síti zachytila zajímavá zpráva, která dobře zapadá
  do katalogu řešení pro automatické testování. Jedná se o <a href=\"http://mockftpserver.sourceforge.net/stubftpserver-features.html\"
  target=\"_blank\">MockFtpServer</a>, který se velmi podobá přístupu SubEtha SMTP
  Serveru, se kterým mám velmi pozitivní zkušenosti.\r\n\r\n"
wordpress_id: 260
wordpress_url: http://blog.novoj.net/?p=260
date: '2008-12-24 11:09:05 +0100'
date_gmt: '2008-12-24 10:09:05 +0100'
categories:
- Programování
- Java
- Testování
tags: []
comments: []
---
<p>Předevčírem se v mé RSS síti zachytila zajímavá zpráva, která dobře zapadá do katalogu řešení pro automatické testování. Jedná se o <a href="http://mockftpserver.sourceforge.net/stubftpserver-features.html" target="_blank">MockFtpServer</a>, který se velmi podobá přístupu SubEtha SMTP Serveru, se kterým mám velmi pozitivní zkušenosti.</p>
<p><a id="more"></a><a id="more-260"></a></p>
<p>Princip je skutečně analogický zmiňovanému SubEtha SMTP Serveru, se kterým lze jednoduše ověřovat správné rozesílání emailů. Jednoduše nakonfigurujeme "virtuální" FTP server a nastartujeme jej na konkrétním portu. V testech pak můžeme ověřovat kód, který komunikuje s FTP serverem, aniž bychom museli vytvářet vlastní stub nebo mock objekty:</p>
<p>[source lang="java"]<br />
public class RemoteFileTest extends TestCase{</p>
<p>protected void setUp() throws Exception {<br />
   FakeFtpServer fakeFtpServer = new FakeFtpServer();<br />
   fakeFtpServer.addUserAccount(new UserAccount("user", "password", "c:\\data"));</p>
<p>   FileSystem fileSystem = new WindowsFakeFileSystem();<br />
   fileSystem.add(new DirectoryEntry("c:\\data"));<br />
   fileSystem.add(new FileEntry("c:\\data\\file1.txt", "abcdef 1234567890"));<br />
   fileSystem.add(new FileEntry("c:\\data\\run.exe"));<br />
   fakeFtpServer.setFileSystem(fileSystem);</p>
<p>   fakeFtpServer.setServerControlPort(9154);<br />
   fakeFtpServer.start();<br />
}</p>
<p>protected void tearDown() throws Exception {<br />
        fakeFtpServer.stop();<br />
}</p>
<p>}<br />
[/source]</p>
<p>V nastavení lze simulovat jak Windows filesystem (case-insensitive, opačná lomítka atd.), tak i Unix filesystem. Je možné poměrně detailně nastavovat oprávnění na jednotlivé složky / soubory, které server dále respektuje.</p>
<p>Ftp server lze konfigurovat i pomocí Springu a také je možné ovlivňovat jeho chování implementací vlastních CommandHandlerů, které zpracovávají jednotlivé FTP příkazy (to kdybychom chtěli simulovat nějaké exotičtější chování FTP serveru, nebo nějaké chybové stavy).</p>
<p>Myslím, že v některých případech může být použití této knihovny pro integrační testy aplikační logiky pracující s FTP protokolem velmi užitečné.</p>
