---
id: 5f3de2c5708b68b90625b1b8
title: Implement Prim's Algorithm
challengeType: 1
isHidden: false
forumTopicId: 84983
---

## Description

<section id='description'>

We have seen Dijkstra’s algorithm finding the shortest path from a given starting vertex to the rest of the vertices in a given graph. Prim’s Algorithm is quite similar.

Prim’s Algorithm is a type of greedy algorithm that finds a minimum spanning tree for a weighted undirected graph.

<strong>Definition of a spanning tree</strong> </br>
A spanning tree of a graph is a subgraph, which is a collection of edges including all vertices of the original graph. A minimum spanning tree (MST) is a spanning tree of a graph whose total edge weight is minimal among all the possible spanning trees. We use Prim’s Algorithm to find such.

<em>Note that there may be more than one valid minimum spanning tree for some graphs.</em>

<strong>Prim’s Algorithm walk-through</strong> </br>
Start with an arbitrary vertex in the graph <em>(Let’s call it Vertex 1).</em>
Add to the minimum spanning tree the least weighted edge of all the edges that connect Vertex 1 to another vertex.
Continue to add the least weighted edge that adds an unvisited vertex to the tree until all vertices have been visited.

<strong>Visualizing Prim’s algorithm</strong> </br>

<div style="display:flex;flex-direction:column;">
    <div style="display:flex;flex-direction:row;margin-bottom: 10px">
        <p>1.</p>
        <!-- Img 1 -->
        <img class='img-responsive' style="margin-left:10px;padding-right: 20px;" src='https://user-images.githubusercontent.com/54512885/90711423-ae7e1580-e26e-11ea-8988-952accf84a26.jpg'>
        <p>2.</p>
        <!-- Img 2 -->
        <img class='img-responsive' style="margin-left:10px;" src='https://user-images.githubusercontent.com/54512885/90711467-cc4b7a80-e26e-11ea-95dc-f1dca8fa57f5.jpg'>
    </div>
    <div style="display:flex;flex-direction:row;margin-bottom: 10px">
        <p>3.</p>
        <!-- Img 3 -->
        <img class='img-responsive' style="margin-left:10px;padding-right: 20px;" src='https://user-images.githubusercontent.com/54512885/90711486-de2d1d80-e26e-11ea-982c-d60b0068f82b.jpg'>
        <p>4.</p>
        <!-- Img 4 -->
        <img class='img-responsive' style="margin-left:10px;" src='https://user-images.githubusercontent.com/36285777/90711412-43c8dc00-e266-11ea-8098-e024a859c025.jpg'>
    </div>
    <div style="display:flex;flex-direction:row;margin-bottom: 10px">
        <p>5.</p>
        <!-- Img 5 -->
        <img class='img-responsive' style="margin-left:10px;padding-right: 20px;" src='https://user-images.githubusercontent.com/36285777/90711414-45929f80-e266-11ea-8c23-491441f38629.jpg'>
        <p>6.</p>
        <!-- Img 6 -->
        <img class='img-responsive' style="margin-left:10px;" src='https://user-images.githubusercontent.com/36285777/90711415-475c6300-e266-11ea-98c4-6cb4a6d7212e.jpg'>
    </div>
</div>

</section>

## Instructions

<section id='instructions'>

In this exercise, you are asked to implement Prim’s Algorithm by writing a function prim, which takes a graph and returns a minimum spanning tree for that graph. For the sake of simplicity, we ask that you start from the first vertex. <em>(i.e. visited[0] is marked true)</em>

</section>

## Tests

<section id='tests'>

```yml
tests:
  - text: <code>output</code> should contain a 5x5 two-dimensional array.
    testString: assert((output.length === 5) && (output[0].length === 5));
  - text: The minimum spanning tree returned should contain an edge of weight 3 between the first and second nodes.
    testString: assert((output[0][1] === 3) && (output[1][0] === 3));
  - text: The minimum spanning tree returned should contain an edge of weight 1 between the second and third nodes.
    testString: assert((output[1][2] === 1) && (output[2][1] === 1));
  - text: The minimum spanning tree returned should contain an edge of weight 2 between the third and fifth nodes.
    testString: assert((output[2][4] === 2) && (output[4][2] === 2));
  - text: The minimum spanning tree returned should contain an edge of weight 3 between the fourth and fifth nodes.
    testString: assert((output[3][4] === 3) && (output[4][3] === 3));
  - text: The minimum spanning tree should not contain extraneous edges.
    testString: assert((output[0][0] === 0) && (output[0][2] === 0) &&(output[0][3] === 0) &&(output[0][4] === 0) &&(output[1][1] === 0) &&(output[1][3] === 0) &&(output[1][4] === 0) &&(output[2][0] === 0) &&(output[2][2] === 0) &&(output[2][3] === 0) &&(output[3][0] === 0) &&(output[3][1] === 0) &&(output[3][2] === 0) &&(output[3][3] === 0) &&(output[4][0] === 0) &&(output[4][1] === 0) &&(output[4][4] === 0))
```

</section>

## Challenge Seed

<section id='challengeSeed'>

<div id='js-seed'>

```js
function prim(graph) {
  let visited = [true, false, false, false, false];
  let mst = [
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0]
  ];
  let smallestEdge1;
  let smallestEdge2;
  let smallestWeight = Infinity;
}

const exampleGraph = [
  [0, 3, 0, 8, 7],
  [3, 0, 1, 0, 4],
  [0, 1, 0, 0, 2],
  [8, 0, 0, 0, 3],
  [7, 4, 2, 3, 0]
];
const output = prim(exampleGraph);
```

</div>
</section>

## Solution

<section id='solution'>

```js
function prim(graph) {
  let visited = [true, false, false, false, false];
  let mst = [
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0],
  ];
  let smallestEdge1;
  let smallestEdge2;
  let smallestWeight = Infinity;
  while(!visited[1] || !visited[2] || !visited[3] || !visited[4] ){
    for(var i = 0; i < mst.length; i++){
        for(var j = 0; j < mst[i].length; j++){
          if(visited[i] && !visited[j]){
            if(graph[i][j] != 0 && graph[i][j] < smallestWeight){
             smallestEdge1 = i;
             smallestEdge2 = j;
             smallestWeight = graph[i][j];
          }
        }
      }
    }
    mst[smallestEdge1][smallestEdge2] = smallestWeight;
    mst[smallestEdge2][smallestEdge1] = smallestWeight;
    visited[smallestEdge2] = true;
    smallestWeight = Infinity;
  }
  return mst;
}
const exampleGraph = [
    [0, 3, 0, 8, 7],
    [3, 0, 1, 0, 4],
    [0, 1, 0, 0, 2],
    [8, 0, 0, 0, 3],
    [7, 4, 2, 3, 0]
  ];
var output = prim(exampleGraph);

Answer for the exampleGraph
[0, 3, 0, 0, 0],
[3, 0, 1, 0, 0],
[0, 1, 0, 0, 2],
[0, 0, 0, 0, 3],
[0, 0, 2, 3, 0]
```

</section>
