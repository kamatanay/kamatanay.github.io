---
id: 31
title: Handling loss of data access due to server downtime
date: 2007-10-03T06:37:58+00:00
author: Anay
layout: post
guid: http://anaykamat.com/2007/10/03/handling-loss-of-data-access-due-to-server-downtime/
permalink: /2007/10/03/handling-loss-of-data-access-due-to-server-downtime/
categories:
  - Technologies
---
<span style="font-family: Georgia">On 28th and 29th of September 2007, P.C. College of Engineering had organized a technical event called &#8216;<a target="_blank" href="http://blitzkrieg.in" title="Blitzkrieg">Blitzkrieg 2007</a>&#8216;. I was involved in creating the script to allow users to register themselves as participants for various competitions. This simple script had two responsibilities.</span>
<!-- more -->
<ul type="disc">
  <li style="margin: 0in 0in 0pt; line-height: 15.6pt; tab-stops: list .5in" class="MsoNormal">
    <span style="font-family: Georgia">Registration of participants</span>
  </li>
  <li style="margin: 0in 0in 0pt; line-height: 15.6pt; tab-stops: list .5in" class="MsoNormal">
    <span style="font-family: Georgia">Listing of all participants</span>
  </li>
</ul>

<span style="font-family: Georgia">The script was pretty simple and worked fine till the day of event. Organizers were able to view all participants who had registered for competitions. However, during the day of event (</span><date Year="2007" Day="28" Month="9"><span style="font-family: Georgia">28th September 2007</span></date><span style="font-family: Georgia">), organizers faced a problem that we had not at all considered. The hosting plan for Blitzkrieg website had provided them with small bandwidth. Due to this, the allocated bandwidth got over on the day of event and organizers were unable to view the site and get participant&#8217;s list.</span><span style="font-family: Georgia">I had never experienced such a problem before. Was it possible for me to write a script in such a way to handle this situation? It was definitely not possible to increase the bandwidth using a PHP script, but yes, there was a trick that would have helped organizers to access the latest data.</span><span style="font-family: Georgia">Before understanding this hacky solution, let’s understand what the actual script used to do:</span>

<ol type="1">
  <li style="margin: 0in 0in 0pt; line-height: 15.6pt; tab-stops: list .5in" class="MsoNormal">
    <span style="font-family: Georgia">Display a registration form to the user</span>
  </li>
  <li style="margin: 0in 0in 0pt; line-height: 15.6pt; tab-stops: list .5in" class="MsoNormal">
    <span style="font-family: Georgia">Get the data provided by user and validate it</span>
  </li>
  <li style="margin: 0in 0in 0pt; line-height: 15.6pt; tab-stops: list .5in" class="MsoNormal">
    <span style="font-family: Georgia">If the data was valid, then store the data and send a mail to registered user (participant), informing him about successful registration.</span>
  </li>
</ol>

<span style="font-family: Georgia">Here, we would have added an extra step to send a mail to organizers after every successful registration with corresponding sql (insert or update sql). This would have given organizers a list of sql commands which if they could have executed on local database. This would have provided them with local access to list of participants even in case of bandwidth failure on central server.</span>

<p style="line-height: 15.6pt">
  <span style="font-family: Georgia">This solution is just a precautionary measure to handle such kind of situations. It has to be implemented before the problem occurs. In our case, we had to call the customer support of our web-host who acted quickly and increased the bandwidth, allowing organizers to view the list of participants.</span>
</p>
