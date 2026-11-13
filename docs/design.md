# Proter - Data Design

## Card
A card has 2 fields:
- suit: text (hearts, diamonds, clubs or spades)
- rank: text (A, 2, 3, 4, 5, 6, 7, 8, 9, 10, J, Q, K)

rank is text, not a number, because of A, J, Q and K.

## Card id
Every card gets a unique id made from rank and suit joined with a dash.
Examples: "7-hearts", "A-spades", "10-clubs".
The id is needed to point to one exact card when it moves between a hand,
the discard pile and a meld, and to send it online later.

## Player
 name: text
- type: text (human, bot or online)
- hand: list of cards (6 at the start of a round)
- score: number (total points over all rounds, lower is better)
- hasMelded: true/false (needed because a player's first meld of the
  round cannot use a wild card)

## Game state
Everything needed to continue the game from any moment:
- players: list of players
- drawPile: list of cards (face down)
- discardPile: list of cards (face up)
- melds: list of melds on the table
- currentPlayerIndex: number (whose turn it is)
- round: number from 1 to 13

## Dealing (3 players, 6 cards each)
3 players x 6 cards = 18 cards dealt.
52 - 18 = 34 cards are left for the draw pile.
Then one card is flipped onto the discard pile (see Open questions),
so the draw pile has 33 cards and the discard pile has 1.

## Open questions
1. Does the discard pile start empty?
   Decision: no. After dealing, flip the top card of the draw pile
   onto the discard pile so the first player has a choice.
2. If a player puts all their cards into melds and has nothing to discard?
   Decision: the round ends immediately and that player scores 0.
3. What if the draw pile runs out?
   Decision: keep the top discard card, shuffle the rest of the discard
   pile and use it as the new draw pile.
4. What if scores are tied at the end of round 13?
   Decision: tied players with the lowest score share the win.