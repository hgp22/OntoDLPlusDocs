---
title: Linguagem
weight: 10
---

# Linguagem

Um ficheiro OntoDL+ começa por `Ontologia` e um nome, segue uma sequência fixa de secções e termina com um ponto. A secção `individuos` é opcional. O OntoDL+ também permite uma secção `atributos` antes dos conceitos e uma secção `restrictions` depois dos triplos.

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

Os nomes reservados das secções na linguagem original estão em português. As relações incorporadas são bilingues: `iof` / `instancia`, `pof` / `parte`, `is-a` / `subclasse`, `synonym` / `sinonimo`.

## Atributos

A mesma propriedade de dados pode ser tipada uma vez na secção `atributos` (ou `attributes`) e depois listada pelo nome em cada conceito. O tipo ainda pode ser indicado em linha, como na OntoDL.

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

A listagem 5.7 da tese também mostra tipos enumerados: `enum (3, 7, 12)` ou `enum ('real', 'fiction')`.

## Agrupamento de triplos

Os triplos que partilham o lado esquerdo podem escrever-se uma só vez. As relações que partilham esse lado esquerdo também podem partilhar uma lista à direita.

```text
triplos {
  duna =[
    iof => Livro [titulo="Duna"];
    escritoPor => herbert
  ]
} .
```

## Propriedades das relações

Uma relação pode declarar `domain`, `codomain` e um conjunto fechado de propriedades. As declarações de inversa podem escrever-se `inverseOf` (tese) ou `inversaDe` (exemplos oficiais).

```text
relacoes {
  escritoPor[domain: Livro, codomain: Autor],
  escreveu[domain: Autor, codomain: Livro, props: inversaDe=escritoPor]
}
```

Propriedades permitidas: `simple`, `entire`, `injective`, `surjective`, `representation`, `function`, `abstraction`, `injection`, `surjection`, `bijection`, e `inverseOf` / `inversaDe`.

## Inclusão de ficheiros

`expand` insere outro ficheiro numa secção. A listagem da tese escreve `expands`; os exemplos publicados usam `expand`.

```text
conceitos {
  expand conceitos.odlp;
}
```

## Restrições

A secção opcional `restrictions` destina-se ao Prolog. Cada regra tem uma cabeça, `:-`, um corpo e um `.` final. Nesta secção, `,` significa *e* e `;` significa *ou*; a conjunção liga mais fortemente do que a disjunção.

```text
restrictions {
  L = escritoPor => A :- L = iof => Livro, A = iof => Autor.
} .
```

## Nomes de secção em inglês

As listagens da tese usam `attributes`, `concepts`, `relations` e `restrictions` a par dos nomes em português. Esses alias fazem parte da gramática reconstruída. Outros nomes propostos na tese (`classes`, `properties`, `triples`) não são tratados como sintaxe aqui, porque não aparecem nas listagens implementadas.
