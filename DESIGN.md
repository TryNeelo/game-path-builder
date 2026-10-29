# Build the Path — demo design

A path-building game for kids aged 6–8 on iPad. The child lays path pieces on a grid, then taps a goal to send the character walking along the path.

## Board

- The world is a big map made of screen-sized sections, about 6×4 squares each, joined in any direction (up, down, left, right).
- The child never scrolls while building. The section being solved always fits on screen.
- Each section has the character's start square, a star (the goal), one or more coins, and several bats.
- **Terrain shows the routes.** Light meadow squares are buildable. Trees, rocks and ponds block squares: a piece dropped there flies back with a "bonk" (a splash for ponds), and tapping one makes it wobble. The open squares form corridors through each section.
- Bats sit on meadow squares, often on the route that looks most direct. Only a spring can go on a bat: a straight or corner dropped there flies back, and the bat wobbles and says "Oops!".

## Pieces

- The tray holds two pieces, a straight and a corner, and they never run out.
- **Place:** drag a piece from the tray onto a square.
- **Rotate:** tap a placed piece to turn it 90° (bounce + click). Four taps bring it back to the start.
- **Remove:** drag a placed piece anywhere off the grid. It vanishes in a puff with a whoosh. The tray glows while dragging as a hint.

## Squares

- Stepping stones connect from any side and take no pieces. There are three kinds: the start, the star and spring stones.
- A coin sits on a normal square. The child places a piece under it, and the coin becomes part of the route.
- Straights and corners can't go on bat squares; only a spring can.
- The piece the character is standing on must point the way she wants to go. It can be turned (tap) or swapped (drop a new piece on it), but not dragged away.

## Movement

- **Tap the star** (or a spring stone to go and get the spring, or the start stone to go back). The character finds a route over the connected pieces and walks it. This works in any direction, including back the way it came.
- Coins can't be tapped. A tap on a coin square turns the piece under it. Coins on the route are collected as the character passes (ding + counter).
- **Road doesn't reach the star yet:** she heads for the road the child built (or turned) last, follows it to where it runs out, and stops. This lets a child try one route for its coins, then build another and send her back along it.
  - If she collected anything on the way (coins or a spring), she ends with a happy hop.
  - If she found nothing, she shows a puzzled "?" and the gap glows.
  - If nothing new was built since she stopped, tapping the star again leaves her where she is, with the "?".
  - The star stays the only trigger: no go button, and no tapping the character, since her square is a road piece that tapping turns.
- **Road ends at a bat:** she walks up to it and stops, and the bat wobbles and says "Oops!", which tells the child the bat is what's in the way.

## Winning a section

- Reaching the star finishes the section. Coins are a bonus.
- A cheer plays, the star becomes a little flag, and the camera pans to the next section in whatever direction it lies. The character hops across the edge onto the new section's start square (a round stepping stone). A ring then flashes around the new star with a "ping".
- Sections sit side by side with no overlap. A thin strip of the neighbouring sections shows around the edges, faded, so the world feels continuous. A bouncing arrow beside the star points the way the journey continues.
- The demo world is 9 sections winding in a spiral over a 3×3 map: right, right, down, down, left, up, left, down.

## Finding the way

- **Peek during the pan** between sections.
- **Edge arrow:** a small bouncing arrow beside the star points to where the next section lies.
- The corner mini-map and full map view were tried and removed: they showed where you are, which children don't ask about, and confused more than they helped.

## Showing progress (built)

- **A row of stars,** one per section, in a small pill centred on the board's bottom edge, half over the board. It stays close to where the play happens, and the top bar keeps just the coins and the music button. Stars already reached are full colour, the current one glows and pulses, and the rest are faint grey. "What's left" is the grey ones, which a child can count.
- **Reaching a star:** a copy of the star flies from the board into its slot and pops in with a ding. After the camera pan, the next slot starts pulsing.
- It isn't a reward, just a sign of how far along the journey the child is. Coins stay the only reward. Still to check: whether Neelo's framework allows an on-screen progress display like this.
- **Not used:** a coin count out of the total, since one run can't collect every coin and it would never feel complete. Also not used: a journey line with the owl moving along it, and progress shown only between sections.

## Teaching by doing

There's no instruction screen. The first sections each teach one new thing, shown by a see-through "ghost hand" that acts out the move once. The game waits until the child copies it.

