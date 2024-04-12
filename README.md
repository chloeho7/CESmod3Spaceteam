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
Our group also had the idea of implementing a "Shake" functionality by having the players press both their buttons at the same time. While we didn't end up implementing it, we thought it would be of interest to share the general concept we were considering in how to make it work. 

The shake functionality requires that all the devices send the same response, so somehow we had to make it such that each device sends out an ASK for "Shake" at seemingly the same time. We thought the best way to do this was by having a chain reaction where each device that recieved an ASK command for shake would immediately send out an ASK command for shake. Somehow we would add markers that would also allow each device to know which DONE command corresponds with the ASK command it recieved.

In order to make sure that the device wouldn't move on until each device had responded, we also thought we could have each device send out only a fraction of the total progress value. Once all the devices have responded, the progress would total to a whole number, but until then the devices would be stuck waiting until their progress was no longer a non-whole number. 

The image below shows how we imagined for this cycle to work:

<img src="https://github.com/chloeho7/CESmod3Spaceteam/blob/master/IMG_9815.jpg" width='200'>
