---
title: Introduction
weight: 1
bookFlatSection: true
---

# OntoDL+

OntoDL+ is a domain-specific language for writing ontologies in a compact, sectioned syntax. The original language, OntoDL, already grouped declarations into concepts, individuals, relations, and triples. OntoDL+ keeps that structure and adds optional sections and shorthand so the same ontology can be written with less repetition.

The compiler, when a specification has no errors, translates the ontology to:

- **OWL** (RDF/XML), for tools such as Protégé
- **DOT**, for graph drawings
- **Alloy**, for static model checking of concepts and relations
- **Prolog**, for querying and for checking the optional constraints section

Java 16 or newer is required:

```text
java -jar OntoDL.jar <targetfile>
```

The JAR, a template, and example ontologies are published by the authors at the [GEPL OntoDL+ site](https://epl.di.uminho.pt/~gepl/GEPL_DS/OntoDL/download.html). This repository does not redistribute that compiler.

OntoDL+ remains compatible with OntoDL: the new constructs are optional, and an OntoDL file is still a valid OntoDL+ file.
