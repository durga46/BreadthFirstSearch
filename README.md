# Breadth First Search
## AIM

To develop an algorithm to find the route from the source to the destination point using breadth-first search.

## THEORY
BFS is a traversing algorithm where you should start traversing from a selected node (source or starting node) and traverse the graph layerwise thus exploring the neighbour nodes (nodes which are directly connected to source node). You must then move towards the next-level neighbour nodes.

## DESIGN STEPS

### STEP 1:
Identify a location in the google map:
<br> 

### STEP 2:
Select a specific number of nodes with distance
<br>

### STEP 3:
Import required packages.
<br>

### STEP 4:
Include each node and its distance separately in the dictionary data structure.
<br>

### STEP 5:
End of program.
<br>

## ROUTE MAP
![map 2](https://user-images.githubusercontent.com/75235704/167242266-ade52fd6-3ec6-429f-8df4-e4f9cb0f8400.png)

### PROGRAM
```python
Prepared by 
C. Obed Otto, 
Department of Artificial Intelligence and Datascience,
Saveetha Engineering College. 602105. India.

Experiment done by
Student name DurgDevi P
Reg No 212220230015


%matplotlib inline
import matplotlib.pyplot as plt
import random
import math
import sys
from collections import defaultdict, deque, Counter
from itertools import combinations
### Problems
This is the abstract class. Specific problem domains will subclass this.

class Problem(object):
   def __init__(self, initial=None, goal=None, **kwds): 
       self.__dict__.update(initial=initial, goal=goal, **kwds) 
       
   def actions(self, state):        
       raise NotImplementedError
   def result(self, state, action): 
       raise NotImplementedError
   def is_goal(self, state):        
       return state == self.goal
   def action_cost(self, s, a, s1): 
       return 1
   
   def __str__(self):
       return '{0}({1}, {2})'.format(
           type(self).__name__, self.initial, self.goal)
           
### Nodes
This is the Node in the search tree. Helper functions (expand, path_actions, path_states) use this Node class. 

### class Node:
   def __init__(self, state, parent=None, action=None, path_cost=0):
       self.__dict__.update(state=state, parent=parent, action=action, path_cost=path_cost)

   def __str__(self): 
       return '<{0}>'.format(self.state)
   def __len__(self): 
       return 0 if self.parent is None else (1 + len(self.parent))
   def __lt__(self, other): 
       return self.path_cost < other.path_cost

failure = Node('failure', path_cost=math.inf) 
cutoff  = Node('cutoff',  path_cost=math.inf)

### Helper functions
def expand(problem, node):
   "Expand a node, generating the children nodes."
   s = node.state
   for action in problem.actions(s):
       s1 = problem.result(s, action)
       cost = node.path_cost + problem.action_cost(s, action, s1)
       yield Node(s1, node, action, cost)
       

def path_actions(node):
   "The sequence of actions to get to this node."
   if node.parent is None:
       return []  
   return path_actions(node.parent) + [node.action]


def path_states(node):
   "The sequence of states to get to this node."
   if node in (cutoff, failure, None): 
       return []
   return path_states(node.parent) + [node.state]

FIFOQueue = deque

### Search Algorithm : Breadth First Search
def breadth_first_search(problem):
   "Search shallowest nodes in the search tree first."
   node = Node(problem.initial)
   if problem.is_goal(problem.initial):
       return node
   frontier = FIFOQueue([node])
   reached = {problem.initial}
   while frontier:
       node = frontier.pop()
       for child in expand(problem, node):
           s = child.state
           if problem.is_goal(s):
               return child
           if s not in reached:
               reached.add(s)
               frontier.appendleft(child)
   return failure
```
## OUTPUT:

## SOLUTION JUSTIFICATION:
Found the minimum distance route from the source to the destination point using breadth-first search.

## RESULT:
Thus the program developed for finding route with drawn map and finding its distance covered.

