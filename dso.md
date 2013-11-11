# Introduction

The **Document Service Ontology (DSO)** is a micro-ontology that defines a set
of typical document-related services such as provided by libraries, museums and
archives.

## Status of this document

This document and RDF serializations of the Document Service Ontology
([**`dso.ttl`**](dso.ttl) in RDF/Turtle and [**`ssss.owl`**](dso.owl) in
RDF/XML) are generated automatically from a source file written in Pandoc
Markdown syntax.^[Documents are generated using
[makespec](http://jakobib.github.io/makespec/).] Sources and updates are
available at <http://github.com/gbv/dso>.

This is version {VERSION}, last modified at {GIT_REVISION_DATE} with revision
{GIT_REVISION_HASH}.

The current version of this ontology is a preliminary draft for open
discussion. [Feedback](https://github.com/gbv/dso/issues) is welcome!

**Revision history**

{GIT_CHANGES}

## Namespaces and ontology

The URI namespace of this ontology is 
[http://purl.org/ontology/dso#](http://purl.org/ontology/dso#).
The namespace prefix `dso` is recommended. The URI of this ontology as a whole
is <http://purl.org/ontology/dso>.

    @prefix dso: <http://purl.org/ontology/dso#> .
    @base        <http://purl.org/ontology/dso> .

The following namespace prefixes are used to refer to [related ontologies]:

    @prefix bibo:   <http://purl.org/ontology/bibo/> .
    @prefix daia:   <http://purl.org/ontology/daia/> .
    @prefix foaf:   <http://xmlns.com/foaf/0.1/> .
    @prefix gr:     <http://purl.org/goodrelations/v1#> .
    @prefix owl:    <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs:   <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix schema: <http://schema.org/> .
    @prefix ssso:   <http://purl.org/ontology/ssso#> .
    @prefix vann:   <http://purl.org/vocab/vann/> .

The Document Service Ontology (DSO) is defined in RDF/Turtle as following:

    <> a owl:Ontology ;
        rdfs:label "Document Service Ontology" ;
        rdfs:label "DSO" ;
        vann:preferredNamespacePrefix "dso" .

# Overview

This ontology defines the core class [DocumentService] representing the set of
possible services related to documents. The set of documents is not limited to
a specific class (such as [bibo:Document] from the Bibliographic Ontology,
[foaf:Document] from FOAF vocabulary, and [schema:CreativeWork] from schema.org
vocabulary) although use of these classes is recommended. A document may be an
abstract entity (e.g. a work or an edition of a book), a physical or digital
copy, or a unique object (e.g. a statue in a museum). Some document services,
however do only make sense with specific types of documents. To link documents
and document services, this ontology defines the inverse properties
[hasDocument] and [hasService]. The ontology further defines a set of [specific
document services](#specific-document-service-classes), typically found in the
context of GLAM (galleries, libraries, archives, and museums) institutions.

[bibo:Document]: http://purl.org/ontology/bibo/Document
[foaf:Document]: http://xmlns.com/foaf/0.1/Document
[schema:CreativeWork]: http://schema.org/CreativeWork

# Document service class

[DocumentService]: #document-service-class

A document service is a kind of service that is somehow related to one or more
documents. To indicate the specific type of document service, one should use a
subclass of this class and assing additional service types, such as
[ssso:ServiceEvent] from the Simple Service Status Ontology, [schema:Offer]
or [schema:Product] from schema.org vocabulary, and [gr:Offering] or
[gr:ProductOrService] from GoodRelations vocabulary.

    dso:DocumentService a owl:Class ;
        rdfs:label "DocumentService" ;
        rdfs:seeAlso ssso:ServiceEvent, gr:Offering, schema:Offer ;
        rdfs:isDefinedBy <> .

[ssso:ServiceEvent]: http://purl.org/ontology/ssso#ServiceEvent
[schema:Offer]: http://schema.org/Offer
[schema:Product]: http:/schema.org/Product
[gr:Offering]: http://purl.org/goodrelations/v1#Offering
[gr:ProductOrService]: http://purl.org/goodrelations/v1#ProductOrService

# Specific document service classes

## Loan

[Loan]: #loan

A loan is a [DocumentService] that involves the temporary transfer of usage
rights of a document from a service provider (e.g. a library) to a service
consumer (e.g. a library patron).

    dso:Loan a owl:Class ;
        rdfs:label "Loan" ;
        rdfs:subClassOf dso:DocumentService ;
        rdfs:isDefinedBy <> .

## Presentation

[Presentation]: #presentation

A presentation involves the display or similar usage of a document in a
restricted environment, e.g.  within the rooms or in the intranet of a library
or museum.

    dso:Presentation a owl:Class ;
        rdfs:label "Presentation" ;
        rdfs:subClassOf dso:DocumentService ;
        rdfs:isDefinedBy <> .

## Interloan

[Interloan]: #interloan

For interloan a document is made accessible mediated by another institution.

    dso:Interloan a owl:Class ;
        rdfs:label "Interloan" ;
        rdfs:subClassOf dso:DocumentService ;
        rdfs:isDefinedBy <> .

## OpenAccess

[OpenAccess]: #openaccess

An Open Access service implies to free accessibility of a document without any
restrictions by the service provider (Open Access or free copies).

    dso:OpenAccess a owl:Class ;
        rdfs:label "OpenAccess" ;
        rdfs:subClassOf dso:DocumentService ;
        rdfs:isDefinedBy <> .


## Digitization

[Digitization]: #digitization

A digitization [DocumentService] creates a digital document from a physical
document, for instance a digital photograph or a 3D-scan of a physical object.

*This class is just a suggestion!*


## Identification

A service to identify a document that is only known with limited properties
(e.g. only parts of the title). In RDF such document is typically expressed by
a blank node.

*This class is experimental!*

# Properties

## hasDocument

[hasDocument]: #hasDocument

Relates a [DocumentService] to a document. The relation is rather lax as it
only tells that a specific document is somehow involved in a specific document
service.  To express more specific relations, one should define and use
sub-properties, such as [daia:availableFor] and [daia:unavailableFor].

    dso:hasDocument a owl:ObjectProperty ;
        rdfs:label "hasDocument" ;
        rdfs:domain dso:DocumentService ;
        owl:inverseOf dso:hasService ;
        rdfs:seeAlso foaf:Document, bibo:Document ;
        rdfs:seeAlso daia:availableFor, daia:unavailableFor ;
        rdfs:isDefinedBy <> .

[daia:availableFor]: http://purl.org/ontology/daia/availableFor 
[daia:unavailableFor]: http://purl.org/ontology/daia/unavailableFor 

## hasService

[hasService]: #hasService

Relates a document to a [DocumentService].

    dso:hasService a owl:ObjectProperty ;
        rdfs:label "hasService" ;
        rdfs:range dso:DocumentService ;
        owl:inverseOf dso:hasDocument ;
        rdfs:seeAlso foaf:Document, bibo:Document ;
        rdfs:seeAlso daia:availableFor, daia:unavailableFor ;
        rdfs:isDefinedBy <> .

# Related ontologies

[related ontologies]: #related-ontologies

The Document Service Ontology is part of a set of micro-ontologies originally
created to describe several aspects of libraries and similar institutions. Some
services defined in DSO have earlier been defined as part of the DAIA ontology,
which now makes use of DSO. The core concept of a service was based on the
definition of a service event in the Simple Service Status Ontology (SSSO), but
broadened to other kinds of services, for instance Products or Offerings as
defined in the GoodRelations vocabulary and in schema.org vocabulary. DSO does
not make formal assumptions about the types of documents. Suitable document
classes are defined in the Bibliographic Ontology, in the FOAF vocabulary and
in schema.org.

# References

## Normative References

* T. Berners-Lee et al.: *Uniform Resource Identifiers (URI): Generic Syntax*.
  August 1998 <http://tools.ietf.org/html/rfc2396>.

## Informative References

* D. Brickley; L. Miller: *FOAF Vocabulary Specification 0.98*.
  August 2010 <http://xmlns.com/foaf/spec/>.

* F. Giasson; B. D'Arcus: *Bibliographic Ontology Specification*.
  November 2009 <http://purl.org/ontology/bibo/>.

* M. Hepp: *GoodRelations Language Reference*.
  October 2011 <http://purl.org/goodrelations/v1>.

* J. Voß: *Document Availability Information API (DAIA)*.
  Work in progress at <http://gbv.github.com/daiaspec/>.

* J. Voß: *Patrons Account Information API*. 2013.
  Work in progress at <http://purl.org/ontology/paia>.

* J. Voß: *Simple Service Status Ontology (SSSO)*.
  February 2013 <http://purl.org/ontology/ssso>.

* *schema.org Vocabulary*. 
  <http://schema.org/>

