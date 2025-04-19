# Multiplayer Word Game  
A C++ project using BSD sockets for networking and Qt for the graphical client.

## Repository

[SK2-Projekt-Gra](https://github.com/Bordomir/SK2-Projekt-Gra)

## 🧩 About the Project

This project is a variant of the multiplayer word game *"Stop the Bus"*, known in Poland as *"Państwa Miasta"*, where players race to submit words based on a randomly selected letter and six given categories.  
It features a TCP server implemented with BSD sockets and a GUI client built using the Qt framework.

## 🎮 Gameplay Overview

- Upon launching the client, the player enters a nickname and connects to the server.
- Once connected, the player sees:
  - a list of all players and their scores,
  - the currently selected letter,
  - the number of players who have already submitted their answers.

Players who join during an active round will start participating from the **next** round.

### 🔤 Round Flow

- The server randomly selects a letter.
- Players must type words that begin with that letter in the following six categories:
  - **Country**
  - **City**
  - **Thing**
  - **Plant**
  - **Animal**
  - **Name**
- Players can choose when to submit their answers.
- A round ends automatically once enough players have submitted their answers.
- After a round, a summary is shown with additional points awarded based on **Uniqueness** and **Speed**
- After the round, a summary is shown and players receive points for their answers and additional points based on:
  - **Uniqueness** of answers
  - **Speed** of submission

## 🔗 Client-Server Communication

The game uses TCP sockets for communication. The server is responsible for:
- Managing connections and disconnections,
- Broadcasting game state updates (e.g. new player joined, answers submitted, round ended),
- Calculating and updating player scores.

The client handles:
- User input (nickname, answers)
- Real-time display of the game state received from the server

## ⚙️ Technologies Used

- **C++** – server and client logic
- **Qt** – GUI for the client
- **BSD sockets (TCP)** – client-server communication

