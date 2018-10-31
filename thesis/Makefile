MAINFILE=main
PDFNAME=$(MAINFILE).pdf

PRESFILE=presentation
PRESPDF=$(PRESFILE).pdf

PRESSHORT=presentation-shortened
SHORTPDF=$(PRESSHORT).pdf

LATEX=pdflatex
LATEXFLAGS=

PRESTEX=latexmk

BIBTEX=biber

HIDEPATTERN=(\.(aux|log|lox|bbl|bcf|toc|blg|run\.xml|nav|snm|out)$$)

TIKZDIR=tikz/
TIKZBLUEPRINT=$(TIKZDIR)tikz-blueprint.tex
TIKZFILES=$(patsubst %.tikz, %.pdf, $(wildcard $(TIKZDIR)*.tikz))

TEXDIR=tex/
TEXFILES=$(wildcard $(TEXDIR)*.tex)

BIBDIR=bib/
BIBFILES=$(wildcard $(BIBDIR)*.bib)

$(SHORTPDF): $(PRESSHORT).tex $(TIKZFILES)
	ls -a | grep -E "\..*$(HIDEPATTERN)" | xargs -I {} rename '.' '' {}
	- $(LATEX) $< && $(LATEX) $<
	#hide auxilliary files again
	ls -a | grep -E "$(HIDEPATTERN)" | xargs -I {} mv {} .{}

$(PRESPDF): $(PRESFILE).tex $(TIKZFILES)
	ls -a | grep -E "\..*$(HIDEPATTERN)" | xargs -I {} rename '.' '' {}
	- $(LATEX) $< && $(LATEX) $<
	#hide auxilliary files again
	ls -a | grep -E "$(HIDEPATTERN)" | xargs -I {} mv {} .{}

$(PDFNAME): $(MAINFILE).tex $(TEXFILES) $(TIKZFILES) $(BIBFILES)
	#unhide hidden auxilliary files
	ls -a | grep -E "\..*$(HIDEPATTERN)" | xargs -I {} rename '.' '' {}
	- $(LATEX) $< && $(BIBTEX) $(MAINFILE) && $(LATEX) $<
	#hide auxilliary files again
	ls -a | grep -E "$(HIDEPATTERN)" | xargs -I {} mv {} .{}

tikz/%.pdf: tikz/%.tikz $(TIKZBLUEPRINT)
	#unhide auxilliary files
	ls -a $(TIKZDIR) | grep -E "\.$*$(HIDEPATTERN)" | xargs -I {} rename '.' '' $(TIKZDIR){}
	- $(LATEX) --jobname=$* -output-directory $(TIKZDIR) '\def\inputfile{$<}\input{$(TIKZBLUEPRINT)}'
	# hide auxilliary files again
	ls -a $(TIKZDIR) | grep -E "$*$(HIDEPATTERN)" | xargs -I {} mv $(TIKZDIR){} $(TIKZDIR).{}
