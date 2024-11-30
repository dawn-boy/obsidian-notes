# Geometry Nodes!
## fields
Fundamentally, a field is a function, a set of instructions that can transform an arbitrary number of inputs into a single output. A field’s result can then be calculated many times with different input data.
### types
1. diamond with a dot
	![[Blender_1.png]]
	The socket can be a field, but it is currently a single value. So above example shows that each element is moved up in z axis by 5 meters.
2. diamond
	![[Blender_2.png]]
	The socket is a function and is currently accepting a variable input. In the example, the position of every element will be doubled as the offset of every point is the point's value.
	Also when a connection is formed between two sockets that support fields, the line gets dashed!
3. circle
	This socket cannot accept field values, only a single real value.
### Field Context
One common misunderstanding is that the same field node tree used in multiple places will output the same data. This is not necessarily true, because the field node tree will be evaluated for every data flow node, potentially retrieving data from a different or changed geometry.
![[Blender_3.png]]
Here, the [Set Position](https://docs.blender.org/manual/en/latest/modeling/geometry_nodes/geometry/write/set_position.html) node’s input field is evaluated once. To evaluate the field, the node traverses backwards to retrieve the inputs from the field input nodes.
![[Blender_4.png]]
When a second Set Position node is added, the same field node tree is evaluated twice, once for each data flow node. At the second Set Position node, the results will be different since its geometry input will already have the changed position from the first node.
![[Blender_5.png]]
However, often it’s necessary to use the same field values even after changing the geometry. The [Capture Attribute Node](https://docs.blender.org/manual/en/latest/modeling/geometry_nodes/attribute/capture_attribute.html) evaluates a field, copying the result to an [anonymous attribute](https://docs.blender.org/manual/en/latest/modeling/geometry_nodes/attributes_reference.html#anonymous-attributes) on the geometry.

Here, a Capture Attribute node stores a copy of the initial position. Notice that evaluating the field input of the Capture Attribute node is an entirely different step. Later on, the input fields to the Set Position nodes don’t use the actual position, but the anonymous attribute copy of it.
### Nested instancing
![[Blender_6.png]]
