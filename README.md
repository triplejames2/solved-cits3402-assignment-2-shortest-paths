Download Link: https://assignmentchef.com/product/solved-cits3402-assignment-2-shortest-paths
<br>









<h1>1      Details</h1>

The goal of this project is to design an implement parallel algorithms to solve the all-pairs-shortest path problem for a number of large graphs using either Dijkstra’s or Floyd-Warshall algorithms. You will use C with the MessagePassing Interface (MPI) to write parallelized code. You will also need to observe and comment on how speedup is affected by changing the size of the problem and the number of nodes you use. A reasonable range for the size of your problems is 1024 to 4096 vertices. A reasonable range for the number of processors is one to 16.




<h2>1.1     Code</h2>

<h2>1.2     Report</h2>

Alongside your code you will also need to write a report addressing the following points:

<ul>

 <li>How your approach partitions data and processing</li>

 <li>A table showing speedup for graphs of 2048 vertices vs 1<em>,</em>2<em>,</em>4<em>,</em>8<em>,</em>16 processors</li>

 <li>A table showing speedup for 4 processors vs graphs of 256<em>,</em>512<em>,</em>1024<em>,</em>2048<em>,</em>4096 vertices.</li>

</ul>

When discussing the performance of your approach, try to relate performance to various factors in your computation (number of compute nodes, load balancing, communication overhead etc.)

<h1>2      Code Requirements</h1>

<h2>File Reading</h2>

Your solution should read a matrix description from file. It is acceptable to implement this with or without flags, for example:

mpirun -n 4 ./my_solution -f file.in

is acceptable as is

mpirun -n 4 ./my_solution file.in

The input file format is essentially a flattened adjacency matrix for a directed, weighted graph. All weights are positive integers. These are binary files (not text files) and will need to be read in as such. More specifically, each file contains:

<ul>

 <li>The number of vertices (numV)</li>

 <li>numV x numV integers specifying the weights for all connections</li>

</ul>

You can read all the information needed by reading the first integer to determine how many vertices there are in the graph, then read numV x numV integers into a freshly allocated array. For example the graph (assuming nodes are labelled from 0 upwards)

corresponds to the following adjacency matrix

(1)

which would be specified by the file example.in

4 0 15 1 1 0 0 3 0 1 3 0 0 0 1 1 0

Being a binary file however, you would not be able to ’read’ the files yourself as such. We have added an .txt files for all of our example inputs if you would like to read them yourself to make sure you are correct.

<h2>File Writing</h2>

The output of either algorithm should be a matrix containing the length of the shortest path from vertex <em>i </em>to vertex <em>j</em>. This file has the same form as the input files. That is, a single array length numV*numV + 1 where the first integer is the number of vertices in the graph. The solution for the example.in file would be example.out

4 0 2 1 1 4 0 3 5 1 3 0 2 2 1 1 0

You can choose to write this file by default, or enable this feature with command line arguments. In any case, specify your choice at the top of your code file.

<h1>3      Hints</h1>

<ul>

 <li>When timing your program for speedup analysis do not count the time taken for file operations.</li>

 <li>Passing command line arguments to MPI programs can be a little tricky compared to standard programs, be careful.</li>

 <li>Dijkstra’s algorithm is made very concise by using a priority queue. Since C has no default data structure library you are not <em>required </em>to implement one. A simpler implementation will be accepted.</li>

 <li>A hint for parallelizing Dijkstra’s is that it is a single-source sortest path algorithm</li>

 <li>A hint for parallelizing the Floyd-Warshall algorithm is that it can be viewed as iterating over 2D distance matrix.</li>

</ul>




<h1>Marking Rubric</h1>

