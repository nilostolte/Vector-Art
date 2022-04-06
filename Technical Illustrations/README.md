# Octree

Vector graphics really excells in technical illustrations. Below the correspondence between the octree data structure and its representation in space is shown. The space is recursively subdivided in eight equal sized regions called octants. The octants are contiguously stored in arrays with eight positions as shown. If the octant is not empty it points to another array of eight positions and so forth until the last level is reached. Here the coordinates of the voxel nearer to the observer in a space with resolution 32³ are placed in a table to show how their bits are grouped to form an index in the array at each of its five levels. In this way one can convert indexes to coordinates and vice-versa.

<p align="center">
<img src="octree-struct.svg" style="width:90%; height: 90%;">
</p>


