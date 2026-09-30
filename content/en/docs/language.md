---
title: Language
weight: 10
---

# Language

An OntoDL+ file starts with `Ontologia` and a name, then a fixed sequence of sections, and ends with a period. `individuos` is optional. OntoDL+ also allows an `atributos` section before the concepts and a `restrictions` section after the triples.

```text
Ontologia biblioteca

conceitos {
  Livro[titulo:string, ano:string],
  Autor[nome:string]
}

individuos {
  duna, herbert
}

relacoes {
  escritoPor
}

triplos {
  duna = iof => Livro [titulo="Duna", ano="1965"];
  herbert = iof => Autor [nome="Frank Herbert"];
  duna = escritoPor => herbert
} .
```

Reserved section names in the original language are Portuguese. Built-in relations are bilingual: `iof` / `instancia`, `pof` / `parte`, `is-a` / `subclasse`, `synonym` / `sinonimo`.

## Attributes

The same data property can be typed once in an `atributos` (or `attributes`) section and then listed by name on each concept. A type may still be given inline, as in OntoDL.

```text
atributos {
  titulo:string,
  nome:string
}

conceitos {
  Livro[titulo],
  Autor[nome]
}
```

Listing 5.7 in the thesis also shows enumerated types: `enum (3, 7, 12)` or `enum ('real', 'fiction')`.

## Triple grouping

Triples that share a left-hand side can be written once. Relations that share that left-hand side can share a right-hand list as well.

```text
triplos {
  duna =[
    iof => Livro [titulo="Duna"];
    escritoPor => herbert
  ]
} .
```

## Relation properties

A relation may declare `domain`, `codomain`, and a closed set of properties. Inverse declarations can be written `inverseOf` (thesis) or `inversaDe` (official examples).

```text
relacoes {
  escritoPor[domain: Livro, codomain: Autor],
  escreveu[domain: Autor, codomain: Livro, props: inversaDe=escritoPor]
}
```

Allowed properties: `simple`, `entire`, `injective`, `surjective`, `representation`, `function`, `abstraction`, `injection`, `surjection`, `bijection`, and `inverseOf` / `inversaDe`.

## File inclusion

`expand` splices another file into a section. The thesis listing writes `expands`; the published examples use `expand`.

```text
conceitos {
  expand conceitos.odlp;
}
```

## Constraints

The optional `restrictions` section is aimed at Prolog. Each rule has a head, `:-`, a body, and a terminating `.`. In this section `,` means *and* and `;` means *or*; conjunction binds tighter than disjunction.

```text
restrictions {
  L = escritoPor => A :- L = iof => Livro, A = iof => Autor.
} .
```

## English section names

Listings in the thesis use `attributes`, `concepts`, `relations`, and `restrictions` alongside the Portuguese names. Those aliases are part of the reconstructed grammar. Further names proposed in the thesis (`classes`, `properties`, `triples`) are not treated as syntax here, because they do not appear in the implemented listings.
