# DSP Notes

## Instruction

- create a branch
- add your notes to a thematic folder.
- remember to update the `index.md` file to include new files

## Markdown references

You can write markdown. Add html to markdown files and it should be rendered normally,
e.g. to render a youtube video (which youtube provides as embedded html code).

- [on GitHub](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax) 
- [a cheatsheet](https://www.markdownguide.org/cheat-sheet/)
- [Markdown Guide](https://www.markdownguide.org/basic-syntax/) 

## Template reference

- find instructions how to create your own technical documentation site using a GitHub template
    at [biosustain/notes_template](https://github.com/biosustain/notes_template)

## Execute website locally

Described in README of template at [biosustain/notes_template](https://github.com/biosustain/notes_template)
but in short:

```bash
pip install -r requirements.txt # into a virtual environment?
sphinx-build -n -W --keep-going -b html ./ ./_build/ # or:
# python -m sphinx -n -W --keep-going -b html ./ ./_build/
```
