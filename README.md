# The implementation of Dijkstra algorithm with python 

## Dijkstra Algorithm

The algorithm is one of the most popular search algorithm used to determine the shortest path between two nodes in the graph. It was designed by computer scientist Edsger W. Dijkstra in 1956 and published three years later. The algorithm can be applied to any problem that can be represented as graph. 

## How it works

* There will be a weigthed graph and initial node.
* Start with the initial node. Check the adjecent nodes.
* Find the node with minimum edge value. 
* Repeat the process until the target node is visited.



Dijkstra's algorithm is applicable for:
* All edges should have nonnegative weights 
* The graph should be connected 

## The steps of the algorithm implementation in python:

```python
def dijkstra(current, nodes, distances):
```
This line defines a function called `dijkstra` that takes three parameters: `current`, which represents the starting node for the shortest path search, `nodes`, which is a tuple containing all the nodes in the graph, and `distances`, which is a dictionary representing the graph structure where keys are nodes and values are dictionaries containing neighboring nodes and their respective distances.

```python
    unvisited = {node: None for node in nodes}
```
Here, a dictionary called `unvisited` is created, where each node from the `nodes` tuple is a key, and the corresponding value is set to `None`. This dictionary will keep track of the shortest distances to each node that have not yet been visited.

```python
    visited = {}
```
This line initializes an empty dictionary called `visited` which will store the shortest distances from the starting node to each visited node.

```python
    currentDistance = 0
    unvisited[current] = currentDistance
```
The distance from the starting node to itself (`current`) is set to `0`, and this value is assigned to the `current` key in the `unvisited` dictionary to signify that the shortest known distance to `current` is `0`.

```python
    while True:
```
This starts an infinite loop. The loop will terminate later when all nodes have been visited.

```python
        for neighbour, distance in distances[current].items():
```
This line iterates through each neighbor of the current node (`current`) and the corresponding distance to that neighbor. It accesses this information from the `distances` dictionary using the current node as the key.

```python
            if neighbour not in unvisited: continue
```
This line checks if the neighbor node has already been visited. If it has been visited, it skips further processing for this neighbor.

```python
            newDistance = currentDistance + distance
```
This calculates the new distance from the starting node to the neighbor node through the current node.

```python
            if unvisited[neighbour] is None or unvisited[neighbour] > newDistance:
                unvisited[neighbour] = newDistance
```
This updates the shortest known distance to the neighbor node (`neighbour`) if the new calculated distance is shorter than the previously known distance or if the neighbor node hasn't been visited yet.

```python
        visited[current] = currentDistance
```
This updates the `visited` dictionary with the shortest known distance from the starting node to the current node (`current`).

```python
        del unvisited[current]
```
This removes the current node from the `unvisited` dictionary since it has been visited now.

```python
        if not unvisited: break
```
This checks if all nodes have been visited. If so, the loop breaks, and the shortest distances have been found.

```python
        candidates = [node for node in unvisited.items() if node[1]]
```
This creates a list of nodes that are still unvisited (i.e., having a distance value) from the `unvisited` dictionary.

```python
        print(sorted(candidates, key = lambda x: x[1]))
```
This line prints the candidates for the next node to visit, sorted by their distance values.

```python
        current, currentDistance = sorted(candidates, key = lambda x: x[1])[0]
```
This line updates the `current` node and `currentDistance` to the node with the shortest distance among the candidates.

```python
    return visited
```
Finally, this line returns the `visited` dictionary containing the shortest distances from the starting node to all other nodes in the graph.

The remaining code after the function definition (`nodes`, `distances`, `current`, and the function call `print(dijkstra(current, nodes, distances))`) sets up the graph and initiates the Dijkstra's algorithm with the given inputs.

## Example Code 
````py
nodes = ('A', 'B', 'C', 'D', 'E')
distances = {
    'A': {'B': 5, 'C': 2},
    'B': {'C': 2, 'D': 3},
    'C': {'B': 3, 'D': 7},
    'D': {'E': 7},
    'E': {'D': 9}}
current = 'A'
  
print(dijkstra(current, nodes, distances))
````

Output:

````

[('C', 2), ('B', 5)]
[('B', 5), ('D', 9)]
[('D', 8)]
[('E', 15)]
{'A': 0, 'C': 2, 'B': 5, 'D': 8, 'E': 15}

````
## Time complexity

The program searchs through all nodes to find the closest within the graph. This means that the initial time complexity will be O(n) for this search. This will bring the total time complexity to O(V^2) where V is the number of nodes in the graph. 

* For each node (V), the connected edges need to be relaxed in order to find the minimum cost edge that connects a node to V. V number of calculations need to be done and each operation takes O(V) times, therefore the time complexity will be  O(V^2).
     * V calculation 
     * Q(V) time
     * Total: Q(V^2)

