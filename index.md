---
layout: post
title: C++ Digital Rain
tags: cpp coding project
  categories: Project
---

# Introduction

Welcome to my project blog. I will be showing you my application called "Digital Rain." Inspired by the iconic rain effect from the Matrix movies, this program simulates different types of weather, including heavy rain and sleet, right in your terminal. 

Using modern C++ features and libraries, such as <random> for advanced random number generation and Windows API for console manipulation, this project demonstrates how creativity and expressing yourself can be achieved in C++ programming! 

I will now dive into the code deeper and show you how Digital Rain brings traditional Irish weather to life on your screen!

# Layout

## Rain.h 
– The header file defining the Rain class, including its methods and member variables.

```
#ifndef RAIN_H
#define RAIN_H

#include <string>
#include <vector>

const int WIDTH = 85;
const int HEIGHT = 20;

class Rain {
public:
    Rain();
    Rain(const Rain& other);
    void start();
    void displayStartMenu();
    void drawClouds();
    void generateRain();
    void generateSleet();
    void playThunder();
    void clearScreen();
    // void testDisplayStartMenu();

private:
    std::vector<std::string> screen; 
};

#endif
 ```

## Rain.cpp 
– The implementation file for the Rain class, containing the logic for rendering rain, sleet, thunder sounds, and user interaction - This whole file is discussed further in the design section.

## main.cpp 
– The entry point of the program, initializing a Rain object and starting the simulation.

```
#include "Rain.h"
#include <iostream>

int main() {
    Rain rainSimulation;
    rainSimulation.start();

    return 0;
}
```

## test.cpp 
– A test file using assertions to validate the output of the displayStartMenu() function - This is shown in the test section.

# Design 

- The random library is used for random number generation, which will be used to generate rainfall.
- mmsytem.h used for playing sounds which will be used when the application is started up and a certain option is chosen within the console [1]
- vector is like a reziable array, and this will be used for my screen in which the DigitalRain will be printed on.
- "Rain.h" is my custom header file, containing class and function definitions related to the rain simulation.
- <iostream> provides input and output stream functionality (e.g., std::cout, std::cin).
- <cstdlib> – includes all the standard library functions like memory allocation, process control, and random number generation.
- <thread> – Supports multithreading operations, allowing concurrent execution of functions in my programme.
- <chrono> – Provides time-related utilities for measuring execution time, delays, and time points.
- <windows.h> – A Windows-specific header providing access to the Windows API for system functions.

```
#include "Rain.h"
#include <iostream>
#include <cstdlib>
#include <vector>
#include <thread>
#include <chrono>
#include <windows.h>
#include <mmsystem.h>
#include <random>
```

- The constructor is initialized as a vector of strings. This Vector has a size of 20 and a width of 85, and it is filled with spaces (' '). This particular setup creates a blank screen of 20 rows and 85 columns, where each cell is originally empty. This is the foundation of displaying the rain and sleet. 

``` Rain::Rain() : screen(HEIGHT, std::string(WIDTH, ' ')) {} ```

- The start menu is the first code that appears on the screen, presentening the user with an amusing start menu. This start menu has ASCII art to be visually appealing to the user, and it also provides text which prompts the user to enter 'H' for heavy rain and 'S' for sleet. 

```
void Rain::displayStartMenu() {
    std::cout << R"(
         __I__
   .-'"  .  "'-.
 .'  / . ' . \  '.
/_.-..-..-..-..-._\ .---------------------------------.
         #  _,,_   ( Choose your weather type! )
         #/    \ /'---------------------------------'
         / / 6 6\ \
         \/\  Y /\/       /\-/\
         #/ 'U \       /a a  \               _
       , (  \   | \     =\ Y  =/-~~~~~~-,_____/ )
       |\|\_/#  \_/       '^--'          ______/
       \/'.  \  /'\         \           /
        \    /=\  /         ||  |---'\  \
        /____)/____)       (_(__|   ((__|

   Welcome to Digital Rain!
   Press 'S' for Sleet (light diagonal rain)
   Press 'H' for Heavy Rain (default)
    )";
}
```
- The start function serves as the entry point for user interaction in the Digital Rain simulation. It begins by displaying the start menu, which provides users with a choice of weather effects. The function then waits for user input, capturing a single character. Depending on whether the user enters 'S' (or 's') for sleet or 'H' (or 'h') for heavy rain, the function will call the respective generation function (generateSleet() or generateRain()). If the input does not match either of these valid options, an error message is displayed, informing the user of the invalid input, and the program exits. This approach ensures that only valid commands trigger the rain effects while maintaining a simple interface.