<table width="604">

 <tbody>

  <tr>

   <td width="121"></td>

   <td width="121">Critera</td>

   <td width="121">HighlySatisfactory</td>

   <td width="121">Satisfactory</td>

   <td width="121">Unsatisfactory</td>

  </tr>

  <tr>

   <td width="121">File Reading (5)</td>

   <td width="121">Program is able to read input files as specified.</td>

   <td width="121">Reads in adjacency files correctly.</td>

   <td width="121">Attempts to read adjacency files.</td>

   <td width="121">No attempt is made to read adjacency files.</td>

  </tr>

  <tr>

   <td width="121">File Writing (5)</td>

   <td width="121">Program is able to write output files as specified.</td>

   <td width="121">Write output files correctly and efficiently.</td>

   <td width="121">Attempts to write output files but are either poorly formatted or written inefficiently.</td>

   <td width="121">No attempt is made to write output files.</td>

  </tr>

  <tr>

   <td width="121">Dijkstra’sAlgorithm orFloyd Warshall(60)</td>

   <td width="121">Dijkstra’s all-pairs shortest path or the FloydWarshall algorithm isimplemented correctly in a parallel fashion. MPI calls are explained.</td>

   <td width="121">Algorithm is implemented correctly and efficiently.Comments indicate an understanding of the parallelism present.</td>

   <td width="121">Algorithm is either incorrect for some cases or inefficient. Parallelism is attempted but not efficiently.</td>

   <td width="121">Algorithm is implementedincorrectly for all cases or missing. Parallelism is not attempted.</td>

  </tr>

  <tr>

   <td width="121">Report (30)</td>

   <td width="121">Addresses all required points and is presented clearly. Testing is thorough and clear.</td>

   <td width="121">Report addresses all points effectively and is presented clearly. Performance testing is thorough and meaningful.</td>

   <td width="121">Report does not address all points required or some minor readiblity issues.</td>

   <td width="121">Report addresses few points or is very difficult to read.</td>

  </tr>

 </tbody>

</table>

<h2>                   A       Graphs</h2>

Graphs and graph theory provides a natural way to model many problems. Power-grids, transport systems, social structures and nervous systems can all be modelled by large graphs for example. For completeness we provide a definition of a graph below:

<ul>

 <li>A <em>graph G </em>is specified by two sets <em>V </em>and <em>E</em></li>

 <li><em>V </em>is a finite set of points called vertices</li>

 <li><em>E </em>is a finite set of <em>edges</em></li>

 <li>An <em>edge e </em>is an ordered pair of two vertices (<em>u,v</em>) indicating that vertex <em>u </em>is connected to vertex <em>v</em>.</li>

 <li>Edges can be weighted or un-weighted. For our assignment, edges are weighted by positive integers. This forms an extra set of weights <em>w </em>to go along with our vertices and edges.</li>

 <li>Graphs can be directed or un-directed (for every (<em>u,v</em>) there exists an edge (<em>v,u</em>))</li>

 <li>Vertices <em>u </em>and <em>v </em>are <em>adjacent </em>to each other if there is an edge (<em>u,v</em>) or (<em>v,u</em>) present</li>

 <li>A <em>path </em>from vertex <em>u </em>to vertex <em>v </em>is a sequence of vertices following edges that exist in our graph.</li>

 <li>The <em>shortest-path </em>from vertex <em>u </em>to vertex <em>v </em>in a weighted graph is a path with minimum sum-weight</li>

</ul>

<h2>                  B        All-Pairs Shortest Paths</h2>

For a weighted graph, the <em>all-pairs shortest paths </em>problem is to find the shortest path between all pairs of vertices.

<h2>                   C        Dijkstra’s Algorithm</h2>

Dijkstra’s algorithm finds the shortest paths from a starting vertex <em>s </em>to all other vertices in the graph. It incrementally selects edges that appear closest to a vertex to build a set of paths, updating the length of a path if a superior option is found. For more reading, you can start with <a href="https://www.codingame.com/playgrounds/1608/shortest-paths-with-dijkstras-algorithm/dijkstras-algorithm">1,</a> <a href="https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/">2</a> or <a href="http://math.mit.edu/~rothvoss/18.304.3PM/Presentations/1-Melissa.pdf">3.</a> An <em>all-pairs </em>shortest path implementation is found by running Dijkstra’s for each possible source.

5

<h2>                  D        Floyd-Warshall Algorithm</h2>

The Floyd-Warshall algorithm is an all-pairs shortest path algorithm which considers the shortest paths possible over zero ’hops’ upwards. Trivially a path of a single hop is the adjacency of all vertices. The computation of all subsequent paths is based on the following observation.

For three vertices <em>i,j,k </em>the shortest path from <em>i </em>to <em>j </em>either includes the paths <em>i </em>to <em>k </em>plus <em>k </em>to <em>j </em>or it does not. This boils down to exceedingly concise pseudo-code. For more reading consult <a href="https://cp-algorithms.com/graph/all-pair-shortest-path-floyd-warshall.html">1</a> <a href="https://www.geeksforgeeks.org/floyd-warshall-algorithm-dp-16/">2</a> <a href="https://brilliant.org/wiki/floyd-warshall-algorithm/">3</a>

6