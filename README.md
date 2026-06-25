# Battleship
## Play the Game 
[Click here to play](https://ellavitti.github.io/Battleship/battleship.html) 
### Features 
- Ship placement phase: place your fleet manually or use random placement
- 5 Standard ships: Carrier (5), Battleship (4), Cruiser (3), Submarine (3), Destroyer (2)
- Ship outlines for easy visibility: each ship is clearly bordered so fleets are easy to read at a glance
- AI opponent with hunt/target logic: searches randomly until a hit, then locks onto the ship until it's sunk
- Visual states for hits, misses, and sunk ships
- Ship status tracker for both fleets
- New Game button to reset and replay
- Coordinate labels: A-J columns and 1-10 rows on both grids for easy shot tracking
- Fully mobile responsive: grids stack vertically on phones, tested at iPhone width 
#### Tools Used
- Devin Desktop: used to build the game and debug Bugs #1-3
- Devin Cloud: audited the codebase across three sessions: found bug #4, added coordinate labels (A-J/1-10), added mobile responsiveness, ran 2000 automated simulated games, and submited three PRs
- Devin Review: automatically reviewed both PRs and independently caught Bug #5 during the PR #2 review
##### Bug Documentation
[View full bug report](https://docs.google.com/document/d/1ySlPv6Ehm5cagyaRcCt9sVeD1scNnE_Cxe70aNpqaGI/edit?usp=sharing): covers 5 bugs found and fixed across manual testing and Devin Cloud's audits, and Devin Review's automated PR analysis. 
