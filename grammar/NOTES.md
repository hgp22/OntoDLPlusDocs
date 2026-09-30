# Grammar reconstruction notes

`OntoDLPlus.g4` is a **syntactic** ANTLR 4 grammar transcribed from Alexandre Costa Dias, *ONTODL+: an ontology description language and its compiler* (University of Minho, 2021, [hdl.handle.net/1822/81340](https://hdl.handle.net/1822/81340)), with surface keywords taken from the compiler examples on the [official site](https://epl.di.uminho.pt/~gepl/GEPL_DS/OntoDL/) when those examples disagree with a thesis listing.

It is not the original compiler grammar. Semantic actions and the Java package `ontodlp` are omitted on purpose.

## Copied from thesis listings

| Listing | Content |
| --- | --- |
| 3.1 | Start symbol `ontologia`: `'Ontologia'` name, `conceitos`, optional `individuos`, `relacoes`, `triplos`, `'.'` |
| 3.2 | `conceitos` / `conceito` / inline `atributos` / `atributo` with `name : type` |
| 3.3 | `individuos` with `TEXT TEXT?` (the unused second `TEXT` is kept) |
| 3.4 | `relacoes` as a comma-separated name list |
| 3.5 | `triplos` / `triplo` with built-in `iof`/`instancia`, `pof`/`parte`, `is-a`/`subclasse`, `synonym`/`sinonimo`, plus a free relation name; instance attributes `name = value` |
| 5.1 | Same triple forms with lexer tokens `IOF`, `POF`, `ISA`, `SYN` |
| 5.2 | Triple grouping: `left =[ relacionamentos (';' relacionamentos)* ']'` and `relMultiplo` |
| 5.3 | Relation details: `domain`, `codomain`, `props`, and the closed property set (`simple`, `entire`, `injective`, `surjective`, `representation`, `function`, `abstraction`, `injection`, `surjection`, `bijection`, `inverseOf=`) |

Listing 5.3 prints `{` and `}` as damaged PDF glyphs (`–` / `˝`). Those tokens are restored as braces, matching listing 3.4 and the published examples.

## Reconstructed from examples (no ANTLR productions in the thesis)

These rules are inferred from listings 4.4, 4.6, 5.5, 5.6, 5.7, and 7.9, and from the official examples page.

- Optional `atributos` / `attributes` section before `conceitos`. Attribute types are required there. In the concepts section, a previously declared attribute may appear by name only (`ConcA [attribA, attribC : string]` in listing 5.5).
- Optional `restrictions` section after `triplos`. Head `:-` body `.` with `,` as conjunction, `;` as disjunction, parentheses, `==`, `\=`, and `not(...)`.
- File inclusion: `expand filename.odlp;` inside a section. Listing 5.6 writes `expands <file.name>;`. The published compiler examples use `expand`, which is what this grammar accepts.
- Optional `=>` before a grouped right-hand side (`relMultiplo`). Listing 5.2 allows only `TEXT`; the official examples page writes `=> lig-brg-gmr` on continuation lines.
- `enum (...)` types, from listing 5.7.
- Inverse keyword: thesis listings use `inverseOf`; the official examples page uses `inversaDe`. Both are accepted.

## Keyword policy

Portuguese section names from listings 3.1–3.5 remain the base language: `Ontologia`, `conceitos`, `individuos`, `relacoes`, `triplos`.

English names that actually appear in implemented listings are accepted as aliases:

- `attributes` (listing 5.5)
- `concepts` (listings 5.5 and 5.7)
- `relations` (listing 5.7)
- `restrictions` (listings 4.4 and 7.9)

Section 4.2.3 proposes further aliases (`classes`, `properties`, `triples`, and English `individuals`). Those words do not appear in the implemented listings, so they are not added here.

## Lexer (not printed in the thesis)

The thesis never shows the `TEXT` lexer rule. It does mention a dedicated comment token. The lexer below is therefore reconstructed:

- `TEXT`: letters (including Latin-1), digits, underscore, hyphen
- `STRING`: double- or single-quoted text, as used in the published examples
- `NUMBER`: integers, as used in `enum` ranges
- `//` line comments and `/* */` block comments
- Whitespace skipped

## Deliberately omitted

- All ANTLR semantic actions and inherited/returned attributes (listings 3.7 and following)
- The Java package `ontodlp` (`Ontology`, `Triple`, `Concept`, `Restriction`, `DataProperty`, `SemError`, `Relation`)
- Preprocessor behaviour beyond recognising `expand` (the compiler splices files into a temporary specification before parsing)
