
# EX 5A 0/1 Knapsack Problem - Branch&Bound 

## AIM:
To Write a Java program to solve 0/1 Knapsack problem using Branch and Bound Approach.
You are heading a college entrepreneurship cell that can invest in up to N student‑startups.

## Algorithm
1. Input & Initialization:
Read number of startups N and budget B.
Store each startup’s cost (c[]) and profit (p[]).
Initialize a global variable best = 0 to track the maximum profit 
2.  Sorting by Efficiency:
Compute the profit-to-cost ratio (p[i]/c[i]) for each startup.
Sort startups in descending order of this ratio to improve bound estimation.
3.  Upper Bound Calculation (bound()):
For a given node (index idx), current weight cw, and current value cv:
Add profits of remaining startups until the budget is filled.
If the next startup doesn’t fit completely, add a fractional profit proportional to the remaining budget.
This provides a maximum possible (fractional) profit estimate for pruning.
4.   Depth-First Search (DFS) with Branch and Bound (dfs()):
If the current path exceeds the budget or bound ≤ current best → prune the branch.
Otherwise, recursively explore:
Including the current startup (if it fits).
Excluding the current startup.
Update best whenever a higher profit is found.
5.   Output:
After exploring all feasible combinations, print the maximum profit best. 

## Program:
```
Developed by: KISHAN SHREE B
Register Number:212223100022
import java.util.*;

public class StartupShowcaseOptimizer {

    
    static int N, B;
    static int[] c, p;          
    static int best = 0;        

    static double bound(int idx, int cw, int cv) {
        if (cw >= B) return cv;                
        double val = cv;
        int rem = B - cw;

        while (idx < N && c[idx] <= rem) {      
            rem -= c[idx];
            val += p[idx];
            idx++;
        }
        if (idx < N) val += p[idx] * (rem / (double) c[idx]); 
        return val;
    }

   
    static void dfs(int idx, int cw, int cv) {
        if (idx == N) {                 
            best = Math.max(best, cv);
            return;
        }
        if (bound(idx, cw, cv) <= best) return; 

        
        if (cw + c[idx] <= B)
            dfs(idx + 1, cw + c[idx], cv + p[idx]);

        
        dfs(idx + 1, cw, cv);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        N = sc.nextInt();
        B = sc.nextInt();
        int[] cost = new int[N];
        int[] prof = new int[N];
        for (int i = 0; i < N; i++) cost[i] = sc.nextInt();
        for (int i = 0; i < N; i++) prof[i] = sc.nextInt();
        sc.close();

       
        Integer[] idx = new Integer[N];
        Arrays.setAll(idx, i -> i);
        Arrays.sort(idx, Comparator.comparingDouble(i -> -(double) prof[i] / cost[i]));

        c = new int[N];
        p = new int[N];
        for (int i = 0; i < N; i++) {
            c[i] = cost[idx[i]];
            p[i] = prof[idx[i]];
        }

        dfs(0, 0, 0);
        System.out.println(best);
    }
}
 

```

## Output:

<img width="508" height="234" alt="image" src="https://github.com/user-attachments/assets/457902e3-ee50-492b-88c7-4bf952af8c60" />


## Result:
The program successfully solved 0/1 Knapsack problem using branch & bound and output is verified. 