1. **Drag + tap.** The character and star are in a straight line with a gap between them. Only the straight piece is in the tray. The hand drags a straight piece into the gap, then taps the star.
2. **Rotate.** A straight piece is already on the board, facing the wrong way. The hand taps it to turn it.
3. **Corner.** The corner piece "unlocks" in the tray with a little fanfare. The route needs a turn.
4. **Bats + removing.** A bat sits on the obvious route, and the one piece already on the board runs straight at it. The hand drags that piece off the board, and the child builds around the bat. Trying to drop a piece on the bat gets an "Oops!".
5. **Coins.** A coin sits on the route, and the counter appears at the top the first time one is collected.
6. **Spring.** The board starts empty. The spring slot unlocks in the tray (×0) with a fanfare. The hand taps the spring stone next to her, and she hops over and picks it up. Then the hand drops it on the pouch bat. The child builds the rest of the road.

Rules for hints:
- Each new thing is taught once, the first time it's needed.
- After that, the hand only comes back if the child is stuck: 3 failed tries, or time without doing anything (6 seconds in the teaching sections, 10 seconds in the free-play sections, since those take more thinking). It points at the next piece that differs from a known good route: a piece to add, remove or turn, or the star once the path is ready.
- The hint never blocks play. Any touch dismisses it.
- No reading needed. Hints are motion and sound only, with an optional one-word label.

Build order: build the game first with these sections as its opening levels, then add the ghost-hand hints on top as a separate step.

## Sound

Everything is generated in code with Web Audio, so there are no audio files:

- Original bouncy 8-bit background music, inspired by the feel of classic platformers without copying any of their themes.
- Effects: drop, spin, whoosh (remove), coin ding, bat flap + "oops", puzzled "?" blip, star fanfare, section pan swoosh.

## Tech

- A web page that plays in Safari on iPad. It can be added to the home screen to run full-screen.
- Touch-first: large touch targets, no hover, no pinch gestures.

## Art

These are in `assets/`:

- `Character.svg`: the owl girl in a white circle.
- `Bat.svg`
- `Coin.svg`
- `Star.svg`

The path tiles and the flag are drawn in code to match the art's style.

## Springs and multiple routes (built)

**Spring piece**
- A third tray piece. Drop it **onto** a bat or rock square. It works like a straight piece: she bounces over that square in an arc and lands on the next square. It works in either direction, and you tap it to turn it like any piece.
- A normal piece on a bat bounces off ("Oops!"). A spring on a bat is a safe hop. That contrast is the lesson.
- Springs can go only on bat and rock squares. Trees are too tall, and ponds are saved for a future bridge piece.
- Springs are collected from spring stones (see "Earned springs" below). The tray shows how many she holds (×0, ×1, ×2). Placing one takes it from the tray, and dragging an unused one off the board gives it back.
- A jump always goes straight: she lands on the next square in the direction she was walking. There is no turning spring. To approach a bat or rock from the side, the road turns before it, on a corner piece or on a stepping stone.

**Why use the spring: pouch bats**
- Some bats hold a little coin pouch, visible before building.
- Springing over a pouch bat startles it: it drops the pouch (+3 coins burst out) and flies away. Plain bats just fly away when hopped.
- **Every jump pays.** Rocks and plain bats have coins on the far side, in a lane you can only reach by springing over them. So every spring is a real "do I want those coins enough to spend my jump here?"
- A spring is **spent** once she bounces on it. It stays on the board as a greyed-out piece that can't be moved or turned. She still bounces over it if she crosses again, but the reward only happens once. Before she uses it, the child can still move it or take it back.
- While a spring is being dragged, every square it can go on gets a pink dashed outline. A spring dropped anywhere else flies back to the tray.
- Pouch bats are a rare treat: one in the spring lesson and one in the finale.

**Ideas considered and set aside**
- Fewest-steps goal: too abstract for ages 6–8.
- Sky coins above bats, saved springs paying out, bat buddies, treasure spots reachable only by spring.

**Fitting the existing game**
- This game has to plug into Neelo's existing game framework, which only supports a coin count. Rewards stay as plain coins, with no extra counters, chests or meters on screen.
- The end of the journey is left as it is for now: the "You built the whole path!" screen with the coin total.

**Spring lesson (section 6)**
- Comes after the coin lesson. A pouch bat blocks the only route, and nothing is pre-built.
- The spring slot unlocks in the tray (×0), and a spring stone sits between her and the bat.
- The hand taps the spring stone. She hops onto it and grabs the spring, which flies into the tray. Then the hand shows dropping the spring on the bat.

