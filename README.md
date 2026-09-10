# BattleShipGame

BattleShipGame is a two-player Battleship desktop application developed in C# using WPF and .NET 8.

The game allows two players to connect over a local network and play Battleship against each other in real time. The application uses TCP/IP communication to exchange game actions and messages between the players.

## Features

* Two-player Battleship game
* Multiplayer over a local network
* Host and client connection modes
* TCP/IP communication
* Real-time exchange of game actions
* Manual ship placement
* Random ship placement
* Horizontal and vertical ship orientation
* Hit and miss detection
* Ship destruction detection
* Turn management
* Game state management
* Game statistics
* In-game chat
* Connection status handling
* Ability to disconnect and reset the game

## Technologies

* C#
* .NET 8
* WPF
* XAML
* TCP/IP
* `TcpListener`
* `TcpClient`
* `NetworkStream`
* Asynchronous programming with `async/await`

The project targets **.NET 8 for Windows** and uses WPF as its desktop UI framework.

## Architecture

The application separates the user interface, game logic, network communication and data models into dedicated components.

```text
BattleShipGame
│
├── Models/
│   ├── Enums.cs
│   ├── GameBoard.cs
│   └── Ship.cs
│
├── Services/
│   ├── ChatService.cs
│   ├── GameLogicService.cs
│   └── NetworkService.cs
│
├── Utilities/
│   └── GameConstants.cs
│
├── App.xaml
├── App.xaml.cs
├── MainWindow.xaml
├── MainWindow.xaml.cs
└── BattleShipGame.csproj
```

The repository follows a simple separation of responsibilities:

* **Models** contain the game data and board representation.
* **Services** contain the game logic, networking and chat functionality.
* **Utilities** contain shared game constants.
* **MainWindow** is responsible for the WPF user interface and interaction with the application services.

## Game Logic

The game uses separate boards for the player and the opponent.

The `GameLogicService` is responsible for:

* ship placement,
* random ship placement,
* validating moves,
* tracking turns,
* processing shots,
* detecting hits and misses,
* detecting sunk ships,
* calculating accuracy,
* determining the winner,
* resetting the game state.

The game contains a predefined fleet with a total of **17 ship cells**.

### Ship Placement

Players can place their ships manually on the board.

The orientation can be changed between:

* horizontal,
* vertical.

There is also an option to place all ships randomly.

Players must finish placing their ships and confirm readiness before the game starts.

## Network Communication

The application uses TCP/IP for communication between the two players.

One player creates a game and starts a TCP server, while the other connects to the server using its IP address and port.

```text
Player 1                         Player 2
   │                                │
   │        TCP connection          │
   │◄──────────────────────────────►│
   │                                │
   │          Game action           │
   │───────────────────────────────►│
   │                                │
   │          Game result           │
   │◄───────────────────────────────│
   │                                │
```

The `NetworkService` is responsible for:

* starting the TCP server,
* accepting connections,
* connecting to a remote server,
* sending messages,
* receiving messages asynchronously,
* detecting connection loss,
* disconnecting from the opponent.

The service uses `TcpListener`, `TcpClient` and `NetworkStream`. Messages are transmitted using UTF-8 encoding.

## In-Game Chat

The application also contains a chat functionality that allows players to exchange messages during the game.

Chat communication is separated into its own `ChatService`, keeping it independent from the core game logic and network connection management.

## Game Flow

```text
Create / Join Game
        │
        ▼
Establish TCP Connection
        │
        ▼
Place Ships
        │
        ├── Manual placement
        │
        └── Random placement
        │
        ▼
Both Players Ready
        │
        ▼
Game Starts
        │
        ▼
Player's Turn
        │
        ▼
Select Enemy Cell
        │
        ├── Hit ───────► Continue Turn
        │
        └── Miss ──────► Opponent's Turn
        │
        ▼
All Enemy Ships Destroyed?
        │
     ┌──┴──┐
    No    Yes
     │      │
     ▼      ▼
 Continue   Game Over
```

## Project Structure

### Models

The `Models` directory contains the main game entities:

* `GameBoard` — represents the game board and manages its cells and ships.
* `Ship` — represents an individual ship and its occupied cells.
* `Enums` — contains enumerations used to represent game and cell states.

### Services

The `Services` directory contains the main application logic:

* `GameLogicService` — handles the rules and state of the game.
* `NetworkService` — handles TCP/IP communication.
* `ChatService` — handles player-to-player chat.

### Utilities

`GameConstants` contains shared constants used throughout the application, including game configuration and network message identifiers.

## Getting Started

### Requirements

* Windows
* .NET 8 SDK
* Visual Studio 2022 or another IDE supporting .NET 8 and WPF

### 1. Clone the repository

```bash
git clone https://github.com/maciejbros/BattleShipGame.git
cd BattleShipGame
```

### 2. Open the solution

Open:

```text
BattleShipGame.sln
```

in Visual Studio.

### 3. Build the project

Build the solution using:

```text
Build → Build Solution
```

### 4. Start a game

Run two instances of the application.

One player should create a game and start the server. The second player should enter the host's IP address and port and join the game.

Both players then place their ships and confirm that they are ready.

## Purpose of the Project

The project was created to practice:

* C# programming,
* WPF application development,
* XAML,
* object-oriented programming,
* separation of responsibilities,
* client-server architecture,
* TCP/IP networking,
* asynchronous programming,
* event-driven programming,
* game state management,
* implementing non-trivial game logic.

## Author

**Maciej Bros**

GitHub: [@maciejbros](https://github.com/maciejbros)
