**Assignment 1 – Vacuum Cleaner** 

**Utility Based Agent** 

We proposed a utiliy based agent whose utility function is to earn as many points as possible. To do this, we develope an algorithm for our robot’s decision mechanism as follows: 

- If the room is dirty, clean the room. (This option will give +1 point) 
- If, the room is already clean, perform the noOp, goLeft or goRight. (If the agent is B, goLeft or goRight operations will decrease the total points by -0.5) 

To perform noOp, goLeft or goRight operations, there is a decision algorithm : we calculate the estimated probabilities (for each room, for each 100 iterations), in each step we increase or decrease some priorities for each room with It’s estimated probabilities of getting dirty. At the end of some comparison between the priorities, the next step will be determined. 

**Source Code For Agent- A** 

We used random and time modules. 

At the beginning of the code, we are setting the seed to ![](Aspose.Words.50d25f13-a29b-4dee-bca8-609bfc33963f.001.png)the current time to make the generation of random numbers appear more unpredictable. 

We considered robot and rooms as an object, so we ![](Aspose.Words.50d25f13-a29b-4dee-bca8-609bfc33963f.002.png)create classes for them. 

In the Rooms class, the room name ( A , B or C), states (Dirty as D, Clean as C), probability (to get dirty), operations (noOp, goLeft, goRight). (suck operation performed if the room is dirty, so we don’t store it as an operation). 

In Robot class, the location of the robot, total points and estimated probabilities of each room stored.  

We define a function that returns the max value. We used this function to determine which room has the ![](Aspose.Words.50d25f13-a29b-4dee-bca8-609bfc33963f.003.png)biggest probability of get dirty. 

We initalize the rooms as dirty.  ![](Aspose.Words.50d25f13-a29b-4dee-bca8-609bfc33963f.004.png)

The given probabilities of rooms by user stored on P variable. 

For each room, It has It’s own operation. (There is no room on A’s left, so only right or noOp operation performed, same as C’s right.) 

We initalize the robot in b and the initial estimated probabilities as 0.5 . According to learning process, the estimated probabilities will be calculated again. 

In each 100 iteration, the estimated ![](Aspose.Words.50d25f13-a29b-4dee-bca8-609bfc33963f.005.png)probabilites recalculated. According to countX (counts the number of suck operation) and totalX (counts the number of visited that room), the division operation gives an approximation about probabilities. 

The round() operation performed for clean results to get 0.x results. 

At the bottom if blocks, If the estimated probabilities results different than the stored in robot’s probabilities, the increment or decrement operations performed. 

This is the learning part of our code. 

The “main room” selected here. According to ![](Aspose.Words.50d25f13-a29b-4dee-bca8-609bfc33963f.006.png)the main room (the probabilistic dirtiest room) we give some prioritisation.  

The reason of why we do this, If the move operation performed according to only probabilities, the robot stays the same room for a long time. 

The calculation of totalX (number of visited ![](Aspose.Words.50d25f13-a29b-4dee-bca8-609bfc33963f.007.png)that specific room) performed here. 

In this block, If the room is dirty, Suck ![](Aspose.Words.50d25f13-a29b-4dee-bca8-609bfc33963f.008.png)operation performed. 

Also the countX (the number of suck operation performed that specific room) calculated here. At the end of this block, the total point incremented and the state changed to Clear.

In first 100 iteration, the robot will perform ![](Aspose.Words.50d25f13-a29b-4dee-bca8-609bfc33963f.009.png)randomly operations. According to that random opearations, robot will have an estimation of probability of getting dirty for each room. According to that estimations, It will update it’s initial suggestions (0.5, 0.5 , 0.5) 

After 100 iteration, If the room is dirty, next ![](Aspose.Words.50d25f13-a29b-4dee-bca8-609bfc33963f.010.png)operation will be selected in here. 

If the room is in X, the priority of other rooms will be incremented by its estimated probabilities and priority of that X room decremented to zero because It’s already cleaned. 

According to priority comparisons, the next operation performed. 

As a result, we use the estimated probabilities to give some priorities to the rooms, and according to that priorization, the next operation is selected. 

This block determines the next operation randomly ![](Aspose.Words.50d25f13-a29b-4dee-bca8-609bfc33963f.011.png)for first 100 iterations. 

**Source Code For Agent-B** 

We use the same code with a few additions; ![](Aspose.Words.50d25f13-a29b-4dee-bca8-609bfc33963f.012.png)0.5 penalty points for move operations. 

Higher priority criteria for move operations. The reason for this is that when we perform a move operation, at the end of this operation we have to gain a 0.5 points. So, we carry out our utility function (get as many points as) 

**Results of The Simulation** 

![](Aspose.Words.50d25f13-a29b-4dee-bca8-609bfc33963f.013.png)

We can see that from configure 5 that Agent A and Agent B perform better when given high probabilities. 

Also, If we look at configure 3 and configure 4, the Agent-A performs slightly worse but Agent-B  performs slightly better. The reason may be that Agent-B stays more in room A than Agent-B. 

If we check configure 1 and configure 2, again Agent-B performs slightly less, but Agent-B performs better. Agent-B probably waits for room A to be sure that other rooms will get dirty. 

If we look at configure 2 and configure 4, the decrease in Pb by 0.1 effect more than increase of Pc by 0.2. Both agents performed less. The reason could be that the room B is in the center. If the robot performs to go C, it needs to be sure that B is also dirty. 
