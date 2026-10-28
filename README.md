

File System Representation and Search Using BFS and DFS

1. PROJECT DESCRIPTION

This project implements a simple file system representation using a graph data structure in C. Files and directories are represented as nodes, and the relationships between them are represented as directed edges. The program uses an adjacency matrix to store the graph and searches for a specified file using two graph traversal algorithms: Breadth-First Search (BFS) and Depth-First Search (DFS).

2. OBJECTIVES

- To represent a file system using a graph.
- To store relationships between files and directories using an adjacency matrix.
- To implement Breadth-First Search (BFS) for file searching.
- To implement Depth-First Search (DFS) for file searching.
- To display the traversal order and search results.

3. TECHNOLOGIES USED

- Programming Language: C
- Data Structure: Graph
- Graph Representation: Adjacency Matrix
- Algorithms: BFS and DFS
- Compiler: GCC or any standard C compiler

4. FEATURES

- Accepts the number and names of files and directories.
- Creates directed edges between parent directories and child nodes.
- Displays the adjacency matrix.
- Searches for a target file using BFS and DFS.
- Displays the traversal order for both algorithms.
- Reports whether the target file is found or not found.
- Handles invalid node names in edges and invalid starting nodes.

5. WORKING PRINCIPLE

1. The user enters the number of nodes and their names.
2. The user enters the edges representing parent-child relationships.
3. The program constructs the graph using an adjacency matrix.
4. The adjacency matrix is displayed.
5. The user enters a starting node and the name of the file to search for.
6. BFS explores the graph level by level using a queue.
7. DFS explores the graph depth-wise using recursion.
8. The program displays the traversal order and search result for both algorithms.

6. ALGORITHMS USED

Breadth-First Search (BFS):

BFS visits nodes level by level, starting from the selected node. It uses a queue to manage the nodes waiting to be visited.

Depth-First Search (DFS):

DFS explores one path as deeply as possible before backtracking. This implementation uses recursion to visit nodes.

7. HOW TO COMPILE AND RUN

Save the program as filesystem.c.

Compile the program using GCC:

gcc filesystem.c -o filesystem

Run the program on Linux or macOS:

./filesystem

On Windows, run:

filesystem.exe

8. SAMPLE INPUT

Enter number of nodes (files/directories): 5
Enter the names of 5 nodes:
Root Documents Images Notes Report
Enter number of edges: 4
Enter 4 edges (parent child):
Root Documents
Root Images
Documents Notes
Documents Report

Enter start node: Root
Enter file to search: Report

9. EXPECTED OUTPUT

Adjacency Matrix:
                  0   1   2   3   4
 0 Root           0   1   1   0   0
 1 Documents      0   0   0   1   1
 2 Images         0   0   0   0   0
 3 Notes          0   0   0   0   0
 4 Report         0   0   0   0   0

--- Searching for 'Report' starting from 'Root' ---

BFS Traversal Order: Root Documents Images Notes Report
BFS Result: File 'Report' FOUND

DFS Traversal Order: Root Documents Notes Report
DFS Result: File 'Report' FOUND

Note: The adjacency matrix and traversal order depend on the node names, edge order, and input graph.

10. TIME AND SPACE COMPLEXITY

Let V represent the number of nodes and E represent the number of edges.

- Finding a node by name: O(V)
- Displaying the adjacency matrix: O(V^2)
- BFS traversal: O(V^2)
- DFS traversal: O(V^2)
- Graph storage: O(V^2)

BFS and DFS take O(V^2) time in this implementation because the graph uses an adjacency matrix and scans all possible adjacent nodes for each visited node.

11. ADVANTAGES

- Simple and easy-to-understand graph representation.
- Demonstrates two important graph traversal algorithms.
- Helps understand relationships between files and directories.
- Provides traversal orders that can be compared.

12. LIMITATIONS

- The program supports a maximum of 50 nodes.
- Node names cannot contain spaces.
- The graph must be entered manually.
- Only nodes reachable from the starting node are searched.
- The program represents directory relationships but does not access the actual operating system file system.

13. CONCLUSION

The project demonstrates how a file system can be represented as a directed graph and how files can be searched using BFS and DFS. It provides a practical understanding of graph representation, adjacency matrices, queues, recursion, and graph traversal algorithms in C.

    printf("Enter the names of %d nodes:\n", n);
    for (int i = 0; i < n; i++)
        scanf("%31s", names[i]);

    memset(adj, 0, sizeof(adj));
    printf("Enter number of edges: ");
    scanf("%d", &e);
    printf("Enter %d edges (parent child):\n", e);
    for (int i = 0; i < e; i++) {
        scanf("%31s %31s", a, b);
        int u = findIndex(a), v = findIndex(b);
        if (u == -1 || v == -1) {
            printf("Skipping invalid edge: %s -> %s\n", a, b);
            continue;
        }
        adj[u][v] = 1;                /* directory u contains v */
    }

    displayMatrix();

    printf("\nEnter start node: ");
    scanf("%31s", startName);
    printf("Enter file to search: ");
    scanf("%31s", targetName);

    int start  = findIndex(startName);
    int target = findIndex(targetName);

    if (start == -1) {
        printf("\nStart node '%s' does not exist.\n", startName);
        return 1;
    }

    printf("\n--- Searching for '%s' starting from '%s' ---\n\n",
           targetName, startName);

    /* If the file isn't a node at all, target = -1 never matches,
       so both traversals visit everything reachable and report not found. */
    int bfsFound = bfs(start, target);
    printf("BFS Result: File '%s' %s\n\n", targetName,
           bfsFound ? "FOUND" : "NOT FOUND");

    int dfsFound = dfs(start, target);
    printf("DFS Result: File '%s' %s\n", targetName,
           dfsFound ? "FOUND" : "NOT FOUND");

    return 0;
}
