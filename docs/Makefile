# Makefile to control Evennia documentation building.
# Most common commands are `make help`, `make quick` and `make local`.
SPHINX_LANGUAGE ?= en
ifeq ($(SPHINX_LANGUAGE), en)
  SOURCEDIR = source
  BUILDDIR  = build
else
  SOURCEDIR = source_$(SPHINX_LANGUAGE)
  BUILDDIR  = build_$(SPHINX_LANGUAGE)
endif

AUTODOCDIR = $(SOURCEDIR)/api
#
# You can set these variables from the command line, and also
# from the environment for the first two.
SPHINXOPTS    ?=
SPHINXBUILD   ?= sphinx-build
SPHINXMULTIVERSION ?= sphinx-multiversion
SPHINXAPIDOC ?= sphinx-apidoc
SPHINXAPIDOCOPTS = --tocfile evennia-api  --module-first --force -d 6 --separate --templatedir=$(SOURCEDIR)/_templates/
SPHINXAPIDOCOPTSQUICK = --tocfile evennia-api  --module-first -d 6 --separate --templatedir=$(SOURCEDIR)/_templates/
SPHINXAPIDOCENV = members,undoc-members,show-inheritance
SPHINXAPIDOCEXCLUDE = ../*/migrations/* ../evennia/game_template/* ../evennia/*/tests/* ../evennia/*/tests.py

# ../evennia/*/tests.py ../evennia/accounts/tests/* ../evennia/commands/tests/* ../evennia/comms/tests/* ../evennia/help/tests/* ../evennia/locks/tests/* ../evennia/objects/tests/* ../evennia/prototypes/tests/* ../evennia/scripts/tests/* ../evennia/server/tests/* ../evennia/typeclasses/tests/* ../evennia/utils/tests/* ../evennia/web/tests/*  # don't exclude contrib tests for tutorial purposes


EVDIR ?= $(realpath ../evennia)
EVGAMEDIR ?= $(realpath ../../gamedir)

cblue = $(shell echo "\033[1m\033[34m")
cnorm = $(shell echo "\033[0m")

# set specific files to only run for quick run (even if unset, will still not build new api docs)
QUICKFILES=


# Put it first so that "make" without argument is like "make help".
help:
	@$(SPHINXBUILD) -M help "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)
	@echo "Evennia-specific: "
	@echo "  $(cblue)install$(cnorm)     to get doc build requirements"
	@echo "  $(cblue)clean$(cnorm)       to remove remnants of a previous build"
	@echo "  $(cblue)quick$(cnorm)       to build local docs but skip the autodocs (for quick testing)"
	@echo "  $(cblue)quickstrict$(cnorm) to build like 'quick' but abort immediately on any error"
	@echo "  $(cblue)local$(cnorm)       to build local html docs of the current branch (no multiversion)."
	@echo "  $(cblue)localupdate$(cnorm) to build local html docs (only update changes)"
	@echo "  $(cblue)mv-local$(cnorm)    to build multiversion html docs, without deploying (req: local git commit first)"
	@echo "  $(cblue)deploy$(cnorm)      to deploy previously built multiversion docs online (req: commit and github push access)"
	@echo "  $(cblue)release$(cnorm)     to build + deploy multiversion docs online (req: commit and github push access)"


.PHONY: help Makefile

# Catch-all target: route all unknown targets to Sphinx using the new
# "make mode" option.  $(O) is meant as a shortcut for $(SPHINXOPTS).
%: Makefile
	@$(SPHINXBUILD) -M $@ "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)

# Evennia - custom commands

# helper targets

_check-env:
	@EVDIR=$(EVDIR) EVGAMEDIR=$(EVGAMEDIR) bash -e checkenv.sh

_multiversion-check-env:
	@EVDIR=$(EVDIR) EVGAMEDIR=$(EVGAMEDIR) bash -e checkenv.sh multiversion

