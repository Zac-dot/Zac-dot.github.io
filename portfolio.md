---
aliases: webportfolio
tags: portfolio
layout: page
title: Portfolio
permalink: /portfolio/
date created: Monday, December 19th 2022, 10:58:17 pm
date modified: Tuesday, December 20th 2022, 12:28:28 am
---

## Projects and Descriptions

Each of these projects are viewable (along with source code) on my GitHub page. You can view this by clicking the link on Viewable at, or by the GitHub logo at the bottom of the page.

### Pianotoy

<p align="center">
	<img src="{{site.baseurl}}/assets/images/pianotoy.jpg" />
</p>

Viewable at: [Zac-dot/Pianotoy](https://github.com/Zac-dot/Pianotoy) <br>
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

### Phase3Repo

<p align="center">
  <img src="{{site.baseurl}}/assets/images/phase3repo.jpg" />
</p>

Viewable at: [Zac-dot/Phase3Repo](https://github.com/Zac-dot/Phase3Repo) <br>
Tech used: Java, JavaFX, MySQL Database, Git<br>
Time to make: 2 weeks<br>
Learned:
- How to make multiple scenes in JavaFX and query data with Text Fields, Grids, and more
- Using DBConnector with a MySQL database to save, edit, query, and pull information from tables.
- Making different text and other object display based on if an admin or user was using an application
- How to communicate with another teammate in a timely manner to complete the project
- Using Git to pull and push changed files as needed to collaborate.

Description: **This was a group project with another person.** The goal of the application was to create a demo that an accounting firm might use for its internal bookkeeping, using a MySQL database in the background to keep information, with a GUI made using JavaFX and Java. In this example, the application is called T&E Accounting, taking the initial from each group projects last name. There are 2 different login screens, one for admins and another for users (or clients in this example), each displaying information on orders made, as well as making a new order or talking to a client through a command prompt.

One caveat of the project was that JavaFX and the code used in Java had problems when it came to displaying some information in the UI. Specifically, on the order screens for both, JavaFX would through an error about a null value and fail to populate the screen, however, the information would be in the database and as a workaround, the information is displayed to the console in case a user would like to see or know about the information.

### Letsguess-project

<p align="center">
  <img src="{{site.baseurl}}/assets/images/letsguess.jpg" />
</p>

Viewable at: [Zac-dot/Letsguess-project](github.com/Zac-dot/Letsguess-project) <br>
Tech used: Java<br>
Time to make: 1 week<br>
Learned:
- The basics of Java and displaying them in the source code.
- Displaying of information and handling human enter information
- Outputting information that was printed to console for later use
- Using a random number function to keep things interesting for the user.

Description:
This program is supposed to be a simple game about guessing numbers. You select how many numbers you wish to guess, and then you attempt to figure out what each number is (between 0 and 10). The main goal of the game is to correctly guess what the numbers are in under three tries. This uses a command line to play, as it does not use or make a GUI application at all, and is meant to demonstrate a basic understanding of Java and the language.

### pyGuesser

<p align="center">
  <img src="{site.baseurl}}/assets/images/pyguesser.jpg" />
</p>

Viewable at: [Zac-dot/pyGuesser](https://github.com/Zac-dot/pyGuesser) <br>
Tech used: Python<br>
Time to make: 3 days<br>
Learned:
- The basics of python syntax and displaying them in the source code
- Translating Java code into Python code (This is based on Letsguess-project)
- Making a program that can run until the user does not want to continue
- Outputting information to screen, randomizing some information, accepting user information
- Outputting information that was in the console to a file for later use.

Description:
This was created for a intro class that taught Python in November of 2020. The user is prompted to choose how many numbers they would like to guess, and has three attempts per number to figure it out. If the person can guess all the numbers, they are congratulated, else they are told the correct number and to reattempt. The results are saved to an external text file for later use. This is for use with a console as it only outputs to it, and does not contain many frills besides this as it was meant to be basic.
