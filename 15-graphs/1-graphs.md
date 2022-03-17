# Graphs
A **graph data structure** consists of a finite (and possibly mutable) set of vertices or nodes or points. Basically a graph is a collection of nodes and connections between those nodes. Or a bunch of nodes with connections between them -- make up a graph structure.

Interconnected Nodes. Superset of trees.

![Trees](./graphs.png)

## Use
1. Social Network
2. Networks (Routing Algorithms)
3. Google Maps (Location / Mapping)
4. Recommendation Engines

## Graphs vs Trees:
In trees, to go from one node to another, there is only one path whereas for graphs, there may be multiple paths.

## Terminology

<img width="250" alt="Screen Shot 2022-03-15 at 8 32 10 PM" src="https://user-images.githubusercontent.com/25594064/158498994-d356c377-25f0-45bc-a464-5353b545b3ab.png">

1. **Vertice**: Nodes of the graph (Nodes and vertex might be used interchangeably but the correct technical term of a node in a graph is a vertex). 
2. **Edge**: Connections between nodes
3. **Directed Graph**: Graph in which we can traverse an edge in only one way. Eg: Instagram Followers Graph

<img width="250" alt="Screen Shot 2022-03-14 at 11 41 07 PM" src="https://user-images.githubusercontent.com/25594064/158307794-20c829f9-173e-4a53-9f44-67fba99419a4.png">

4. **Undirected Graph**: Graph in which nodes can be traversed in both directions. Eg: Facebook Friends Graph

<img width="250" alt="Screen Shot 2022-03-14 at 11 39 07 PM" src="https://user-images.githubusercontent.com/25594064/158307605-ed44aacc-032b-40f0-a148-f26fbb13b226.png">

5. **Unweighted Graph**: Edges have no value associated with them.

<img width="255" alt="Screen Shot 2022-03-14 at 11 45 37 PM" src="https://user-images.githubusercontent.com/25594064/158308418-9fd1ecd0-979f-4aa6-93db-3acdc3049a4b.png">

6. **Weighted Graph**: Edges have some value associated with them.

<img width="250" alt="Screen Shot 2022-03-14 at 11 45 45 PM" src="https://user-images.githubusercontent.com/25594064/158308320-b6914d85-e9f4-4069-9e33-e90589dd5a12.png">

## Representing Graphs
There are two ways of representing graphs:

1. Adjacency Matrix:

<img width="400" alt="Screen Shot 2022-03-15 at 8 42 58 PM" src="https://user-images.githubusercontent.com/25594064/158499921-3ef7b3f2-631c-4443-bd56-ab8c28b0a688.png">


Is a matrix of size VxV where V is the number of Vertices.

The 1s represent true, 0 represents false. Boolean values. True/false whether there is a connection between vertices. For example A and B have a connection, so does D and C.

The matrix for the above graph would be:
```
		A	B	C	D	E	F
	==================================================
	A	0	1	0	0	0	1
	
	B	1	0	1	0	0	0

	C	0	1	0	1	0	0

	D	0	0	1	0	1	0

	E	0	0	0	1	0	1

	F	1	0	0	0	1	0
```

2. Adjacency List:

<img width="350" alt="Screen Shot 2022-03-15 at 8 54 26 PM" src="https://user-images.githubusercontent.com/25594064/158501137-f10776f4-3d6d-48db-a0ed-d5ab2525ffc2.png">

Graph is stored in a list or hashmap:
```javascript
[
  [1, 5],
  [0, 2],
  [1, 3],
  [2, 4],
  [3, 5],
  [4, 0]
]

{
  0 : [1, 5], 
  1 : [0, 2], 
  2 : [1, 3],
  3 : [2, 4], 
  4 : [3, 5],
  5 : [4, 5]
}
```

For one with letters it would look something like this below: 

<img width="385" alt="Screen Shot 2022-03-15 at 8 55 58 PM" src="https://user-images.githubusercontent.com/25594064/158501314-9aa54c0e-5852-4d86-8e9e-21b3ae090c9e.png">

## Complexity Comparision

<img width="500" height="300" alt="Screen Shot 2022-03-15 at 8 57 59 PM" src="https://user-images.githubusercontent.com/25594064/158501502-7cf8696e-210e-4b0f-a38c-ac14eaf7851d.png">

1. Add Vertex:
* Matrix: O(v<sup>2</sup>)
* List: O(1)

2. Add Edge:
* Matrix: O(1)
* List: O(1)

3. Remove Vertex:
* Matrix: O(v<sup>2</sup>)
* List: O(v + e)

4. Remove Edge:
* Matrix: O(1)
* List: O(e)

5. Query:
* Matrix: O(1)
* List: O(v + e)

6. Storage:
* Matrix: O(v<sup>2</sup>)
* List: O(v)
