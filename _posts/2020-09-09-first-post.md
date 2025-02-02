---
title: "A novel computationally efficient method to return safe trajectories"
date: 2020-09-09 00:00:00 -0400
categories: research
# classes: wide
---

<div style="font-size: medium; line-height: 2em;">
<center><strong> A Fast and Safe Motion Planning Algorithm in Cluttered Environment using Maximally Occupying Convex Space</strong> <br>
  Youngsang Suh, Jiseock Kang, Dongjun Lee <br>
  International Conference on Control, Automation and Systems (ICCAS) 2020 <br>
  <a href="/assets/pdf/A fast and safe motion planning algorithm in cluttered environment using maximally occupying convex space.pdf" target="_blank">paper</a> / <a href="https://youtu.be/USFbCB9flEY" target="_blank">video1</a> / <a href="https://youtu.be/HF0Jnxxzqnk" target="_blank">video2</a> / <a href="https://youtu.be/v_M_JT0jAIw" target="_blank">video3</a>   <br> </center>
</div>

<div style="font-size: 15px; line-height: 25px;">
<br>
This work presents a new planning method in cluttered environment using a newly defined concept called maximally occupying convex space (MOCS). Motion planning methods that use safe flight corridor (SFC) generally construct SFC in every new trial based on each initial path. We define MOCS in three-dimensional rectangular world to be prebuilt as SFC prior to the initial path computation. This approach enables to omit constructing SFC every new trial, and our experiment shows computation efficiency compared to a state-of-the-art algorithm based on SFC. <br>
 
</div>

<hr class="one">
<strong> Background </strong><br>

<div style="font-size: 15px; line-height: 25px;">
<strong>SFC? </strong> <br>

SFC consists of overlapping convex spaces that guarantee collision avoidance when waypoints are located inside the overlapping areas. Through utilizing SFC, the system can return safe trajectories owing to the property of SFC. <br><br>

<center><img src="/assets/images/SFC_.png" border="0" width="300" height="330"/> </center> <br>
</div>

<hr class="one">
<strong> Motivation </strong> <br>

<div style="font-size: 15px; line-height: 25px;"> 
Fast and safe motion planning of UAV is still a crucial task to achieve. However, previous studies that utilize SFC need seed points or initial paths to construct SFC. If we generate every possible SFC in the free space priori, the system can have computational efficiency to return safe trajectories. It is because SFC does not have to be constructed every trial, which reduces computation time. <br>
</div>

<hr class="one">
<strong> Task </strong> <br>

<div style="font-size: 15px; line-height: 25px;">
To prebuild every possible SFC, we have to define a convex space and prove that those spaces represent every feasible path in the free space. After the proof, an algorithm that generates every defined convex space should be devised. <br>

</div>

<hr class="one">
<strong> Approach </strong> <br>
 
<div style="font-size: 15px; line-height: 25px;">
How should we define a specific convex space to fill the whole free space without seed points? <br> <br>
Our approach is to use inclusion relation with other convex spaces. With this approach, one can simply (1) make locally maximum convex spaces and (2) use mathematical knowledge to prove the equivalence between feasible paths.

<br>
Furthermore, we use dynamic programming method to construct the algorithm. Dynamic programming is a powerful technique because almost all of the algorithms can be made by this method. <br>
</div>

<hr class="one">
<strong> Maximally Occupying Convex Space </strong> <br>

<div style="font-size: 15px; line-height: 25px;">
<strong>MOCS definition </strong> <br>
Given a rectangular world free space <img src="http://latex.codecogs.com/svg.latex?\mathbb{W}"/>, a set <img src="http://latex.codecogs.com/svg.latex?\mathbb{C}"/> of convex subsets in <img src="http://latex.codecogs.com/svg.latex?\mathbb{W}"/> and a set <img src="http://latex.codecogs.com/svg.latex?\mathbb{O}"/> of cuboid obstacles, a cuboid convex closed set <img src="http://latex.codecogs.com/svg.latex?C"/> is a maximally occupying convex space if and only if <img src="http://latex.codecogs.com/svg.latex?~\forall c \in"/> <img src="http://latex.codecogs.com/svg.latex?\mathbb{C}"/> s.t. <img src="http://latex.codecogs.com/svg.latex?c \not\subset C"/>, <img src="http://latex.codecogs.com/svg.latex?c \cup C"/> is not convex set. <br><br>

<center><img src="/assets/images/MOCS example.jpg" border="0" width="430" height="330"/> </center> <br>
Left: green convex space is not a MOCS, due to its union with red rectangle is a convex space. Right: green, light blue, purple convex spaces are MOCS that contain a blue point. <br><br>

