[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/sh5wcqPS)
# Homework 2: MeshEdit

## ══✿══╡°˖✧✿✧˖°╞══✿══ OVERVIEW ══✿══╡°˖✧✿✧˖°╞══✿══	
> Give a high-level overview of what you have implemented in this assignment. Think about what you have built as a whole. Share your thoughts on what interesting things you have learned from completing this assignment. <br>
> > [ANSWER HERE]
> 
## ══✿══╡°˖✧✿✧˖°╞══✿══ SECTION 1 ══✿══╡°˖✧✿✧˖°╞══✿══	
### PART 1
> *** Briefly explain de Casteljau's algorithm and how you implemented it in order to evaluate Bezier curves. ***
> > [ANSWER HERE]
> 
> ** Take a look at the provided .bzc files and create your own Bezier curve with 6 control points of your choosing. Use this Bezier curve for your screenshots below:
> > Show screenshots of each step / level of the evaluation from the original control points down to the final evaluated point. Press E to step through. Toggle C to show the completed Bezier curve as well... <br>
> > [IMG]
> > <br> Show a screenshot of a slightly different Bezier curve by moving the original control points around and modifying the parameter _t_ via mouse scrolling... <br>
> > [IMG]
>
### PART 2
> *** Briefly explain how de Casteljau algorithm extends to Bezier surfaces and how you implemented it in order to evaluate Bezier surfaces. ***
> > [ANSWER HERE]
> 
> > Show a screenshot of bez/teapot.bez (not .dae) evaluated by your implementation... <br>
> > [IMG]
> 
## ══✿══╡°˖✧✿✧˖°╞══✿══ SECTION 2 ══✿══╡°˖✧✿✧˖°╞══✿══	
### PART 3
> *** Briefly explain how you implemented the area-weighted vertex normals. *** <br>
> > [ANSWER HERE]
> 
> > Show screenshots of dae/teapot.dae (not .bez) comparing teapot shading with and without vertex normals. Use Q to toggle default flat shading and Phong shading.. <br>
> > [IMG]
> 
### PART 4
> *** Briefly explain how you implemented the edge flip operation and describe any interesting implementation / debugging tricks you have used. ***
> > [ANSWER HERE]
> 
> > Show screenshots of a mesh before and after some edge flips...
> > <br> [IMG]
> 
> ** Write about your eventful debugging journey, if you have experienced one. <br>
> > [ANSWER HERE]
>
### PART 5
> *** Briefly explain how you implemented the edge split operation and describe any interesting implementation / debugging tricks you have used. ***
> > [ANSWER HERE]
>
> > Show screenshots of a mesh before and after some edge splits. <br>
> > [IMG]
> > <br> Show screenshots of a mesh before and after a combination of both edge splits and edge flips. <br>
> > [IMG]
> 
> ** Write about your eventful debugging journey, if you have experienced one. <br.
> > [ANSWER HERE]
> 
> ** If you have implemented support for boundary edges, show screenshots of your implementation properly handling split operations on boundary edges. <br>
> > [ANSWER HERE]
> 
### PART 6
> *** Briefly explain how you implemented the loop subdivision and describe any interesting implementation / debugging tricks you have used. ***
> > [ANSWER HERE]
> 
> ** Take some notes, as well as some screenshots, of your observations on how meshes behave after loop subdivision:
> > What happens to sharp corners and edges? Can you reduce this effect by pre-splitting some edges?
> > [IMG]
>
> ** Load dae/cube.dae. Perform several iterations of loop subdivision on the cube. Notice that the cube becomes slightly asymmetric after repeated subdivisions:
> > Can you pre-process the cube with edge flips and splits so that the cube subdivides symmetrically? Document these effects and explain why they occur. <br>
> > [ANSWER HERE] <br>
> > Also explain how your pre-processing helps alleviate the effects. <br>
> > [ANSWER HERE] <br>
> 
> If you have implemented any extra credit extensions, explain what you did and document how they work with screenshots.
> > no attempt. 


<br> You can view the spec for this project at [Assignment 2: MeshEdit](https://cs184.eecs.berkeley.edu/sp24/docs/hw2-spec).
