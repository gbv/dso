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

The current version of this ontology is a draft for open discussion.
[Feedback](https://github.com/gbv/dso/issues) is welcome!

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

    @prefix bibo:    <http://purl.org/ontology/bibo/> .
    @prefix cc:      <http://creativecommons.org/ns#> .
    @prefix daia:    <http://purl.org/ontology/daia/> .
    @prefix dct:     <http://purl.org/dc/terms/> .
    @prefix foaf:    <http://xmlns.com/foaf/0.1/> .
    @prefix gr:      <http://purl.org/goodrelations/v1#> .
    @prefix owl:     <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs:    <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix schema:  <http://schema.org/> .
    @prefix service: <http://purl.org/ontology/service#> .
    @prefix ssso:    <http://purl.org/ontology/ssso#> .
    @prefix vann:    <http://purl.org/vocab/vann/> .
    @prefix voaf:    <http://purl.org/vocommons/voaf#> .
    @prefix vs:      <http://www.w3.org/2003/06/sw-vocab-status/ns#> .
    @prefix xsd:     <http://www.w3.org/2001/XMLSchema#> .

The Document Service Ontology (DSO) is defined in RDF/Turtle as following:

    <> a owl:Ontology, voaf:Vocabulary ;
        dct:title "Document Service Ontology" ;
        rdfs:label "DSO" ;
        vann:preferredNamespacePrefix "dso" ;
        vann:preferredNamespaceUri "http://purl.org/ontology/dso#" ;
        dct:description "A micro-ontology that defines a set of typical document-related services such as provided by libraries, museums and archives."@en ; 
        dct:modified "{GIT_REVISION_DATE}"^^xsd:date ;
        owl:versionInfo "{VERSION}" ;
        cc:license <http://creativecommons.org/licenses/by/3.0/> ;
        dct:creator "Jakob Voß" 
    .

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

# DocumentService

[DocumentService]: #documentservice
[Service]: http://dini-ag-kim.github.io/service-ontology/service.html#Service

A document service is a kind of [Service], as defined in the [Service
Ontology], that is somehow related to one or more documents. To indicate the
specific type of document service, one should use a subclass of this class and
assing additional service types, such as [ssso:ServiceEvent] from the Simple
Service Status Ontology, [schema:Offer] or [schema:Product] from schema.org
vocabulary, and [gr:Offering] or [gr:ProductOrService] from GoodRelations
vocabulary.

    dso:DocumentService a owl:Class ;
        rdfs:label "DocumentService"@en ;
        rdfs:subClassOf service:Service ;
        rdfs:isDefinedBy <> ;
        rdfs:seeAlso ssso:ServiceEvent, gr:Offering, schema:Offer ;
        vs:term_status "testing" .

[service:Service]: http://purl.org/ontology/service#Service
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
        rdfs:label "Loan"@en ;
        rdfs:subClassOf dso:DocumentService ;
        rdfs:isDefinedBy <> ;
        vs:term_status "testing" .

## Presentation

[Presentation]: #presentation

A presentation [DocumentService] involves the display or similar usage of a
document in a restricted environment, e.g.  within the rooms or in the intranet
of a library or museum.

    dso:Presentation a owl:Class ;
        rdfs:label "Presentation"@en ;
        rdfs:subClassOf dso:DocumentService ;
        rdfs:isDefinedBy <> ;
        vs:term_status "testing" .

## Interloan

[Interloan]: #interloan

For an interloan [DocumentService] a document is made accessible mediated by
another institution.

    dso:Interloan a owl:Class ;
        rdfs:label "Interloan"@en ;
        rdfs:subClassOf dso:DocumentService ;
        rdfs:isDefinedBy <> ;
        vs:term_status "testing" .

## OpenAccess

[OpenAccess]: #openaccess

An Open Access [DocumentService] implies to free accessibility of a document
without any restrictions by the service provider (Open Access or free copies).

    dso:OpenAccess a owl:Class ;
        rdfs:label "OpenAccess"@en ;
        rdfs:subClassOf dso:DocumentService ;
        rdfs:isDefinedBy <> ;
        vs:term_status "testing" .


## Digitization

[Digitization]: #digitization

A digitization [DocumentService] creates a digital document from a physical
document, for instance a digital photograph or a 3D-scan of a physical object.

    dso:Digitization a owl:Class ;
        rdfs:label "Digitization"@en ;
        rdfs:subClassOf dso:DocumentService ;
        rdfs:isDefinedBy <> ;
        vs:term_status "unstable" .

*This class is experimental!*

## Identification

A service to identify a document that is only known with limited properties
(e.g. only parts of the title). In RDF such document is typically expressed by
a blank node.

*This class is just a suggestion!*

# Properties

## hasDocument

[hasDocument]: #hasDocument

Relates a [DocumentService] to a document. The relation is rather lax as it
only tells that a specific document is somehow involved in a specific document
service.  To express more specific relations, one should define and use
sub-properties, such as [daia:availableFor] and [daia:unavailableFor].

    dso:hasDocument a owl:ObjectProperty ;
        rdfs:label "hasDocument"@en ;
        rdfs:domain dso:DocumentService ;
        owl:inverseOf dso:hasService ;
        rdfs:seeAlso foaf:Document, bibo:Document ;
        rdfs:seeAlso daia:availableFor, daia:unavailableFor ;
        rdfs:isDefinedBy <> ;
        vs:term_status "testing" .

[daia:availableFor]: http://purl.org/ontology/daia/availableFor 
[daia:unavailableFor]: http://purl.org/ontology/daia/unavailableFor 

## hasService

[hasService]: #hasService

Relates a document to a [DocumentService].

    dso:hasService a owl:ObjectProperty ;
        rdfs:label "hasService"@en ;
        rdfs:range dso:DocumentService ;
        owl:inverseOf dso:hasDocument ;
        rdfs:seeAlso foaf:Document, bibo:Document ;
        rdfs:seeAlso daia:availableFor, daia:unavailableFor ;
        rdfs:isDefinedBy <> ;
        vs:term_status "testing" .

# Related ontologies

[related ontologies]: #related-ontologies

The Document Service Ontology is part of a set of micro-ontologies originally
created to describe several aspects of libraries and similar institutions. Some
services defined in DSO have earlier been defined as part of the DAIA ontology,
which now makes use of DSO. The core concept of a service was first based on
the definition of a service event in the Simple Service Status Ontology (SSSO),
but broadened to the class [service:Service] which includes any kinds of
services, for instance Products or Offerings as defined in the GoodRelations
vocabulary and in Schema.org vocabulary. DSO does not make formal assumptions
about the types of documents. Suitable document classes are defined in the
Bibliographic Ontology, in the FOAF vocabulary and in Schema.org Vocabulary.

# References

## Normative References

* T. Berners-Lee et al.: *Uniform Resource Identifiers (URI): Generic Syntax*.
  August 1998 <http://tools.ietf.org/html/rfc2396>.

* J. Voß: *The Service Ontology*.
  December 2013 <http://purl.org/ontology/service>.

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

[Service Ontology]: http://dini-ag-kim.github.io/service-ontology/