<strong>Lemma </strong> <br>
For <img src="http://latex.codecogs.com/svg.latex?x \in"/> <img src="http://latex.codecogs.com/svg.latex?\text{int}(\mathbb{W})"/>, convex set <img src="http://latex.codecogs.com/svg.latex?S \subset \mathbb{W}"/>, let us define <img src="http://latex.codecogs.com/svg.latex?d_S(x) = min \{\| x-y \| ~|~ y \in \partial S \}"/>, <img src="http://latex.codecogs.com/svg.latex?D(x) = max\{ d_C(x) ~|~ x \in"/> <img src="http://latex.codecogs.com/svg.latex?\text{int}(C), ~ C \in M \}"/>. Then, <img src="http://latex.codecogs.com/svg.latex?D(x) > 0"/>. <br><br>

<strong>Theorem </strong> <br>
For <img src="http://latex.codecogs.com/svg.latex?\forall{x, y} \in \text{int}(\mathbb{W})"/>, there exists feasible path from <img src="http://latex.codecogs.com/svg.latex?x"/> to <img src="http://latex.codecogs.com/svg.latex?y"/> if and only if there exists a sequence <img src="http://latex.codecogs.com/svg.latex?\mathbb{C} = \{C_1, C_2, ... ~, C_n\}"/> s.t. <img src="http://latex.codecogs.com/svg.latex?x \in C_1, y \in C_n, C_i \in M, \text{int}(C_i) \cap \text{int}(C_{i+1}) \neq \phi"/>. <br><br>

Please refer to our paper for further details and proofs.
</div>
  
<hr class="one">
<strong> Algorithmic Implementation </strong> <br>

<div style="font-size: 15px; line-height: 25px;">
We use dynamic programming method to implement an algorithm. We divide a problem into small solvable problems and merge it together at last. You can check our <a href="https://youtu.be/USFbCB9flEY" target="_blank">MOCS construction</a> video for visual explanation. <br><br>
  
After MOCS construction phase, we represent the free space as a simplified undirected graph through connecting every overlapping MOCS. Reasonable function is adopted for an edgecost  function and Dijkstra algorithm is implemented for computation. <br>

</div>

<hr class="one">
<strong> Results </strong> <br>

<div style="font-size: 15px; line-height: 25px;">
<strong> Simulation </strong> <br>
The proposed method turns out to be feasible through simulations. Simple cuboid obstacles and obstacle that is not cuboid are created for simulations. <a href="https://youtu.be/HF0Jnxxzqnk" target="_blank">Simulation 1</a> <a href="https://youtu.be/v_M_JT0jAIw" target="_blank">Simulation 2</a>   
  <br><br>
<center><img src="/assets/images/Simulationpath.png" border="0" width="430" height="330"/> </center>
  
<br><br>

<strong> Computation time comparison </strong> <br>
Among previous studies that use SFC, we compare the proposed method with Gao’s method [1]. Our method returns safe trajectory 1.7 times faster than Gao's method in our simulated environment.<br> <br>
<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  overflow:hidden;padding:10px 5px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
.tg .tg-j4pq{background-color:#efefef;border-color:#000000;text-align:center;vertical-align:top}
.tg .tg-wp8o{border-color:#000000;text-align:center;vertical-align:top}
</style>
<table class="tg">
<thead>
  <tr>
    <th class="tg-j4pq">Proposed method</th>
    <th class="tg-j4pq">MOCS (once)</th>
    <th class="tg-j4pq">Dijkstra</th>
    <th class="tg-j4pq">Optimization</th>
    <th class="tg-j4pq">Total</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-wp8o">Time (ms)</td>
    <td class="tg-wp8o">8.24</td>
    <td class="tg-wp8o">0.03</td>
    <td class="tg-wp8o">44.22</td>
    <td class="tg-wp8o">52.49</td>
  </tr>
  <tr>
    <td class="tg-j4pq">Gao's method (0.1 m resolution) [1]</td>
    <td class="tg-j4pq">A*</td>
    <td class="tg-j4pq">SFC construction</td>
    <td class="tg-j4pq">Optimization</td>
    <td class="tg-j4pq">Total</td>
  </tr>
  <tr>
    <td class="tg-wp8o">Time (ms)</td>
    <td class="tg-wp8o">1.30</td>
    <td class="tg-wp8o">74.14</td>
    <td class="tg-wp8o">15.08</td>
    <td class="tg-wp8o">90.52</td>
  </tr>
</tbody>
</table> 

<br>
Please refer to our paper for further details. <br><br>
[1] F. Gao, W. Wu, Y. Lin, and S. Shen, “Online safe trajectory generation for quadrotors using fast marching method and bernstein basis polynomial,” in 2018 IEEE International Conference on Robotics and Automation (ICRA). IEEE, 2018, pp. 344–351. <br>
</div>

