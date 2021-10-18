# Diamonds Are Forever

<p align="center">
<img src="https://user-images.githubusercontent.com/80269251/137795482-74352769-e8d2-4173-bd8f-64b9612f92a4.png">
</p>

## 3D Diamond

The diamond was produced using two poligons with 17 equal sides, the top (the small polygon) and the middle part 
(the big polygon) of the diamond, and the point defining its bottom and then visualaizing it in the space. This 
was written in PostScript.

The resulting diamond is the most aesthetically pleasing:

<p align="center">
<img src="https://user-images.githubusercontent.com/80269251/137802304-1203179d-91e3-4dfd-a1ee-9a7ad24ab0c8.png">
</p>

This is another example of a diamond with polygins with 30 equal sizes. As one can see, it is not 
as attractive as the previous:

<p align="center">
<img src="https://user-images.githubusercontent.com/80269251/137803596-88642d88-f9fc-4a84-86bb-d84bd163c98f.png">
</p>

## Culling Hidden Polygons

The viewpoint is ajusted in such a way that the trapezes conecting both polygons are automatically culled when the top of the diamond is drawn. 

However the triangles at the bottom are culled by hand by enumerating only the visible triangles.
