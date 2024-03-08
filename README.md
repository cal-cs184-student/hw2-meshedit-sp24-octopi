[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/sh5wcqPS)
# Homework 2: MeshEdit

## ══✿══╡°˖✧✿✧˖°╞══✿══ OVERVIEW ══✿══╡°˖✧✿✧˖°╞══✿══	
> Give a high-level overview of what you have implemented in this assignment. Think about what you have built as a whole. Share your thoughts on what interesting things you have learned from completing this assignment. <br>
> > [ANSWER HERE]
> 
## ══✿══╡°˖✧✿✧˖°╞══✿══ SECTION 1 ══✿══╡°˖✧✿✧˖°╞══✿══	
### PART 1  ฅ/ᐠ๏⋏๏ᐟ\\=
> *** Briefly explain de Casteljau's algorithm and how you implemented it in order to evaluate Bezier curves. ***
> > <br> Bezier curves are used to represent smooth curves defined by a set of control points. A Bezier curve of degree n is defined by n + 1 control points. The curve starts at the first control point and ends at the last one, while the intermediate control points and weights influence its shape. De Casteljau's algorithm supports Bezier curves given its control points and a param t, it does this by: recursively subdividing the curve into smaller segments until it comes to a single point (the red point in the following photos) and iteratively interpolates points between control points, effectively "approximating" points along the curve.
> > <br> As stated above, I implement De Casteljau's algorithm to evaluate Bezier curves by recursively subdividing the curve into segments and performing linear interpolation between adjacent control points. Using the equation: p1 * (1 - t) + (p2 * t) to lerp, it calculates intermediate points along each segment, defined by the parameter 't' ranging from 0 to 1. This equation comes from the HW2 spec which states "Given n (possibly intermediate) control points p_​1 ​​,..., p_n ​​and the parameter t, we can use linear interpolation to compute the n−1 intermediate control points at the parameter in the next subdivision level p'\_1 ,...,p'\_(​n−1)​​. After, interpolated points are stored in a vector, representing points lying on the Bezier curve which are used to render the provided test curve (see below).
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

