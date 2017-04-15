# AI4G-Errata
Errata for the second edition of [Artificial Intelligence for Games](https://www.amazon.com/Artificial-Intelligence-Games-Ian-Millington/dp/0123747317).This page is based on a backup of the official errata webpage and the arrata at [perl-hackers.net](http://perl-hackers.net/doku.php?id=games:aigerrata).

## Chapter3: Movement

### Page 47 and 57
first code block, line 13, `orientation` should read `rotation`.

	7 # Update the position and orientation 
	8 position += velocity * time 
	9 orientation += rotation * time 
	10 
	11 # and the velocity and rotation 
	12 velocity += steering.linear
	13 rotation += steering.angular
### Page 49
code block, line 8, `static` should read `velocity`
### Page 50
We use the `Static` data structure should read We use the `Kinematic` data structure
### Page 70
code block, line 37, `explicitTarget` should read target (this class target, not the super class one)
### Page 72
first code block, line 20, `explicitTarget` should read `target` (this class target, not the super class one)
### Page 75
code block, line 34 and 38 should use `target.position `instead of `target`
### Page 78
code block, line 21, `currentPos` should read `currentParam`
### Page 79
code block, line 29, `currentPos` should read `currentParam`
### Page 83
code block, line 30, `direction` should be calculated the other way around, or the objects will attract and not separate.

	30 direction = character.position - target.position
### Page 88/89
An error in the source code, line 66. In the source code for collision avoidance, there is a mistake on line 66.The variable 'distance' is referred to, but that variable has fallen out of scope by this point. Line 66 should read:

	if firstMinSeparation <= 0 or firstDistance < 2*radius:

in the code block, the steering variable is not initialized as usual. So, for instance, on line 74, should be:

	74 steering = new Steering
in the code block, line 35 and 67 should be calculated the other way around:

	35  relativePos = character.position - target.position
	...
	67  relativePos = character.position - firstTarget.position 
### Page 91
in the algorithm, line 34 should use target.position
### Page 98
in the end of the algorithm, max value is computed, min should be. Also, it should be pointed out that we are overloading Min with the possibility to compare a vector (steering.linear) with a real value (maxAcceleration).

	26  steering.linear = min(steering.linear, maxAcceleration)   # this is the overloaded one
	27  steering.angular = min(steering.angular, maxRotation)
### Page 113
line 33 of the algorithm is not needed. That variable is never used. Maybe it was there for a less-algorithmic approach, where `break continue` wasn't allowed.

line 42 of the algorithm, should use `constraint.willViolate(path)`, accordingly with API defined in the next pages.
### Page 118
first code block, line 14 should use `start` and `end`, instead of `startNode` and `endNode`.

In the same block, before calling Astar, heuristic should be initialized. Probably it is worth a `heuristicNode` information, to compute the heuristic only if the end node changed from last time the heuristic was used?
### Page 122
An error in equation 3.3. The two terms used to calculate the change in height are reversed, changing the sign of the delta-height.
In the parentheses under the square root, it should read:

pyt - py0
### Page 199 
method `suggest` should have a first line with `segment = path[problemIndex]`
### Page 141
for correctness, method `checkJumpTime` should `return canAchieve`

## Chapter 4: Pathfinding

### Page 210 
code block:
line 28, `goal` should read `end`;
line 31, `current` should read `current.node`;
line 78, `goal` should read `end`;
line 93 should be: `current = closed.find(current.connection.getFromNode())`
### Page 220 
code block:
line 32, `goal` should read `end`;
line 35, `current` should read `current.node`
line 81, `.cost` should read `.estimatedTotalCost`
line 114, `goal` should read `end`;
line 129 should be: `current = closed.find(current.connection.getFromNode())`
### Section 4.3.4 - Contents comment:
This section is interesting and relevant, but misses some strong opinions to the casual reader. When reading the heaps section the reader will be convinced that that data structure is great. But it is not clear, for someone not familiar with heaps, that the `find`, the `contains` and the `remove-element` methods are too inefficient (full tree look-up, and probably full heap reordering during random element removal. Removal is just a problem for A*, given that Dijkstra removes only the tree head.
### Page 259 
When discussing que Average Minimum Distance, the paragraph concludes with “So the average cost of moving from C to D is 31/2”, where it should be 7/2, or if you want to use the same digits, “3 1/2” :smile:
### Page 261 
The algorithm “as is” does not work, as it has an infinite loop, as `currentLevel` doensn't get changed. My correction is presented below. Also, line 7 is not needed, as `startNode` gets rewritten in the loop.

	21: currentLevel--
	22:
	23: # Are the start and end node the same? 
	24: if startNode == endNode:
	25:    # Skip this level
	26:    continue
	27:
	28: # Otherwise we can perform the plan
	29: graph.setLevel(levelOfNodes)
	30: ...
### Page 264 
 Figure 4.42, can't understand how the maximin costs were computed. For example, the route from the upper room to the smaller center room, should be 8 (the maximum of all minimum routes). So, not sure this example is correct. A fixed (?) example on [perl-hackers.net](http://perl-hackers.net/lib/exe/detail.php?id=games%3Aaigerrata&media=games:hieracost2.png)

## Chapter 5: Decision Making

### Page 301 
class Action should extend DecisionTreeNode.
### Page 307 
the code should be a class, not a struct.
### Page 326 
first code block, like 11 should be `result = UpdateResult()` for consistency with line 35 of page 327. Also, I would add a `parent` variable, of type HSMBase, that is already used in the algorithm. It would be None at the top level, and would include its parent on other levels.
### Page 352 
 the Pause task should return True, not the non initialized variable `result`
### Page 400 
lines 26/27 of the code should appear before the foreach look in line 20.
### Page 400 
line 50 of the algorithm, should read `currentTime = resetTime`
### Page 407 in the algorithm:
line 8 could cycle through `actions[1..]` like previous algorithms.
line 23 is `for goal in goals`
line 28 should call `getDiscontentment(newValue)` – but I would use `discontentment += newValue * newValue`
line 29 is missing `return discontentment`
### Page 408 
I can't see why setting the getDiscontentment method in a class (see previous item)
### Page 410 in the algorithm:
line 7 is `for goal in goals`
line 16 is missing `return discontentment`
### Page 430 
In the bottom paragraphs, “The last two items” should refer “The last item”.
### Page 438 
Code, line 8, should say 'isInstanceOf' instead of 'insistence'
Page 438 
Code, line 11, should use 'if not identifier.isWildcard()'
### Page 439 
Code, line 8, should say 'isInstanceOf' instead of 'insistence'
### Page 439 
Code, line 11, should use 'identifier.isWildcard()' as the previous algorithm

## Chapter 6: Learning

### Page 586 
line 24 of the algorithm, `function` should be called with the full array, just like in the beginning of the algorithm.
### Page 592 
line 24 of the algorithm, `function` should be called with the full array, just like in the beginning of the algorithm.
### Page 596 
after 20 times should read after 100 times.
### Page 604
Subarray selections (slices) are kind of weird, or my mind complete blow up.
Line 40, `subActions = actions[i:nValue-1]`
### Page 611
Code, line 17, there is no need for attribute `self`
