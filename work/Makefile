# Makefile
#
# Note: This simple tool is available only for Maintainer.

TARGET = org-ja.pdf

TEXI = ../org.texi
TEXI_JA = org-ja.texi
TEXI_JA_PATCH = org-ja.texi.patch
TEX = ptex
PERL = perl
TEXOPTION = '-kanji=utf8'
POT = org.pot
PO = ../org-ja.po
INFO = org
TRANSLATE = po4a-translate
GETTEXTIZE = po4a-gettextize
TEXIFMT = texifmt.pl

$(TARGET): $(TEXI) $(POT) $(PO) $(TEXI_JA) texinfo.tex
	$(TEX) $(TEXOPTION) $(TEXI_JA)
	texindex org-ja.??
	$(TEX) $(TEXOPTION) $(TEXI_JA)
	texindex org-ja.??
	$(TEX) $(TEXOPTION) $(TEXI_JA)
	dvipdfmx org-ja.dvi

# -w 1000
$(TEXI_JA): $(PO)
	$(TRANSLATE) -f texinfo -m $(TEXI) -M UTF-8 -p $(PO) -l $(TEXI_JA) -k 0
	patch -p0 < org-ja.texi.patch
	$(PERL) $(TEXIFMT) > texifmt.log

$(INFO): $(TEXI_JA)
	makeinfo --no-split $(TEXI_JA) -o $(INFO) --fill-column=72

$(POT): $(TEXI)
	$(GETTEXTIZE) -f texinfo -m $(TEXI) -M UTF-8 -p $(POT)

info: $(INFO)
texi: $(TEXI_JA)
clean:
	rm -f *.aux *.cp *.cps *.dvi *.fn *.fns *.ky *.kys *.log *.mo *.pg *.pgs *.tmp *.vr *.vrs *.toc *.tp *.tps *.rej
