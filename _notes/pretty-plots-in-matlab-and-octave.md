---
title: Pretty Plots in Matlab and Octave
---

<!--[[University]]-->
<!--[[Programming]]-->

Matlab:
```matlab
figures = findobj(0, 'type', 'figure');
for i = 1 : length(figures)
    print(figs(i), '-depsc', sprintf('figure%d.eps', i));
end
```
Then in LaTeX include the figures normally with `\includegraphics[width=0.33\textwidth]{figure.eps}`.