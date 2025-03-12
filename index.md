---
layout: post
title: C++ Digital Rain
tags: cpp coding project
  categories: Project
---

## Introduction

*Welcome to my project blog. I will be showing you my application called "Digital Rain." Inspired by the iconic rain effect from the Matrix movies, this program simulates different types of weather, including heavy rain and sleet, right in your terminal. Using modern C++ features and libraries, such as <random> for advanced random number generation and Windows API for console manipulation, this project demonstrates how creativity and expressing yourself can be achieved in C++ programming! I will now dive into the code deeper and show you how Digital Rain brings traditional Irish weather to life on your screen!*

## Design and Test

The Rain class contains all the functionality required to simulate the weather effects. It includes methods for starting the simulation, displaying the start menu, drawing clouds, generating rain and sleet, playing thunder sounds, and clearing the screen.

<img src="https://raw.githubusercontent.com/G00293495/DigitalRainCPP/main/docs/assets/images/rainheader.png" width="400" height="300">

The constructor is initialized as a vector of strings. This Vector has a size of 20 and a width of 85, and it is filled with spaces (' '). This particular setup creates a blank screen of 20 rows and 85 columns, where each cell is originally empty. This is the foundation of displaying the rain and sleet. 

<img src="https://raw.githubusercontent.com/G00293495/DigitalRainCPP/main/docs/assets/images/constructor.png" width="400" height="200">

The start menu is the first code that appears on the screen, presentening the user with an amusing start menu. This start menu has ASCII art to be visually appealing to the user, and it also provides text which prompts the user to enter 'H' for heavy rain and 'S' for sleet. 

<img src="https://raw.githubusercontent.com/G00293495/DigitalRainCPP/main/docs/assets/images/startmenu.png" width="400" height="300">

The start function is a simple UserInput function. This gives the code the appropriate letter to enter to start either Heavy or sleet rain. If the input is invlaid, print out that the Input isnt right and exit the programme. 

<img src="https://raw.githubusercontent.com/G00293495/DigitalRainCPP/main/docs/assets/images/start.png" width="400" height="300">







## Algorithim


## Problem Solving


## Modern C++ Insight and Reflection


Font can be *Italic* or **Bold**.

Code can be highlighted with 'backticks'.

Hyperlinks look like this: [GitHub Help](https://help.github.com/).

A bullet list:

- vectors
- algorithms
- iterators

You can add an impage that has been uploaded to the repository in a /docs/assets/images folder.

<img src="https://raw.githubusercontent.com/G00293495/DigitalRainCPP/main/docs/assets/images/Test.png" width="400" height="300">
