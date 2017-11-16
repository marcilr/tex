# -*- Mode: Makefile -*-
#
# Makefile for a single-file LaTeX document plus optional BibTeX file.
#
# Comment out the BibTeX run in the `dvi' target if you don't have a
# bibliography.

RM = /bin/rm -f
LATEX = /usr/bin/latex
BIBTEX = /usr/bin/bibtex
DVIPS = /usr/bin/dvips
PS2PDF = /usr/bin/ps2pdf

BASENAME = essential

SRC = $(BASENAME).tex
BIB = $(BASENAME).bib
BLG = $(BASENAME).blg
BBL = $(BASENAME).bbl
LOG = $(BASENAME).log
AUX = $(BASENAME).aux
TOC = $(BASENAME).toc
DVI = $(BASENAME).dvi
PS  = $(BASENAME).ps
PDF = $(BASENAME).pdf

cycle: clean dvi ps pdf

all: dvi ps pdf

clean:
	$(RM) $(LOG) $(AUX) $(TOC) $(DVI) $(PS) $(BBL) $(BLG) $(PDF)

dvi:
	$(LATEX) $(SRC)
#	$(BIBTEX) $(BASENAME)
# Rerun LaTeX again to get the xrefs right.
	$(LATEX) $(SRC)
	$(LATEX) $(SRC)

ps: dvi
# Embed type 1 fonts, optimize for pdf
	$(DVIPS) -f -Ppdf < $(DVI) > $(PS)
# Embed type 1 fonts.
#	$(DVIPS) -f -Pcmz < $(DVI) > $(PS)
# Embed type 3 (bitmapped) fonts.
#	$(DVIPS) $(DVI) -o

pdf: ps
	$(PS2PDF) $(PS)

	