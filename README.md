# d3-labs
d3 lab code 

## Demonstration

<centre>Lab 4</centre>

![Lab 4](https://github.com/OopsRyan/d3-labs/blob/master/themes/lab4_demo.jpg?raw=true)

<centre>Lab 5</centre>
### Transitions

![Lab 5](https://github.com/OopsRyan/d3-labs/blob/master/themes/lab5_population_transition.gif?raw=true)
---
![Lab 5](https://github.com/OopsRyan/d3-labs/blob/master/themes/lab5_points_transition.gif?raw=true)
---
![Lab 5](https://github.com/OopsRyan/d3-labs/blob/master/themes/lab5_scale_transition.gif?raw=true)


#### Scale !!!
when the objects on the axis are continuous values, you should use ScaleLinear()
when the objects on the axis are bars, you should use ScaleBand()
when the objects on the axis are time, you should use ScaleTime()
If you use the wrong Scale function to initialize your scale, the tick will be a mass. ~~~~~~~

#### change axis values dynamically
If we want one axis to animate, we can change its scale domain in the callback function.

#### what transition really means
When joining data with elements, the invoking order of transition() is really important.
For example, in the code below, after enter(), the elements will be created first, and then appear from the yScale value to the axis. If transition() is called immediately after enter(), the elements will show from the up left corner to the axis. Anyway, I think invoking transition after assigning the ordinates looks better.

	/******** HANDLE ENTER SELECTION ************/
	// Create new elements in the dataset
	bars.enter()
            .append("rect")
            .attr("x", function(d, i) {
               return xScale(d.Company);
            })
            .attr("y", function(d) {
               return yScale(+d.Share) ;
            })
            .style("fill", "Blue")
            .transition()
            .duration(500)
            .attr("width", xScale.bandwidth())
            .attr("height", function(d) {
               return svg_height - yScale(+d.Share);
            });

Moreover, when the transition is completed, we can use transition() to display the disapperation of elements, so we set their height value as 0, which means a display of the element declining to 0.

	/******** HANDLE EXIT SELECTION ************/
	// Remove bars that not longer have a matching data eleement
	bars.exit()
	    .transition()
	    .duration(500)
	    .ease(d3.easeBounce)
	    .style("fill", "red")
	    .attr("y", svg_height)
	    .attr("height", 0)
	    .remove();
