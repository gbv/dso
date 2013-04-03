This repository contains the **Document Service Ontology (DSO)**

The URI of this ontology is going to be <http://purl.org/ontology/dso> and it's
URI namespace is going to be <http://purl.org/ontology/dso#> (not registered
yet).

# Feedback

Feedback is welcome most in form of git pull requests or tracked issues:

* https://github.com/gbv/dso/issues

# Development

The ontology is created by *document driven development* using
[makespec](https://github.com/jakobib/makespec). The source file `dso.md` is written in [Pandoc
Markdown](http://johnmacfarlane.net/pandoc/demo/example9/pandocs-markdown.html).
Both the RDF serialization in RDF/Turtle (or RDF/XML) and the documentation in
HTML are automatically derived from this source file. This requires:

* [Pandoc](http://johnmacfarlane.net/pandoc/), at least 1.9
* [Rapper](http://librdf.org/raptor/rapper.html) from Raptor RDF library

All rules are included in `Makefile`. Just call `make` to (re)create everything, 
or `make html`, `make ttl`, `make owl` to only create selected parts.

To clone this repository:

    git clone git://github.com/gbv/dso.git
    git submodule update --init

To also clone the HTML version branch, which is presented at
<http://gbv.github.com/dso>:

    git checkout -b gh-pages origin/gh-pages

