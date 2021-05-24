## Death Valley

![DeathValley](https://user-images.githubusercontent.com/80269251/110996994-c15f5100-834a-11eb-9acd-aad27660dc43.png)

This design started with a photo of the Death Valley

![death-valley photo org](https://user-images.githubusercontent.com/80269251/110987171-b271a200-833c-11eb-81c8-48d8d7766e6f.jpg)

Which was than transformed in black and white

![death-valley photo nb](https://user-images.githubusercontent.com/80269251/110987228-c917f900-833c-11eb-8644-38fc554122d8.jpg)

And then vectorized

![Death valley vectorized](https://user-images.githubusercontent.com/80269251/110987582-4c394f00-833d-11eb-9f3b-0b78fda83f36.png)

After the vectorization, the sun disappeared. This problem has been solved by generating a stylized sun with the brewery logo. 
This has been coded in PostScript as shown:

```PostScript
/sol { 140 175 } def
<<
	/r1 60
	/vect { % x0 y0 x1 y1
		3 -1 roll sub 3 1 roll 
		exch sub exch
	}
	/vadd { % x0 y0 x1 y1
		3 -1 roll add 3 1 roll
		add exch
	}
	/ia 40 def
	/m1 ia 2 div cos 62 .5 mul mul
	/fin 360 ia sub def
>>
begin
gsave
0 0 .8 0 setcmykcolor
/ang 0 def

newpath
sol exch r1 add exch moveto
{
	/ang ang ia add def
	{ r1 ang cos mul  r1 ang sin mul } dup
	exec
	sol currentpoint vect
	vadd m1 div exch m1 div exch sol vadd
	1 index 1 index 5 -1 roll exec sol vadd curveto
	ang fin gt { exit } if
} loop
fill
grestore
end
```
The basic algorithm behind this code is to operate with 2D vectors and angle incrementation. Initially, a library to operate 
with vectors appears between << and >> (which in PostScript diefines a _dictionary_, which works similarly to a class in any 
other programming language). It also contains some data to define the graphics, where

1. **r1** <br>
is the radius of limiting the size of the figure
2. **ia** <br>
It is the incremental angle. Since its value is 40, it indicates this figure will have 9 parts, which are the sun _"
spikes"_.
3. **m1** <br>
Is just a contant to decrease the langth of the bisector vector
4. **fin** <br>
fin = 360 - ia, the last part of the figure which actually ientifies the end of the loop
5. **sol** <br>
This is a global variable that stores the coordinates of the center of the figure.

Before starting the loop a variable **ang** is initialized with zero. This variable will contain the angle of each part of 
the figure. Also the **currentpoint** is set to the point with the same y coordinate as the central point (**sol**) and with 
a x coordinate displaced of **r1** towards the right. This is the initial point of the figure, which is the first point of the
first bezier curve of the figure.

The loop starts by incrementing **ang** by **ia**. It then determines the vector between the extreme point of the next part 
and the central point. This is done using the projections of the radius that has angle **ang** according to both coordinate 
axes as indicated. It is executed (**exec**) because it is defined as a function. A copy of the function is left in the stack.
The bisector vector between the current part and the next is calculated (by adding the vector between the currentpoint and 
the center and the vector calculated through the function), scaled down using the constant **m1** and added to the central point. 
The resulting point is then duplicated. These two points are the control points of the bezier curve that is being defined. Its final
point is the point obtained by adding the central point to the vector of the next part calculated using the function left in the 
stack. The bezier curve starting at the currentpoint is then drawn using **curveto**.

This loop continues until the last (9th) part has been drawn. In this case this _path_ is filled with a yellow color.




