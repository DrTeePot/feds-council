LATEX:=pdflatex
LATEXOPT:=--shell-escape
NONSTOP:=--interaction=nonstopmode

LATEXMK:=latexmk
LATEXMKOPT:=-pdf
CONTINUOUS:=-pvc

mkfile_path:=$(abspath $(lastword $(MAKEFILE_LIST)))

MAIN:=$(notdir $(patsubst %/,%,$(dir $(mkfile_path))))
CONFIDENTIAL:=$(MAIN)-confidential
PUBLIC:=$(MAIN)-public
SOURCES:=$(CONFIDENTIAL).tex Makefile
OUTPUT:=bin

all: confidential public

watch:    $(CONFIDENTIAL).pdf

.refresh:
	touch .refresh

$(CONFIDENTIAL).pdf: .refresh $(SOURCES)
	$(LATEXMK) $(LATEXMKOPT) $(CONTINUOUS) \
		-pdflatex="$(LATEX) $(LATEXOPT) $(NONSTOP) %O %S" $(CONFIDENTIAL) \
		-jobname=$(OUTPUT)/$(CONFIDENTIAL)

confidential:
	$(LATEXMK) $(LATEXMKOPT) \
		-pdflatex="$(LATEX) $(LATEXOPT) $(NONSTOP) %O %S" $(CONFIDENTIAL) \
		-jobname=$(OUTPUT)/$(CONFIDENTIAL)
	mv ./$(OUTPUT)/$(CONFIDENTIAL).pdf ./$(CONFIDENTIAL).pdf


public:
	$(LATEXMK) $(LATEXMKOPT) \
		-pdflatex="$(LATEX) $(LATEXOPT) $(NONSTOP) %O %S" $(PUBLIC) \
		-jobname=$(OUTPUT)/$(PUBLIC)
	mv ./$(OUTPUT)/$(PUBLIC).pdf ./$(PUBLIC).pdf

clean:
	$(LATEXMK) -C $(MAIN)
	rm -f $(MAIN).pdfsync
	rm -rf *~ *.tmp
	rm -f *.bbl *.blg *.aux *.end *.fls *.log *.out *.fdb_latexmk

debug:
	$(LATEX) $(LATEXOPT) $(MAIN)

.PHONY: clean force public confidential watch
