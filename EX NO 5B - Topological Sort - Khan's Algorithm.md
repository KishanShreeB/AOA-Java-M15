
# EX 5B Topological Sort - Khan's Algorithm

## AIM:
To write a Java program to for given constraints.

A software development team is preparing for a product release. The release consists of multiple tasks, each dependent on other tasks being completed first. You are to determine a valid order in which all tasks can be completed. If it's not possible due to cyclic dependencies, output that the release cannot be scheduled.




## Algorithm
1. Input & Graph Construction:
Read number of tasks n and dependencies m.
Build an adjacency list where b → a means task a depends on b.
Maintain an indegree array to count how many prerequisites each task has
2. Initialize the Queue:
Add all tasks with indegree = 0 (no dependencies) to a queue — these can be executed first.
3. Process Tasks (Topological Sort):
While the queue is not empty:
Remove a task from the queue and add it to the final order list.
For each dependent task, decrease its indegree by 1.
If any dependent task’s indegree becomes 0, add it to the queue.
4.  Cycle Detection:
After processing, if the total tasks in the order list ≠ n,
→ a cycle exists (some tasks depend on each other),
→ output: “Release cannot be scheduled.”
5. Output:
If no cycle is detected, print the tasks in the valid topological order,
representing a feasible schedule of task execution.  

## Program:
```
Program to implement Reverse a String
Developed by: KISHAN SHREE B
Register Number:212223100022
import java.util.*;

public class prog {

    public static List<Integer> findTaskOrder(int n, int[][] dependencies) {
       
        List<List<Integer>> adj = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            adj.add(new ArrayList<>());
        }

        int[] indegree = new int[n];

       
        for (int[] dep : dependencies) {
            int a = dep[0];
            int b = dep[1];
            adj.get(b).add(a); 
            indegree[a]++;
        }

        
        Queue<Integer> queue = new LinkedList<>();
        for (int i = 0; i < n; i++) {
            if (indegree[i] == 0)
                queue.add(i);
        }

        List<Integer> order = new ArrayList<>();

      
        while (!queue.isEmpty()) {
            int task = queue.poll();
            order.add(task);

            for (int next : adj.get(task)) {
                indegree[next]--;
                if (indegree[next] == 0)
                    queue.add(next);
            }
        }

      
        if (order.size() != n)
            return null;

        return order;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(); 
        int m = sc.nextInt(); 
        int[][] dependencies = new int[m][2];
        for (int i = 0; i < m; i++) {
            dependencies[i][0] = sc.nextInt(); 
            dependencies[i][1] = sc.nextInt(); 
        }

        List<Integer> result = findTaskOrder(n, dependencies);

        if (result == null) {
            System.out.println("Release cannot be scheduled");
        } else {
            for (int task : result) {
                System.out.print(task + " ");
            }
        }
    }
}

```

## Output:

<img width="732" height="532" alt="image" src="https://github.com/user-attachments/assets/1fd0a1e3-31df-4c30-ae4c-30a7d4971aae" />


## Result:
The program successfully implemented and the expected output is verified.
