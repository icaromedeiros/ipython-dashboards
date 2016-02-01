# Interactive Dashboards in iPython

The goal is to test some alternatives of tools to create dashboards in (i)Python.

This is by no means an extensive benchmark.
Note that even claims about some missing feature might be a consequence of lack of understanding or because I have only read the standard examples.

Requirements include:

- The same dashboard prototyped in Jupyter notebooks should be easily used in a "blank" environment, i.e. a Web page/system of its own
- The visualization tool must be easy to use
- The visualization tool must be easily integrated with Pandas
- The visualization engine on the client side must be able to get streaming data from a big data source without relevant performance loss

## TODO

- Check whether tools can be used in combination (e.g. bokeh for major tasks and d3 integrated with ipython when some low-level stuff is needed)
- Check https://plot.ly/python/dashboard/
- Fork dash (https://github.com/plotly/dash) and rewrite the API and examples to work with offline plots.

# What to use: ipywidgets, bokeh or d3?

Short answer: XXX.

## ipywidgets

### Pros

**iPython integration**

The tool is an official part of the iPython project.

However, widgets inside Jupyter notebook lack documentation and seem to be in a transition state where some features are unstable under the newest versions of Jupyter and data visualization libraries.

Another difficulty is that most examples are iPython notebooks on Github,
but interactive widgets are not rendered.

### Cons

**Documentation**

Confusing. http://ipywidgets.readthedocs.org/en/latest/ is rather empty.

On github there are some using ipython notebook examples, but the interaction is not rendered.
That sucks. I have not found any API reference either.

**Using oustide Jupyter Notebook**

Not tested. Might be difficult.

Also, as stated in https://jakevdp.github.io/blog/2013/12/05/static-interactive-widgets/,
ipywidgets "save the generated frames within divs that are hidden and shown whenever the widget is changed". Maybe this is not true as for now (the post is from 2013).

However, I haven't found any evidence that ipywidgets scales to streaming data and million data points. To create "live" dashboards, this can be a challenge.
I've encountered many examples with slow rendering.

**Open Source Community**

Although iPython is a dynamic project, ipywidgets does not seem to hold the same interest.

## bokeh

### Pros

**Open Source community**

The project seems to be in active development.
3.6k stars, 730 forks, 668 open issues, 1519 closed (as of 24-01-2016).

Moreover, as a Continuum Analytics project,
I think the open source community is more welcome than in plotly.
Continuum states on their page their commitment to open source.

It also seems there's is a clear goal that projects can be easily integrated with other PyData components such as Jupyter, Anaconda, Pandas, etc.

**Easiness of use**

Bokeh glyphs are better than the "all in one" dictionary of Plotly,
although plotly dictionary is good for overall API consistency between languages.

The advantage of glyphs is that one line represent one item on the graph.

The code is more legible this way:
adding one line can be written as

```
p.line(x, y0, legend="y=x^2", line_width=3)

```

This will include a new line on the graph.
It is clearer and cleaner than to update a dictionary as in plotly.

**Integration with Pandas**

The high level `charts` module seems to work nicely with Pandas dataframes but it is not the standard example.
It makes me think if integration with Pandas is a priority within the project.

I hope that `charts` module is as flexible as the `plotting` library,
maybe I need to dive into this module more.

### Cons

**Integration with JS**

Bad. Writing JS in a Python string is test-unfriendly and simply ugly.
http://bokeh.pydata.org/en/latest/docs/user_guide/interaction.html?#customjs-for-selections

This is bad for flexibility on the Web client side.

**Code quality**

I was amazed that such a big project does not follow PEP8.
Also, I was surprised that ``plotting.Line`` is a function, rather than a class.
It smells bad.

## d3

**Integration with streams of data**

TODO.

### Pros

**Integration with JS**

Total low-level integration.

### Cons

**Need to write JS**

As a low level library, using "pure" d3 demand to write lots of JS.

## Plotly

### Pros

**Easiness of use**

The API is easy and creates beautiful visualizations.
The API is also very flexible, with a large number of possible configurations.
See https://plot.ly/python/reference/.

**Integration with JS**

TODO.

### Cons

**Documentation**

Even after the open sourcing process some examples are focused on online plots or tools that seem to be descontinued such as cufflinks.

# Sources

- http://blog.ibmjstart.net/2015/08/21/declarative-widget-system-for-jupyter-notebooks/
- https://jakevdp.github.io/blog/2013/12/05/static-interactive-widgets/
- http://blog.dominodatalab.com/interactive-dashboards-in-jupyter/
- https://groups.google.com/a/continuum.io/forum/#!topic/bokeh/xaGsrSc0nW4
- https://www.reddit.com/r/datascience/comments/2yatjn/d3js_and_bokeh_anyone_with_experience_explain_the/
- http://stackoverflow.com/questions/19453430/examples-of-interactive-plots-through-python
- https://www.continuum.io/content/painless-streaming-plots-bokeh
- https://plot.ly/javascript/open-source-announcement/
- https://plot.ly/4/~streaming-demos/
- https://plot.ly/python/matplotlib-to-plotly-tutorial/
