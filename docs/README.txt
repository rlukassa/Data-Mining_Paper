DBLP Conference Association Mining - Revised RQ5 Manuscript

Files:
- paper.tex: IEEE conference LaTeX source
- paper.pdf: compiled manuscript
- fig_trend.png: annual venue publication trends
- fig_lift.png: association-rule lift plots
- fig_runtime.png: Apriori and FP-Growth runtime comparison

RQ5 revision:
- Temporal analysis is centered on rule persistence, newly qualifying rules, and rules no longer detected across consecutive periods.
- Venue fields are interpreted after mining rather than preselected as NLP, ML, and computer-vision groups.
- The LLM timeline is treated as context, not as a causal explanation.

Compile twice with pdfLaTeX:
  pdflatex paper.tex
  pdflatex paper.tex
