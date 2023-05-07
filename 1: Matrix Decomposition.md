# Mathematics for Computer Science
# Linear Algebra (Part 2)

## LU decomposition: Definition

> Definition
> An LU decomposition (or LU factorisation) of a square matrix A is a (product) representation A = LU where L is lower triangular and U is upper triangular.

Example: one can check that: 

<img width="511" alt="image" src="https://user-images.githubusercontent.com/126205612/236697963-705ec813-dda1-472f-bd35-d0be942bda21.png">

## Why should you care?
1. Suppose you want to solve Ax = y for x, where x & y column vectors
2. How many operations?
3. Using Gaussian elimination, O(n3)
4. If you want to solve Ax1 = y1 . . . Axk = yk for x1 to xk ?
5 .O(kn3)
6. But using LU decomposition? O(n3 + kn2)
(O(n3) to decompose into LU form, O(n2) to use LU to solve one system of equations)
7. Useful when k = ω(1)

Assume that we know an LU-decomposition A = LU.
Consider the following algorithm for solving the linear system Ax = b:
1. re-write Ax = b as LUx = b,
2. denote Ux = y and substitute it in LUx = b to obtain Ly = b,
3. solve the triangular linear system Ly = b for y,
4. now we know y and solve the triangular linear system Ux = y for x

Example:

Solve the following linear system Ax = b.

<img width="310" alt="image" src="https://user-images.githubusercontent.com/126205612/236698054-3c7a41e5-b5db-41d9-9a92-c5250cd16a12.png">

First get its LU decomposition. We know an LU decomposition for A:

<img width="516" alt="image" src="https://user-images.githubusercontent.com/126205612/236698077-b25f192c-9bc9-4578-ba8f-43cf5bc1835e.png">

Step 1: Rewrite the system as: 

<img width="407" alt="image" src="https://user-images.githubusercontent.com/126205612/236698093-bb62b2ad-4ed9-4c64-ac2d-06c58f4f7a2e.png">

<img width="542" alt="image" src="https://user-images.githubusercontent.com/126205612/236698124-ebcb2130-4770-47b5-836e-70319cb274a3.png">


Step 2. Denote Ux = y and substitute into the above equation to get: 

<img width="311" alt="image" src="https://user-images.githubusercontent.com/126205612/236698162-f730ccb9-f52e-4b14-af93-8e7c6bae20f7.png">

In equations, this is: 

<img width="246" alt="image" src="https://user-images.githubusercontent.com/126205612/236698171-6a625f87-0dc5-470c-9dbb-990a4d804bf2.png">


Step 3: Solve the above (lower triangular) system by *forward substitution*:
Find y1 = 1 from the 1st equation.
Substitute y1 into the 2nd equation and find y2 = 5.
Substitute both y1 and y2 into the 3rd equation and find y3 = 2.

Step 4: Now we know y, solve the linear system Ux = y:

<img width="291" alt="image" src="https://user-images.githubusercontent.com/126205612/236698245-1e213310-990f-42ca-838e-a011566bcf96.png">

In equations, this is:

<img width="194" alt="image" src="https://user-images.githubusercontent.com/126205612/236698260-38b92354-96b6-49db-82d3-2bfc19c92af7.png">

This is an upper triangular system, can solve it by backward substitution:
Find x3 = 2 from the 3rd equation, then substitute it into the 2nd equation and find x2 = −1,
then substitute both values into the 1st equation and find x1 = 2.

## Recap & Next Step: 

**U method**: Reduce solving a linear system to solving two triangular systems.
Use: When repeatedly solving a number of equations with same left-hand side.
Ax1 = b1
Ax2 = b2
Ax3 = b3
Next step: How do we find the LU decomposition of a matrix?
But before that: Can every matrix A be decomposed into LU?

## Sufficient condition for existence
Let A be a square matrix and let U be its (non-reduced) row echelon form, obtained by Gaussian elimination. Note that U is always upper triangular.

## Theorem
> If A and U are as above and no row exchanges were performed while obtaining U from A, then
> A can be factored A = LU, where L is lower triangular.

We exchange rows while computing U only when we get 0 in a pivot position.
The condition “no row exchanges” means that we never get this situation.

## How to find it

### Elementary matrix: 
matrix different from identity matrix by 1 elementary row operation
1. Row switching
2. Row multiplication
3. Row addition
### LU decomposition process:
1. Keep track of row operations used to compute U by Gaussian elimination
2. Let E<sub>1</sub>, . . . , E<sub>k</sub> be the corresponding elementary matrices (E<sub>1</sub> corresponding to the first row operation and  E<sub>k</sub> to the last)
3. Then the inverse (elementary) matrices E<sub>1</sub><sup>-1</sup> , . . . , E<sub>k</sub><sup>-1</sup> are easy to find
4. Compute E<sub>1</sub><sup>-1</sup> , . . . , E<sub>k</sub><sup>-1</sup> e.g., by applying the corresponding row operations (starting from E<sub>k</sub><sup>-1</sup>) to the identity matrix *I*.

### Example:

<img width="550" alt="image" src="https://user-images.githubusercontent.com/126205612/236698826-1fb9df25-0271-47ae-8cf8-2cbf10cab1ba.png">

### Observation: 
Entries in L can in fact be computed in parallel to computing *U* – in the same order as we create 1s and 0s in *U*. (This is a general rule.)

<img width="508" alt="image" src="https://user-images.githubusercontent.com/126205612/236698871-fd09a793-513f-4b53-b8c5-1a2b0790b9ae.png">
