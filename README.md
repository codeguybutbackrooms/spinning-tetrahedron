# Spinning Tetrahedron

This demo renders a spinning **tetrahedron** (a triangular pyramid) in pure ASCII. It uses only JavaScript with basic linear algebra, trigonometry, and a 2D character buffer, no graphics libraries.

## Tetrahedron

A **tetrahedron** has:

- **4 vertices**  
- **4 triangular faces**  
- **6 edges**


We position its vertices symmetrically about the origin:

```js
const vertices = [
  [ 1,  1,  1],   // A
  [-1, -1,  1],   // B
  [-1,  1, -1],   // C
  [ 1, -1, -1]    // D
];
```
Optionally, to rest the tetrahedron on one face rather than a corner, you can pre-tilt by rotating each vertex around the X-axis by $`\theta = \arccos(1/3) \approx 70.53^\circ`$

## Edges
There are 6 edges connecting each pair of vertices:

```js
const edges = [
  [0,1], [0,2], [0,3],
  [1,2], [1,3],
  [2,3]
];
```
Each [i,j] draws a line between vertices[i] and vertices[j].

## Rotation
The shape spins continuously around both the Y-axis and X-axis:
1. Y-axis rotation:

$`\begin{bmatrix}
\cos(\theta) & 0 & -\sin(\theta) \\
0 & 1 & 0 \\
\sin(\theta) & 0 & \cos(\theta)
\end{bmatrix}`$

```js
x1 = x*cosY - z*sinY;
z1 = x*sinY + z*cosY;
```
2. X-axis rotation (vertical tilt)
$`\begin{bmatrix}
1 & 0 & 0 \\
0 & \cos(\phi) & -\sin(\phi) \\
0 & \sin(\phi) & \cos(\phi)
\end{bmatrix}`$
```js
y1 = y*cosX - z1*sinX;
z2 = y*sinX + z1*cosX;
```
