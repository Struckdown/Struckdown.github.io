---
layout: default
title: Outdoors Club Rental System
permalink: /OutdoorsClub/
---

In Fall 2018, I took CMPUT 401: Software Process/Product Management, which has us take on a real-world project for the course of the semester. Normally you get teams of around 4-6 people who work on this project for the semester, and then hand it off to the client at the end, which might get used if it's sufficiently good enough. We ended up having an 8 person team and were tasked with working with the [University of Alberta Outdoors Club](https://outdoorsclub.ca) to create an online rental system to replace their current paper-heavy one.

Our team was composed of:
* [Boris Fleysher](https://github.com/Struckdown)
* [Bennett Hreherchuk](https://github.com/Hreherch)
* [Ceegan Hale](https://github.com/Perplex)
* [Alex Dong](https://github.com/dong-alex)
* [Henry Tang](https://github.com/Hk-tang)
* [Shardul Shah](https://github.com/shardul-shah)
* [David Laycock](https://github.com/LaycockD)
* [Kevin Chang](https://github.com/hiufungk)

We ended up successfully creating a rental system that allows for users to rent out equipment and pay for it online through PayPal. Executives help facilitate the rental process by modifying the status of reservations once users come in to actually take out the gear and return it. Admins have full control and can modify what gear is available, who can rent out and even change system variables such as how far in advance equipment can be rented out, how much equipment can be rented at once, and so forth. The system also features automatic emails to remind users that gear is to be picked up soon, due soon or overdue.

![Screenshot of Rental Page](RentalPage.png)

To actually develop this application, we divided into two teams, the front-end and the backend. Ceegan, Shardul and I composed the backend team, while Ben, Alex, Henry, David and Kevin worked on the front-end. The backend worked with Django (using Python), REST framework, SMTP and the Paypal API while the front-end dealt primarily with React. I worked with setting up backend calls that modified the state of the database, such as updating member lists, blacklists, gear, gear status, reservations and system variables. Likewise, for every function I implemented, I was responsible for writing the tests associated with it. I was also the primary point of contact with the Outdoors Club, helping organize meetings and dealing with emails.
