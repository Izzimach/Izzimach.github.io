---
layout: default
title: react-three Interactive Example
---

# The interactive example from react-three

This is the interactive example from
[react-three](https://github.com/Izzimach/react-three),
a javascript library built on top of
[React](https://github.com/https://github.com/facebook/react) and
[three.js](https://github.com/mrdoob/three.js).
This allows you to use the declarative component structure of React to
create and manipulate the 3D scene objects used by three.js.

Click on the cherry cube to add a lollipop cube at a random position
and orientation. Click on a lollipop cube to remove it.

<div id="three-box"></div>

Normally when using a scene-graph library such as three.js you can manually
manipulate a scene-graph to change what is drawn on the screen.  If you want an
additional object drawn in a 3D scene, you create a mesh object and add it to the
scene graph so that three.js will draw it the next time you call render().

Using this library you can manipulate three.js objects using React.
Instead of creating and destroying three.js objects manually, you manipulate
some sort of application state and use that to "drive" what exists in the scene graph,
and thus effect what gets drawn on the screen.

The application state for this example is simply a dictionary (set of key-value pairs). All of the
current removable cubes (the green lollipop cubes) are stored as an array of dictionaries.
The application state typically has no three.js objects in it, so (for example) you could
save the application state to disk or send it over the network via JSON and reconstruct
the 3D scene somewhere else.

~~~javascript
g_applicationstate = {
  borderpx:6,
  cubes:[{...cube 1 data...}, {...cube 2 data...},...],
  xsize:500,
  ysize:500,
  zsize:500
};
~~~

Next you use React to create components.  A component
defines a relationship between parts of the application state and
the three.js scene graph. For example, the relationship between an instance of cube data
and the three.js mesh is pretty simple. The component uses a predefined cube
geometry and looks up the (generated and cached) three.js material
to use based on a texture name stored in the cube data.

~~~~javascript
    render: function() {
        var boxmaterial = lookupmaterial(this.props.materialname);
        var cubeprops = _.clone(this.props);
        cubeprops.geometry = boxgeometry;
        cubeprops.material = boxmaterial;
        return ReactTHREE.Mesh(cubeprops);
    }
~~~~

Small low-level components are composed together into larger components. Eventually
you will reach the top-level component which typically represents the entire
"application" or in our case the canvas/scene used by three.js.

To change something in the scene, you don't manually manipulate the scene graph. Instead
you change the application state (perhaps adding or removing a single cube) and then
pass the new state to React, which will update the scene appropriately to reflect this
new application state:

~~~javascript
// if the application state is modified call this to update the GUI

function updateApp() {
  g_reactinstance.setProps(g_applicationstate);
}
~~~

Note that in this example the geometry and material(s) are generated elsewhere, not in line.
The react-three library won't do automatic management of these resources for you, just as
three.js doens't prescribe a certain way to load and cache resources.

You can look in the
[interactive example code directory](https://github.com/Izzimach/react-three/tree/master/examples/interactive)
for more information.

<script src="scripts/lodash.min.js"></script>
<script src="scripts/three.min.js"></script>
<script src="scripts/react-three.js"></script>
<script src="scripts/interactive.js"></script>
<script>
window.onload = interactiveexamplestart;
</script>
