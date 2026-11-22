# Using Read the Docs

## Visualizing Plotly Figures in ReadTheDocs

For plotly6 it is needed to set the renderer in ReadTheDocs to `notebook` in order 
to visualize the figures correctly, additionally to adding the required JavaScript 
libraries as before.
Plotly normally decides itself fine which renderer to use, so keep it to RTD see  
[plotly.com/python/renderers](https://plotly.com/python/renderers/#setting-the-default-renderer).
But using an environment variable it is possible to set a global default renderer
for all plotly figures

```python
# conf.py
import os

# List of JavaScript libraries to use on the built HTML pages
# needed for Plotly figures
html_js_files = [
    # older versions of Plotly used require.js, but now it is not needed
    # "https://cdnjs.cloudflare.com/ajax/libs/require.js/2.3.7/require.min.js",
    # https://plotly.com/javascript/getting-started/
    "https://cdn.plot.ly/plotly-3.0.1.min.js",
]


if os.environ.get("READTHEDOCS", None) == "True":
    # Set the default renderer to 'notebook' for ReadTheDocs
    os.environ["PLOTLY_RENDERER"] = "notebook"
```

This can be done in the `conf.py` file of the Sphinx documentation,
which is used on ReadTheDocs.
