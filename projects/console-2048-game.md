# 2048 Console Game in C++

A simple console-based implementation of the classic puzzle game 2048, written in C++ as an example of object‑oriented programming.

## Repository

[console-2048-game](https://github.com/Bordomir/console-2048-game)

## Building

To compile the project:

1. Open a command prompt in the project directory.  
2. Run the compiler:
    ```
    g++ *.cpp -o 2048.exe
    ```
3. The executable `2048.exe` will be created in the same directory.

## Running

To start the game:

1. Open a command prompt in the project directory.  
2. Launch the executable:
    ```
    2048.exe
    ```
3. The game will run directly in the console window.

## Controls
| Key | Direction |
|-----|-----------|
| 8   | Up        |
| 2   | Down      |
| 4   | Left      |
| 6   | Right     |

- Enter the digit corresponding to your desired move.  
- Only the first character of your input is considered.  
- Invalid inputs are ignored and you will be prompted again.

## Project Architecture

The project consists of five main classes:

- **Game**  
  Manages the overall game loop, player score, and interaction between components.  
- **Board**  
  Contains a two‑dimensional array of pointers to `Tile` objects and handles tile placement, merging, and win/loss detection.  
- **Tile** (abstract)  
  Defines the interface and common data (e.g. tile value) for all tile types.  
- **NumberTile**  
  Inherits from `Tile`; represents a tile with a numeric value and implements display logic.  
- **BlankTile**  
  Inherits from `Tile`; represents an empty cell on the board.

## Object‑Oriented Programming Concepts

1. **Encapsulation**  
   - `Board`’s internal array and `Tile` contents are private; access is provided via public methods (`getContents()`, `show()`).  
   - `Game` exposes only its constructors and the `play()` method.  
2. **Inheritance**  
   - `NumberTile` and `BlankTile` inherit from the abstract `Tile` class, sharing common data and methods.  
3. **Abstraction**  
   - `Tile` defines general behavior for all tiles, while subclasses implement specifics (number display vs. blank display).  
4. **Polymorphism**  
   - The board holds `Tile*` pointers, allowing uniform handling of `NumberTile` and `BlankTile` in move and merge operations.

## Gallery

Start of game  
![image](https://github.com/user-attachments/assets/6d640520-0ca2-466d-9eac-25fbf23cb66c)  
Tried to move right which is invalid move  
![image](https://github.com/user-attachments/assets/882a1f24-3c11-4a3e-8682-bf54e92826da)  
Moved up and merged 2 tiles  
![image](https://github.com/user-attachments/assets/4c6f6625-24aa-49a8-89dc-4ff86a412252)  
Game state after some moves  
![image](https://github.com/user-attachments/assets/55cb962d-1ce9-4807-aeec-6ac581ba2e6b)  

