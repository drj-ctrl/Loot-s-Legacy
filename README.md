Loot's Legacy
Welcome to the official repository for Loot's Legacy, a web-based multiplayer card game built with a resilient and modern architecture. This document provides all the information you need to understand, run, and contribute to the project.

The Game: Gilded Hoard
Gilded Hoard is a strategic card game that blends trick-taking, push-your-luck, and direct player interaction. Players compete to accumulate the most coins by winning tricks, strategically banking their loot, and cleverly stealing from opponents. It's a game of wits, risk, and occasional backstabbing.

The ultimate goal is to be the wealthiest player. The game's end-phase is triggered when one player banks 250 coins, after which the player with the highest total coin value for two consecutive rounds is declared the winner.

Core Features
Gilded Hoard is more than just a card game; it's a robust web application with several key features:

Dynamic Trick-Taking Gameplay: A rich card game experience with a permanent trump suit, special power cards, and unique effects that change every round.

Push-Your-Luck Banking: A thrilling core mechanic where players must decide whether to risk their unbanked loot for a bigger payout or play it safe.

Interactive Player vs. Player: Steal loot from your rivals using various Thief cards, and defend your stash with Guards.

Resilient Host/Join Model: The game is architected to handle common web issues. If a player—or even the Host—disconnects or refreshes their page, they can seamlessly rejoin the session without interrupting the game.

Serverless Multiplayer: Utilizes PeerJS and WebRTC for direct browser-to-browser communication, creating a fast, low-latency experience without the need for a dedicated backend server.

Technology Stack
This project uses a lightweight and powerful stack, chosen for rapid development and high performance.

Frontend: HTML5, CSS3, and modern JavaScript (ES6 Modules)

Development Environment: Vite for a fast development server and optimized builds.

Multiplayer Communication: PeerJS (WebRTC) for real-time, direct peer-to-peer connections.

Asset Storage: All static assets like images and sounds are hosted directly within the GitHub repository.

Project Structure
The codebase is organized into logical modules to ensure clarity and maintainability.

/
|-- index.html              # The main entry point for the application
|-- styles.css              # All application styles
|-- package.json            # Project dependencies and scripts
|-- /src
|   |-- /modules
|   |   |-- network.js      # Handles all PeerJS logic (Host/Client, connections)
|   |   |-- ui.js           # Manages all DOM manipulation and UI rendering
|   |   |-- state.js        # Defines the game state structure and initial state
|   |   |-- game.js         # HOST-ONLY: Contains all core game logic functions
|   |   |-- constants.js    # Static game data (e.g., card definitions)
|   |-- main.js             # Initializes the UI and Network modules
|-- /assets/
    |-- /images/            # Game art and UI elements

Getting Started (For Developers)
To run this project on your local machine, follow these steps.

Prerequisites
You must have Node.js (which includes npm) installed on your system.

Installation
Clone the repository:

git clone https://github.com/your-username/loots-legacy.git
cd loots-legacy

Install dependencies:
The project uses servor for a simple development server.

npm install

Running the Project
To start the local development server, run:

npm run start

This will launch the game in your default web browser. You can open multiple tabs to simulate a multiplayer session.

How to Play
To Host a Game: Open the game and click the "Host New Game" button. You will be given a Host ID. Share this ID with your friends.

To Join a Game: Open the game, paste the Host ID you received into the input field, and click "Join Game".

Start the Game: Once all players have joined the lobby, the Host can click the "Start Game" button.

Core Architectural Principles
The architecture of Loot's Legacy is built on two fundamental principles:

Host Authority: The Host's game instance is the absolute source of truth. All game logic—from shuffling the deck to resolving tricks—is executed on the Host's machine. Clients are responsible only for rendering the game state they receive and sending user inputs to the Host. This prevents cheating and ensures consistency.

Resilience through Caching: The game is designed to survive page refreshes and temporary network disconnects.

Session & Player IDs: The Host generates a unique sessionId for the game, and each player receives a unique playerId. These are saved to the browser's localStorage.

Host-side State Caching: After every action, the Host saves the entire gameState to their localStorage, keyed by the sessionId.

Reconnection Flow: If any player's page is reloaded, the application checks localStorage. If session data is found, it automatically attempts to reconnect to the Host. If the Host reloads, their browser finds the cached game state and re-establishes their hosting session, allowing all clients to seamlessly reconnect.
