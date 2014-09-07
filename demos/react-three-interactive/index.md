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
create and manipulate 3D scenes which are managed and drawn by three.js.

Using this library you can use three.js objects using React in the same way you would
use DOM elements in vanilla React. For example, here is the render method from the
"ClickableCube" component which shows up in the scene as a cube that responds to clicks:

{% highlight javascript %}
    render: function() {
        var boxmaterial = lookupmaterial(this.props.materialname);
        var cubeprops = _.clone(this.props);
        cubeprops.geometry = boxgeometry;
        cubeprops.material = boxmaterial;
        return ReactTHREE.Mesh(cubeprops);
    }
{% endhighlight %}

Note in this case that the geometry and material(s) are generated elsewhere, not in line.
The react-three library won't do automatic management of these resources for you, just as
three.js doens't prescribe a certain way to load and cache resources.

You can look in the
[interactive example code directory](https://github.com/Izzimach/react-three/tree/master/examples/interactive)
for more information.

<script src="scripts/lodash.min.js"></script>
<script src="scripts/three.js"></script>
<script src="scripts/react-three.js"></script>
<script src="scripts/interactive.js"></script>
<div id="three-box"/>
<script>
window.onload = interactiveexamplestart;
</script>


