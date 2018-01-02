---
status: publish
published: true
title: Jak nainstalovat MySQL server na Windows Vista
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Nedávno jsme celá firma obnovili notebookový park a přešli na Windows Vista.
  Při zprovozňování infrastruktury jsem narazil na problém s instalací MySQL server
  verze 5.1. Instalace serveru jako taková proběhla bez potíží, když se ale měl nastartovat
  konfigurační průvodce pro zprovoznění serveru k ničemu nedošlo. V event logu windows
  jem narazil pouze na tuto hlášku:\r\n\r\n<i>Activation context generation failed
  for \"C:\\Program Files\\MySQL\\MySQL Server 5.1\\bin\\MySQLInstanceConfig.exe\".Error
  in manifest or policy file \"C:\\Program Files\\MySQL\\MySQL Server 5.1\\bin\\MySQLInstanceConfig.exe\"
  on line 6. The value \"asAdministrator\" of attribute \"level\" in element \"urn:schemas-microsoft-com:asm.v1^requestedPrivileges\"
  is invalid.</i>\r\n\r\n"
wordpress_id: 57
wordpress_url: http://blog.novoj.net/2008/03/29/jak-nainstalovat-mysql-server-na-windows-vista/
date: '2008-03-29 21:19:11 +0100'
date_gmt: '2008-03-29 20:19:11 +0100'
categories:
- Softwarové nástroje
tags: []
comments: []
---
<p>Nedávno jsme celá firma obnovili notebookový park a přešli na Windows Vista. Při zprovozňování infrastruktury jsem narazil na problém s instalací MySQL server verze 5.1. Instalace serveru jako taková proběhla bez potíží, když se ale měl nastartovat konfigurační průvodce pro zprovoznění serveru k ničemu nedošlo. V event logu windows jem narazil pouze na tuto hlášku:</p>
<p><i>Activation context generation failed for "C:\Program Files\MySQL\MySQL Server 5.1\bin\MySQLInstanceConfig.exe".Error in manifest or policy file "C:\Program Files\MySQL\MySQL Server 5.1\bin\MySQLInstanceConfig.exe" on line 6. The value "asAdministrator" of attribute "level" in element "urn:schemas-microsoft-com:asm.v1^requestedPrivileges" is invalid.</i></p>
<p><a id="more"></a><a id="more-57"></a></p>
<p>Po nějaké době hledání jsem objevil i <a href="http://bugs.mysql.com/bug.php?id=30823" target="_new">odpovídající issue na MySQL trackeru</a>. Řešení popsané Gunnarem Gudvardarsonem se nalézá v závěrečné části a je tak trochu hackerské :-) :</p>
<p>To install MySQL Server 5.0.51a in Vista</p>
<ol>
<li>Use mysql-essential-5.0.51a-win32.msi</li>
<li>Download and run Resource Hacker <a href="http://www.angusj.com/resourcehacker/" target="_new">http://www.angusj.com/resourcehacker/</a></li>
<li>Open ...\MySQL Server 5.0\bin\MySQLInstanceConfig.exe with Resource Hacker</li>
<li>Navigate to 24\1\1033</li>
<li>Delete all text in the window</li>
<li>Press "Compile script"</li>
<li>Exit Resource Hacker and save the result (overwrite the initial MySQLInstanceConfig.exe)</li>
<li>Now MySQLInstanceConfig.exe should start normally.</li>
</ol>
<p>Uvedený návod naštěstí funguje. Tak trochu se ale obávám, co bude za dalším rohem ;-)</p>
<h4>Migrace Putty</h4>
<p>Trochu nesouvisející informace, ale pokud se vám nechce přepisovat při migraci nastavení Putty, stačí postupovat podle tohoto návodu.</p>
<p><a href="http://www.downloadsquad.com/2007/02/01/howto-transfer-your-putty-settings-between-computers/" target="_new">http://www.downloadsquad.com/2007/02/01/howto-transfer-your-putty-settings-between-computers/</a></p>
