# ExpNo 4 : Implement A* search algorithm for a Graph
# Name: RITIKAA SV
# Register Number: 212224060217
# Aim:

To ImplementA * Search algorithm for a Graph using Python 3.

# Algorithm:
```
// A* Search Algorithm
1.  Initialize the open list
2.  Initialize the closed list
    put the starting node on the open 
    list (you can leave its f at zero)

3.  while the open list is not empty
    a) find the node with the least f on 
       the open list, call it "q"

    b) pop q off the open list
  
    c) generate q's 8 successors and set their 
       parents to q
   
    d) for each successor
        i) if successor is the goal, stop search
        
        ii) else, compute both g and h for successor
          successor.g = q.g + distance between 
                              successor and q
          successor.h = distance from goal to 
          successor (This can be done using many 
          ways, we will discuss three heuristics- 
          Manhattan, Diagonal and Euclidean 
          Heuristics)
          
          successor.f = successor.g + successor.h

        iii) if a node with the same position as 
            successor is in the OPEN list which has a 
           lower f than successor, skip this successor

        iV) if a node with the same position as 
            successor  is in the CLOSED list which has
            a lower f than successor, skip this successor
            otherwise, add  the node to the open list
     end (for loop)
  
    e) push q on the closed list
    end (while loop)
```

# Sample Graph I

<img width="1590" height="1079" alt="image" src="https://github.com/user-attachments/assets/00895031-8c9d-4f1b-9340-142ac6aa3777" />


# Sample Input
```
10 14
A B 6
A F 3
B D 2
B C 3
C D 1
C E 5
D E 8
E I 5
E J 5
F G 1
G I 3
I J 3
F H 7
I H 2
A 10
B 8
C 5
D 7
E 3
F 6
G 5
H 3
I 1
J 0
```
# Sample Output

Path found: ['A', 'F', 'G', 'I', 'J']

# PROGRAM
```
from collections import defaultdict
H_dist ={}
def aStarAlgo(start_node, stop_node):
    open_set = set(start_node)
    closed_set = set()
    g = {}  
    parents = {}   
    g[start_node] = 0
    parents[start_node] = start_node
    while len(open_set) > 0:
        n = None
        for v in open_set:
            if n == None or g[v] + heuristic(v) < g[n] + heuristic(n):
                n = v
        if n == stop_node or Graph_nodes[n] == None:
            pass
        else:
            for (m, weight) in get_neighbors(n):
                if m not in open_set and m not in closed_set:
                    open_set.add(m)
                    parents[m] = n
                    g[m] = g[n] + weight
                else:
                    if g[m] > g[n] + weight:
                        g[m] = g[n] + weight
                        parents[m] = n
                        if m in closed_set:
                            closed_set.remove(m)
                            open_set.add(m)
        if n == None:
            print("Path does not exist!")
            return None
        if n == stop_node:
            path = []
            while parents[n] != n:
                path.append(n)
                n = parents[n]
            path.append(start_node)
            path.reverse()
            print('Path found: {}'.format(path))
            return path
        open_set.remove(n)
        closed_set.add(n)
    print('Path does not exist!')
    return None
def get_neighbors(v):
    if v in Graph_nodes:
        return Graph_nodes[v]
    else:
        return None
def heuristic(n):
    return H_dist[n]
graph = defaultdict(list)
n,e = map(int,input().split())
for i in range(e):
    u,v,cost = map(str,input().split())
    t=(v,int(cost))
    graph[u].append(t)
    t1=(u,int(cost))
    graph[v].append(t1)
for i in range(n):
    node,h=map(str,input().split())
    H_dist[node]=int(h)
Graph_nodes=graph
start=input()
goal=input()
aStarAlgo(start, goal)

```

# OUTPUT

<img width="991" height="624" alt="image" src="https://github.com/user-attachments/assets/72122b65-7811-47a8-b15c-e0d119bf45ea" />

# Sample Graph II
<img width="1560" height="1027" alt="image" src="https://github.com/user-attachments/assets/e14d9532-9d6c-42a3-9576-38a44755ccf1" />

# Sample Input
```
6 6
A B 2
B C 1
A E 3
B G 9
E D 6
D G 1
A 11
B 6
C 99
E 7
D 1
G 0

```
# Sample Output

Path found: ['A', 'E', 'D', 'G']

# PROGRAM
```
from collections import defaultdict
H_dist ={}
def aStarAlgo(start_node, stop_node):
    open_set = set(start_node)
    closed_set = set()
    g = {}  
    parents = {}   
    g[start_node] = 0
    parents[start_node] = start_node
    while len(open_set) > 0:
        n = None
        for v in open_set:
            if n == None or g[v] + heuristic(v) < g[n] + heuristic(n):
                n = v
        if n == stop_node or Graph_nodes[n] == None:
            pass
        else:
            for (m, weight) in get_neighbors(n):
                if m not in open_set and m not in closed_set:
                    open_set.add(m)
                    parents[m] = n
                    g[m] = g[n] + weight
                else:
                    if g[m] > g[n] + weight:
                        g[m] = g[n] + weight
                        parents[m] = n
                        if m in closed_set:
                            closed_set.remove(m)
                            open_set.add(m)
        if n == None:
            print("Path does not exist!")
            return None
        if n == stop_node:
            path = []
            while parents[n] != n:
                path.append(n)
                n = parents[n]
            path.append(start_node)
            path.reverse()
            print('Path found: {}'.format(path))
            return path
        open_set.remove(n)
        closed_set.add(n)
    print('Path does not exist!')
    return None
def get_neighbors(v):
    if v in Graph_nodes:
        return Graph_nodes[v]
    else:
        return None
def heuristic(n):
    return H_dist[n]
graph = defaultdict(list)
n,e = map(int,input().split())
for i in range(e):
    u,v,cost = map(str,input().split())
    t=(v,int(cost))
    graph[u].append(t)
    t1=(u,int(cost))
    graph[v].append(t1)
for i in range(n):
    node,h=map(str,input().split())
    H_dist[node]=int(h)
Graph_nodes=graph
start=input()
goal=input()
aStarAlgo(start, goal)
```

# OUTPUT
<img width="463" height="385" alt="image" src="https://github.com/user-attachments/assets/0b734be9-c9d5-4739-ad31-3e73204b13e7" />

# RESULT :

Thus a graph was constructed and implemantation of A star Search for the same graph was done successfully.
