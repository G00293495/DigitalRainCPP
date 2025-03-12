---
layout: post
title: C++ Digital Rain
tags: cpp coding project
  categories: Project
---

## Introduction

*Welcome to my project blog. I will be showing you my application called "Digital Rain." Inspired by the iconic rain effect from the Matrix movies, this program simulates different types of weather, including heavy rain and sleet, right in your terminal. Using modern C++ features and libraries, such as <random> for advanced random number generation and Windows API for console manipulation, this project demonstrates how creativity and expressing yourself can be achieved in C++ programming! I will now dive into the code deeper and show you how Digital Rain brings traditional Irish weather to life on your screen!*

## Design and Test

- The Rain class contains all the functionality required to simulate the weather effects. It includes methods for starting the simulation, displaying the start menu, drawing clouds, generating rain and sleet, playing thunder sounds, and clearing the screen.

<img src="https://raw.githubusercontent.com/G00293495/DigitalRainCPP/main/docs/assets/images/rainheader.png" width="400" height="300">

- The constructor is initialized as a vector of strings. This Vector has a size of 20 and a width of 85, and it is filled with spaces (' '). This particular setup creates a blank screen of 20 rows and 85 columns, where each cell is originally empty. This is the foundation of displaying the rain and sleet. 

<img src="https://raw.githubusercontent.com/G00293495/DigitalRainCPP/main/docs/assets/images/constructor.png" width="300" height="100">

- The start menu is the first code that appears on the screen, presentening the user with an amusing start menu. This start menu has ASCII art to be visually appealing to the user, and it also provides text which prompts the user to enter 'H' for heavy rain and 'S' for sleet. 

<img src="https://raw.githubusercontent.com/G00293495/DigitalRainCPP/main/docs/assets/images/startmenu.png" width="400" height="300">

- The start function is a simple UserInput function. This gives the code the appropriate letter to enter to start either Heavy or sleet rain. If the input is invlaid, print out that the Input isnt right and exit the programme. 

<img src="https://raw.githubusercontent.com/G00293495/DigitalRainCPP/main/docs/assets/images/start.png" width="400" height="300">

- DrawClouds uses the GoToXY function. This function is used as a utility function to set the cursor position in the console window. This allows me to have control over where the text is printed on the screen, allowing me to draw cool clouds and start the rain in certain positions. DrawClouds contains 2 clouds, cloud 1 and cloud 2. Cloud 1 is positioned at one fourth of the screen width and cloud 2 is positioned at 2 fourhts of the screen width. The GoToXY function is used multiple times to draw the cloud art that I found on the ASCII art website. 

<img src="https://raw.githubusercontent.com/G00293495/DigitalRainCPP/main/docs/assets/images/gotoXY.png" width="600" height="200">
<img src="https://raw.githubusercontent.com/G00293495/DigitalRainCPP/main/docs/assets/images/drawclouds.png" width="400" height="300">

## Algorithim
- The hConsole Handle gets the handle to the console output. The random generator (random_device and mt19937) is used to generate random numbers between 1 and 9. This is used to create random rain drops. PlaySound is part of the <mmsystem.h> library. This is used to play a thunderSound which resembles the sound heard when rain is heavy. If the user has speakers, they can hear it when heavy rain is generated! The SND_LOOP ensures the sound loops when its reached its length ensuring a good user experience always when in the console.

- The for loop for shifting the rain down shifts each row of the screen vector down by one position (for (int i = HEIGHT -1; i > 0; --i), which simulates downwards movement like rain falling from the sky. It generates new rain by clearing the top row and then randomly placing rain drops with the character ('|') with a 20% chance for each column (if dis(gen) < 2). The rain is then printed and a delay is implemented by pausing the loop for 100 milliseconds to control the animation speed. The rain is also coloured dark blue using the SetConsoleTextAttribute. 

<img src="https://raw.githubusercontent.com/G00293495/DigitalRainCPP/main/docs/assets/images/raingeneration.png" width="500" height="400">

- generateSleet is similar to generateRain. Instead of shifting each row of the vector straight down, it shifts it down and to the right by one position, which simulates diagonal movement like sleet is.	(for (int i = HEIGHT - 1; i > 0; --i) { for (int j = 0; j < WIDTH - 1; j++) { screen[i][j + 1] = screen[i - 1][j]; }). The top row is cleared again and then the sleet is randomly placed with drops '\' or '/' with a 10% chance of rain, making it less heavy than heavier rain, like sleet is in real life. Its also a lighter colour than the heavy rain, appearing a light blue colour.

<img src="https://raw.githubusercontent.com/G00293495/DigitalRainCPP/main/docs/assets/images/sleetgeneration.png" width="500" height="400">

- A copy constructor is present at the bottom of my code, however it is empty. I didnt have a use for this, but its inculded to show my understanding of these types of constructors and how to implement them into C++ code in the future.
- 
<img src="https://raw.githubusercontent.com/G00293495/DigitalRainCPP/main/docs/assets/images/copyconstructot.png" width="400" height="300">

## Problem Solving


## Modern C++ Insight and Reflection


Font can be *Italic* or **Bold**.

Code can be highlighted with 'backticks'.

Hyperlinks look like this: [GitHub Help](https://help.github.com/).

A bullet list:

- vectors
- algorithms
- iterators

