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
\usepackage{soul}

\ul{ content }
```

### Box around text

```
\framebox[\textwidth]{
\parbox{\dimexpr\linewidth-2\fboxsep-2\fboxrule}{

content

} }
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

### Algorithm2e side by side

```
\usepackage[vlined]{algorithm2e} 

\begin{minipage}[t]{8cm}
	
  \vspace{0pt}  
  %\RestyleAlgo{boxruled}

  \begin{algorithm}[H]

 state $\leftarrow plaintext$\\
 \For{$r\in1..9$}{
  AddRoundKey(state,$k_{r-1}$)\\
  ShiftRows(state)\\
 
 }
  \end{algorithm}

\end{minipage}


\begin{minipage}[t]{8cm}
  \vspace{0pt}
  \begin{algorithm}[H]

  state $\leftarrow plaintext$\\
 \For{$r\in1..9$}{
  AddRoundKey(state,$k_{r-1}$)\\
  ShiftRows(state)\\
 
 }

  \end{algorithm}
  
	\end{minipage}
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

### Same footnote in different places

```
\usepackage{scrextend}

Text1 \footnote{This is a registered trade name. \label{refnote}}
Text2 \footref{refnote}
```