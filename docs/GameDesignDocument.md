# GAME DESIGN DOCUMENT (GDD)

**Game Name:** Gathering of Chaos

**Genre:** Strategy / Multiplayer Card Battler / Tabletop

**Game Elements:** Poker-style combat scaling, deck building and manipulation, triggering "Berserk" state interrupts, and locking in suit-based buffs.

**Players:** 1 to 4, however, currently it supports 1 player against 1-3 AI oppoenents

## TECHNICAL SPECS
* **Technical Form:** 2D graphics (flat) for the current rapid prototype, transitioning to 3D graphics (form) for the final release to enhance the tabletop feel.
* **View:** Top-down camera view.
* **Platform:** PC
* **Language:** C# (Unity Engine)
* **Device:** PC

## GAME PLAY
Gathering of Chaos drops players into a card game where they draw from a central deck to build poker-styled hands. Some examples being playing a Straight Flush immediately halves the target's HP, bypassing standard armor, while deploying a Void card permanently bans a mechanic from the table and more!

### Game Play Outline
* **Opening the game application:** Main menu with Play, Options, and Exit.
* **Game options:** Future Audio settings and a future ruleset reference screen.
* **Story synopsis:** Travelers meet at a tavern and decide to fight it out with magic in order to be the last one standing.
* **Modes:** Free-for-all multiplayer.
* **Game elements:** Central deck, discard pile, player hands, health trackers, and permanent buff zones.
* **Game levels:** The game scales through Round 1, with the Joker card injected into the deck after Round 3.
* **Player's controls:** Mouse-driven click-to-select for playing cards and choosing targets.
* **Winning:** Being the last player alive.
* **Losing:** Health points reaching zero.
* **End:** A final score screen showing the surviving player and total damage dealt.
* **Why is all this fun?:** It combines structured card math with betrayals, and massive power swings.

## Key Features
* **Poker-Scaling Combat:** Utilize actual Poker hands (Pairs, Triples, Straights) to mathematically scale damage output.
* **The Berserk State Interrupt:** A retaliation system that instantly hijacks the turn order to punish players for teaming up.
* **The Joker Class Mutation:** A physical card injected mid-game that permanently mutates a player's ruleset and abilities.
* **The Four 10s Ultimatum:** A game-shifting choice mechanic that pauses the game and forces a brutal table-wide decision.

## DESIGN DOCUMENT

### Design Guidelines
Card data would ideally be decoupled to keep things modular, and the turn order must utilize a stack based state machine to accommodate the Berserk interrupt without breaking the game loop as well as maintaing state between other players and actions.

### Game Design Definitions
The main focus of the gameplay is risk management. A player wins by surviving to the end or eliminating all opponents, and loses when their HP hits zero. Transitions between rounds occur automatically when all players have completed their Draw, Action, and Discard phases.

## Game Flowchart
* **Menu:** Start -> Loads Main Scene.
* **Synopsis:** Hand distribution -> Guaranteed 1 Spade, 1 Heart, 1 Diamond, 1 Club, 1 non-duplicate Nine, 1 random card.
* **Game Play:** Draw -> Action (Play up to 5 cards) -> Resolve Damage -> Discard.
* **Player Control:** Select cards -> Choose target -> Confirm Attack.
* **Game Over:** Last player standing wins; elimination upon 0 HP.

## Player Definition

### Player Stats
* **Health:** Each player starts with 180 HP.
* **Weapons:** A 52-card base deck and 24 Special Cards.
* **Actions:** Play up to 5 cards per attack, lock in 4 suit cards for a permanent buff, trigger Berserk interrupts, or activate Joker dice rolls.

### Player Properties
* **Current Health:** Drops when attacked; feedback is a visual depletion of the UI health bar and floating damage text.
* **Active Buffs:** Changes when 4 suits are locked in; feedback is a visual UI token appearing in the Permanent Buff Zone.
* **Class Status:** Changes if the Joker is drawn; feedback is an updated player portrait and new stat modifiers applied to the HUD.

### Player Cards (Power-Ups, Special Cards, and Pick-Ups)

**The Special Cards (24 Total in Deck):**
* **Double Damage Card (4x):** Empowers your next attack to deal 2x damage. Returns to pile.
* **Damage Per Round Card (4x):** Applies ongoing passive damage to a target every round. Returns to pile.
* **Heal 30 HP Card (4x):** Replenishes 30 health instantly. Returns to pile.
* **Reveal 4 Cards (4x):** Forces all players at the table to reveal 4 cards from their hand. Removed from the game after use.
* **AoE Attack Card (4x):** Attacks all players simultaneously without consuming your main attack for the turn. Removed from the game after use.
* **Forced All-In Card (3x):** Choose a target. Both you and the target are forced to immediately play all cards in your hands against each other.
* **The Void Card (1x):** The ultimate ban card. Used once per game to permanently ban 1 special card type and 2 normal number ranks from the table. Cannot be undone.

**The Buffs (Requires 2 matching suit cards to lock in; can be swapped at any time before the turn ends, can only do swap once per round):**
* **Spades Suit Buff:** Grants a permanent +1 bonus damage and deals 2 passive chip damage to one random opponent at the end of your turn.
* **Hearts Suit Buff:** Grants immunity to passive chip damage. Once per game, if you take lethal damage, you survive with 1 HP, but your locked Heart cards are permanently destroyed.
* **Diamonds Suit Buff:** Grants +1 flat defense. Once per game, you can activate this buff to gain a temporary 20 HP shield for one round.
* **Clubs Suit Buff:** Once per round, force an opponent to roll a 6-sided die. On a roll of 1 or 2, they take 25 damage.
* **The Joker Card:** Injected into the deck after Round 3. Drawing it allows the player to mutate their class, gaining +15% Max HP, +1 Attack, +1 Defense, and unique dice-roll abilities.

## User Interface (UI)
Control of the game will be mouse-dependent on PC, utilizing left-clicks to select cards from the Hand panel and clicking opponent portraits to target them. To ensure playability and avoid overlapping elements, the prototype utilizes a clean, physical separation of data zones (Central Board, Player Mats) in a 2D top-down view.
