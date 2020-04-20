TARGET := homework
LATEX  := latexmk
LATEXOPTS := -quiet -f -pdf -lualatex -use-make

# Spell checking using aspell
ASPELL=aspell
CHECK_ARGS=check
CHECK=$(ASPELL) $(CHECK_ARGS)

# Commands for running continuous preview with latexmk
PREVIEW_ARGS=$(LATEXOPTS) -pvc
PREVIEW=$(LATEX) $(PREVIEW_ARGS)

STYLES = $(wildcard styles/**/*.cls)
CONTENT = $(wildcard content/**/*.tex)
FIGS = $(wildcard figures/**/*) # all figures

pdf: $(TARGET).pdf

$(TARGET).pdf: $(TARGET).tex $(CONTENT) $(FIGS) $(STYLES)
	# Compile pdf
	$(LATEX) $(LATEXOPTS) $(TARGET).tex $(CONTENT)
	$(LATEX) $(LATEXOPTS) $(TARGET).tex $(CONTENT)
	$(LATEX) $(LATEXOPTS) $(TARGET).tex $(CONTENT)

preview:
	# Continuous preview of paper while editing
	$(PREVIEW) $(TARGET)

submit:
	make clean
	make $(TARGET).pdf

grayscale:
	# Grayscale pdf
	make clean
	make
	gs -sDEVICE=pdfwrite -dProcessColorModel=/DeviceGray -dColorConversionStrategy=/Gray -dPDFUseOldCMS=false -o $(G).pdf -f $(TARGET).pdf

check:
	# Spell checker
	for f in $(CONTENT) ; do echo $$f ; $(CHECK) $$f | sort | uniq -c ; done

clean:
	# Clean latex garbage
	rm -rf *.aux *.bbl *.blg *.log *.nav *.out *.snm *.toc *.synctex* *.xdv *.fdb_latexmk *.fls $(TARGET).pdf content/*.aux
