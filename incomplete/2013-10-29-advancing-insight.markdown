---
layout: post
title:  "(Slow but certain) Advancing insight in Haskell"
date:   2013-10-29 21:00:37
categories: programming haskell
---

TL;DR I tried to implement something in Haskell but had some trouble.
I then went to hang out at the Haskell irc channel and they directed me towards a better implementation, making me a little bit smarter.

I am in the process of learning Haskell.
Coming from iterative languages, thinking in a functional way is quite challenging.
Recently, I encountered a situation where I had trouble finding an elegant solution.
I mucked around for a bit and after I found something that worked somewhat, I headed over to the Haskell irc channel where the great folks directed me to a much better solution.


I am a basketball fan and I had written a small *play-by-play* parser using Parsec.
The outcome of this parser gave an overview of actions that happened in the game, such as "PlayerX" grabbed a rebound, "PlayerY" missed a shot.
Satisfied with my little experiment using Parsec, I then wanted to aggregate these actions and arrive at a traditional *box-score*.
The parser output and needed data-types look as follows:

    data Event = Action String ActionType deriving (Show)
    data ActionType = MissedShot
                    | MadeShot
                    | Rebound
                    deriving (Show)

    output = [Action "PlayerA" MissedShot, Action "PlayerB" Rebound, Action "PlayerB" MadeShot, ...]

The new output should be a list of players with aggregated stats, so I created (after learning about Data.Map) a player data type as follows:

	import qualified Data.Map as M
    data Player = Player Int Int Int deriving (Show)
	--- integers stand for: made shots, missed shots, rebounds
	type Players = M.map String Player

In my first attempt, I defined functions to add shots and rebounds.
I then defined a function that takes the list of events together with the existing players and updates these existing players with each event.
It looked as follows:

	addRebound :: Maybe Player -> Player
	addRebound (Just (Player made missed rebound)) = Player made missed (rebound + 1)
	addRebound Nothing = Player 0 0 1 

	addMadeShot :: Maybe Player -> Player
	addMadeShot (Just (Player made missed rebound)) = Player (made + 1) missed rebound
	addMadeShot Nothing = Player 1 0 0 

	addMissedShot :: Maybe Player -> Player
	addMissedShot (Just (Player made missed rebound)) = Player made (missed + 1) rebound
	addMissedShot Nothing = Player 0 1 0

	aggregate :: [Event] -> Players -> Players
	aggregate [] p = p 
	aggregate ((Action name MadeShot):rest) players = aggregate rest (M.insert name (addMadeShot (M.lookup name players)) players)
	aggregate ((Action name MissedShot):rest) players = aggregate rest (M.insert name (addMissedShot (M.lookup name players)) players)
	aggregate ((Action name Rebound):rest) players = aggregate rest (M.insert name (addRebound (M.lookup name players)) players)

	-- hint, you can run this piece of code in ghci as follows:
	-- $ :load filename
	-- $ import Data.Map as M
	-- $ aggregate output M.empty

The iterative tendencies are easily spotted, those add... methods are simply record updates.
It is clear that this approach is neither elegant or "haskelly".
When one would want to account for extra actions, such as steals for example, a new method would have to be added as well and the "aggregate" function would have to be able to recognise that new category.

The folks on irc advised me to look at the Player data type with a different mindset.
Instead of updating fields, players should be added together.
There should be a "zeroPlayer", with all fields initialised to 0.
There should also be a "reboundPlayer", a player with 1 rebound.
Similar for the "madeShotPlayer" and "missedShotPlayer".
By defining these players and a generic player addition function, the different add... methods can be eliminated.
I also changed my parser slightly so the actions are of type `Action String Player` and I used the "record" syntax for data type definition.

	import qualified Data.Map as M
	data Player = Player { madeShot :: Int, missedShot :: Int, rebound :: Int} deriving (Show)
	data Event= Action String Player deriving (Show)

	type Players = M.Map Name Player

	addPlayer :: Player -> Player -> Player
	addPlayer (Player a1 a2 a3) (Player b1 b2 b3) = Player (a1+b1) (a2+b2) (a3+b3)

	zeroPlayer = Player 0 0 0
	madeShotPlayer = zeroPlayer {madeShot = 1}
	missedShotPlayer = zeroPlayer {missedShot = 1}
	reboundPlayer = zeroPlayer {rebound=1}

	aggregate :: [Event] -> Players -> Players
	aggregate [] p = p
	aggregate ((Action name p):rest) players = aggregate rest (M.insertWith (addPlayer) name players)

    output = [Action "playera" madeShotPlayer, Action "playerb" missedShotPlayer, Action "playera" madeShotPlayer]

When writing the above piece of code, it seemed as if the language was working with me instead of against me, definitely a good sign!
The next steps include using "folding" in the aggregate function and maybe using a map to hold the different statistic categories in the player data type.

Would you write this piece of code differently? Let me know in the comments!
