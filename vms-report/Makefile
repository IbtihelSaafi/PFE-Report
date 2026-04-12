# Makefile for VMS LaTeX Report
# Usage: make pdf | make clean | make view

MAIN = main
LATEX = pdflatex
BIBTEX = bibtex
GLOSSARY = makeglossaries

.PHONY: all pdf clean view help

all: pdf

pdf:
	@echo "==> Building PDF (pass 1)..."
	$(LATEX) -interaction=nonstopmode $(MAIN).tex
	@echo "==> Running BibTeX..."
	$(BIBTEX) $(MAIN)
	@echo "==> Building glossary..."
	$(GLOSSARY) $(MAIN)
	@echo "==> Building PDF (pass 2)..."
	$(LATEX) -interaction=nonstopmode $(MAIN).tex
	@echo "==> Building PDF (pass 3 - final)..."
	$(LATEX) -interaction=nonstopmode $(MAIN).tex
	@echo ""
	@echo "✅  PDF generated: $(MAIN).pdf"

quick:
	@echo "==> Quick single-pass build..."
	$(LATEX) -interaction=nonstopmode $(MAIN).tex
	@echo "✅  Done: $(MAIN).pdf"

clean:
	@echo "==> Cleaning auxiliary files..."
	rm -f *.aux *.log *.toc *.lof *.lot *.out *.bbl *.blg \
	       *.gls *.glo *.glg *.acn *.acr *.alg *.ist \
	       *.fls *.fdb_latexmk *.synctex.gz *.idx *.ilg *.ind
	@echo "✅  Cleaned."

distclean: clean
	rm -f $(MAIN).pdf

view: pdf
	@if command -v evince >/dev/null 2>&1; then evince $(MAIN).pdf &; \
	elif command -v okular >/dev/null 2>&1; then okular $(MAIN).pdf &; \
	elif command -v open >/dev/null 2>&1; then open $(MAIN).pdf; \
	else echo "No PDF viewer found. Open $(MAIN).pdf manually."; fi

help:
	@echo ""
	@echo "VMS Report Build System"
	@echo "========================"
	@echo "  make pdf       - Full build (recommended)"
	@echo "  make quick     - Single-pass quick build"
	@echo "  make clean     - Remove auxiliary files"
	@echo "  make distclean - Remove all generated files including PDF"
	@echo "  make view      - Build and open PDF"
	@echo ""
	@echo "Requirements: pdflatex, bibtex, makeglossaries"
	@echo "  Ubuntu/Debian: sudo apt install texlive-full"
	@echo "  macOS:         brew install --cask mactex"
	@echo ""
