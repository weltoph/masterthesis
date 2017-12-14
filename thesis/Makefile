MAINFILE=main.tex
PDFNAME=$(patsubst %.tex, %.pdf, $(MAINFILE))

LATEX=pdflatex
LATEXFLAGS=

TIKZDIR=tikz/
TIKZBLUEPRINT=$(TIKZDIR)tikz-blueprint.tex
TIKZFILES=$(patsubst %.tikz, %.pdf, $(wildcard $(TIKZDIR)*.tikz))

$(PDFNAME): $(MAINFILE) $(TIKZFILES) $(TIKZBLUEPRINT)
	pdflatex $<

tikz/%.pdf: tikz/%.tex
	@echo pdf-rule:
	pdflatex -output-directory $(TIKZDIR) $<

tikz/%.tex: tikz/%.tikz
	sed -r "/%%FILE%%/r $<" $(TIKZBLUEPRINT) > $@
