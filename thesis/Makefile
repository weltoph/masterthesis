MAINFILE=main.tex
PDFNAME=$(patsubst %.tex, %.pdf, $(MAINFILE))

LATEX=pdflatex
LATEXFLAGS=

HIDEPATTERN=(\.aux$$|\.log$$|\.lox$$)

TIKZDIR=tikz/
TIKZBLUEPRINT=$(TIKZDIR)tikz-blueprint.tex
TIKZFILES=$(patsubst %.tikz, %.pdf, $(wildcard $(TIKZDIR)*.tikz))

$(PDFNAME): $(MAINFILE) $(TIKZFILES)
	#unhide auxilliary files
	ls -a | grep -E "$(HIDEPATTERN)" | xargs -I {} rename '.' '' {}
	pdflatex $<
	pdflatex $<
	#hide auxilliary files again
	ls -a | grep -E "$(HIDEPATTERN)" | xargs -I {} mv {} .{}

tikz/%.pdf: tikz/%.tikz $(TIKZBLUEPRINT)
	#unhide auxilliary files
	ls -a $(TIKZDIR) | grep -E "$*$(HIDEPATTERN)" | xargs -I {} rename '.' '' $(TIKZDIR){}
	pdflatex --jobname=$* -output-directory $(TIKZDIR) '\def\inputfile{$<}\input{$(TIKZBLUEPRINT)}'
	#hide auxilliary files again
	ls -a $(TIKZDIR) | grep -E "$*$(HIDEPATTERN)" | xargs -I {} mv $(TIKZDIR){} $(TIKZDIR).{}
