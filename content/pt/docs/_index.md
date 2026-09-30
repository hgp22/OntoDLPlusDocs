---
title: Introdução
weight: 1
bookFlatSection: true
---

# OntoDL+

O OntoDL+ é uma linguagem de domínio específico para escrever ontologias com uma sintaxe compacta, organizada por secções. A linguagem original, OntoDL, já agrupava as declarações em conceitos, indivíduos, relações e triplos. O OntoDL+ mantém essa estrutura e acrescenta secções opcionais e atalhos para que a mesma ontologia se possa escrever com menos repetição.

O compilador, quando a especificação não tem erros, traduz a ontologia para:

- **OWL** (RDF/XML), para ferramentas como o Protégé
- **DOT**, para desenhos em grafo
- **Alloy**, para verificação estática de modelos de conceitos e relações
- **Prolog**, para consultas e para verificar a secção opcional de restrições

É necessário Java 16 ou posterior:

```text
java -jar OntoDL.jar <targetfile>
```

O JAR, um modelo e ontologias de exemplo são publicados pelos autores no [sítio GEPL do OntoDL+](https://epl.di.uminho.pt/~gepl/GEPL_DS/OntoDL/download.html). Este repositório não redistribui esse compilador.

O OntoDL+ permanece compatível com a OntoDL: as novas construções são opcionais, e um ficheiro OntoDL continua a ser um ficheiro OntoDL+ válido.
