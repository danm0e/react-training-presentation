## Architecture<!--.element: class="r-fit-text" -->
---
<!-- .slide: data-auto-animate="true" -->
<div class="container">
<div class="col" markdown="1">

![alt text](./assets/conway.png)

Melvin Conway<!-- .element: class="fragment" -->

</div>
<div class="col">
</div>
</div>
Note: Who's this?

Melvin Conway - Computer sceintist. Developer co-routines in 1958. Worked on Pascal. Taught in Massachusetes. 
---
<!-- .slide: data-auto-animate="true" -->
<div class="container">
<div class="col" markdown="1">

![alt text](./assets/conway.png)

Melvin Conway

</div>
<div class="col" markdown="1">

### Conway's Law

_Any organization that designs a system (defined broadly) will produce a design whose structure is a copy of the organization's communication structure._

</div>
</div>
---
<!-- .slide: data-auto-animate="true" -->
<div class="container">
<div class="col" markdown="1">

![alt text](./assets/conway.png)

Melvin Conway

</div>
<div class="col" markdown="1">

### Conway's Law

 (Paraphrased)

_The structure of the software will mirror the structure of the organization that built it_

</div>
</div>

Note: If you have lots of small teams that are distibuted you will create a small distirbuted microarchitecture
If you have on large team you will create one large monolithic architecture
Conway understood that software coupling is enabled and encouraged by human communication
If an architecture is designed at odds with the development organization's structure, then tensions appear in the software structure. Module interactions that were designed to be straightforward become complicated, because the teams responsible for them don't work together well. Beneficial design alternatives aren't even considered because the necessary development groups aren't talking to each other.

Teams organized by software layer (eg front-end, back-end, and database) lead to dominant PresentationDomainDataLayering structures, which is problematic because each feature needs close collaboration between the layers.
Similarly dividing people along the lines of life-cycle activity (analysis, design, coding, testing) means lots of hand-offs to get a feature from idea to production.
Createing a team that will soully be responsible for all components will create a consistant design across the organisation, but could require longer lead times on innovative UI approaches
---
### Choices
- Ignore<!-- .element: class="fragment" -->
- Accept<!-- .element: class="fragment" -->
- Inverse Conway Maneuver<!-- .element: class="fragment" -->
---
## Inverse Conway Maneuver
- Understand the desired architecture<!-- .element: class="fragment" -->
- Identify the key boundaries<!-- .element: class="fragment" -->
- Align team responsibilities<!-- .element: class="fragment" -->
- Minimize dependancies<!-- .element: class="fragment" -->
- Sense & Respond<!-- .element: class="fragment" -->
Note: The term “inverse Conway maneuver” was coined by Jonny LeRoy and Matt Simons in an article published in the December 2010 issue of the Cutter IT journal.

