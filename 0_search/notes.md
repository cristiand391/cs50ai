# Search Problems

Puzzles, mazes, directions.

## Terminology:

#### Agent

Entity that perceives its environment and acts upon that environment.

#### State

A configuration of the agent and its environment.

#### Initial state

The state in which the agent begins.

#### Actions

Choices that can be made in a state.

ACTIONS(_s_) returns the set of actions that can be executed in state _s_.

#### Transition model

A description of what state results from performing any applicable action in any state.

RESULT(_s_, _a_) returns the state resulting from performing action _a_ in state _s_.

#### State space

The set of all states reachable from the initial state by any sequence of actions.

#### Goal test

Way to determine whether a given state is a goal state.

#### Path cost

Numerical cost associated with a given path.

#### Solution

A sequence of actions that leads from the initial state to a goal state.

#### Optimal solution

A solution that has the lowest path cost among all solutions.

#### Node

A data structure that keeps track of:

- a **state**
- a **parent** (node that generated this node)
- an **action** (action applied to parent to get node)
- a **path cost** (from initial state to node)

#### Frontier

A data structure that stores all available options (nodes) to explore.

#### Stack

LIFO (last-in, first-out) data type.

#### Queue

FIFO (first-in, first-out) data type.

## Problem solving

### First Approach:

- Start with a frontier that contains the initial state.
- Repeat:
  - If the frontier is empty, then no solution.
  - Remove a node from the frontier.
  - If node contains goal state, return the solution.
  - Expand node, add resulting nodes to the frontier.

The problem with this approach is that, in some cases, we can fall into a loop by exploring states (nodes) that links to previously explored ones.

### Revised Approach:

- Start with a frontier that contains the initial state.
- Start with an empty explored set.
- Repeat:
  - If the frontier is empty, then no solution.
  - Remove a node from the frontier.
  - If node contains goal state, return the solution.
  - Add the node to the explored set.
  - Expand node, add resulting nodes to the frontier if they aren't already in the frontier or the explored set.

Now we store explored nodes in a dedicated set and only add to the frontier those who aren't already in it or in the explored set.

## Possible search options

#### Depth-first search

A search algorithm that always expands the deepest node in the frontier.

It starts exploring the first node (or some arbitrary node in the case of a graph) and keep going deeper through the search tree exploring all possible branches before backing up.
It uses a stack as the frontier.

As long as the search space is finite, it will always find a solution.

#### Breadth-first search

A search algorithm that always expands the shallowest node in the frontier.

This one uses a queue as the frontier, so it explores all of the neighbor nodes at the present depth before moving on to the next level.

## Types of search algorithms

### Uninformed search

A search strategy that uses no problem-specific knowledge.
Examples: DFS and BFS

### Informed search

A search strategy that uses problem-specific knowledge to find solutions more efficiently.

Some examples:

#### Greedy best-first search

A search algorithm that expands the node that is closest to the goal, as estimated by a heuristic function _h(n)_.

#### A\* search

A search algorithm that expands node with lowest value of _g(n)_ + _h(n)_

_g(n)_ = cost to reach node  
_h(n)_ = estimated cost to goal

It is optimal if:

- _h(n)_ is admissible (never overestimates the true cost), and
- _h(n)_ is consistent (for every node **n** and successor **n'** with step cost _c, h(n) ≤ h(n') + c)_