```
void Rain::start() {
    displayStartMenu();

    char userInput;
    std::cin >> userInput;

    if (userInput == 'S' || userInput == 's') {
        generateSleet();
    }
    else if (userInput == 'H' || userInput == 'h') {

        generateRain();
    }
    else {
        std::cout << "Invalid input. Exiting...\n";
    }
}
```

- DrawClouds uses the GoToXY function. This function is used as a utility function to set the cursor position in the console window. This allows me to have control over where the text is printed on the screen, allowing me to draw cool clouds and start the rain in certain positions. DrawClouds contains 2 clouds, cloud 1 and cloud 2. Cloud 1 is positioned at one fourth of the screen width and cloud 2 is positioned at 2 fourhts of the screen width. The GoToXY function is used multiple times to draw the cloud art that I found on the ASCII art website. 

```
void GotoXY(int x, int y) {
    COORD coord;
    coord.X = x;
    coord.Y = y;
    SetConsoleCursorPosition(GetStdHandle(STD_OUTPUT_HANDLE), coord);
}
```

```
void Rain::drawClouds() {
    int cloud1X = (WIDTH / 4) - 10;
    int cloud2X = (3 * WIDTH / 4) - 10;

    int cloudY = 3;

    // First cloud
    GotoXY(cloud1X, cloudY);   std::cout << "       .-~~~-.";
    GotoXY(cloud1X, cloudY + 1); std::cout << "  .- ~ ~-(       )_ _";
    GotoXY(cloud1X, cloudY + 2); std::cout << " /                     ~ -.";
    GotoXY(cloud1X, cloudY + 3); std::cout << "|                           \\";
    GotoXY(cloud1X, cloudY + 4); std::cout << " \\                         .'";
    GotoXY(cloud1X, cloudY + 5); std::cout << "   ~- . _____________ . -~";

    // Second cloud
    GotoXY(cloud2X, cloudY);   std::cout << "       .-~~~-.";
    GotoXY(cloud2X, cloudY + 1); std::cout << "  .- ~ ~-(       )_ _";
    GotoXY(cloud2X, cloudY + 2); std::cout << " /                     ~ -.";
    GotoXY(cloud2X, cloudY + 3); std::cout << "|                           \\";
    GotoXY(cloud2X, cloudY + 4); std::cout << " \\                         .'";
    GotoXY(cloud2X, cloudY + 5); std::cout << "   ~- . _____________ . -~";
}
 ```

# Algorithim
- For generate rain, The hConsole Handle gets the handle to the console output. The random generator (random_device and mt19937) is used to generate random numbers between 1 and 9. This is used to create random rain drops. PlaySound is part of the <mmsystem.h> library. This is used to play a thunderSound which resembles the sound heard when rain is heavy. If the user has speakers, they can hear it when heavy rain is generated! The SND_LOOP ensures the sound loops when its reached its length ensuring a good user experience always when in the console.

