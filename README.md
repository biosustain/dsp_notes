# DSP Notes

## Instruction

- create a branch
- add your notes to a thematic folder.
- remember to update the `index.md` file to include new files

## Markdown reference

- [on GitHub](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax) 
- [a cheatsheet](https://www.markdownguide.org/cheat-sheet/)

## Template reference

- find instructions how to create your own technical documentation site using a GitHub template
    at [biosustain/notes_template](https://github.com/biosustain/notes_template)

Here we fetch some markdown files from other sources additionally to the documentation.
To build locally you need to run:

```bash
pip install -r requirements.txt
python fetch_files.py
python -m sphinx -n -W --keep-going -b html ./ ./_build/
```