**Multiple routes (free-play sections 7–9)**
- Each section has two or three ways to the star. Once a child taps the star they've committed, so the choice happens while building and it has to be about coins:

  | Section | Safe route | Spring over a rock | Spring over a plain bat |
  |---|---|---|---|
  | 7 | 0 coins | quick, +2 | long way round, +3 |
  | 8 | 0 coins | quick, +2 | the spring stone sits right before the bat: turn on it and jump, +3. With a spring saved from section 7: over the rock, through the stone, then over the bat, +5 |

- Sections 7 and 8 each have one spring stone. Spend the spring there or save it.
- The finale (section 9) has no spring to pick up and a safe route, so it depends on what was saved: 0 springs, take the safe route; 1 spring, the pouch bat (+3); 2 springs, a rock and then a plain bat, each with coins behind (+4).
- Hints look at every route to the star. They pick the one that reuses the most pieces the child has already placed, then the one with the fewest changes, and point at its next missing piece. With nothing built, that's the shortest route.
- 9 sections fill the whole 3×3 map.
- Total coins on the journey: 21 (15 ground coins plus 2 pouch bats at +3 each). One run can't collect them all, which gives a reason to replay.
- Hints know about spring stones: if the chosen route needs a spring she doesn't have yet, the hint first builds out to the spring stone and taps it.

## Earned springs: spring stones (built)

- **A spring waits on its own stepping stone,** round like the start and the star. It bobs gently every few seconds. Nothing else on the board moves by itself, so it catches the eye.
- **Tap the stone to go and get it.** She walks the road to it, the spring flies into the tray, and the stone stays a plain stepping stone. Reaching it is a small goal, not a "?". Walking over it on the way somewhere else also collects it.
- **The stone connects on every side,** so the road can turn on it. That solves the "no corner for the jump" problem: a stone placed right before a bat lets her turn and jump.
- **She can always go back for it.** She walks from wherever she stands, so a missed spring can be fetched any time before the star.
- **The star stays the main goal.** When a section opens, the big ring and "ping" go on the star first. A moment later a smaller pink ring and a "boing" mark the spring stone.
- **The empty tray points the way.** Tapping the spring slot at ×0 wobbles it and rings the spring stone, if the section has one.
- **You keep what you collect.** Unused springs stay in the tray into later sections, so a child can spend one right away or save it.
- **Pouch bats are a rare treat:** one in the spring lesson and one in the finale. Sections 7 and 8 use rocks and plain bats with coins behind them.
- **Finale:** has a safe route, since a child may arrive with no springs. Saved springs open the pouch bat (one spring) or the rock plus the plain bat (two springs).
- **Broken roads:** if the road runs out, she still stops at a spring stone on the way when the child built road to it, or when it's closer to the target than where she stands. With nothing built, she stays put.
- **Tried and dropped:** springs lying on ordinary meadow squares. Collecting one meant tapping the star with an unfinished road, walking into a dead end and showing "?", so it felt like failing. And since a spring jump can't turn, a spring sitting right under a bat was a trap.

## Lessons world (built, branch expansion-lessons-bridge)

**The idea.** The child explores and carries sun drops (the stars). Along the way they meet lesson characters. The sun drops help the character overcome something, and that happens in the lesson or quiz. In the real game a lesson can hold four or five lesson or quiz loops.

**A second version beside the first.** The lessons world doesn't replace the path world or follow on from it. Two buttons at the top ("Path" and "Lessons") switch between them, and work from the title screen too. The lessons world is `index.html?world=lessons`. It assumes straights, corners and springs are already known: all three are in the tray from the start, with springs at ×0.

**Lesson stones**
- A light shines down onto a lit stepping stone, and the lesson character or object floats in it, bobbing. The beam stays inside its own square, with room on each side. A character comes as a round portrait and is drawn a little smaller than an object, so the light shows around it.
- The lessons take turns between the bird (`assets/Friend.svg`) and the rain cloud, which is drawn in code: bird, cloud, bird, cloud.
- Tapping the stone sends her there. On arriving, the friend steps up to the stone's corner to make room for her, and the lesson card opens: a placeholder labelled "Lesson / Quiz" with an arrow to continue.
- After the arrow: coins burst out like a pouch bat's (+3), the light goes off, the cloud cheers up, and a copy of the friend flies into the progress row. Then the star wakes, and any stones that were waiting for the lesson fill.

