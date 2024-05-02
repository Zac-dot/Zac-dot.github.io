---
aliases: webportfolio
tags: portfolio
layout: page
title: Portfolio
permalink: /portfolio/
date created: Monday, December 19th 2022, 10:58:17 pm
date modified: Thursday, May 2nd 2024, 12:27 pm 
---

---
## Projects and Descriptions

Each of these projects are viewable (along with source code) on my GitHub page. You can view this by clicking the link on Viewable at, or by the GitHub logo at the bottom of the page.

---

#### Learnix - Senior Capstone Project

<p align="center">
  <img src="{{site.baseurl}}/assets/images/portfolio/learnix-mobile.png" style="border-radius:4px"/>
</p>

**Viewable at:** [EvilDragovka/Capstone_Project_One](https://github.com/EvilDragovka/Capstone_Project_One) <br>
Tech used: Python, TypeScript, JavaScript, Node.js, LangChain, Capacitor (JS -> Android Webview), Llama2, Flask <br>
Time to make: 2 months<br>
Learned:
- How to develop an Android application utilizing generative AI
- Work and communicating efficiently as part of a six person team
- Utilizing Flask as a backend to route API requests to database and AzureAI
- Integrating Llama2-70B-Chat model into the application, ensuring safety for academic use, and enabling external connections to Wikipedia, arXiv, and DuckDuckGo Search
- Utilzing LangChain to handle system prompts, routing logic, user memory of last 4 search and response pairs, and Requests Python library
- Deploying a server on AWS for Flask, and using NGINX to handle IP and connection logic between the Android Application and the backend
- Using Capacitor to translate code for the frontend from TypeScript and JavaScript to an Android Webview based application wth Node.js

Description: This project was a part of a senior capstone where I, alongside 5 other individuals, had a goal make an Android application that integrated a LLM for academic usage targeted at college students.

---

#### TEAccountingProject

<p align="center">
  <img src="{{site.baseurl}}/assets/images/portfolio/phase3repo.jpg" style="border-radius:4px"/>
</p>

**Viewable at:** [Zac-dot/TEAccountingProject](https://github.com/Zac-dot/TEAccountingProjec) <br>
Tech used: Java, JavaFX, MySQL Database, Git<br>
Time to make: 2 weeks<br>
Learned:
- How to make multiple scenes in JavaFX and query data with Text Fields, Grids, and more
- Using DBConnector with a MySQL database to save, edit, query, and pull information from tables.
- Making different text and other object display based on if an admin or user was using an application
- How to communicate with another teammate in a timely manner to complete the project
- Using Git to pull and push changed files as needed to collaborate.

Description: This was a group project with another person. The goal of the application was to create a demo that an accounting firm might use for its internal bookkeeping, using a MySQL database in the background to keep information, with a GUI made using JavaFX and Java. In this example, the application is called T&E Accounting, taking the initial from each group projects last name. There are 2 different login screens, one for admins and another for users (or clients in this example), each displaying information on orders made, as well as making a new order or talking to a client through a command prompt.

One caveat of the project was that JavaFX and the code used in Java had problems when it came to displaying some information in the UI. Specifically, on the order screens for both, JavaFX would through an error about a null value and fail to populate the screen, however, the information would be in the database and as a workaround, the information is displayed to the console in case a user would like to see or know about the information.

---

#### Pianotoy

<p align="center">
	<img src="{{site.baseurl}}/assets/images/portfolio/pianotoy.jpg" style="border-radius:4px"/>
</p>

**Viewable at:** [Zac-dot/Pianotoy](https://github.com/Zac-dot/Pianotoy) <br>
Tech used: C++, GTK 4<br>
Time to make: 2 weeks<br>
Learned:
- Using GTK 4 Framework in conjunction with C++ code
- How to make a GUI application in C++
- Invoking system libraries to play audio or change terminal colors
- Basics of C++ and showing such in the application

Description: 
This is meant to be a simple program to demonstrate my abilities to use C++ and the GTK UI framework to display a UI. It is a simple small keyboard that displays 7 buttons, each of which plays a .wav audio file when pressed. Each key has a letter on it corresponding to the note to play. The pitch of the notes that are played can be altered through the **Note** button in the menubar.

The program was also used as a final project for my C++ class, specifically CS 361. As such, some additional features were added in order to hit what was required, such as the **Shapes** button in the menubar. While these do not have much to do with a keyboard, they were added for that reason, and can be removed if desired.

