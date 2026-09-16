
# EX 5E Minimum Spanning Tree -Boruvka's Algorithm

## AIM:
To write a Java program to for given constraints.
Boruvka's Algorithm - Minimum Spanning Tree

## Algorithm
1. Input the Graph
Read the number of vertices V and edges E.
Store all edges with their source (src), destination (dest), and weight (weight) in a list.
2. Initialize Components
Create a parent[] array where each vertex is its own parent (disjoint set initialization).
Set the number of connected components to V (each vertex starts as a separate component).
3. Repeat Until Only One Component Remains
Create an array cheapest[] to store the cheapest edge for each component.
4. Find the Cheapest Edge for Each Component
For every edge (u, v):
Find the component (set) of u and v using the find() operation.
If they belong to different components:
Update the cheapest edge for both components if this edge has a smaller weight.
5.  Add the Cheapest Edges to the MST
For each vertex i, if cheapest[i] is not null:
Find the components of its source and destination.
6. Once all vertices are connected (components = 1), print all selected edges and the total MST weight.  

## Program:
```
Program to implement Reverse a String
Developed by: KISHAN SHREE B
Register Number:212223100022
import java.util.*;

public class BoruvkaMST {
    static int[] parent;

  
    static int find(int i) {
        if (parent[i] != i)
            parent[i] = find(parent[i]);
        return parent[i];
    }

   
    static void union(int x, int y) {
        int xset = find(x);
        int yset = find(y);
        parent[xset] = yset;
    }

    static int boruvkaMST(int V, List<Edge> edges) {
        parent = new int[V];
        for (int i = 0; i < V; i++) parent[i] = i;

        int components = V;
        int mstWeight = 0;

        
        while (components > 1) {
            Edge[] cheapest = new Edge[V];

            
            for (Edge e : edges) {
                int set1 = find(e.src);
                int set2 = find(e.dest);

                if (set1 == set2) continue; 

                if (cheapest[set1] == null || cheapest[set1].weight > e.weight)
                    cheapest[set1] = e;

                if (cheapest[set2] == null || cheapest[set2].weight > e.weight)
                    cheapest[set2] = e;
            }

      
            for (int i = 0; i < V; i++) {
                Edge e = cheapest[i];
                if (e != null) {
                    int set1 = find(e.src);
                    int set2 = find(e.dest);

                    if (set1 == set2) continue;

                
                    System.out.println("Edge: " + e.src + "-" + e.dest + " Weight: " + e.weight);
                    mstWeight += e.weight;
                    union(set1, set2);
                    components--;
                }
            }
        }

        return mstWeight;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int V = sc.nextInt();
        int E = sc.nextInt(); 

        List<Edge> edges = new ArrayList<>();
        for (int i = 0; i < E; i++) {
            edges.add(new Edge(sc.nextInt(), sc.nextInt(), sc.nextInt()));
        }

        int totalWeight = boruvkaMST(V, edges);
        System.out.println("Total Weight of MST: " + totalWeight);

        sc.close();
    }
}

class Edge {
    int src, dest, weight;
    Edge(int s, int d, int w) {
        src = s;
        dest = d;
        weight = w;
    }
}
  

```

## Output:
<img width="663" height="497" alt="image" src="https://github.com/user-attachments/assets/3ef60c93-c172-4f4c-b4a0-42a4b4791c3f" />



## Result:
The program successfully implemented and the expected output is verified.
