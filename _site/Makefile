# targets that aren't filenames
.PHONY: all clean deploy build serve

all: build

BIBBLE = bibble

_includes/pubs.html: bib/pubs.bib bib/publications.tmpl
	mkdir -p _includes
#	$(BIBBLE) $+ > $@
	python bibble/bibble.py $+ > $@

build: _includes/pubs.html
	bundle exec jekyll build

# you can configure these at the shell, e.g.:
# SERVE_PORT=5001 make serve
SERVE_HOST ?= 131.123.39.99
SERVE_PORT ?= 5000

serve: _includes/pubs.html
	bundle exec jekyll serve --port $(SERVE_PORT) --host $(SERVE_HOST)

clean:
	$(RM) -r _site _includes/pubs.html

DEPLOY_HOST ?= 131.129.39.99
DEPLOY_PATH ?= /var/www/html/
RSYNC := rsync --compress --recursive --checksum --itemize-changes --delete -e ssh

deploy: clean build
	$(RSYNC) _site/ $(DEPLOY_HOST):$(DEPLOY_PATH)
