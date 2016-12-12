### Font size

```
\Huge
\huge
\LARGE
\Large
\large
\normalsize (default)
\small
\footnotesize
\scriptsize
\tiny
```

### Links

```
\usepackage{hyperref}
\url{}
```

### Images
```
\usepackage{graphicx}
\includegraphics[scale=0.6]{image.png}
```
### Colors

```
\usepackage{xcolor}
\definecolor{custom-gray}{gray}{0.9}
\definecolor{darkgreen}{HTML}{3b7e30}
```

### Underline with text wrapping

```
package: soul

\ul{ content }
```

### Minted
```
\begin{minted}[bgcolor=custom-gray,frame=lines]{python}

\end{minted}
```

### Beamer - references at end of page

```
\newcommand{\myvfill}{\vskip0pt plus 1filll}

\begin{flushright}
[\ref{foo}]
\end{flushright}
```

### Embed ASCII art in Verbatim

```
\usepackage{fancyvrb}
\usepackage{boxedminipage}

\begin{center}\begin{minipage}{8cm}
\begin{Verbatim}[frame=lines, fontsize=\normalsize, commandchars=\\\{\}]

content

\end{Verbatim}
\end{minipage}\end{center}
```

### Table padding

```
\def\arraystretch{1.5}%  1 is the default, change whatever you need
\begin{tabular}{|c|...}
```

### No indentation in paragraphs

`\setlength\parindent{0pt}`


### Itemize and enumerate

* Redefine bullet points: ` \def\labelitemi{$\cdot$}`

* Roman enumeration: `\begin{enumerate}[label={\it \roman*)}]`

* No space in itemize: `\begin{itemize}[noitemsep,nolistsep]`

