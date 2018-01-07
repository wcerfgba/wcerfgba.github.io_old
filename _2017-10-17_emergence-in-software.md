---
title: "Emergence in software"
---

Recently, I have come to think that one way in which software can be difficult 
is in a lack of emergence, usually at the user interface level. I am defining 
emergence as the existence of structures/behaviours/patterns at one level, 
caused by the interactions or natural dynamics of patterns at another level. 
For example, there are many macro scale patterns present in snowflakes, all 
exhibiting spectacular variety of form while maintaining six-fold symmetry, 
caused by the strict hexagonal bonding at the molecular level of the water 
molecules.

PIC

In the context of software, the analogy can be applied to user interface or 
HCI. Often when developing software, we aim to define all of the user flows in 
code, so as to accurately model a domain problem and solution. One example is 
the recent work we have done at Residently, where we are allowing residents to 
set up future rent payments using Direct Debit. To build this we have had to 
consider UX, develop a UI, code up the view, the data model, and specify the 
valid states for the system.

This user flow approach usually requires a large chunk of effort in order to 
deliver a feature, like carving a path out of stone: over a matter of days we 
build a stable, smooth channel to direct the flow. This is the standard way 
'product software' is built, and with the continuing development of software 
engieering practices from agile onwards, this method seems to be working quite 
well for building products.

However, software built like this often lacks emergence in a number of ways. 
First, the UI is built to have a finite number of elements: static elements 
like text, and minutely dynamic elements like buttons and text fields which 
permit a very restricted set of interactions. This is not a problem when we are 
focusing on forms, because we want the user to be able to efficiently and 
comfortably enter data, and there are only a limited number of interactions 
that are required to do that well.

Compare this to the original paper form. Paper posesses inherent emergence 
because it is tangible: it can be torn, folded, crumpled. A pen is not terribly 
emergent, but combined with paper we can write and draw. Because paper has 
physical properties and exists within a space governed by physical laws, its 
state can be transformed to any valid configuration under those laws. If we 
wished to, we could implement a 'folding mode' for a web page, or provide for 
the user to scribble over the page with the cursor, or drag the fields around, 
but these behaviours are not 'emergent' in the sense that I mean because they 
have to be manually specified or enabled. In contrast, we do not have to make 
paper that can be folded, because paper is thin and flexible, and made from a 
mesh of fibers which can be individually broken with a moderate amount of 
force. [references] You could say that we get folding 'for free', which is 
exactly what some systems like [Naked 
Objects](http://wiki.c2.com/?TheNakedObjectsFramework) intend to provide direct 
manipulation of domain objects for free by generating the UI directly from the 
definitions of domain objects. I find this very cool, but it has obvious 
limitations and problems, one in particular being that often software is 
'deep', and a feature can cut vertically through many layers of different 
technologies; it is not necessarily possible to derive all necessary detail of 
the system from the domain objects, nor is it necessarily easy to customise at 
the generated or driven levels.

Games often make good examples of software that has good capacity for 
emergence, because they are usually engineered around a system of entities and 
contraints. Consider a 3D game like Tabletop Simulator, which allows you to 
flip the table. The flipping had to be coded in in order to place the action in 
the menu, and to specify the force that should be applied to the table when the 
action is triggered, but the resulting momenta of the table and the object on 
it is derived by simulating a physical system.

In the case of physical simulation, we have a good deal of capacity for 
emergence in the 'UI' -- if we consider the UI to be the camera and scene, and 
any movable objects in the scene (including the camera) -- but all of these 
laws still had to be manually programmed into the simulation: if the laws of 
electromagnetic theory were not included, then there would be no 
electromagnetic effects for the user or objects to exhibit. This indicates that 
emergence is not a property of UI or UX alone, but also a property of the code 
itself.

[what does emergence mean in code?]

[is emergence the right word for all this?]

One area with high emergence in both UX and code is in artistic coding. The 
text editor is a canvas and the code is as much a part of the art as the 
audio/video produced by it. Additionally, it is usually the case that the art 
will come about by experimentation, and there is a very tight feedback loop 
during development. Often there will be algorithms with tunable parameters 
which can be changed in real-time by the programmer to create the work.
