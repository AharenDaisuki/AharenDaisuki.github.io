---
title: 'Minimax Algorithm: variations & implementations'
date: 2023-02-06
permalink: /posts/2023/02/minimaxAlgo/
tags:
- Artificial Intelligence
- Game Theory
- Game Programming
---

Minimax algorithm is a recursive algorithm for choosing the next move in an n-player game, usually a two-player game.

Roadmap
======
I Minimax

II Negamax

III AB Negamax

Alpha Beta Pruning
======

Pseudo-code
------

```
function alphaBetaPruning(node, depth, {alpha, beta}, MAXIMIZE_PLAYER):

1. if node is a leaf node:
    return node value
   end if

2. if MAXIMIZE_PLAYER == true:
    v := -inf
    for all child of node:
        v := max(v, alphaBetaPruning(child, depth+1, {alpha, beta}, false))
        alpha := max(alpha, v) // update alpha in maximize player's turn
        if beta <= alpha:
            break // beta pruning
        end if
    end for
    return v
    
   else:
    v := inf
    for all child of node:
        v := min(v, alphaBetaPruning(child, depth+1, {alpha, beta}, true))
        beta := min(beta, v) // update beta in minimize player's turn
        if beta <= alpha:
            break // alpha pruning
        endif
    end for
    return v
   end if 
```

``` 
// invoke (MAX game)
alphaBetaPruning(root, depth, {-inf, inf}, true)
```

test case
------
[alpha_beta_pruning](https://www.javatpoint.com/ai-alpha-beta-pruning)

intuitive
------
alpha: the lower bound of proposal solution received by MIN player (from MAX player)

beta: the upper bound of proposal solution received by MAX player (from MIN player)

alpha value is updated by MAX player and constrains MIN player while beta value is updated by 
MIN player and constrains MAX player.

AB Negamax
======

Pseudo-code
------
```python
def abNegamax(node, maxDepth, currentDepth, alpha, beta):
    # leaf node
    if node.isLeafNode() or currentDepth == maxDepth:
        return node.getValue(), None
    
    # intermediate
    bestMove = None
    bestScore = -inf
    
    # dfs
    for move in node.getMoves():
        recursedScore, currentMove = abNegamax(move, maxDepth, currentDepth+1, -beta, -max(alpha, bestScore))
        currentScore = -recursedScore
        if currentScore > bestScore:
            bestScore = currentScore
            bestMove = move
        # pruning    
        if bestScore >= beta:
            return bestScore, bestMove
        
    return bestScore, bestMove
```

Performance
------
O(d) in memory, O(nd) in time complexity, where d is the maximum depth and n is branch factor.

Implementation (to be modified)
------
```python
# constant
INT_INF = 0x7fffffff
MIN_PLAYER = 0
MAX_PLAYER = 1
```
```python
class Node:
    
    def __init__(self, child, index=-1, alphaBeta=(-INT_INF, INT_INF), value=-INT_INF, strategy=MIN_PLAYER, depth=0):
        self.index_ = index # node index
        self.alphaBeta_ = alphaBeta # alpha beta 
        self.child_ = child # child nodes
        self.value_ = value # utility score
        self.strategy_ = strategy # play strategy
        self.depth_ = depth # node depth
        self.pruned_ = False
        
    def __str__(self):
        return "[{}]: (value: {}, alpha:{}, beta: {}, pruned: {})".format(
            self.index_, 
            "-inf" if self.value_ == -INT_INF else str(self.value_), 
            "-inf" if self.alphaBeta_[0] == -INT_INF else str(self.alphaBeta_[0]),
            "inf" if self.alphaBeta_[1] == INT_INF else str(self.alphaBeta_[1]),
            self.pruned_)
    
    def getChild(self):
        return self.child_
    
    def addChild(self, child):
        self.child_.append(child)
        
    def getStrategy(self):
        return self.strategy_
    
    def getDepth(self):
        return self.depth_
    
    def getIndex(self):
        return self.index_
    
    def getValue(self):
        return self.value_
    
    def setValue(self, value):
        self.value_ = value
        
    def setStrategy(self, strategy):
        self.strategy_ = strategy
        
    def setDepth(self, depth):
        self.depth_ = depth
        
    def setIndex(self, index):
        self.index_ = index 
        
    def setAlphaBeta(self, alphaBeta):
        self.alphaBeta_ = alphaBeta
        
    def markPruned(self):
        """all postnodes all skipped"""
        self.pruned_ = True
```
```python
class ABbot():
    
    def __constructTree(self, tree):
        """given tree data, construct a tree without initializing node strategy and depth. return root node"""
        if type(tree) is int:
            return Node(child=[], value = tree)
        rootNode = Node(child=[])
        for subtree in tree:
            childNode = self.__constructTree(subtree)
            rootNode.addChild(childNode)
        return rootNode
    
    def __adjustTree(self, root, strategy, depth):
        root.setStrategy(strategy)
        root.setDepth(depth)
        root.setIndex(self.node_n_)
        self.node_n_ += 1
        for child in root.getChild():
            self.__adjustTree(child, strategy ^ 1, depth + 1)
            
    def __printTree(self, root):
        print(root.__str__())
        for child in root.getChild():
            assert(child.getDepth() == root.getDepth() + 1)
            assert(child.getStrategy() ^ 1 == root.getStrategy())
            self.__printTree(child)
        
        
    def __init__(self, gameTree, rootStrategy=MIN_PLAYER):
        self.treeRoot_ = self.__constructTree(gameTree) # game tree
        self.node_n_ = 0
        self.depth_n_ = 0
        
        ## adjust tree
        self.__adjustTree(self.treeRoot_, rootStrategy, 0)
    
    def __abNegamax(self, node, alpha, beta):
        # set alpha beta
        node.setAlphaBeta((alpha, beta))
        # leaf node
        if len(node.getChild()) == 0:
            return node.getValue()
        # recurse
        bestScore = -INT_INF
        for child in node.getChild():
            newAlpha = -beta
            newBeta = -max(alpha, bestScore)
            recursedScore = self.__abNegamax(child, newAlpha, newBeta)
            currentScore = -recursedScore
            # update best score
            if currentScore > bestScore:
                bestScore = currentScore
            # check beta bound
            if bestScore >= beta:
                child.markPruned()
                node.setValue(bestScore)
                return bestScore 
            node.setValue(bestScore)
        return bestScore       
    
    # bot interface
    def getRoot(self):
        return self.treeRoot_
    
    def printTreeInterface(self):
        self.__printTree(self.treeRoot_)
    
    def abNegamaxInterface(self):
        self.__abNegamax(self.treeRoot_, -INT_INF, INT_INF)
```
```python
# test
test_bot = ABbot([[[[13, 78], [63, 69]], [[77, 82], [97, 75]]], [[[73, 96], [24, 50]], [[46, 15], [16, 89]]]], 
                 MAX_PLAYER)
test_bot.abNegamaxInterface()
test_bot.printTreeInterface()
```