_clean_api_index:
	rm -f $(SOURCEDIR)/api/*

_clean_api_rsts:
	rm -f $(SOURCEDIR)/api/*.rst

# remove superfluos 'module' and 'package' text from api headers
_reformat_apidoc_headers:
	for f in $(SOURCEDIR)/api/*.rst; do\
        perl -pi -e 's/(module|package)$$// if $$. == 1' $$f ;\
  done

_autodoc-index:
	make _clean_api_index
	@EVDIR=$(EVDIR) EVGAMEDIR=$(EVGAMEDIR) SPHINX_APIDOC_OPTIONS=$(SPHINXAPIDOCENV) $(SPHINXAPIDOC) $(SPHINXAPIDOCOPTS) -o $(SOURCEDIR)/api/ $(EVDIR) $(SPHINXAPIDOCEXCLUDE)
	make _reformat_apidoc_headers
	python pylib/api_rst2md.py

_quick_autodoc-index:
	@EVDIR=$(EVDIR) EVGAMEDIR=$(EVGAMEDIR) SPHINX_APIDOC_OPTIONS=$(SPHINXAPIDOCENV) $(SPHINXAPIDOC) $(SPHINXAPIDOCOPTSQUICK) -o $(SOURCEDIR)/api/ $(EVDIR) $(SPHINXAPIDOCEXCLUDE)

_multiversion-autodoc-index:
	make _autodoc-index
	git diff-index --quiet HEAD || git commit -a -m "Updated API autodoc index." || :

_html-build:
	@EVDIR=$(EVDIR) EVGAMEDIR=$(EVGAMEDIR) $(SPHINXBUILD) $(SPHINXOPTS) "$(SOURCEDIR)" "$(BUILDDIR)/html"

_quick-html-build:
	@NOAUTODOC=1 EVDIR=$(EVDIR) EVGAMEDIR=$(EVGAMEDIR) $(SPHINXBUILD) $(SPHINXOPTS) "$(SOURCEDIR)" "$(BUILDDIR)/html" $(QUICKFILES)

_multiversion-build:
	@EVDIR=$(EVDIR) EVGAMEDIR=$(EVGAMEDIR) $(SPHINXMULTIVERSION) $(SPHINXOPTS) "$(SOURCEDIR)" "$(BUILDDIR)/html" $(SPHINXOPTS)

_multiversion-deploy:
	@python deploy.py
	# @bash -e deploy.sh

_latex-build:
	@NOAUTODOC=1 EVDIR=$(EVDIR) EVGAMEDIR=$(EVGAMEDIR) $(SPHINXBUILD) -M latexpdf "$(SOURCEDIR)" "$(BUILDDIR)/latex" $(QUICKFILES)

install:
	@pip install -r requirements.txt

clean:
	@rm -Rf $(BUILDDIR)
	@git clean -f -d docs/
	@echo "Cleaned old build dir and leftover files."

# not fully working at this time
pdf:
	make _latex-build
	@echo ""
	@echo "Documentation built (single version, no autodocs)."
	@echo "To see result, open evennia/docs/build/latex/evennia.pdf in a PDF reader."

quick:
	make _check-env
	make _html-build
	@echo ""
	@echo "Documentation built (single version, no autodocs)."
	@echo "To see result, open evennia/docs/${BUILDDIR}/html/index.html in a browser."

# abort on warnings too (not working atm)
quickstrict:
	SPHINXOPTS=-W make quick

# we build index directly for the current branch
local:
	make _check-env
	make _autodoc-index
	make _html-build
	@echo ""
	@echo "Documentation built (single version + autodocs)."
	@echo "To see result, open evennia/docs/${BUILDDIR}/html/index.html in a browser."

# build only that which updated since last run (no clean or index-creation)
localupdate:
	make _check-env
	make _html-build
	@echo ""
	@echo "Documentation built (single version, only updates, no autodocs)."
	@echo "To see result, open evennia/docs/${BUILDDIR}/html/index.html in a browser."

# note that this should be done for each relevant multiversion branch.
mv-index:
	make _multiversion-autodoc-index
	@echo "(Re)Built and committed api rst files for this branch only."

mv-local:
	make _multiversion-check-env
	make _multiversion-build
	@echo ""
	@echo "Documentation built (multiversion + autodocs)."
	@echo "To see result, open evennia/docs/${BUILDDIR}/html/<version>/index.html in a browser."

# note - don't run deploy/release manually, the result will clash with the
# result of the github actions! 
deploy:
	make _multiversion-deploy
	@echo "Documentation deployed."

# build and prepare the docs for release
release:
	make mv-local
	make deploy
	@echo "Release complete."
