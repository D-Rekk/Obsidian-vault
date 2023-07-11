# JavaScript 05. Datastructures

Created: July 19, 2022 1:48 PM
Status: Open
URL: https://adrianmejia.com/data-structures-for-beginners-graphs-time-complexity-tutorial/
Updated: November 23, 2022 2:45 PM

# DataStructures

A **data structure** is a particular way of organizing data in a computer so that it can be used effectively.

# Linked List

A linked list is an ordered collection of data elements.A data element can be represented as a **node** in a linked list.
Each node consists of two parts: *data & pointer to the next*.

Unlike arrays, data elements are not stored at contiguous locations. The data elements or nodes are linked using pointers, hence called a linked list.

- A linked list has the following properties:
    - Successive nodes are connected by pointers.
    - The last node points to `null`.
    - A `head` pointer is maintained which points to the first node of the list.
    - A linked list can grow and shrink in size during execution of the program.
    - It allocates memory as the list grows, unlike arrays, which have fixed size. Therefore, the upper limit on the number of elements must be known in advance. Generally, the allocated memory is equal to the upper limit irrespective of the usage. This is one of the key advantages of using a linked list over an array
- Drawbacks
    - In contrast, Random access of data elements is not allowed. Nodes must be accessed sequentially starting from the first one. Therefore, the search operation is slow on a linked list.
    - It uses more memory than arrays because of the storage used by their pointers.

**Types of Linked List**

The most popular Linked List are: singly, doubly and circular.

---

# Graph

A **Graph** is a non-linear data structure. Represents *pair-wise* relationship or connection between a set of objects.

Abstractly, a **graph** $G$ is simply a set $V$ of **vertices**, also called *nodes*, and a *set* $E$ of pairs vertices, called **edges**.

*Edges* can be defined as:
**Directed**: edge $(u,v)$ is not the same as $(v,u)$.

**Un-Directed**: pair of unordered vertices. $(u,v) = (v,u) ⇒ \{u,v\}$

A graph whose edges are all undirected is called **undirected graph**. Likewise, if all the edges are directed, the graph is called **digraph**. If it containst both, it’ll be called **mixed graph**.

---

### Graph Applications

1. **Networks topology** - We can use the graph *DS* when modeling network topology, such as the internet or friends on Faceobok
2. **Optimization**: We can use the graph in conjuction with an optimization algorithm for determining an optimal path, such as GPS.
3. **Precedence Constraints** - Situations where there are certain pre-requisites that need to be fullfilled in order to continue. Ex. In order to have Y course, you need to pass course X.

### Graph Representation

There are generally **two ways** to represent a graph data-structure: **Adjacency Matrix** and **Adjacency List**.

### **************Adjacency Matrix**************

Represents graph with **V** nodes into *VxV 0-1* **matrix**.

In the $A$ matrix representation, we think of vertices as being the integers in the *set* $\{0,1,…, n-1 \}$ and the edges as being pairs of two integers. Cell $A_{ij}$ = 1 means that verteces $*i_{row}-j_{col}$* are  a reference to **edge** $e$ and its endpoints are connected.
$A[i][j] = A[j][i]$ in undirected graph.

[https://www.figma.com/file/cQcQBMHE3wd56cl7VZGxpw/Adjacency-Matrix?node-id=0%3A1&t=3VRLz8j2Pkkgvusu-1](https://www.figma.com/file/cQcQBMHE3wd56cl7VZGxpw/Adjacency-Matrix?node-id=0%3A1&t=3VRLz8j2Pkkgvusu-1)

This *undirected graph* has 5 vertexes, 

Each vertex is both column and row. All diagonal elements are 0, meaning that it doesn’t contain any **self-loop**.

$\begin{matrix}
  & 0 & 1 & 2 & 3 & 4 \\
0 & . & e & . & . & f\\
1 & e & . & g & h & i\\
2 & . & g & . & l & .\\
3 & . & h & l & . & i\\
4 & f & i & . & i & .
\end{matrix}$

Advantages of matrix:

- Easy to implement.
- `getEdge($u,v$)` and `removeEdge($e$)` takes $O(1)$ time.
- Queries like whether there is an edge from vertex $u$ to vertex $v$ are efficient and can be done in constant time $O(1)$ (Just need to check if value $[u][v]$ is 0 or 1).
- If edges don’t have auxiliary data, a **boolean** can use one bit per edge slot.

Disadvantages of matrix:

- Consumes more space:  $O(V^2)$
- Adding a vertex is $O(V^2)$ time
- If the graph is **dense**( non-null entries ), number of edges will be proportional to $n^2$. Yet most graph are **sparse**, making the use of adjacency matrix **inefficient**

### **************Adjacency List/Map**************

Represents graph with **array of lists** of length **V**.  For each vertex $v$, we mantain a collection of entries, called **incidence collection** $l(v)$, whose entries are edges *incident* to its $v$. 

Array (for elements from 0 to n-1) or Positional List/Hashmap(for non repeating keys)  are used to represent the  primary structure. The secondary structure is a linked list, with a reference to its vertex if it’s ordered hash-based map (edges as key, vertex as value)

[https://www.figma.com/file/lfClKi2WIH2WWqEW3bg0WN/Untitled?node-id=0%3A1&t=lbzMm0WB8k5wSxxG-1](https://www.figma.com/file/lfClKi2WIH2WWqEW3bg0WN/Untitled?node-id=0%3A1&t=lbzMm0WB8k5wSxxG-1)

$[arr]$ is the primary structure. It consists of $V$ number of vertices. Each $v$ vertix  has a secondary $l(v)$ list containing all the edges$deg(v)$ ( in this case, since it’s been used a hash-map, each node $e$ has a reference to its other end-point ). 

Advantages of adjacency list:

- An adjacency list is **storage efficient**. Space usage is $O(n + m)$
- `insertVertex($x$)`, `insertEdge($u,v,x$)` and `removeEdge($e$)` are $O(1)$ operation
- Adjacency map `getEdge($v$)` is *expected* $O(1)$

Disadvantages of adjacency list

- `removeVerted($v$)` and all its incident edges is $O(deg(v))$ ( incident edges of $v$ vertex ).

---
##### Code
```jsx
class Node {
  constructor(value) { // vertex value
    this.value = value;
    this.adjacents = []; // adjacency list
  }

  addAdjacent(node) {
    this.adjacents.push(node);
  }

  removeAdjacent(node) {
    const index = this.adjacents.indexOf(node);
    if(index > -1) {
      this.adjacents.splice(index, 1);
      return node;
    }
  }

  getAdjacents() {
    return this.adjacents;
  }

  isAdjacent(node) {
    return this.adjacents.indexOf(node) > -1;
  }
}

/*
		let’s build the Graph class to perform operations such as 
		adding/removing vertices and edges.
*/

class Graph {
  constructor(edgeDirection = Graph.DIRECTED) { // default parameter
    this.nodes = new Map();
    this.edgeDirection = edgeDirection;
  }
  // ...
}

Graph.UNDIRECTED = Symbol('undirected graph'); // two-ways edges
Graph.DIRECTED = Symbol('directed graph'); // one-way edges
```


#
---

<aside>
💡

</aside>

 Something

---