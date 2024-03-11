[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/sh5wcqPS)
# Homework 2: MeshEdit

[GITHUB LINK](https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi)
<br> [SUBMISSION LINK](https://cs184.eecs.berkeley.edu/sp24/p/muuncakez/assignment/5)

## ══✿══╡°˖✧✿✧˖°╞══✿══ OVERVIEW ══✿══╡°˖✧✿✧˖°╞══✿══	
> Give a high-level overview of what you have implemented in this assignment. Think about what you have built as a whole. Share your thoughts on what interesting things you have learned from completing this assignment. <br>
> > This assignment covers the implementation of Bezier curves and surfaces using the de Casteljau algorithm, along with Loop subdivision for mesh detail enhancement. It involves recursively subdividing control points to approximate curves and surfaces while maintaining smoothness and continuity. Additionally, the implementation includes mesh subdivision techniques such as edge flipping and splitting to adjust vertex positions while preserving mesh integrity. Overall, the assignment provides practical experience in computer graphics algorithms and emphasizes the importance of maintaining mesh integrity during subdivision processes. 
> 
## ══✿══╡°˖✧✿✧˖°╞══✿══ SECTION 1 ══✿══╡°˖✧✿✧˖°╞══✿══	
### PART 1  ฅ/ᐠ๏⋏๏ᐟ\\=
> *** Briefly explain de Casteljau's algorithm and how you implemented it in order to evaluate Bezier curves. ***
> > <br> Bezier curves are used to represent smooth curves defined by a set of control points. A Bezier curve of degree n is defined by n + 1 control points. The curve starts at the first control point and ends at the last one, while the intermediate control points and weights influence its shape. De Casteljau's algorithm supports Bezier curves provided the control points and a param t, it does this by: _recursively subdividing_ (see img below *) the curve into smaller segments until it comes to a single point (the red point in the render imgs) and iteratively interpolates points between control points, effectively "approximating" points along the curve.
> > <br> As stated above, I implement De Casteljau's algorithm to evaluate Bezier curves by recursively subdividing the curve into segments and performing linear interpolation between adjacent control points. Using the equation: p1 * (1 - t) + (p2 * t) to lerp, it calculates intermediate points along each segment, defined by the parameter 't' ranging from 0 to 1. This equation comes from the HW2 spec which states "Given n (possibly intermediate) control points p_​1 ​​,..., p_n ​​and the parameter t, we can use linear interpolation to compute the n−1 intermediate control points at the parameter in the next subdivision level p'\_1 ,...,p'\_(​n−1)​​. After, interpolated points are stored in a vector, representing points lying on the Bezier curve which are used to render the provided Bezier curve. <br>
> > <img width="800" alt="Screen Shot 2024-03-08 at 3 04 08 PM" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/132e3fb5-8c66-48a7-b780-ef1d2cd49b5e">
> > <br> * "control polygons converge to Bezier curves under _recursive subdivision_ from left to right"
> > <br> I found this note very helpful in conceptualizing: [SubDivision](https://www.clear.rice.edu/comp360/lectures/old/SubdivisionTextNew.pdf), photo and quote from source as well. 
> 
> ** Take a look at the provided .bzc files and create your own Bezier curve with 6 control points of your choosing. Use this Bezier curve for your screenshots below:
> > Show screenshots of each step / level of the evaluation from the original control points down to the final evaluated point. Press E to step through. Toggle C to show the completed Bezier curve as well... <br>
> > <img width="300" alt="bcvure, c" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/a623725f-4096-4b77-94ce-6589fae6748e">
> > <img width="300" alt="bcurve, c and e1" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/1e48e6f1-31c0-4d96-84a8-3b2e63753381">
> > <img width="300" alt="bcurve, c and e2" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/a74f5829-fe3c-4eb8-adfc-69c4a96ce2f1">
> > <img width="300" alt="bcurve, c and e3" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/3032cb2f-7595-48dc-8519-76dcfacb280d">
> > <img width="300" alt="bcurve, c and e4" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/cab89b23-29be-4517-8758-b125a75a71e5">
> > <img width="300" alt="bcurve, c and e5" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/2114936f-5971-4e1b-8072-7a0202d9d113">

> > <br> Show a screenshot of a slightly different Bezier curve by moving the original control points around and modifying the parameter _t_ via mouse scrolling... <br>
> > <img width="300" alt="bcurve, t scroll L" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/f299c9e9-aadf-46a4-85d3-00649bbeae80">
> > <img width="300" alt="bcurve, t scroll M" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/08590c5f-c774-4f54-8002-4f4153be5c1a">
> > <img width="300" alt="bcurve, t scroll R" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/cccadbf5-0c99-4489-a58c-694482ba68c3">
> > <br> . ︵‿︵‿୨ ♡ ୧‿︵‿︵ . ︵‿︵‿୨ ♡ ୧‿︵‿︵ . ︵‿︵‿୨ ♡ ୧‿︵‿︵ . ︵‿︵‿୨ ♡ ୧‿︵‿︵ . ︵‿︵‿୨ ♡ ୧‿︵‿︵ . ︵‿︵‿୨ ♡ ୧‿︵‿︵ . ︵‿︵‿୨ ♡ ୧‿︵‿︵ .

> 
### PART 2
> *** Briefly explain how de Casteljau algorithm extends to Bezier surfaces and how you implemented it in order to evaluate Bezier surfaces. ***
> > <br> De Casteljau algorithm can be extended to Bezier surfaces by applying it recursively in two dimensions (2D) instead. Just as in the case of Bezier curves where De Casteljau's algorithm iteratively interpolates points along a curve defined by control points, for Bezier surfaces, it iteratively interpolates points across 2D, creating a grid of points across the surface. For example, if I have a grid of 3x3 points then I want to recursively travel to interpolate each row of 3 points. Doing so will create 3 Bezier curves, then I want to param u to obtain 3 control points, one on each of the 3 Bezier curves. From here I want to param v in order to apply eval1D to our 3 points, now held in a vector, to obtain a Bezier curve across the other axis.
> > <br>  As stated above, I implement this by completing 3 functions.. 1. evaluateStep(vector, points, t), this function, almost exaclty like task 1, evaluates intermediate control points at a given parameter t within a single subdivision level of the surface. Intead, t is a scalar interpolation parameter that is passed into the function. 2. evaluate1D(vector, points, t), eval1D is called to interpolate across the 3 points mentioned in the example above and later to obtain a Bezier curve across the other axis with v in the function evaluate(u, v). It iteratively calls evaluateStep to refine the control points until only one point remains. 3. As previously mention, evaluate(u, v), obtains every point defined in the 3x3 grid by using u and v which will be used to find our 3 curves (using u) and effectively "sweep" across them with the found curve across the other axis (using v). 
> > <br> For further learning: [Making Things with Math by Steven W. ](https://acko.net/tv/wdcode/), timestamp: 18:40 for Bezier surfaces.
> 
> Show a screenshot of bez/teapot.bez (not .dae) evaluated by your implementation... <br>
> > <img width="950" alt="de Casteljau b surface" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/c677d6df-1871-44e5-a668-bb476554cf46">
> 
## ══✿══╡°˖✧✿✧˖°╞══✿══ SECTION 2 ══✿══╡°˖✧✿✧˖°╞══✿══	
### PART 3
> *** Briefly explain how you implemented the area-weighted vertex normals. *** <br>
> > First, I want to initialize variables: HalfedgeCIter h_edge = halfedge(); to start my traversal and Vector3D norm_sum = Vector3D(0, 0, 0); to hold the total sum of all the found normals. Then I loop through all the neighboring edges, it iterates as long as the current half edge (h_edge) is not equal to the original half edge associated with the vertex (aka full circle). Inside the loop, I retrieve the positions of the vertices of the current triangle edges, calculate the cross product of the 2 edges, and then add this found norm to the norm_sum variable defined earlier. After, update the current half_edge to be a neighbor to continue the loop. Once complete, return the tot norm_sum! 
> 
> > Show screenshots of dae/teapot.dae (not .bez) comparing teapot shading with and without vertex normals. Use Q to toggle default flat shading and Phong shading.. <br>
> > flat: <br>
> > <img width="450" alt="flat_shading" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/44979ac7-9869-4ed8-a636-dc6ada8bb46a">
> > <img width="450" alt="flat_shading_wires" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/0f5b760a-82e7-411a-9eb2-21e014548efc">
> > <br> phong: <br>
> > <img width="450" alt="phong_shading" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/2e430d8e-756a-4642-8e05-5d186a1fd2aa">
> > <img width="450" alt="phong_shading_wires" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/f2a7a694-9b3a-4138-8d45-5d085748cc75">

> > <br> flat shading on the left, phong shading on the right

## preface: pt4 and pt5...
> > For parts 4 and 5 whenever I am assigning the pointer values I am using the terms next and twin to traverse the edges of each triangle, this is a photo I used for referece when drawing out the traversal of a triangle and debugging: <br>
> > <img width="491" alt="Screen Shot 2024-03-10 at 10 38 21 PM" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/06884488-8b92-425a-81d7-1ba9cbe2ca2a">
> > <br> Image from [An Introduction to the Half-Edge Data Structure](https://cs184.eecs.berkeley.edu/sp24/docs/half-edge-intro)
> > <br> I also referred to [Iterators vs. Pointers](https://cs184.eecs.berkeley.edu/sp24/docs/iterators-vs-pointers) for using pointers. 

### PART 4
> *** Briefly explain how you implemented the edge flip operation and describe any interesting implementation / debugging tricks you have used. ***
> > <img width="1157" alt="flip_edge" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/01a24e04-8dae-464e-b743-3e5a7f399c77">
> > [image provided by HW2 spec](https://cs184.eecs.berkeley.edu/sp24/docs/hw2-spec#p4)
> > <br> First, init all my variables and then check if the edge is a boundary or not. The test case in the if statement checks if the edge _is not_ a boundary...
> > <br> If True --> then assign values to the half_edges, edges, vertices, and faces from the provided edge, e0. I also defined an e0 pointer, e00, to better ensure all pointers of all elements in the modified mesh have been properly set and I am not needlessly by accident processing e0 (plus, as stated by the spec, "for every element in the modified mesh, set all of its pointers to the correct element in the modified mesh, even if the element being pointed to has not changed"). After setting up, I set their neighbors using setNeighbor(next, twin, vertex, edge, face) to update all the relationships. Lastly, set the half_edge pointers for edges, vertices, and faces to ensure full connectivity. (all using pointers !!)
> > <br> If False --> return immediately as to never flip a boundary and by returning e0, a EdgeIter is still returned with no other changes made.
> 
> > Show screenshots of a mesh before and after some edge flips... <br>
> > <img width="450" alt="teapot_before" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/79b62ff6-024f-463a-9fc0-277a7a4931eb">
> > <img width="450" alt="teapot_after" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/ca58df68-452e-4ac6-b3a1-0b42f8449f76">
> > <img width="450" alt="under_before" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/036ed8b8-1546-450d-8a0f-877b825221e2">
> > <img width="450" alt="under_after" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/70a002a8-972c-48e8-b5f9-f795b47203b3">
> 
> ** Write about your eventful debugging journey, if you have experienced one. <br>
> > <img width="953" alt="just a hole" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/c01e0d84-f66c-4242-b0ed-1c3d62ab3e4a">
> > nothing eventful just a persistent hole (┛ಠДಠ)┛彡┻━┻
> > I later found my issue was caused by incorreclty assigning the halfedges for one of the faces and as I continued to flip nearby edges the hole would grow. I found drawing it out (espically after my debugging fiasco with task 6, more on that later) was helpful to reassure what I was assigning to what correctly.
>
### =/ᐠ*.ꞈ.ᐟ\ฅ PART 5
> *** Briefly explain how you implemented the edge split operation and describe any interesting implementation / debugging tricks you have used. ***
> > <img width="1111" alt="split_edge" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/84c15ff7-a0f6-41a1-bfc5-66e995a641e3">
> > [image provided by HW2 spec](https://cs184.eecs.berkeley.edu/sp24/docs/hw2-spec#p5)
> > <br> Split edge is quite similar to flip edge when init my pointers, however it also requires the creation of 6 new half_edges, 3 new edges, 2 new faces, and 1 new vertex. First, init all my variables and then the test case in the if statement checks if the edge _is not_ a boundary...
> > <br> If True --> proceed to setup the half_edge, edge, vertex, and face pointers of the current mesh. When doing so, I also created the new half_edges, edges, vertices, and faces as mentioned above, these are coming from the 2 new triangles created when splitting an edge in half. When splitting I must also define a middle vertice that is the bisection between the two edges that create my "split". This mid_vect is found by: (v1->position + v0->position) / 2. Then, setNeighbors(...), to update the component relationships. Lastly, set the half_edge pointers to ensure the pointers are correctly associated. 
> > <br> If False --> return immediately as to never split a boundary edge and by returning e0->halfedge()->vertex() the current VertexIter is returned with no other changes made. 
> > <br> ** Note that splitting a boundary edge does make sense, but flipping a boundary edge does not make sense. (Can you reason why this is the case?) **
> > <br> Flipping an edge involves swapping the vertices of the edge, which could result in connecting two boundary vertices that were previously not connected or flip in such a way that causes an interior vertex to become an exterior (boundary) vertex. Both of which violates the definition of a boundary and can create inconsistencies in the mesh topology.
>
> > Show screenshots of a mesh before and after some edge splits. <br>
> > <br> The Before-Fore: <br>
> > <img width="950" alt="cow_before" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/41d0ec39-9c6c-4d97-9ab6-4706357f5ac4">
> > <img width="450" alt="cow_after_split" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/710700b5-1220-4113-a9cb-d6fdd345c873">
> > <img width="450" alt="cow_after_split_zoomed" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/1dc736d1-aabe-4f11-a0b6-4f44073c1d79">
> > <br> Show screenshots of a mesh before and after a combination of both edge splits and edge flips. <br>
> > <img width="450" alt="cow_after_split_flip" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/147da9a4-2f81-4747-abd9-17623ce5cac5">
> > <img width="450" alt="cow_after_sf_zoomed" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/302e3eac-a342-4d05-a20f-7df7ccdecaa1">
> 
> ** Write about your eventful debugging journey, if you have experienced one. <br.
> > I do not have an eventful debugging journey to recount, \*phew\*
> 
> ** If you have implemented support for boundary edges, show screenshots of your implementation properly handling split operations on boundary edges. <br>
> > no attempt.
>
### PART 6
> *** Briefly explain how you implemented the loop subdivision and describe any interesting implementation / debugging tricks you have used. ***
> > These are the steps as provided by the starter code and my implemention:
> > Plese Note: All implemented loops in this task are _while loops_ as recommended by [Possible Pitfalls of Iterating Mesh Elements](https://cs184.eecs.berkeley.edu/sp24/docs/half-edge-primer)
> > | Starter Code Steps | My Implementation |
> > | :---- | :----: |
> > | Step A: | Compute the positions of both new and old vertices using the original mesh... |
> > | 1. Compute new positions for all the vertices in the input mesh | Loop through all the vertices in the mesh. For each vertex, initialize the variable norm_sum to accumulate the sum of neighboring vertex positions and compute the weight factor u based on the vertex's degree, n. Then, iterate through the incident half-edges of the vertex, totaling the positions of neighboring vertices into norm_sum. After, using the provided Loop subdivision formula: (1 - n * u) * original_position + u * original_neighbor_position_sum, compute the new position for the vertex by combining its original position and the weighted sum of neighboring vertexs. Finally, mark each vertex as belonging to the og mesh by setting its isNew flag to false.  |
> > | 2. Compute the updated vertex positions associated with edges | Loop through every edge in the mesh and retrieve the positions of four adjacent vertices: vect_A, vect_B, vect_C, and vect_D. Using these vertex positions, compute the new position for the edge according to the provided Loop subdivision formula: 3/8 * (A + B) + 1/8 * (C + D). After computing the new position, increment the old_edges proccessed counter by one to effectively count the tot # of edges in the og mesh for later use and move to the next edge; mark each edge as belonging to the og mesh by setting its isNew flag to false. |
> > | Step B: | subdivide the _original mesh_ with splits and flips... |
> > | 3. Split every edge in the mesh, in any order | Loop through the total amount of edges found in step 2 using old_edges, I don't need to know the edge object itself, just that an edge has been visited in the old mesh. Split every existing edge of the mesh in any order using mesh.splitEdge(edge) which yeilds a new vertex. After splitting, assign the new vertex's position to the newPosition attribute of the current edge. Finally, update the current edge to the next edge using the temp value and increment the edge processed counter.|
> > | 4. Flip any new edge that connects an old and new vertex | Loop through every edge and then check the edge isNew flag... if False --> do nothing. if True --> retrieve the two vertices connected by the edge. With the two vertices check if the isNew flags are different (v1->isNew != v2->isNew), if True --> one of the vertices is marked as new (aka it belongs to the subdivided mesh, the _new_ mesh) while the other vertex is not marked as new (aka it belongs to the original mesh, the _old_ mesh). This means the edge must be flipped, there is no need to set the edge to false as it has already been done for all edges in 2.   
> > | Step C: | Update all vertex positions in the subdivided mesh using the values already computed.| 
> > | 5. Copy the new vertex positions into final. | Copy the new position to the final position of the vertex which is necessary to update the geometry of the mesh with the results of the subdivision process. See below for if I only update when the vert->isNew = false and when vert->isNew = true (b/c they look cool and almost "opposite" of each other not just in the sense of isNew but with what is rendered too).|
> > <img width="950" alt="task 6_icosahedron" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/08a49943-376f-4266-a6ef-88c155fdd712">
> > <br> vert->isNew = false: <br>
> > <img width="450" alt="isNew-false_wireframe" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/a3c9ec8f-28cc-4df7-91f7-dbf9365ae55d">
> > <img width="450" alt="isNew-false" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/b0e962e7-f7eb-4952-9bc6-1386a3151b29">
> >
> > <br> vert->isNew = true: <br>
> > <img width="450" alt="isNew-true_wireframe" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/172d3200-013f-48c5-a09e-4ecfddd91326">
> > <img width="450" alt="isNew-true" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/7077d5de-b4c1-49bb-bd31-9e6c47587dc7">
> 
> ** Take some notes, as well as some screenshots, of your observations on how meshes behave after loop subdivision:
> > What happens to sharp corners and edges? It smooths out edges!<br>
> > <img width="450" alt="task 6_icosahedron_0" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/7e0d3144-bc7e-4309-8fac-01702e4bd662">
> > <img width="450" alt="task 6_icosahedron_0-no-wire" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/abdc3386-cf73-490b-8ef1-be2d2ea995ce">
> > <img width="225" alt="task 6_icosahedron_1" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/e1b87a03-df1c-4534-9893-d8214a981281">
> > <img width="225" alt="task 6_icosahedron_2" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/475630d4-6e30-454c-9d39-9b916e17604e">
> > <img width="225" alt="task 6_icosahedron_3" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/56fcceab-7ad6-45ff-bffc-97f2860a7405">
> > <img width="225" alt="task 6_icosahedron_4" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/03f58bf9-3fb7-4ad5-af1e-ae22645a86ef">
> > <img width="450" alt="task 6_icosahedron_5" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/e6a70bd2-6cf8-4c03-aa4d-30e28ce3c916">
> > <img width="450" alt="task 6_icosahedron_5-no-wire" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/775347d4-d388-4302-bd66-23ce0235c816">

> > <br> Can you reduce this effect by pre-splitting some edges? <br>
> > <img width="300" alt="pre-split1" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/3c810a4f-9bc3-434e-ad68-21767d43385e">
> > <img width="300" alt="pre-split2" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/e34f31a9-66cc-4cda-9bca-1f84dc580d57">
> > <img width="300" alt="pre-split3" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/cc202642-5ab0-4f2d-a4a9-c24df956f1e9">
> > <img width="300" alt="pre-split4" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/1c112f70-a2de-43e1-b3c2-86ed88bcafa0">
> > <img width="300" alt="pre-split5" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/448562b7-6049-4f2c-b6c9-5dd86bfb66f1">
> > <img width="300" alt="pre-split6" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/d4c307d8-7948-4dd1-8141-d3e6b346d0b9">
> > Pre-splitting an area will preserve the edge adjacent to it! However my implementation seems to cause pre-split parts to begin to grow out from the original shape. I am not 100% sure why this occurs but I am unfortantely short on time. I believe it entirely has to do with a small missed consideration in creating my loop subvision that is manifesting as a greater problem when a large handful of pre-splits is present. 
>
> ** Load dae/cube.dae. Perform several iterations of loop subdivision on the cube. Notice that the cube becomes slightly asymmetric after repeated subdivisions:
> > Can you pre-process the cube with edge flips and splits so that the cube subdivides symmetrically? Document these effects and explain why they occur. <br>
> > <img width="300" alt="pre-process0" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/0aab6445-736d-4da1-9291-e4e98ef3ae6d">
> > <img width="300" alt="pre-process1" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/77f5892f-4511-4ffb-8c0c-8addd6f4457c">
> > <img width="300" alt="pre-process2" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/688a2e3e-3731-4e29-bbd9-257fad45f5e0">
> > <img width="300" alt="pre-process3" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/f81d05bd-dc7c-474f-baed-cc984df6f596">
> > <img width="300" alt="pre-process4" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/f953d880-ef3e-4e75-9cc8-6c6022d26abe">
> > <img width="300" alt="pre-process5" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/6686a9ad-7961-4dc5-9c77-350e81331106">

> > <br> Not pre-processing the cube will lead to it subdividing asymmetrically, this is due to the edges becoming asymmetric after one loop subdivision (evident in the second img). <br>
> > Also explain how your pre-processing helps alleviate the effects. <br>
> > <img width="300" alt="split-preprocess" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/f2de81b0-27e3-4544-b597-20eaf1a6fa6d">
> > <img width="300" alt="split-preprocess1" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/e33cbed7-6ac6-48ee-953e-67af95dcc8be">
> > <img width="300" alt="split-preprocess2" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/901bfa04-0710-45b3-83b2-2113edb1e251">
> > <img width="300" alt="split-preprocess3" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/283ef74e-56d4-4c77-8249-2b2acac9b146">
> > <img width="300" alt="split-preprocess4" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/f9e85352-3088-476b-8afd-a7dfcd886b08">
> > <img width="300" alt="split-preprocess5" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/2812dd84-5526-4a10-954e-033c8bca7caf">
> > <br> Based on the imgs, pre-processing the cube by splitting the front facing edge once will lead to symmetrical subdivision! Again, my implementation is experiencing some upsampling errors which is leading to a more oblonged shape. Despite this setback, its evident that the pre-split improved the mesh based on the wireframes and its more symmetric. <br>
>
> > <br> Task 6 Error Analysis: my task 4, 5 were mostly correct, I was mismapping some of the old verices to the new edges so the when things split upon hitting L (aka upsampling), my edges would go ~~a little~~ very haywire and exponentionally degrade from there. The main issues, however, was I was not flagging ALL the old vertices and edges in my unsample function so upon hitting L my cube turned into a crumbled ball of paper: <br>
> > <img width="300" alt="task 6 - integrity fail 0" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/b195725b-fef7-4391-8b30-11f552a52d4b">
> > <img width="300" alt="task 6 - integrity_fail 1" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/e6ac1032-e3f8-4ab8-ac9a-2113b2ba2986">
> > <img width="300" alt="task 6 - integrity_fail 2" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/7d275e1f-6f05-4bfc-a286-f31fe73c71be">


> If you have implemented any extra credit extensions, explain what you did and document how they work with screenshots.
> > no attempt. 


<br> You can view the spec for this project at [Assignment 2: MeshEdit](https://cs184.eecs.berkeley.edu/sp24/docs/hw2-spec).
<br> 
<br> .... .....  .. ᘛ⁐̤ᕐᐷ .... ... ..  ....     .... ....  . ........ .. ..... . .. .    .        .   ..     .  .  . .. . .. ... .. 🧀  ...  .
