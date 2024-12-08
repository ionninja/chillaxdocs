# Blackjack Game Logic

<primary-label ref="stable"/>
<secondary-label ref="beta"/>

<tldr>
  <p>This module implements the core logic for a Blackjack game, including player actions, dealer actions, and game phases.</p>
  <img src="flowchart.png" alt="Flowchart of Blackjack Game Logic"/>
</tldr>

<procedure title="To manage a Blackjack game:" id="procedure-id">
   <step>Initialize the game by creating a new `Lobby` instance.</step>
   <step>Add players to the lobby and manage their bets.</step>
   <step>Deal cards to players and the dealer.</step>
   <step>Handle player actions such as hit, stand, double, and split.</step>
   <step>Resolve the game by revealing the dealer's hand and determining the outcomes.</step>
   <p>Congratulations! You have successfully managed a Blackjack game.</p>
   <p>Need more help? Checkout the <a href="Installation-guide.md">Installation-guide</a>!</p>
</procedure>

While not strictly necessary, the following things are highly recommended:

* Ensure that the database schema and models are correctly defined to support the queries used in this module.
* Implement proper error handling and logging mechanisms to capture and address any issues that may arise during the execution of the game logic.

## Classes

### `JackError`

Custom error class for handling game-specific errors.

### `PlayingCard`

Represents a playing card with a rank and suit.

### `Hand`

Represents a hand of cards for a player or dealer.

### `Player`

Represents a player in the game.

### `Dealer`

Represents the dealer in the game.

### `Deck`

Represents a deck of playing cards.

### `Lobby`

Manages the game state, player actions, and game phases.

## Functions

### `getPerfectPairs`

Calculates the payout for the Perfect Pairs side bet.

### `get21Plus3`

Calculates the payout for the 21+3 side bet.

### `sleep`

Utility function to pause execution for a specified duration.

## Game Phases

1. **Waiting Phase**: The game is waiting for players to join.
2. **Betting Phase**: Players place their bets.
3. **Dealing Phase**: Cards are dealt to players and the dealer.
4. **Insurance Phase**: Players can take insurance if the dealer shows an Ace.
5. **Turning Phase**: Players take their turns to hit, stand, double, or split.
6. **Revealing Phase**: The dealer reveals their hand and the game outcomes are determined.

## Player Actions

- **HIT**: Draw an additional card.
- **STAND**: Keep the current hand.
- **DOUBLE**: Double the bet and draw one final card.
- **SPLIT**: Split the hand into two separate hands if the first two cards have the same value.

## Example Usage

```typescript
const lobby = new Lobby("table1");
const player = new Player({ id: "player1", displayName: "John", currency: "USD" });

lobby.addPlayer(player, 0);
lobby.playerBet("player1", 0, [{ type: "main", amount: 100 }]);
lobby.playerAction("player1", 0, 0, "HIT");