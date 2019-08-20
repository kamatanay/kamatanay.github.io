---
id: 55
title: Fixing NTLM authentication in Windows 2003
date: 2008-10-28T05:20:46+00:00
author: Anay
layout: post
guid: http://anaykamat.com/?p=55
permalink: /2008/10/28/fixing-ntlm-authentication-in-windows-2003/
categories:
  - Technologies
  - Tips
tags:
  - active directory
  - alfresco
  - NTLM
  - windows 2003
  - windows xp
---
We had an application written in C# .Net, which used to communicate with Alfresco Enterprise Document/Content Management System. The application was using Alfresco’s NTLM component for authenticating users against their AD (Active Directory) user account.

The application worked perfectly while we were testing it on Windows XP system. However, on Windows 2003 64 Bit system, the application started failing as it could not authenticate users on alfresco server using NTLM.

So we had a situation where NTLM authentication used to fail only when our application was running on Windows 2003 Operating System. We tried disabling “Internet Explorer Enhanced Security Configuration”, but it didn’t help. Finally, after spending a lot of time on Google, we came across following article on Microsoft Knowledge Base:

> **&#8220;<a title="Microsoft Knowledge Base Article Link" href="http://support.microsoft.com/kb/954387" target="_blank">You may experience authentication issues when you access a network-attached storage device after you upgrade to Windows Server 2008, to Windows Vista, to Windows Server 2003, or to Windows XP</a>&#8220;**

This article talks about configuring the system to use appropriate NTLM version. In our Windows 2003 system, the value of **“lmcompatibilitylevel”** (Under **HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\LSA** subkey) was set to **2**. We just changed this value to **1**, and the client application started working properly in Windows 2003 system as well.

If you are also facing a similar issue on Windows 2003, then you can try the solution mentioned here. If setting the value of “lmcompatibilitylevel” to 1 makes no difference, then change this value to 0, which is the default value of “lmcompatibilitylevel” in Windows XP.