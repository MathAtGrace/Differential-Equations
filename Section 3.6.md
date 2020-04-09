
# Activity 3.6.1

We use sage to solve this in three different ways.  My personal favorite is the third way.


```python
A = matrix([[1,-1],[-1,2]])
```

### Finding eigenvalues and eigenvectors numerically

Notice the small rounding errors


```python
u = A.eigenvalues()
T = A.eigenmatrix_right()[1]
show(u)


```


<html><script type="math/tex; mode=display">\newcommand{\Bold}[1]{\mathbf{#1}}\left[0.3819660112501051?, 2.618033988749895?\right]</script></html>



```python
show(T)
```


<html><script type="math/tex; mode=display">\newcommand{\Bold}[1]{\mathbf{#1}}\left(\begin{array}{rr}
1 & 1 \\
0.618033988749895? & -1.618033988749895?
\end{array}\right)</script></html>



```python
show(T^(-1)*A*T)
```


<html><script type="math/tex; mode=display">\newcommand{\Bold}[1]{\mathbf{#1}}\left(\begin{array}{rr}
0.3819660112501051? & 0.?e-18 \\
0.?e-18 & 2.618033988749895?
\end{array}\right)</script></html>


### Find eigenvalues and eigenvectors symbolically

Notice that Sage doesn't automatrically know that it should simplfy.  You need to tell is using `(your_matrix_here).simplify_full()`


```python
u1 = (3 + sqrt(5))/2
u2 = (3 - sqrt(5))/2
v1 = vector([1, (-1-sqrt(5))/2])
v2 = vector([1, (-1 + sqrt(5))/2])
```


```python
T = matrix([v1,v2]).transpose()
show(T)
```


<html><script type="math/tex; mode=display">\newcommand{\Bold}[1]{\mathbf{#1}}\left(\begin{array}{rr}
1 & 1 \\
-\frac{1}{2} \, \sqrt{5} - \frac{1}{2} & \frac{1}{2} \, \sqrt{5} - \frac{1}{2}
\end{array}\right)</script></html>



```python
show(T.inverse()*A*T)
```


<html><script type="math/tex; mode=display">\newcommand{\Bold}[1]{\mathbf{#1}}\left(\begin{array}{rr}
-\frac{1}{20} \, {\left(\sqrt{5} {\left(\sqrt{5} + 1\right)} - 4 \, \sqrt{5} - 10\right)} {\left(\sqrt{5} + 1\right)} - \frac{1}{10} \, \sqrt{5} {\left(\sqrt{5} + 1\right)} + \frac{1}{5} \, \sqrt{5} + 1 & \frac{1}{20} \, {\left(\sqrt{5} {\left(\sqrt{5} + 1\right)} - 4 \, \sqrt{5} - 10\right)} {\left(\sqrt{5} - 1\right)} - \frac{1}{10} \, \sqrt{5} {\left(\sqrt{5} + 1\right)} + \frac{1}{5} \, \sqrt{5} + 1 \\
\frac{1}{20} \, {\left(\sqrt{5} {\left(\sqrt{5} + 1\right)} - 4 \, \sqrt{5}\right)} {\left(\sqrt{5} + 1\right)} + \frac{1}{10} \, \sqrt{5} {\left(\sqrt{5} + 1\right)} - \frac{1}{5} \, \sqrt{5} & -\frac{1}{20} \, {\left(\sqrt{5} {\left(\sqrt{5} + 1\right)} - 4 \, \sqrt{5}\right)} {\left(\sqrt{5} - 1\right)} + \frac{1}{10} \, \sqrt{5} {\left(\sqrt{5} + 1\right)} - \frac{1}{5} \, \sqrt{5}
\end{array}\right)</script></html>



```python
show((T.inverse()*A*T).simplify_full())
```


<html><script type="math/tex; mode=display">\newcommand{\Bold}[1]{\mathbf{#1}}\left(\begin{array}{rr}
\frac{1}{2} \, \sqrt{5} + \frac{3}{2} & 0 \\
0 & -\frac{1}{2} \, \sqrt{5} + \frac{3}{2}
\end{array}\right)</script></html>


### Finding eigenvalues and eigenvectors using field extensions

I cannot fully explain this without going into material from Abstract Algebra, but when you do it this way Sage always simplifies.


```python
#We'll use 'sqrt5' as the name of our special number, and 'F' will be the rational numbers plus powers of sqrt5.
#We define sqrt5 to be one of the solutions of 'x^2 - 5 = 0'
F.<sqrt5> = QQ.extension(x^2 - 5)
```


```python
u1 = (3 + sqrt5)/2
u2 = (3 - sqrt5)/2
v1 = vector([1, (-1-sqrt5)/2])
v2 = vector([1, (-1+sqrt5)/2])
```


```python
T = matrix([v1,v2]).transpose()
```


```python
show(T)
```


<html><script type="math/tex; mode=display">\newcommand{\Bold}[1]{\mathbf{#1}}\left(\begin{array}{rr}
1 & 1 \\
-\frac{1}{2} \mathit{sqrt}_{5} - \frac{1}{2} & \frac{1}{2} \mathit{sqrt}_{5} - \frac{1}{2}
\end{array}\right)</script></html>



```python
T.det()
```




    sqrt5




```python
show(T.inverse())
```


<html><script type="math/tex; mode=display">\newcommand{\Bold}[1]{\mathbf{#1}}\left(\begin{array}{rr}
-\frac{1}{10} \mathit{sqrt}_{5} + \frac{1}{2} & -\frac{1}{5} \mathit{sqrt}_{5} \\
\frac{1}{10} \mathit{sqrt}_{5} + \frac{1}{2} & \frac{1}{5} \mathit{sqrt}_{5}
\end{array}\right)</script></html>



```python
#An intermediate step to help me check my work.
show(T.inverse()*A)
```


<html><script type="math/tex; mode=display">\newcommand{\Bold}[1]{\mathbf{#1}}\left(\begin{array}{rr}
\frac{1}{10} \mathit{sqrt}_{5} + \frac{1}{2} & -\frac{3}{10} \mathit{sqrt}_{5} - \frac{1}{2} \\
-\frac{1}{10} \mathit{sqrt}_{5} + \frac{1}{2} & \frac{3}{10} \mathit{sqrt}_{5} - \frac{1}{2}
\end{array}\right)</script></html>



```python
show(T.inverse() * A * T)
```


<html><script type="math/tex; mode=display">\newcommand{\Bold}[1]{\mathbf{#1}}\left(\begin{array}{rr}
\frac{1}{2} \mathit{sqrt}_{5} + \frac{3}{2} & 0 \\
0 & -\frac{1}{2} \mathit{sqrt}_{5} + \frac{3}{2}
\end{array}\right)</script></html>



```python

```
