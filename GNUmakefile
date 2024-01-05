
TARGETTEX = software-license.tex
TARGETPDF = $(patsubst %.tex,%.pdf,$(TARGETTEX))

PICDIR = pic
FIGDIR = fig
STYDIR = sty

LATEX = env TEXINPUTS=".//:" uplatex
PDFLATEX = env TEXINPUTS=".//:" pdflatex -file-line-error
BIBTEX = pbibtex
DVIPDF = dvipdfm
PIC = pic

SOURCESTY = $(wildcard $(STYDIR)/*.sty)

SOURCETEX = $(wildcard *.tex)
SOURCEBIB = $(wildcard *.bib)

SOURCEPIC = $(wildcard $(PICDIR)/*.pic)
TARGETPIC = $(patsubst %.pic,%.tex,$(SOURCEPIC))

TARGETEPS = $(wildcard $(FIGDIR)/*.eps)
FIGPDF = $(wildcard $(FIGDIR)/*.pdf)

FIGURES = $(TARGETPIC) $(TARGETEPS) $(FIGPDF)

default: pdf

pdf: $(TARGETPDF)

pics: $(TARGETPIC)
$(PICDIR)/%.tex: $(PICDIR)/%.pic
	$(PIC) -z -t $< > $@

# %.pdf: %.tex $(SOURCESTY) $(SOURCETEX) $(SOURCEBIB) $(FIGURES)
# 	$(PDFLATEX) $*
# 	-$(BIBTEX) $*
# 	$(PDFLATEX) $*
# 	$(PDFLATEX) $*

%.pdf: %.dvi
	$(DVIPDF) $*
%.dvi: %.tex $(SOURCESTY) $(SOURCETEX) $(SOURCEBIB) $(FIGURES)
	$(LATEX) $*
	-$(BIBTEX) $*
	$(LATEX) $*
	$(LATEX) $*

clean:
	$(RM) *.aux *.bbl *.blg *.dvi *.log *.out *.toc *~
	$(RM) $(TARGETPIC) $(TARGETPDF)

