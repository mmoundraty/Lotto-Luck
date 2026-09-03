# Lotto Luck

**Game Design Document**

## High-Level Concept

A player or party spawns in a casino and gambles at a slot machine to grow their money. Every win draws attention: enemy NPCs enter the casino and attack. Money is health. Taking damage costs money. The goal is to bank as much as possible in the cash-out cage before the casino takes it back.

**Core Loop:** Choose your bet → Spin → Outcome → Wave Spawns → Combat → Repeat.

## Tools for this Game

- Roblox Studio
- Rojo
- Moon Animator 2

## Inspirations

- Spiderman PS5
- Payday 2
- Jujutsu Shenanigans
- Ink Game
- Right 2 Fight

## Core Resources

| Resource | Functionality | Notes |
| --- | --- | --- |
| Wallet | Health & Betting Power | Lost on damage, gained on wins and enemy drops |
| Cage | Permanent Score | Safe forever, but cannot defend you or fund bets |

## Slot Machine

### Bet Types

| Bet Type | Stake |
| --- | --- |
| Safe Bet | 1/5 of wallet |
| Risky Bet | 1/2 of wallet |
| All In | 100% of wallet |

**All-In Loss Floor:** A player who goes All In and loses drops to $1, not to zero. They do not die instantly.

### Outcome Tables

Payout values are return multipliers on the stake.

#### Safe Bet

| Outcome | Rate | Payout |
| --- | --- | --- |
| Lose | .25 | 0x |
| Small Win | .45 | 1.4x |
| Fair Win | .20 | 2.2x |
| Jackpot | .08 | 4x |
| Cursed | .02 | 0x + Relic |

#### Risky Bet

| Outcome | Rate | Payout |
| --- | --- | --- |
| Lose | .32 | 0x |
| Small Win | .35 | 1.6x |
| Fair Win | .22 | 2.6x |
| Jackpot | .08 | 5.5x |
| Cursed | .03 | 0x + Relic |

#### All In

| Outcome | Rate | Payout |
| --- | --- | --- |
| Lose | .35 | 0x (floor to $1) |
| Small Win | .23 | 1.8x |
| Fair Win | .22 | 3x |
| Jackpot | .15 | 7x |
| Cursed | .05 | 0x + Relic |

## Enemy Roster

| Enemy | Role |
| --- | --- |
| Normal | Baseline melee, counterable |
| Fast | Weaker but faster attacks |
| Tank | Heavy attacks but more time before an attack |
| Ranged | Line of Fire attacks, forces dodges |
| Cloaker | Takes half of your money but is very weak and will try to run off to an exit. If it escapes, the player loses their money. Once killed, a player gets their full money back. |
| Healer | Support, heals enemies |

Every enemy tracks how much money it personally took from each player. Once an enemy dies, it drops 10% to 50% of the money it took from each player (Example: If an enemy has taken $10 from Player 1 and $50 from Player 2, they both get their money back depending on the RNG). Players will get their money back in their wallet automatically; it won't be a physical drop.

Enemy damage and health scale across waves. The number of enemies spawned will depend on the party size. Enemies will keep track of each player's wallet so they know how much damage to deal for each player.

## Cash-Out Cage (Scoring)

- Score is money deposited in the cage. Wallet money is not score.
- Money in the cage is permanently safe, but no longer defends the player or funds bets.
- The cage cannot be reached while a wave is active.
- The cage takes a 5% cut and decreases by 1% each wave until 0 after 5 waves. Then resets again to 5% after a player cashes in.
- A player cannot cash out until they have completed their first spin.

## Combat

Combat is inspired by Right 2 Fight. You can perform a light attack, heavy attack, combos, dodge, and counterattacks.

### Attacking

| Input | Output |
| --- | --- |
| M1 | Chain 1 (Light Attack) |
| M1 → M1 | Chain 2 |
| M1 → M1 → M1 | Chain 3 |
| M1 → M1 → M1 → M1 | Chain 4 (Full Combo) |
| M2 | Heavy Attack |

### Defense

A player can have a blocking meter; it can only drain if enemies attack the player and will slowly regain the meter. Players can counter if the blocking meter is not empty, and countering will regain the meter.

### Heat Meter

A player has a heat meter which can be used as an ultimate move against an enemy (one shot). A player can gain progress on their heat meter if they keep killing enemies.

### Movement

The camera will always be third-person and can be moved by mouse.

## Player Death

If a player dies, then they will spectate their party until everyone dies. Once everyone in the party dies, then they can restart the game or go back to the lobby. After the game's demo, there could be a revive feature like in Fortnite or a buy-back feature to get back into the game if the player has not been revived on time.
