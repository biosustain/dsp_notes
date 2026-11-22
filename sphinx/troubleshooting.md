# Troubleshooting

As we use mystnb as an addon, I will also put examples both for rst and markdown
syntax here.

## Adhere to strict heading hiearchy

- only have one main heading
- title in sidebar can be renamed using crosslinks: `my title <path/to/file>`

## Include markdown in non-subfolder (e.g. README of root folder)

In order to import a markdown file from anywhere, you can include it into another local file.
For example, being in the `docs` folder, you can include the README from the main folder using

```rst
.. include:: ../README.md
   :parser: myst_parser.sphinx_
   :start-line: 0
```

or in markdown (which offers some additional features):

````markdown
```{include} ../README.md
:parser: myst_parser.sphinx_
:start-line: 0
:relative-docs: docs
:relative-images:
```
````


If you save the above in a file `other/project_readme.rst`, you can include it the main `index.rst`
using

```rst
.. toctree::
   :maxdepth: 1
   :caption: Other Readmes

   other/project_readme
```

and in markdown

````markdown
```{toctree}
:caption: Other Readmes
:maxdepth: 1

other/project_readme
```
````

Have a look at the 
[`index.md`](https://github.com/biosustain/dsp_notes/blob/HEAD/index.md)
of this website for an example.
