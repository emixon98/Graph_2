# Graph_2
Second graph search algorithm lab concerning Dijkstra's and an example of failing negative weights.
### Graph Example


### Reasoning for Dijkstra's Algorithm failing on the example that includes negative weights.
Dijkstra's assumes that if it reaches its destination with a specified weight that any option must be >= to that weight. For example, in my diagram we start at A, our destination is B, the path directly from A to B is 2, but the path from A to C is 5, our algorithm is going to assume that any path following along C is going to be >= 5. Negative weight interupt this logic and cause a finalized path to not be able to be updated when a negative value is introduced. Expand on this
