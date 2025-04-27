# Chroniken 2

## 04.02.2025

LaTeX Release: https://github.com/Ilaris-Tools/IlarisTex/releases/tag/v0.1.2-rc2

### ilaris.cls

#### biglittlecap

```
\ExplSyntaxOn
\NewDocumentCommand{\biglittlecap}{m}
{
    \sheljohn_biglittecap:nn { #1 }
}
\tl_new:N \l__sheljohn_biglittecap_input_tl
\cs_new_protected:Npn \sheljohn_biglittecap:nn #1
{
    % store the string in a variable   
    \tl_set:Nn \l__sheljohn_biglittecap_input_tl { \small{#1} }
    \regex_replace_all:nnN
    % search a capital letter (or more)
    { ([A-Z]+ | \cC.\{?[A-Z]+\}?) }
    % replace the match with \huge{match}
    { \cB\{\c{normalsize}\1\cE\} }   % <=== could use large, Large (or some other command...)
    \l__sheljohn_biglittecap_input_tl
    \tl_use:N \MakeUppercase{\l__sheljohn_biglittecap_input_tl}
}
\ExplSyntaxOff
```

#### probenkasten 

Added a `\vspace{0.25}` at the beginning and end.

#### Probenkasten Transparenz

Set opacity in probenkasten

`\node[anchor=center,opacity=0.7] at (frame.center) {\includegraphics[width=\ProbeBgscale mm]{gfx/proben/\ProbeBild_bg.png}};`

### Fonts

und die `rogolan.otf` in `texmf/fonts/opentype/ilaris` ablegen.

### Bilder
#### Probenkastenbilderbereinigung

Da waren noch Artefakte, die ich entfernt habe.

## Smaller PDF sizes

`cpdf -squeeze input.pdf -o output.pdf`

`gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.5 -dPDFSETTINGS=/ebook -o output.pdf input.pdf`

| Option      | Color & Grayscale DPI | Monochrome DPI | Purpose |
|------------|----------------------|---------------|---------|
| `/screen`  | **72 DPI**            | 72 DPI        | Smallest file size, optimized for screen viewing. |
| `/ebook`   | **150 DPI**           | 300 DPI       | Good balance of size and quality for eBooks. |
| `/printer` | **300 DPI**           | 600 DPI       | High quality, suitable for printing. |
| `/prepress`| **300-400 DPI**       | 1200 DPI      | Very high quality, retains metadata and color profiles. |

## PDF Check

~~Zusätzlich können wir noch alle Links im PDF überprüfen, ob sie auf valide Websiten zeigen: https://pypi.org/project/pdf-link-checker/ Interne Links werden dabei nicht überprüft.~~

Habe ich probiert, hat für mich aber nicht funktioniert, da das Paket interne Fehler hat.