> 
### PART 2
> *** Briefly explain how de Casteljau algorithm extends to Bezier surfaces and how you implemented it in order to evaluate Bezier surfaces. ***
> > <br> De Casteljau algorithm can be extended to Bezier surfaces by applying it recursively in two dimensions (2D) instead. Just as in the case of Bezier curves where De Casteljau's algorithm iteratively interpolates points along a curve defined by control points, for Bezier surfaces, it iteratively interpolates points across 2D, creating a grid of points across the surface. For example, if I have a grid of 3x3 points then I want to recursively travel to interpolate each row of 3 points. Doing so will create 3 Bezier curves, then I want to param u to obtain 3 control points, one on each of the 3 Bezier curves. From here I want to param v in order to apply eval1D to our 3 points, now held in a vector, to obtain a Bezier curve across the other axis.
> > <br>  As stated above, I implement this by completing 3 functions.. 1. evaluateStep(vector, points, t), this function, almost exaclty like task 1, evaluates intermediate control points at a given parameter t within a single subdivision level of the surface. Intead, t is a scalar interpolation parameter that is passed into the function. 2. evaluate1D(vector, points, t), eval1D is called to interpolate across the 3 points mentioned in the example above and later to obtain a Bezier curve across the other axis with v in the function evaluate(u, v). It iteratively calls evaluateStep to refine the control points until only one point remains. 3. As previously mention, evaluate(u, v), obtains every point defined in the 3x3 grid by using u and v which will be used to find our 3 curves (using u) and effectively "sweep" across them with the found curve across the other axis (using v). 
> 
> > Show a screenshot of bez/teapot.bez (not .dae) evaluated by your implementation... <br>
> > <img width="950" alt="de Casteljau b surface" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/c677d6df-1871-44e5-a668-bb476554cf46">
> 
## ══✿══╡°˖✧✿✧˖°╞══✿══ SECTION 2 ══✿══╡°˖✧✿✧˖°╞══✿══	
### PART 3
> *** Briefly explain how you implemented the area-weighted vertex normals. *** <br>
> > First, I want to initialize variables: HalfedgeCIter h_edge = halfedge(); to start my traversal and Vector3D norm_sum = Vector3D(0, 0, 0); to hold the total sum of all the found normals. Then I loop through all the neighboring edges, it iterates as long as the current half edge (h_edge) is not equal to the original half edge associated with the vertex. Inside the loop, I retrieve the positions of the vertices of the current triangle edges, calculate the cross product of 2 edges, and then add this found norm to the total norma sum variable defined earlier. After, update the current half_edge to be a neighbor to continue the loop. Once complete, return the tot norm_sum! 
> 
> > Show screenshots of dae/teapot.dae (not .bez) comparing teapot shading with and without vertex normals. Use Q to toggle default flat shading and Phong shading.. <br>
> > <img width="450" alt="flat_shading" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/44979ac7-9869-4ed8-a636-dc6ada8bb46a">
> > <img width="450" alt="phong_shading" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/2e430d8e-756a-4642-8e05-5d186a1fd2aa">
> > <br> flat shading on the left, phong shading on the right
> 
### PART 4
> *** Briefly explain how you implemented the edge flip operation and describe any interesting implementation / debugging tricks you have used. ***
> > <img width="1157" alt="flip_edge" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/01a24e04-8dae-464e-b743-3e5a7f399c77">
> > [image provided by HW2 spec](https://cs184.eecs.berkeley.edu/sp24/docs/hw2-spec#p4)
> > <br> First, check if the edge is a boundary or not. The first test case in the if statement checks if the edge _is not_ a boundary...
> > <br> if true then assign values to the half_edges, edges, vertices, and faces from the provided edge, e0. I also defined an e0 pointer to better ensure all pointers of all elements in the modified mesh have been properally set and I am not direclty modifying an edge. As stated by the spec, "for every element in the modified mesh, set all of its pointers to the correct element in the modified mesh, even if the element being pointed to has not changed." So, after setting up, I also explicitly set the half_edge pointers for edges, vertices, and faces to effectively "doubly link" half_edges and their respective components. After which I set their neighbors using setNeighbor(next, twin, vertex, edge, face) to update all the relationships between half_edges and their twins. (all while using pointers !! )
> > <br> if false, return immediately as to never flip a boundary and by returning e0, a EdgeIter is still returned with no other changes made.
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
> > I later found my issue was caused by incorreclty assigning the halfedges for one of my face iter.  
>
### =/ᐠ*.ꞈ.ᐟ\ฅ PART 5
> *** Briefly explain how you implemented the edge split operation and describe any interesting implementation / debugging tricks you have used. ***
> > <img width="1111" alt="split_edge" src="https://github.com/cal-cs184-student/hw2-meshedit-sp24-octopi/assets/90167734/84c15ff7-a0f6-41a1-bfc5-66e995a641e3">
> > [image provided by HW2 spec](https://cs184.eecs.berkeley.edu/sp24/docs/hw2-spec#p5)
> > <br> Split edge is quite similar to flip edge, however it requires the creation of 6 new half_edges, 3 new edges, 2 new faces, and 1 new vertex. 
> > <br> if true, proceed to setup the initial alf_edges, edges, vertices, and faces. When doing so, I also created the new half_edges, edges, vertices, and faces. Again, set the half_edge pointers and the new components are respectively integrated do ensure the pointers are also correctly associated. Lastly, setNeighbors(...), to update the component relationships. 
> > <br> if false, return immediately as to never split a boundary edge and by returning e0->halfedge()->vertex() a VertexIter is still returned with no other changes made. 
> > <br> Note that splitting a boundary edge does make sense, but flipping a boundary edge does not make sense. (Can you reason why this is the case?)
> > <br> Flipping an edge involves swapping the vertices of the edge, which could result in connecting two boundary vertices that were previously not connected or even flip in such a way that causes an interior vertex to become an exterior (boundary) vertex. Both of which violates the definition of a boundary and can create inconsistencies in the mesh topology.
>
> > Show screenshots of a mesh before and after some edge splits. <br>
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
> > [ANSWER HERE]
> 
> ** Take some notes, as well as some screenshots, of your observations on how meshes behave after loop subdivision:
> > What happens to sharp corners and edges? Can you reduce this effect by pre-splitting some edges?
> > [IMG]
> > [ANSWER HERE]
>
> ** Load dae/cube.dae. Perform several iterations of loop subdivision on the cube. Notice that the cube becomes slightly asymmetric after repeated subdivisions:
> > Can you pre-process the cube with edge flips and splits so that the cube subdivides symmetrically? Document these effects and explain why they occur. <br>
> > [IMG?]
> > [ANSWER HERE] <br>
> > Also explain how your pre-processing helps alleviate the effects. <br>
> > [IMG?]
> > [ANSWER HERE] <br>
> 
> If you have implemented any extra credit extensions, explain what you did and document how they work with screenshots.
> > no attempt. 


<br> You can view the spec for this project at [Assignment 2: MeshEdit](https://cs184.eecs.berkeley.edu/sp24/docs/hw2-spec).
<br> 
<br> .... .....  .. ᘛ⁐̤ᕐᐷ .... ... ..  ....     .... ....  . ........ .. ..... . .. .    .        .   ..     .  .  . .. . .. ... .. 🧀  ...  .
