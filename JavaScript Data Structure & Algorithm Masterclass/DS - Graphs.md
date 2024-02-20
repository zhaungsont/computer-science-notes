## Terminology
- Vertex: a node
- Edge: connection between nodes
- Weighted/Unweighted: values assigned to distances between vertices

**Weighted Graph**
![[weighted graph.png]]

**Directed Graph**
![[directed graph.png]]
**Weighted Directed Graph**
![[weighted directed graph.svg]]

### Adjacency Matrix
Illustrated as a two-dimensional array.

![[adjacencymatrix.webp]]


Below is another one, courtesy of ChatGPT:
![[unweighted undirected graph.png]]
```
[ 
	[0, 1, 0, 0, 1], 
	[1, 0, 1, 1, 0], 
	[0, 1, 0, 1, 0], 
	[0, 1, 1, 0, 1], 
	[1, 0, 0, 1, 0] 
]
```

### Adjacency List

![[adjacencymatrix.webp]]
The code above can be represented in code as below:
```
const adjacenyMatrix = 
[
	[1, 2, 4],
	[0, 2],
	[0, 1, 3, 4],
	[2],
	[0, 2],
]
```

In the case where we cannot use the node's index, we can use something like this to represent the adjacency list:
![[Adjacency List w A to F.png]]
```
{
	'A': {'B', 'C', 'E', 'F'},
	'B': {'A', 'C', 'D', 'E'},
	'C': {'A', 'B'},
	'D': {'B', 'E'},
	'E': {'A', 'B', 'D'},
	'F': {'A'}
}
```

## Difference in Time Complexity Between Adjacency List & Adjacency Matrix

| Operation       | Adjacency List       | Adjacency Matrix     |
|-----------------|----------------------|----------------------|
| Add Vertex      | $$ O(1) $$           | $$ O(V^2) $$         |
| Add Edge        | $$ O(1) $$           | $$ O(1) $$           |
| Remove Vertex   | $$ O(V + E) $$       | $$ O(V^2) $$         |
| Remove Edge     | $$ O(E) $$           | $$ O(1) $$           |
| Query           | $$ O(V + E) $$           | $$ O(1) $$           |
| Storage         | $$ O(V + E) $$       | $$ O(V^2) $$         |

- **V** represents the number of vertices.
- **E** represents the number of edges.

1. **Add Vertex**
   - **Adjacency List:** Adding a vertex is $O(1)$ because it typically involves just adding an entry to the list.
   - **Adjacency Matrix:** Adding a vertex is $O(V^2)$ because you need to create a new matrix with one additional row and column, which involves copying the entire matrix.

2. **Add Edge**
   - **Adjacency List:** Adding an edge is $O(1)$ assuming we have direct access to the connections of the involved vertices, as it's a matter of appending to a list.
   - **Adjacency Matrix:** Adding an edge is $O(1)$ because you only need to update the value at the specific row and column corresponding to the two vertices.

3. **Remove Vertex**
   - **Adjacency List:** Removing a vertex is $O(V + E)$ because you need to find and remove the vertex and also remove all edges associated with it, affecting other vertices' lists.
   - **Adjacency Matrix:** Removing a vertex is $O(V^2)$ since it involves creating a new matrix without the row and column of the removed vertex, which requires shifting parts of the matrix.

4. **Remove Edge**
   - **Adjacency List:** Removing an edge is $O(E)$ because, in the worst case, you might have to search through all edges to find the one to remove.
   - **Adjacency Matrix:** Removing an edge is $O(1)$ as it only requires setting the value at the specified row and column to zero.

5. **Query (Check if an edge exists)**
   - **Adjacency List:** Querying is $O(V)$ because, in the worst case, you may need to search through all vertices' edges.
   - **Adjacency Matrix:** Querying is $O(1)$ as it involves accessing the value at the row and column corresponding to the two vertices.

6. **Storage**
   - **Adjacency List:** The storage complexity is $O(V + E)$ as each vertex and edge is stored once.
   - **Adjacency Matrix:** The storage complexity is $O(V^2)$ because it maintains a value for every possible edge, even if the edge doesn't exist.

## Pros & Cons of Adjacency List VS. Adjacency Matrix
- **Adjacency List**: 
	- **Pro**: Can take up less space (in sparse graphs)
	- Pro: Faster to iterate over all edges
	- **Con**: Can be slower to lookup specific edge
- **Adjacency Matrix:**
	- **Con**: Takes up more space (in sparse graphs)
	- **Con**: Slower to iterate over all edges
	- **Pro:** Faster to lookup specific edge

```js
class Graph {
    constructor() {
        this.adjacencyList = {};
    }

    addVertex(vertex) {
        if (!this.adjacencyList[vertex]) {
            this.adjacencyList[vertex] = [];
        }
        return this.adjacencyList;
    }

    addEdge(v1, v2) {
        if (this.adjacencyList[v1] && this.adjacencyList[v2]) {
            this.adjacencyList[v1].push(v2);
            this.adjacencyList[v2].push(v1);
        }
        return this.adjacencyList;
    }

    removeEdge(v1, v2) {
        if (this.adjacencyList[v1] && this.adjacencyList[v2]) {
            this.adjacencyList[v1] = this.adjacencyList[v1].filter(v => v !== v2);
            this.adjacencyList[v2] = this.adjacencyList[v2].filter(v => v !== v1);
        }
        return this.adjacencyList;
    }

    removeVertex(vertex) {
        if (this.adjacencyList[vertex]) {
            this.adjacencyList[vertex].forEach(v => this.removeEdge(v, vertex));
            delete this.adjacencyList[vertex];
        }

        return this.adjacencyList;
    }
}

const graph = new Graph();
graph.addVertex('Tokyo');
graph.addVertex('San Fransisco');
graph.addVertex('Taipei');
graph.addEdge('Taipei', 'Tokyo');
graph.addEdge('Taipei', 'San Fransisco');
graph.addEdge('San Fransisco', 'Tokyo');
graph.removeEdge('San Fransisco', 'Taipei');
graph.removeVertex('Tokyo')



```