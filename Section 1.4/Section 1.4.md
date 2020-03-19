

```python
x_min = 0
x_max = 1
h = 0.2
num = (x_max-x_min)/h
x_vals = [RR(i)/num for i in range(num+1)]
Y_vals = [1]
for x_i in x_vals:
    Y_prime = x_i + x_i*Y_vals[-1]
    Y_vals.append(Y_vals[-1] + h*Y_prime)
zip(x_vals, Y_vals)
```




    [(0.000000000000000, 1),
     (0.200000000000000, 1.00000000000000),
     (0.400000000000000, 1.08000000000000),
     (0.600000000000000, 1.24640000000000),
     (0.800000000000000, 1.51596800000000),
     (1.00000000000000, 1.91852288000000)]




```python
x, y = var('x, y')
f(x, y) = x + x*y
p = plot_slope_field(f, (x,-1,2), (y,0,3), headaxislength=3, headlength=3, axes_labels=['$x$','$y(x)$'], fontsize=12)
p += desolve_rk4(f, y, ics=[0,1], ivar=x, output='plot', end_points=[0,1], thickness=2)
p += list_plot(zip(x_vals, Y_vals), plotjoined=True, color='purple', thickness=2)
p += points(zip(x_vals, Y_vals), color = 'red', size = 20)
p.show(xmin = -1, xmax = 2, ymin = 0, ymax = 3)  #set the size of the plot window
```


![png](output_1_0.png)



```python

```