**The sleeping star**
- In a lesson section the star is on the board from the start, grey and asleep. While it sleeps it counts as a closed square, like a tree: she can't walk onto it or land a jump on it, so a saved spring or bridge can't skip the lesson.
- Tapping it makes it wobble and rings the lesson stone. When a section opens, the big ring goes on the lesson, not the star.
- In the map key, `s` and `g` are spring and bridge stones that fill only after the lesson. They are stepping stones from the start, so the road can turn on them.

**The bridge**
- A fourth tray piece, collected from its own stone like a spring. It goes only on a pond square and works like a straight piece, laid over the water's ripples. Once she has walked across it, it stays where it is. Unused bridges come along to the next section.
- Section 2 teaches it, and is also the first road the child builds. The bridge slot unlocks at ×0 and the bridge stone rings. The hand taps the stone next to her, drags a straight piece out to the pond, then lays the bridge on the pond. The last piece to the star is left to the child (the hand helps after a few idle seconds).

**Swipe to explore**
- Press on her square and flick a direction. She sets off as soon as the finger has moved, before it lifts, and follows the road until it ends or she reaches a stepping stone. If nothing is built that way, she leans over and comes back with a small sound.
- A tap on her square still turns the piece she's standing on. The swipe only exists in the lessons world.
- Section 1 teaches it, together with turning a piece: the road to the star is already built, coins and all, but one straight piece is turned the wrong way. The hand taps it to turn it, then presses on her and flicks along the road. The crooked piece is never the one under her, so the tap and the swipe can't get mixed up.

**Stepping stones stay tappable.** An empty spring or bridge stone can still be tapped to send her there, in both worlds.

**Hints keep springs and bridges in hand.** When there's a way round on land, the hand never suggests spending a spring or bridge. Pieces the child has already laid count as free. After that, hints prefer reusing what's built, then the fewest changes, then the shortest route.

**Progress row:** the four friends, faint until their lesson is done. The next one pulses.

**The 12 sections** (a 4×3 map, snaking right, down, left, down, right). There's a lesson in every third section, so one lesson for every three sun drops. Each section is mostly blocked, leaving about 6 to 11 open squares, and they ease in one new thing at a time.

| # | What it's about |
|---|---|
| 1 | Turn and swipe: the road to the star is built, with three coins on it, but one piece is turned the wrong way. Tap it, then swipe |
| 2 | Bridge lesson and first building: fetch the bridge, drag a straight to the pond, lay the bridge, then one more straight to the star |
| 3 | First lesson (bird), kept gentle, and the first turn piece she lays: the hand drags it next to her, then taps it round. A short road to the lesson, then on to the star. Coins sit on short side spurs, worth a swipe |
| 4 | A long land route with 2 coins that passes a spring stone (keep it), or a bridge shortcut |
| 5 | A bat with coins behind it: spend the spring, or take the long safe way |
| 6 | Lesson (cloud). The spring fills after the lesson, and the only way to the star is a jump over the rock beside it |
| 7 | Pouch bat (+3), a rock jump, or the safe way round. A spring stone sits just off the start |
| 8 | A pond column with three crossings. The bridge stone is next to the start |
| 9 | Lesson (bird), reached only across a pond. The spring fills after the lesson, for a rock jump to the star |
| 10 | A safe route, a rock jump, or a spring stone on the way to a bat with coins |
| 11 | A safe route, or a bridge to reach a spring stone, then a spring over the pouch bat |
| 12 | Lesson (cloud), the finale. A bridge and a spring both fill after the lesson |

- Total coins: 44 (26 on the ground, 2 pouch bats at +3, 4 lessons at +3). One run can't collect them all.
- Every section was checked by playing through the whole world using only the hints.
- **Preview:** locally for now. The live link only shows `main`.

## Saved for later

- **The rule for any new piece to collect:** it waits on its own stepping stone, which is a side destination. The star stays the only goal and the main thing to tap. There's no go button: tapping the star or a stone is both the goal and the action (decided 2026-10-28).

- **Bonus paths:** a door square that leads into a side path full of coins. At its end, the child returns to the main path at the door they entered through.
- Fixed piece counts per level, a star that stays locked until all coins are collected, and item squares that only connect on certain sides. These are all harder variants for later levels.
- A quiz or story moment on reaching the star. The demo uses a cheer instead.
