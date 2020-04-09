

```python
t,x = var('t,x')
f(t,x)=x-t
plot_slope_field(f, (t, -2, 2), (x, -2, 2), headaxislength=3, headlength=3, axes_labels=['$t$','$x(t)$'])
```




![png](output_0_0.png)




```python
t,x = var('t,x')
p = desolve_rk4(x - t, x, ics = [0,0.5], ivar = t, output = 'slope_field', end_points = [0, 3], thickness = 2, color = 'blue')
p
```




![png](output_1_0.png)




```python
x, y, t = var('x y t')
F = [x*(5-x+y/2), y*(1-y+x)]
P = desolve_system_rk4(F,[x, y],ics=[0,1,.5],ivar=t,end_points=10,step=0.01)
Q = [ [j,k] for i,j,k in P]
p = line(Q, axes_labels=['$x(t)$','$y(t)$'], thickness=2)
n = sqrt(F[0]^2 + F[1]^2)
F_unit = [F[0]/n, F[1]/n]
p += plot_vector_field(F_unit, (x,-4,20), (y,-4,20), axes_labels=['$x(t)$','$y(t)$'], xmax = 20, xmin = -4, ymax = 20, ymin = -4, aspect_ratio=1)
p += implicit_plot(F[0], (x,-4,20), (y,-4,20), color="green")
p += implicit_plot(F[1], (x,-4,20), (y,-4,20), color="red")
p
```




![png](output_2_0.png)




```python

```
