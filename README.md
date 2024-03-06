texlive.js 
==========

This is a port of TeX live 2019 to Javascript. 
It creates PDF files from LaTeX code and supports packages.


To run the demo
---------------

To run an example document (in the `input` directory) through pdflatex in your browser:

1. Clone this repo
2. Run a local webserver in the root of this repo, e.g. using `python3 -m http.server`
3. Open http://localhost:8000/test.html in a web browser, open the JS console, and hit the "run" button. You should see the first page of a paper (we render the whole paper to PDF, it's only the PDF viewer that currently displays only one page).

Most of the paper seems to render okay: the overall layout, fonts, TikZ figures, and embedded images all work. Known problems:

- Page 1 currently has some junk on it, and for some reason the paper content doesn't start till page 2
- Citations and references are question marks; to fix this we need to run latex twice and feed the aux file from the first run into the second
- bibtex currently doesn't work


To build from source
--------------------

Install [Emscripten](https://emscripten.org/), add its environment variables to your shell (`source emsdk_env.sh`), and then run `make` in the root of this repo. As I understand it, this does the following:

1. Download the latest source release of [texlive](https://www.tug.org/texlive/)
2. Compile for the local OS target, which we need for the toolchain to build pdftex (in particular the Web2C tool, which translates source in Donald Knuth's WEB language into C)
3. Build using Emscripten
