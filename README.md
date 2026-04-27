# Graph_2
Second graph search algorithm lab concerning Dijkstra's and an example of failing negative weights.
### Graph Example
<img width="706" height="417" alt="DijkstraEx" src="https://github.com/user-attachments/assets/e280737c-a9a6-46e0-b51f-a7d4125ea171" />

### Reasoning for Dijkstra's Algorithm failing on the example that includes negative weights.
#### All reasoning was derived from the pseudocode given in the text, it will be pasted below. 
In the graph example I created the goal is to find the shortest path to B starting at node A, visually we can see that if we go directly to B from A the distance is 2, however if we go A -> C -> D -> B the distance is 0. Dijkstra's algorithm begins its process by setting every vertex's distance to infinity and predecessor to 0, enqueuing all of them into an unvisited queue that we will continue to utilize until we have visited all nodes. We start at node A, set its distance to 0, and dequeue it as the current minimum distance after attaching it to a tracked variable, we then compare its distance to its adjactent neighbors, in this case B and C. We check the weight, one at a time of B and C and add A's distance to an alternative path var, which is A's distance of 0 plus the edge weight to B (2), this distance is 0+2 which is less than B's current distance that was set to infinity when enqueued, and its predecessor is A, C's alternative distance is 0 + 6 which is < infinity, and its predecessor is A. Here is where the problem lies. We need a new current vertex to compare and traverse down, B is the smaller of the two, and while B is the destination, unvisited queue is not empty so we must continue our algorithm. So we use B as our next current vertex and dequeue it from our unvisited queue, this means that we cannot alter B moving forward, its predecessor will always be A and its distance 2. Dijkstra's continues and will update D through C -> D, and even find that D -> B is a shorter path, but B has already been dequeued and thus no longer allows us to alter it, the pseudocode offers no path to handle a negative weight leading to a cheaper path deeper in the graph. As a result Dijkstra's behaves very much of first impressions, using the first two comparisons as an example, that any path that follows A -> B must be >= 2 and that any path that follows A -> C must be  >= 6. Dijkstra in turn assumes that once a node is dequeued that no future path can improve it, and a negative edge invalidates this idea.

### Pseudocode Dijkstra's Algorithm
```
DijkstraShortestPath(startV) {
   for each vertex currentV in graph {
      currentV⇢distance = Infinity
      currentV⇢predV = 0
      Enqueue currentV in unvisitedQueue
   }

   // startV has a distance of 0 from itself
   startV⇢distance = 0

   while (unvisitedQueue is not empty) {
      // Visit vertex with minimum distance from startV
      currentV = DequeueMin unvisitedQueue

      for each vertex adjV adjacent to currentV {
         edgeWeight = weight of edge from currentV to adjV
         alternativePathDistance = currentV⇢distance + edgeWeight
            
         // If shorter path from startV to adjV is found,
         // update adjV's distance and predecessor
         if (alternativePathDistance < adjV⇢distance) {
            adjV⇢distance = alternativePathDistance
            adjV⇢predV = currentV
         }
      }
   }
}
```
