- polyextrude
	extrudes really
- delete 
	has delete by normal facing direction. Help for procedurals.
- divide 
	subdivides but boxy ig
- facet
	unique points
- add
	deletes geo but keeps points
- group
	has lots of grouping methods, includes edge grouping
- polybevel
- facet
	compute new normals
- fuse
	fuses the points
- join
	joins the points
- mirror
- clip
	deletes a section of the geo
- revolve
	revolves a bunch of copies of the geo
- copy to points
- vop attribute
	- mix
	- ramp
	- sine and cosine
	- int to float
	- float to vec and vec to float
	- fit range
- copy and transform
- merge 
- attribute create
- grouprange (select n points from a total of m points)
- attribute wrangle (all vex glory)

## vex
```vex
// to create a variable
dataType@variable_name = value;

i@colorData = 0;
f@scalarData = 0.234;
v@positionData = set(1,2,3);

f@sine = sin(@ptnum);
//gives the total number of points
i@len = npoints(0);
```

## attributes
### pscale
drives the scale value for each point
### PT
generates each points number
### rand(end_value)
generates a random value

### fit01(max,min,fit_range)
fits the given min to max value in the given range.
### stamp("from_where_to_copy_from","which_var_to_copy",default_value)
copies a variable from another node to here.



