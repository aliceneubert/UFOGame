Method: Because I had direct access to the game’s source code, I decided to build the learning directly into the game.
I refactored the keystroke reading to allow keystrokes from other sources. Then, I created a “random” player for the game, that inputs up, down, left, right, or nothing randomly every frame.
Then, I tested the average score of this player to compare against the various machine learning techniques. 
Then, I set about altering the game to make it easier to measure. I changed the number of asteroids to 1, in order to get results faster. I also changed the game to skip rendering unimportant frames so that it could test itself quicker. I also added an average score display and eliminated the need to press keys to start or restart a round. 
Then, I built a template for a machine learning game player. This player would take data produced by the random game player, or a human game player, and produce a keystroke every frame. This template could be filled in by any classifier.
I then implemented this for many different classifiers. I used several classifiers from Sci-Kit Learn, as well as the Keras wrapper for tensorflow neural networks to test this.

Feature Extraction: Because I had access to the source code for this game, I was able to extract the features directly from the objects. I had a few different sets of features to try. The first one was the x and y locations and velocities for both the ufo and the asteroid. 

The second set of features I tried was an attempt to make simpler, easier to understand features. The first set of features had too much variation for something like a decision tree to understand. Good results took gigabytes of data to achieve. I separated the play area into a grid. Where before, I gave the exact location of each object, now I would give the learning algorithm a grid, with the UFO’s location marked with a 1 and an asteroid’s location with a 2. A zone containing both will be marked with a 3. This was attempted both containing the velocities of the ufo/asteroid and without them.

To teach the classifiers to win, rather than to imitate a random number generator, all frames within 150 frames of dying were forgotten. Because there are far more good moves than bad in a 1-asteroid scenario, it should be most important to learn the moves that do not kill the player.

![](https://github.com/ZacNeubert/UFOGame/blob/master/stats/humaninputvsrng.png?raw=true)
