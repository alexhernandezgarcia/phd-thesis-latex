# PhD thesis in LaTeX  - [PDF](https://alexhernandezgarcia.github.io/thesis.pdf)

This repository contains the source files of my PhD thesis, [Data augmentation and image understanding](https://alexhernandezgarcia.github.io/thesis.pdf), written in LaTeX. I'm sharing it with a [CC BY-NC-SA 4.0 License](#license), so feel free to clone the repository and use it as a template for your own thesis or any other document. You are also welcome to get in touch if you have any questions!

## How to use this package

### Overview of the structure

This LaTex document is built in a [modular](https://en.wikibooks.org/wiki/LaTeX/Modular_Documents) way. That means that different parts of the document are contained in separate files and organised in a high-level structure. This has a number of advantages, especially for large documents: it is possible to easily compile only some parts of the document, keep track of changes and in general have a more organised structure.

This project has the following structure concept:

```bash
.
├── includes
│   ├── prologue
│   │   └── prologue.tex
│   ├── chapter1
│   │   ├── chapter1.tex
│   │   └── img
│   │       └── img1-chapter1.png
│   │       └── img2-chapter1.png
│   ├── chapter2
│   │   ├── chapter2.tex
│   │   └── img
│   │       └── img1-chapter2.png
│   │       └── img2-chapter2.png
│   └── epilogue
│       └── epilogue.tex
├── main.tex
├── structure.sty
├── references.bib
└── bibliography.bst
```

* `main.tex` is the main `.tex` file of the project: it is the file that is compiled and that defines the overall structure of the document. It incorporates the rest of the files through `\input{}` and `\include{}` commands. 
* `structure.sty` defines the style of the document, for example through `\usepackage{}` commands.
* `references.bib` contains the list of BiBTeX entries.
* `bibliography.bst` defines the style of the bibliography section.

An example of `main.tex` could be the following:

```
\documentclass[a4paper]{book}

\usepackage{structure}

\begin{document}

\input{includes/prologue/prologue}
\include{includes/chapter1/chapter1}
\include{includes/chapter2/chapter2}
\input{includes/epilogue/epilogue}

\end{document}          
```
### Two versions of the document: print and digital

One of the great advantages of creating a document with LaTeX is that it allows us to easily define multiple style versions, while keeping the content separate.

For this project, I defined two versions:

* Print: for the hard-copy version of the thesis. It essentially uses a book style, defining different styles for left and right pages, setting blank pages, it uses higher-resolution versions of the images, etc.
* Digital: for the PDF version of the thesis. It does not differentiate the style of odd and even pages, does not introduce blank pages, uses lower-resolution images, etc.

In order to define these two documents, there are essentially three things to take into account in this project:

1. Separate style files: [`structure-print.sty`](./structure-print.sty) and [`structure-digital.sty`](./structure-digital.sty)
2. Separate main files: [`main-print.tex`](./main-print.tex) and [`main-digital.tex`](./main-digital.tex)
3. Separate image directories: `./includes/<subfolder>/img/` and `./includes/<subfolder>/img-hd/`. Note that `img-hd` directories are not pushed to GitHub ([see below](#how-to-compile))

### How to compile

First, you will need a working LaTeX installation in order to compile the project and create a PDF. Let's face it, installing LaTeX can be painful experience. I attempted to mitigate this pain for others (and my future self) with a [brief guide on how to get LaTeX working on Linux](https://github.com/alexhernandezgarcia/linux-config-utils/blob/master/latex/latex.md). Depending on your installation, you may have to install some additional packages and fonts (for example `upl` Palatino). You may take a look at [`structure-print.sty`](./structure-print.sty) and [`structure-digital.sty`](./structure-digital.sty) to see the packages used or simply install them as the compiler complains.

Alternatively, you may use an online LaTeX editors, such as [Overleaf](https://www.overleaf.com/).

Second, you can clone this repository into your local machine:
```
git clone https://github.com/alexhernandezgarcia/phd-thesis-latex.git
```

At this point, if all the LaTeX packages are installed, it should be possible to compile [`main-digital.tex`](./main-digital.tex) without errors. If you generate a PDF, it should look like [this one](https://alexhernandezgarcia.github.io/thesis.pdf).

In order to compile [`main-print.tex`](./main-print.tex), you have to take an additional step because it will try to use images stored in `./includes/<subfolder>/img-hd/`, but this directories are not uploaded to GitHub in order to spare storage space. You can simply create dummy `img-hd` directories by copying the `./includes/<subfolder>/img/` directories, with the following in the command line:o
```
for dir in $(ls -d includes/*/img/); do cp -r $dir $(echo $dir | sed -e "s/img/img-hd/g"); done
```

After this, it should be possible to also compile [`main-print.tex`](./main-print.tex) (though with standard resolution images, of course).

Please get in touch if you want some help!

## Citation

If you want to cite this thesis in a scientific document, you may use the following:

*Alex Hernandez-Garcia, 2020. Data augmentation and image understanding. PhD thesis, Institute of Cognitive Science, University of Osnabrück*

	@phdthesis{hergar2020phdthesis,
		author = {Hernandez-Garcia, Alex},
		title = {Data augmentation and image understanding},
		school = {Institute of Cognitive Science, University of Osnabr{\"u}ck},
		year = {2020},
	}

## License

[Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-nc-sa/4.0/)

[![License: CC BY-NC-SA 4.0](https://licensebuttons.net/l/by-nc-sa/4.0/80x15.png)](https://creativecommons.org/licenses/by-nc-sa/4.0/)
