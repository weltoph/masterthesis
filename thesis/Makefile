MAINFILE=main
PDFNAME=$(MAINFILE).pdf

LATEX=pdflatex
LATEXFLAGS=

BIBTEX=biber

HIDEPATTERN=(\.(aux|log|lox|bbl|bcf|blg|run\.xml)$$)

TIKZDIR=tikz/
TIKZBLUEPRINT=$(TIKZDIR)tikz-blueprint.tex
TIKZFILES=$(patsubst %.tikz, %.pdf, $(wildcard $(TIKZDIR)*.tikz))

TEXDIR=tex/
TEXFILES=$(wildcard $(TEXDIR)*.tex)

$(PDFNAME): $(MAINFILE).tex $(TEXFILES) $(TIKZFILES)
	#unhide hidden auxilliary files
	ls -a | grep -E "\..*$(HIDEPATTERN)" | xargs -I {} rename '.' '' {}
	- $(LATEX) $< && $(BIBTEX) $(MAINFILE) && $(LATEX) $<
	#hide auxilliary files again
	ls -a | grep -E "$(HIDEPATTERN)" | xargs -I {} mv {} .{}

tikz/%.pdf: tikz/%.tikz $(TIKZBLUEPRINT)
	#unhide auxilliary files
	ls -a $(TIKZDIR) | grep -E "$*/\..*$(HIDEPATTERN)" | xargs -I {} rename '.' '' $(TIKZDIR){}
	- $(LATEX) --jobname=$* -output-directory $(TIKZDIR) '\def\inputfile{$<}\input{$(TIKZBLUEPRINT)}'
	#hide auxilliary files again
	ls -a $(TIKZDIR) | grep -E "$*$(HIDEPATTERN)" | xargs -I {} mv $(TIKZDIR){} $(TIKZDIR).{}
