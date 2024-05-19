Install Instructions:

Start on the `ifml_template` folder and run the following:


Step 1. Create and activate a conda environment.

Step 2. Install Sphinx.

```bash
conda install sphinx
```

Step 3. Install the html theme.

```bash
pip install insipid-sphinx-theme
```

Step 4. Modify the content in `./source/index.rst`.

Step 5. Change the `html_title` in `source/conf.py`, and add the bibtex to `source/_static/bibtex.bib`.

Step 6. Run `make html` in the `ifml_template` folder (the folder which has the `Makefile`).

Step 7. Open `./build/html/index.html` to view the webpage. Copy over the `./build/html` to your webdomain or wherever else it needs to be hosted. 

*Note*: Rename the `./build/html` folder to the name of the project and then share it. 



References.

[Sphinx](https://www.sphinx-doc.org/en/master/usage/quickstart.html)

[Insipid theme](https://insipid-sphinx-theme.readthedocs.io/en/0.2.4/index.html)

