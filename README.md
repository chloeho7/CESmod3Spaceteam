# CESmod3Spaceteam
Team: Chloe, Julia, Annika, Orli, Canyon, Raven

## Module 3 Overview
The goal of this Module was to give us experience with building and modifying distributed systems through an ESP32 Space Team game. We had to add new functionality to the existing ESP32 Space Team code in 

## Project
Our goal for this Module was to add levels of increasing difficulty to the existing Space Team game. Initially we also wanted to add a "SHAKE" functionality to the game like in the iPhone Space Team, but adding levels ended up taking a lot longer than we thought it would, and we did not end up getting to this. We leave it to future work!

## Adding Levels
We added levels to the Space Team game and with each increasing level, the time you have to fulfill a request decreases by 5 seconds. We also added a win game condition after beating Level 5 where you only have 5 seconds to fulfill each request. 

Originally, we wanted to accomplish this using NVS (Non-volatile Storage) to keep track of our `level` and `expireLength` variables across ESP restarts. We were able to implement variable storage in memory, but then ran into the problem of when to fully reset the variables back to `level=1` and `expireLength=25`. Taking this question into account, we decided to get rid of the `ESP.restart()` after each level and just manually reset the `progress` back to 0 so that we could keep track of variables across levels.

## Adding SHAKE (attempt)