- The for loop for shifting the rain down shifts each row of the screen vector down by one position (for (int i = HEIGHT -1; i > 0; --i), which simulates downwards movement like rain falling from the sky. It generates new rain by clearing the top row and then randomly placing rain drops with the character with a 20% chance for each column (if dis(gen) < 2). The rain is then printed and a delay is implemented by pausing the loop for 100 milliseconds to control the animation speed. The rain is also coloured dark blue using the SetConsoleTextAttribute. 

```
void Rain::generateRain() {
    HANDLE hConsole = GetStdHandle(STD_OUTPUT_HANDLE);
    std::random_device rd;
    std::mt19937 gen(rd());
    std::uniform_int_distribution<> dis(0, 9);

    system("cls");

    PlaySound(TEXT("thunder.wav"), NULL, SND_ASYNC | SND_LOOP);

    while (true) {
        drawClouds();
        // Shift rain down
        for (int i = HEIGHT - 1; i > 0; --i) {
            screen[i] = screen[i - 1];
        }

        // New rain
        screen[0] = std::string(WIDTH, ' ');
        for (int i = 0; i < WIDTH; i++) {
            if (dis(gen) < 2) {
                screen[0][i] = '|';
            }
        }

        // Print the rain in blue
        for (int i = 0; i < HEIGHT; i++) {
            GotoXY(0, i + 9); // below clouds
            SetConsoleTextAttribute(hConsole, 9); // blue
            std::cout << screen[i];
        }

        SetConsoleTextAttribute(hConsole, 7);

        std::this_thread::sleep_for(std::chrono::milliseconds(100));
    }
}
```

- generateSleet is similar to generateRain. Instead of shifting each row of the vector straight down, it shifts it down and to the right by one position, which simulates diagonal movement like sleet is.	(for (int i = HEIGHT - 1; i > 0; --i) { for (int j = 0; j < WIDTH - 1; j++) { screen[i][j + 1] = screen[i - 1][j]; }). The top row is cleared again and then the sleet is randomly placed with drops '\' or '/' with a 10% chance of rain, making it less heavy than heavier rain, like sleet is in real life. Its also a lighter colour than the heavy rain, appearing a light blue colour.

```
void Rain::generateSleet() {
    HANDLE hConsole = GetStdHandle(STD_OUTPUT_HANDLE);
    std::random_device rd;
    std::mt19937 gen(rd());
    std::uniform_int_distribution<> dis(0, 9);
    std::uniform_int_distribution<> dir_dis(0, 1);

    system("cls");

    while (true) {
        drawClouds();

        // Shift rain down diagonally
        for (int i = HEIGHT - 1; i > 0; --i) {
            for (int j = 0; j < WIDTH - 1; j++) {
                screen[i][j + 1] = screen[i - 1][j]; // Diagonal shift
            }
        }

        // Generate new sleet
        screen[0] = std::string(WIDTH, ' ');
        for (int i = 0; i < WIDTH; i++) {
            if (dis(gen) < 1) {
                screen[0][i] = (dir_dis(gen) == 0) ? '\\' : '/'; // Randomly pick diagonal direction
            }
        }

        // Print the sleet in light blue
        for (int i = 0; i < HEIGHT; i++) {
            GotoXY(0, i + 9);
            SetConsoleTextAttribute(hConsole, 11); // Light Blue
            std::cout << screen[i];
        }

        SetConsoleTextAttribute(hConsole, 7);
        std::this_thread::sleep_for(std::chrono::milliseconds(100));
    }
}
 ```

- A copy constructor is present at the bottom of my code, however it is empty. I didnt have a use for this, but its inculded to show my understanding of these types of constructors and how to implement them into C++ code in the future. Copy contructors are extremely useful in C++ code, allowing a user to create a new object from an existing one by initialization. 

```
Rain::Rain(const Rain& other) : screen(other.screen) {
} 
```

# Problem Solving
- One problem that I encountered during my project was the clouds flickering on and off very quickly while the rain was being printed. This meant that a choppy effect was present, and it did not look user friendly or clean. To fix this, I made use of the system("cls") function. This function was used after the user picked what type of rain they wanted. The system("cls") function simply clears the whole screen. The <cstdlib> function is needed in order for it to work. When the screen cleared, the draw clouds function was then used to draw the clouds and keep them present on the screen while the rain was printing. This ensured a smooth trainsition from one screen to the next on the console, allowing a visually pleasent representation of digital rain.

- I also encountered a problem where, for a while, my clouds were not printing at all, only the rain. This was because i did not have the drawclouds() function in my while true loop. This while true loop was used for rain generation. When it was outside the loop, the clouds would draw but be instantly cleared by the system("cls") function. This meant a blank space was created above the rain and it looked like it was coming from nowhere. When the draw clouds was in the while true loop, it printed with the rain, so it wasnt cleared and printed cleanly on the screen. 

<img src="https://raw.githubusercontent.com/G00293495/DigitalRainCPP/main/docs/assets/images/problem1.png" width="500" height="400">

# Test
- For this project, I implemented a unit test to verify the functionality of the displayStartMenu() method in my Digital Rain Simulation. This method is responsible for displaying the start menu, where users can choose between different weather types.

- Purpose of the Test
The goal of this test is to ensure that the correct text appears when displayStartMenu() is called. Since this function prints to the console, I need to capture and verify its output.

 How the Test Works

- Redirecting Console Output:
Normally, std::cout prints directly to the console.
The test redirects this output into a buffer (std::ostringstream), so I can check its contents and see if they are correct.

- Running the Function:
I created an instance of the Rain class.
I then called displayStartMenu(), which writes output to the buffer instead of the console.

- Verifying the Output:
I checked if the output contains key menu phrases like "Welcome to Digital Rain!", "Press 'S' for Sleet", and "Press 'H' for Heavy Rain".
If these phrases exist, the test passes; otherwise, it fails.

- Restoring std::cout:
After the test, we restore std::cout to ensure normal console behavior.
If the test fails, the program throws an assertion error, helping us identify issues.

```
 #include "Rain.h"
#include <iostream>
#include <sstream>
#include <cassert>


void testDisplayStartMenu() {
    std::ostringstream outputBuffer;  
    std::streambuf* oldCout = std::cout.rdbuf(outputBuffer.rdbuf());  

    Rain rainTest;
    rainTest.displayStartMenu();  

    std::cout.rdbuf(oldCout); 

    std::string output = outputBuffer.str();
    assert(output.find("Welcome to Digital Rain!") != std::string::npos);
    assert(output.find("Press 'S' for Sleet") != std::string::npos);
    assert(output.find("Press 'H' for Heavy Rain") != std::string::npos);

    std::cout << "Test Passed: displayStartMenu() output is correct!" << std::endl;
}
 ```

# Modern C++ Insight and Reflection
I thoroughly enjoyed working on this Modern c++ project. It proved to be a technical but rewarding experience. 

When I first started, after viewing example projects, I knew i wanted to make something lightweight yet effective, and something slightly different from the matrix rain with letter thats I saw lots of. I knew i wanted to use real time console animation and it was a valuable experience, giving me a great insight to how modern C++ can provide such fine details on the terminals. 

I found myself diving head first into many different concepts like multithreading which was to ensure smooth execution of my programme, while chrono based timing was essential in the control of my heavy rain and sleet. 

I researched and familiarized myself with the windows API function, and I saw the benefits that could be used by manipulating the console output in a dynamic way. The SetConsoleCursorPosition() was essential, allowing me to repoistion the cursor without clearing the screen, making sure there was no flickering effect on my screen. I also used the SetConsoleTextAttribute() function to have my heavy rain in a darker blue and my sleet in a lighter colour blue, which was more visually appealing for the user. 

I used random number generation in a slightly different way, using it to make the rain movement feel more ogranic and relaistic, rather than really repetitive. I used an algorithim in a way that only printed rain when a certain condition like (a number being less than another number), which I think worked really well. 

A system I found and had great enjoyment using was the mmsytem.h library, this really made my project come to life. This allowed me to add a thundery sound to my heavy rain, which had a real immersive touch on my project. It amde the simulation feel alive, and definetely made it feel like proper Irish rain, which we are well used to!

I also gained not only an insight, but greater appreciation for Object Oriented Programming (OOP), especially with my Rain class that I designed, as it was the backbone of my project. It contains all necessary functionality, from generating and animating raindrops to playing thunder sounds. The screen vector acted as a buffer to store and manipulate the rain’s state before rendering it to the console, reducing unnecessary screen clearing operations. I also implemented a copy constructor, which was not really used in my project, but i still added it slightly to show my understanding of how it may work in future projects.

Overall, the project was a really enjoyable experience, and I would be lying if I said my C++ coding skills now are extemely more advanced than when I first started. Bringing a digital rain project to life was so satisfying, and problem solving along the way gave me a sense of drive and purpose to get the project finished. I discovered new depths in the tools that can be used in C++.

# Heavy Rain

<img src="https://raw.githubusercontent.com/G00293495/DigitalRainCPP/main/docs/assets/images/heavyrain.png" width="500" height="400">

# Sleet

<img src="https://raw.githubusercontent.com/G00293495/DigitalRainCPP/main/docs/assets/images/sleet.png" width="500" height="400">

# References
[1] Using winmm library in C. Stack Overflow. [Online] Available: https://stackoverflow.com/questions/14014141/using-winmm-library-in-c

[2] ChatGPT. (GPT-4). Open AI. [Online]. Available: https://chatgpt.com/

[3] Windows. Create and remove project dependencies. [Online]. Available: https://learn.microsoft.com/en-us/visualstudio/ide/how-to-create-and-remove-project-dependencies?view=vs-2022
