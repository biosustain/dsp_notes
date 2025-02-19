# Documentation using Sphinx, MyST-NB

Like this notes website, we can create a documentation website using Sphinx and MyST-NB
using our template [here](https://github.com/biosustain/notes_template), including
the instructions on how to set it up.

Below you can find some additional hints.


## Setting explicit targets (cross-references on a website)

In order to reference other contents in a Sphinx built website using markdown, you can 
set explicit targets. This is explained 
[here](https://docs.readthedocs.com/platform/stable/guides/cross-referencing-with-sphinx.html#explicit-targets).

In short:

```markdown
(My_target)=
# Explicit target heading

Reference [link-to-target](My_target).
```


