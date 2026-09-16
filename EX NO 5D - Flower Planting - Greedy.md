
# EX 5D Flower Planting.

## AIM:
To write a Java program to for given constraints.
You are given n gardens, labelled from 1 to n.

You also have a list called paths, where each element paths[i] = [xi, yi] represents a bidirectional road connectingthe  garden xi and garden yi.


## Algorithm
1. Input the Data
Read the number of gardens n and the number of paths m.
Read each of the m paths that connect two gardens and store them in an adjacency list (undirected graph). 
2. Build the Adjacency List
For each path (x, y), add y to the adjacency list of x and vice versa (convert to 0-based indexing).
3. Initialize Flower Assignment
Create an array ans[] of size n to store the flower type (1–4) for each garden.
Each garden will eventually have one flower type assigned.
4.  Assign Flowers Greedily
For each garden:
Create a boolean array used[5] to track which flower types are already used by its adjacent gardens.
For every neighbor, mark its flower type as used.
5. Output the Result
Print the flower type assigned to each garden in order.  

## Program:
```

Program to implement Reverse a String
Developed by: KISHAN SHREE B
Register Number:212223100022
import java.util.*;

public class GardenFlowerPlanner {

    public static int[] assignFlowers(int n, int[][] paths) {
        @SuppressWarnings("unchecked")
        List<Integer>[] adj = new ArrayList[n];
        for (int i = 0; i < n; i++) {
            adj[i] = new ArrayList<>();
        }

       
        for (int[] path : paths) {
            int x = path[0] - 1;
            int y = path[1] - 1;
            adj[x].add(y);
            adj[y].add(x);
        }

        int[] ans = new int[n]; 

        for (int i = 0; i < n; i++) {
            boolean[] used = new boolean[5];

            
            for (int neighbor : adj[i]) {
                if (ans[neighbor] != 0) {
                    used[ans[neighbor]] = true;
                }
            }

            
            for (int color = 1; color <= 4; color++) {
                if (!used[color]) {
                    ans[i] = color;
                    break;
                }
            }
        }

        return ans;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt(); 
        int m = sc.nextInt(); 

        int[][] paths = new int[m][2];
        for (int i = 0; i < m; i++) {
            paths[i][0] = sc.nextInt();
            paths[i][1] = sc.nextInt();
        }

        int[] result = assignFlowers(n, paths);

        for (int flower : result) {
            System.out.print(flower + " ");
        }
        System.out.println();
        
        sc.close();
    }
}
  
```

## Output:

<img width="514" height="468" alt="image" src="https://github.com/user-attachments/assets/6405940e-8a92-43bd-9956-5d3527a15d63" />


## Result:
The program successfully implemented and the expected output is verified.
