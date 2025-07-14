# GuessTheNumber Game - Comprehensive API Documentation

## Table of Contents
1. [Overview](#overview)
2. [Architecture](#architecture)
3. [Public APIs and Functions](#public-apis-and-functions)
4. [Game Components](#game-components)
5. [Usage Instructions](#usage-instructions)
6. [Examples](#examples)
7. [Error Handling](#error-handling)
8. [Contributing](#contributing)

## Overview

**GuessTheNumber** is a console-based C++ game where players attempt to guess a randomly generated number between 1 and 100. The game features three difficulty levels with varying numbers of attempts allowed.

### Key Features
- Three difficulty levels (Easy, Medium, Difficult)
- Random number generation
- Interactive console interface
- Hint system (higher/lower feedback)
- Replay functionality

## Architecture

### Dependencies
```cpp
#include <cstdlib>   // For rand(), srand(), exit()
#include <ctime>     // For time() function
#include <iostream>  // For input/output operations
```

### Namespace
```cpp
using namespace std;
```

## Public APIs and Functions

### Main Function

#### `int main()`
**Description:** Entry point of the application that manages the game loop and user interactions.

**Return Type:** `int`
- Returns `0` on successful program termination

**Functionality:**
- Displays welcome message and game instructions
- Manages difficulty level selection
- Handles game termination
- Coordinates all game logic

**Flow Control:**
- Infinite loop (`while(true)`) for continuous gameplay
- Switch-like logic using `if-else` statements for difficulty selection

---

## Game Components

### 1. Welcome System

#### Welcome Message Display
```cpp
cout << "Welcome to GuessTheNumber game!" << endl;
cout << "You have to guess a number between 1 and 100. "
        "You'll have limited choices based on the "
        "level you choose. Good Luck!" << endl;
```

**Purpose:** Introduces the game and explains basic rules to the player.

### 2. Difficulty Selection System

#### Difficulty Menu
```cpp
cout << "\nEnter the difficulty level: \n";
cout << "1 for easy!\t";
cout << "2 for medium!\t";
cout << "3 for difficult!\t";
cout << "0 for ending the game!\n" << endl;
```

**Input Variable:** `int difficultyChoice`

**Valid Options:**
- `0` - Exit game
- `1` - Easy mode (10 attempts)
- `2` - Medium mode (7 attempts)  
- `3` - Difficult mode (5 attempts)

### 3. Random Number Generation System

#### Secret Number Generation
```cpp
srand(time(0));
int secretNumber = 1 + (rand() % 100);
```

**Components:**
- **`srand(time(0))`** - Seeds random number generator with current time
- **`rand() % 100`** - Generates random number 0-99
- **`1 + (rand() % 100)`** - Shifts range to 1-100

**Return:** Random integer between 1 and 100 (inclusive)

### 4. Game Logic Engine

#### Easy Mode (Difficulty Level 1)
```cpp
if (difficultyChoice == 1) {
    // 10 attempts allowed
    int choicesLeft = 10;
    for (int i = 1; i <= 10; i++) {
        // Game logic
    }
}
```

**Parameters:**
- **Attempts:** 10
- **Range:** 1-100
- **Feedback:** Higher/Lower hints provided

#### Medium Mode (Difficulty Level 2)
```cpp
else if (difficultyChoice == 2) {
    // 7 attempts allowed
    int choicesLeft = 7;
    for (int i = 1; i <= 7; i++) {
        // Game logic
    }
}
```

**Parameters:**
- **Attempts:** 7
- **Range:** 1-100
- **Feedback:** Higher/Lower hints provided

#### Difficult Mode (Difficulty Level 3)
```cpp
else if (difficultyChoice == 3) {
    // 5 attempts allowed
    int choicesLeft = 5;
    for (int i = 1; i <= 5; i++) {
        // Game logic
    }
}
```

**Parameters:**
- **Attempts:** 5
- **Range:** 1-100
- **Feedback:** Higher/Lower hints provided

### 5. Input Validation System

#### Player Choice Input
```cpp
cout << "\n\nEnter the number: ";
cin >> playerChoice;
```

**Variable:** `int playerChoice`
**Expected Range:** 1-100
**Type:** Integer input from user

### 6. Feedback System

#### Win Condition
```cpp
if (playerChoice == secretNumber) {
    cout << "Well played! You won, " << playerChoice
         << " is the secret number" << endl;
    cout << "\t\t\t Thanks for playing...." << endl;
    cout << "Play the game again with us!!\n\n" << endl;
    break;
}
```

#### Hint System
```cpp
if (playerChoice > secretNumber) {
    cout << "The secret number is smaller than the number you have chosen" << endl;
}
else {
    cout << "The secret number is greater than the number you have chosen" << endl;
}
```

#### Loss Condition
```cpp
if (choicesLeft == 0) {
    cout << "You couldn't find the secret number, it was " 
         << secretNumber << ", You lose\n\n";
    cout << "Play the game again to win\n\n";
}
```

### 7. Game Termination System

#### Exit Function
```cpp
else if (difficultyChoice == 0) {
    exit(0);
}
```

**Purpose:** Cleanly terminates the application when user selects option 0.

## Usage Instructions

### Compilation
```bash
g++ -o guessthegame README.md
```

### Execution
```bash
./guessthegame
```

### Gameplay Flow
1. **Start Game:** Run the compiled executable
2. **Select Difficulty:** Choose from options 1-3 or 0 to exit
3. **Make Guesses:** Enter numbers between 1-100
4. **Receive Feedback:** Get hints about whether to guess higher or lower
5. **Win/Lose:** Game ends when you guess correctly or run out of attempts
6. **Replay:** Choose a new difficulty level to play again

## Examples

### Example 1: Easy Mode Gameplay
```
Welcome to GuessTheNumber game!
You have to guess a number between 1 and 100. You'll have limited choices based on the level you choose. Good Luck!

Enter the difficulty level: 
1 for easy!	2 for medium!	3 for difficult!	0 for ending the game!

Enter the number: 1

You have 10 choices for finding the secret number between 1 and 100.

Enter the number: 50
Nope, 50 is not the right number
The secret number is greater than the number you have chosen
9 choices left. 

Enter the number: 75
Nope, 75 is not the right number
The secret number is smaller than the number you have chosen
8 choices left. 

Enter the number: 63
Well played! You won, 63 is the secret number
			 Thanks for playing....
Play the game again with us!!
```

### Example 2: Game Exit
```
Enter the difficulty level: 
1 for easy!	2 for medium!	3 for difficult!	0 for ending the game!

Enter the number: 0
[Program terminates]
```

### Example 3: Invalid Input Handling
```
Enter the difficulty level: 
1 for easy!	2 for medium!	3 for difficult!	0 for ending the game!

Enter the number: 5
Wrong choice, Enter valid choice to play the game! (0,1,2,3)
```

## Error Handling

### Input Validation
- **Invalid difficulty choice:** Displays error message and prompts for valid input (0,1,2,3)
- **Out of range guesses:** No explicit validation (assumes user inputs valid integers)

### Edge Cases
- **Multiple games:** Game supports continuous play through the main loop
- **Random seed:** Uses system time to ensure different random numbers each execution

## API Reference Summary

### Functions
| Function | Return Type | Parameters | Description |
|----------|-------------|------------|-------------|
| `main()` | `int` | None | Main game loop and entry point |

### Variables
| Variable | Type | Scope | Purpose |
|----------|------|-------|---------|
| `difficultyChoice` | `int` | Function | Stores user's difficulty selection |
| `secretNumber` | `int` | Function | Stores randomly generated target number |
| `playerChoice` | `int` | Function | Stores user's guess |
| `choicesLeft` | `int` | Block | Tracks remaining attempts |

### Constants
| Constant | Value | Description |
|----------|-------|-------------|
| Number Range | 1-100 | Valid range for secret number and guesses |
| Easy Attempts | 10 | Maximum attempts in easy mode |
| Medium Attempts | 7 | Maximum attempts in medium mode |
| Difficult Attempts | 5 | Maximum attempts in difficult mode |

## Contributing

### Code Style Guidelines
- Use descriptive variable names
- Follow consistent indentation
- Add comments for complex logic
- Maintain separation between game logic and I/O operations

### Potential Enhancements
1. **Input Validation:** Add bounds checking for player guesses
2. **Statistics:** Track win/loss ratios and best scores
3. **Custom Ranges:** Allow user-defined number ranges
4. **Difficulty Scaling:** Dynamic difficulty based on performance
5. **Save/Load:** Persistent game state
6. **Multiplayer:** Support for multiple players

### Testing Recommendations
- Test all difficulty levels
- Verify random number generation
- Test edge cases (boundary values)
- Validate input handling
- Test game termination scenarios

---

*This documentation covers all public APIs, functions, and components of the GuessTheNumber game. For additional support or feature requests, please refer to the contributing guidelines above.*