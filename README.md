# Chroniken 2

## 04.02.2025

LaTeX Release: https://github.com/Ilaris-Tools/IlarisTex/releases/tag/v0.1.2-rc2

Außerdem in die ilaris.cls hinzufügen:

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

und die `rogolan.otf` in `texmf/fonts/opentype/ilaris` ablegen.