---
id: 35
title: Why software projects fail?
date: 2007-12-09T06:44:20+00:00
author: Anay
layout: post
guid: http://anaykamat.com/2007/12/09/why-software-projects-fail/
permalink: /2007/12/09/why-software-projects-fail/
categories:
  - Programming
  - Technologies
---
Developing of software project is not just a task related to computer programming. Software development involves of lot planning, understanding of requirements, proper design, maintainability and of course, programming. As software planning involves so many tasks, it should be very easy to guess that software projects don’t fail just because of wrong programming, but mostly because, other tasks involved in software development are not handled properly. Recently, I got a chance to review some projects that are being developed in one educational institute in Goa. In this article, I will try to look at some faults that will eventually render these projects useless practically.

**Database security:** One of the projects developed inside the institute is to get the marks of students and prepare the report of failed students. The application is totally window based program developed in C# which connects to the central database. User need to start the program, login with his username as password, enter the marks for students and create report based on it. Looks like a perfect piece of software. But there is one major security loophole.

Management feels that the software is quite secure as no one can enter or change the marks unless the user logs in with his username and password. The biggest fault being overlooked here is an access to the central DBMS. The connection string required to connect to the central database is stored in a ‘application_name.exe.config’ file which is present in the same folder where application is installed. In other words, this simple text file is installed on every single client machine and any user can read it. Any student can directly login to the central database using the username and password mentioned in the connection string, and can change his marks or delete all records.

This problem could have been easily handled by creating a web service to handle the database tasks and by making the application use this web service. In this way, the connection string would have been in the ‘web.config’ file on the central server and away from any third party access.

**Password storage:** Care should be taken while user information is stored in the database. User sensitive information should be stored as securely as possible. This is one reason why normally people use MD5 to obtain the hashed password which is then stored in the database. MD5 is one way hash and it is not possible to obtain the original password from hash. People normally keep the same password for different accounts. For example, an user can have same password for his Gmail as well as Yahoo mail account. If the password is stored directly, an administrator having access to yahoo mail’s central database can easily obtain the password of the user and hack his gmail account.

There is another project being developed called inventory management system for the departmental stores. Here, the lead person wants the password not to be hashed but to be encrypted so that it could be retrieved back. Clearly, there is a big security loophole.

**Improper use of software development concepts:** Software could be programmed either in procedural way or in object oriented way. The program is being written in objected oriented language like C# doesn’t mean that program is object oriented. Program becomes object oriented when the whole program is designed using classes such that there is code reusability along with use of abstraction. Care should be taken that internal structure of class is not exposed. When software is developed in this way, it makes code more maintainable and extendable. Handling of bugs becomes much easier this way.

However, the lead person who is in charge of inventory management system wants the system to be developed neither in procedural nor in object oriented way. He wants to use something that he calls as “Hybrid” way of software development. I have never heard or seen any projects developed in this way. If someone knows, please let me know.

Software programming could be an easy task, but software development is definitely not an easy task. It needs lot of effort to design a software application and plan its development. Care must be taken while developing applications where security is going to play a key role. We should keep our mind open to learn from others mistakes and also from the approach followed by successful software developers. It takes time and hard work to develop a software application and thus, it’s the responsibility of every person involved in the project to develop it properly. Software should be designed to survive and not to fail.