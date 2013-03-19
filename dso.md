% Document Service Ontology (DSO)
% Jakob Voß (VZG)
% GIT_REVISION_DATE

# Introduction

The **Document Service Ontology (DSO)** is a micro-ontology that defines a set
of typical document-related services such as provided by libraries, museums and
archives.

## Status of this document

This HTML document and RDF serializations of the Document Service Ontology
([**`dso.ttl`**](dso.ttl) in RDF/Turtle and [**`ssss.owl`**](dso.owl) in
RDF/XML) are generated automatically from a source file written in Pandoc
Markdown syntax. Sources and updates are available at
<http://github.com/gbv/dso>. The current version of this document was last
modified at GIT_REVISION_DATE with revision GIT_REVISION_HASH.

The current version of this ontology is a preliminary draft for open
discussion.

## Terminology

The keywords "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in RFC 2119.

## Namespaces and ontology

The URI namespace of this ontology is <http://purl.org/ontology/dso#>. The
namespace prefix `dso` is recommeded. The URI of this ontology as a whole
is <http://purl.org/ontology/dso>.

    @prefix dso: <http://purl.org/ontology/dso#> .
    @base        <http://purl.org/ontology/dso> .

The following namspace prefixes are used to refer to [related ontologies]:

    @prefix bibo:  <http://purl.org/ontology/bibo/> .
    @prefix foaf:  <http://xmlns.com/foaf/0.1/> .
    @prefix owl:   <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs:  <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix ssso:  <http://purl.org/ontology/ssso#> .
    @prefix vann:  <http://purl.org/vocab/vann/> .

The Document Service Ontology (DSO) is defined in RDF/Turtle as following:

    <> a owl:Ontology ;
        rdfs:label "Document Service Ontology" ;
        rdfs:label "DSO" ;
        vann:preferredNamespacePrefix "dso" .


# Overview

...

This ontology does not make any assumptions about types of documents. A
document may be an abstract entity (e.g. a work or an edition of a book), a
physical or digital copy, or a unique object (e.g. a statue in a museum).

...


# Classes

## Service

[Service]: #service

A document service is a kind of service event ([ssso:ServiceEvent]) that is
somehow related to one or more documents.

    dso:Service a owl:Class ;
        rdfs:label "Service" ;
        rdfs:subClassOf ssso:ServiceEvent ;
        rdfs:isDefinedBy <> .

*should this class be renamed to "DocumentService"?*

[ssso:ServiceEvent]: http://purl.org/ontology/ssso#ServiceEvent

## Loan

[Loan]: #loan

A loan is a service event that involes the temporary transfer of usage rights
of a document from a service provider (e.g. a library) to a service consumer
(e.g. a library patron).

    dso:Loan a owl:Class ;
        rdfs:label "Loan" ;
        rdfs:subClassOf dso:Service ;
        rdfs:isDefinedBy <> .

## Presentation

[Presentation]: #presentation

A presentation involves the display or similar usage of a document in a
restricted environment, e.g.  within the rooms or in the intranet of a library
or museum.

    dso:Presentation a owl:Class ;
        rdfs:label "Presentation" ;
        rdfs:subClassOf dso:Service ;
        rdfs:isDefinedBy <> .

## Interloan

[Interloan]: #interloan

For interloan a document is made accessible mediated by another institution.

    dso:Interloan a owl:Class ;
        rdfs:label "Interloan" ;
        rdfs:subClassOf dso:Service ;
        rdfs:isDefinedBy <> .

## OpenAccess

[OpenAccess]: #openaccess

An Open Access service implies to free accessibility of a document without any
restrictions by the service provider (Open Access or free copies).

    dso:OpenAccess a owl:Class ;
        rdfs:label "OpenAccess" ;
        rdfs:subClassOf dso:Service ;
        rdfs:isDefinedBy <> .


## Digitization

[Digitization]: #digitization

A digitization service creates a digital document from a physical document, for
instance a digital photograph or a 3D-scan of a physical object.

*This class is just a suggestion!*


## Identification

A service to identify a document that is only known with limited properties
(e.g. only parts of the title). In RDF such document is typically expressed by
a blank node.

*This class is just a suggestion!*


# Properties

## withDocument

[withDocument]: #withdocument

Relates a document [service] to a document. The relation is rather lax as it
only tells that a specific document is somehow involved in a specific document
service event.  To express more reliable relations, one should define and use
more specific sub-properties, such as [daia:availableFor] and
[daia:unavailableFor].

    dso:withDocument a owl:ObjectProperty ;
        rdfs:label "withDocument" ;
        rdfs:domain dso:Service ;
        rdfs:range bibo:Document, foaf:Document ;
        owl:inverseOf ssso:consumedBy ;
        rdfs:isDefinedBy <> .


# Related ontologies

[related ontologies]: #related-ontologies

The Document Service Ontology is part of a set of micro-ontologies originally
created to describe several aspects of libraries and similar institutions. Some
services defined in DSO have earlier been defined as part of the DAIA ontology,
which now makes use of DSO. The core concept of a service is based on the definition
of a service event in the Simple Service Status Ontology (SSSO).


# References

## Normative References

* **[RFC 2119]** S. Bradner: *Key words for use in RFCs to Indicate Requirement Levels*. 
  March 1997 <http://tools.ietf.org/html/rfc2119>.

* **[RFC 2396]** T. Berners-Lee et al.: *Uniform Resource Identifiers (URI): Generic Syntax*.
  August 1998 <http://tools.ietf.org/html/rfc2396>.

* **[SSSO]** J. Voß: *Simple Service Status Ontology (SSSO)*.
  February 2013 <http://purl.org/ontology/ssso>.

## Informative References

* **[DAIA]** J. Voß: *Document Availability Information API (DAIA)*.
  Work in progress at <http://gbv.github.com/daiaspec/>.

* ...
