# Battleship
## Play the Game 
[Click here to play](https://ellavitti.github.io/Battleship/battleship.html) 
## Features 
- Ship placement phase: place your fleet manually or use random placement
- 5 Standard ships: Mothership (5), Warship (4), Cruiser (3), Stealth Pod (3), Fighter (2)
- Space warfare theme: star field background, animated title screen, sound effects
- Hit pulse animation, destroyed vessel visuals, asteroid miss indicators
- Ship status tracker for both fleets
- Coordinate labels: A-J columns and 1-10 rows on both grids for easy shot tracking
- AI opponent with hunt/target logic: searches randomly until a hit, then locks onto the ship until it's sunk
- New Mission button to reset and replay
- Fully mobile responsive: grids stack vertically on phones, tested at iPhone width 
## Tools Used
- Devin Desktop: used to build the game and debug Bugs #1-3
- Devin Cloud: audited the codebase across three sessions: found bug #4, added coordinate labels (A-J/1-10), space themes, animation, sound effects, mobile responsiveness, ran 2000 automated simulated games, and submitted 5 PRs
- Devin Review: automatically reviewed all 5 PRs and independently caught Bug #5-8
## Bug Documentation
[View full bug report](https://docs.google.com/document/d/1ySlPv6Ehm5cagyaRcCt9sVeD1scNnE_Cxe70aNpqaGI/edit?usp=sharing): covers 8 bugs found and fixed across manual testing, Devin Cloud's audits, and Devin Review's automated PR analysis. 
