
# Derivative rules lab

In this lab, we will practice our knowledge of rules that we can apply to derivatives.  This lab will review your understanding of the following:

1. The power rule
2. The constant factor rule
3. The addition rule

As you know we can represent polynomial functions as a list of tuples.  For example, we've represented the $f(x)=2x^3+7x$ in Python as `[(2, 3), (7, 1)]`.  Each term is represented as a single tuple, for example, `(2, 3)`.

Let's start with writing a function called `find_derivative_term` that returns a derivative of a single term.  The function takes the derivative of one term represented as a tuple: $(1, 3)$, and returns it's derivative, also represented as a tuple.  For example, if the derivative $f'(x) = 2x^3$, then the function `find_derivative_terms` should return `(2, 3)`.


```python
one_x_cubed = (1, 3)
```


```python
def find_term_derivative(term):
    pass
```


```python
find_term_derivative(one_x_cubed) # (3, 2)
two_x_squared = (2, 2)
find_term_derivative(two_x_squared) # (4, 1)
```

Ok, now that we have a Python function called `find_derivative` that can take a derivative of a term, write a function that take as an argument our multitermed function, and return the derivative of the multiterm function represented as a list of tuples.  


```python
def find_derivative(function_terms):
    pass
```


```python
first_terms = [(4, 3), (-3, 1)]
find_derivative(first_terms)
```

One gotcha to note is that when a term is raised to the zero power, it means it is just a number like 12, and taking the derivative of a constant should give us a term of zero, and therefore can be removed.


```python
second_terms = [(3, 2), (-11, 0)]
find_derivative(second_terms) # [(6, 1)]
```

Our next function is called, `derivative_at`, which when provided a list of terms, and a value $x$ at which to evaluate the derivative returns the value of derivative at that point.


```python
def derivative_at(terms, x):
    pass
```


```python
# second_terms = [(3, 2), (-11, 0)]
find_derivative(second_terms) # [(6, 1)]
derivative_at(second_terms, 2) # 12

find_derivative(first_terms) # [(12, 2), (-3, 0)]
derivative_at(first_terms, 1) # 9
```


```python
from graph import plot
from plotly.offline import iplot, init_notebook_mode
init_notebook_mode(connected=True)

def output_at(function_terms, x_value):
    total = 0
    for term in function_terms:
        total += term[0]*x_value**term[1]
    return total

def polynomial_function_trace(function_terms, x_values):
    y_values = list(map(lambda x: output_at(function_terms, x), x_values))
    return {'x': x_values, 'y': y_values}

def tangent_line(function_terms, x_value, line_length = 4):
    pass
```


<script>requirejs.config({paths: { 'plotly': ['https://cdn.plot.ly/plotly-latest.min']},});if(!window.Plotly) {{require(['plotly'],function(plotly) {window.Plotly=plotly;});}}</script>



```python
first_terms = [(4, 3), (-3, 1)]
tangent_line(first_terms, 8, line_length = 3)
# {'x': [5, 8, 11], 'y': [-271, 2024, 4319]}

second_terms = [(3, 2), (-11, 0)]
tangent_at_five_trace = tangent_line(second_terms, 5, line_length = 4) or {}
tangent_at_five_trace  # {'x': [1, 5, 9], 'y': [-56, 64, 184]}
```




    {}




```python
second_terms_trace = polynomial_function_trace(second_terms, list(range(-10, 10))) or {}
plot([second_terms_trace, tangent_at_five_trace])
```


<div id="dded19ef-55cb-47bc-ab44-350eae11fa08" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("dded19ef-55cb-47bc-ab44-350eae11fa08", [{"x": [-10, -9, -8, -7, -6, -5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9], "y": [289, 232, 181, 136, 97, 64, 37, 16, 1, -8, -11, -8, 1, 16, 37, 64, 97, 136, 181, 232]}, {}], {}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


We can also write a function that given a list of terms can plot the derivative across multiple values.  After all, the derivative is just a function.  For example, when $f(x) = 3x^2 - 11$, $f'(x) = 6x$.  

We know that we can plot multiterm functions with our `polynomial_function_trace`.  So write a function called `derivative_function_trace` that given a function representing $f(x)$ plots a function $f'(x)$.  


```python
def derivative_function_trace(terms, x_values):
    pass
```


```python
second_terms = [(3, 2), (-11, 0)]
second_terms_derivative_trace = derivative_function_trace(second_terms, list(range(-5, 5))) or {}
second_terms_derivative_trace
# {'x': [-5, -4, -3, -2, -1, 0, 1, 2, 3, 4],
#  'y': [-30, -24, -18, -12, -6, 0, 6, 12, 18, 24]}
```




    {}



Take a second to look at the side by side plots of the underlying function, $f(x) = 3x^2 - 11$ and $f'(x) = 6x $.


```python
from plotly import tools
import plotly
import plotly.plotly as py

def plot_side_by_side(left_trace, right_trace):
    fig = tools.make_subplots(rows=1, cols=2)
    fig.append_trace(left_trace, 1, 1)
    fig.append_trace(right_trace, 1, 2)
    plotly.offline.iplot(fig)
    
plot_side_by_side(second_terms_trace, second_terms_derivative_trace)
```

    This is the format of your plot grid:
    [ (1,1) x1,y1 ]  [ (1,2) x2,y2 ]
    



<div id="946f7f02-9e6d-4daf-be68-f9d82963801f" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("946f7f02-9e6d-4daf-be68-f9d82963801f", [{"type": "scatter", "x": [-10, -9, -8, -7, -6, -5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9], "y": [289, 232, 181, 136, 97, 64, 37, 16, 1, -8, -11, -8, 1, 16, 37, 64, 97, 136, 181, 232], "xaxis": "x1", "yaxis": "y1"}, {"type": "scatter", "xaxis": "x2", "yaxis": "y2"}], {"xaxis1": {"domain": [0.0, 0.45], "anchor": "y1"}, "yaxis1": {"domain": [0.0, 1.0], "anchor": "x1"}, "xaxis2": {"domain": [0.55, 1.0], "anchor": "y2"}, "yaxis2": {"domain": [0.0, 1.0], "anchor": "x2"}}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


Note that when the $x$ values of $f(x)$ are positive, the $f(x)$ begins increasing, therefore $f'(x)$ is greater than zero, which the graph on the right displays.  And the more positive the values $x$ for $f(x)$, the faster the rate of increase.  When our function $f(x)$ is negative, the function is decreasing, that is for every change in $x$, the change in $f(x)$ is negative, and therefore $f'(x)$ is negative.


```python

```
