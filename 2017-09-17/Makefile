LATEX:=pdflatex
LATEXOPT:=--shell-escape
NONSTOP:=--interaction=nonstopmode

LATEXMK:=latexmk
LATEXMKOPT:=-pdf
CONTINUOUS:=-pvc

CONFIDENTIAL:=confidential.tex
PUBLIC:=public.tex

mkfile_path:=$(abspath $(lastword $(MAKEFILE_LIST)))

MAIN:=$(notdir $(patsubst %/,%,$(dir $(mkfile_path))))
CONFIDENTIAL_OUT:=$(MAIN)-confidential
PUBLIC_OUT:=$(MAIN)-public
OUTPUT:=bin

SOURCES:=$(CONFIDENTIAL).tex Makefile

all: confidential public

watch:    $(CONFIDENTIAL_OUT).pdf

.refresh:
	touch .refresh

$(CONFIDENTIAL_OUT).pdf: .refresh $(SOURCES)
	$(LATEXMK) $(LATEXMKOPT) $(CONTINUOUS) \
		-pdflatex="$(LATEX) $(LATEXOPT) $(NONSTOP) %O %S" $(CONFIDENTIAL) \
		-jobname=$(OUTPUT)/$(CONFIDENTIAL_OUT)

confidential:
	$(LATEXMK) $(LATEXMKOPT) \
		-pdflatex="$(LATEX) $(LATEXOPT) $(NONSTOP) %O %S" $(CONFIDENTIAL) \
		-jobname=$(OUTPUT)/$(CONFIDENTIAL_OUT)
	mv ./$(OUTPUT)/$(CONFIDENTIAL_OUT).pdf ./$(CONFIDENTIAL_OUT).pdf


public:
	$(LATEXMK) $(LATEXMKOPT) \
		-pdflatex="$(LATEX) $(LATEXOPT) $(NONSTOP) %O %S" $(PUBLIC) \
		-jobname=$(OUTPUT)/$(PUBLIC_OUT)
	mv ./$(OUTPUT)/$(PUBLIC_OUT).pdf ./$(PUBLIC_OUT).pdf

clean:
	$(LATEXMK) -C $(MAIN)
	rm -f $(MAIN).pdfsync
	rm -rf *~ *.tmp
	rm -f *.bbl *.blg *.aux *.end *.fls *.log *.out *.fdb_latexmk

debug:
	$(LATEX) $(LATEXOPT) $(MAIN)

.PHONY: clean force public confidential watch
