# OntoDL+

OntoDL+ is a domain-specific language for writing ontologies and translating them to OWL, DOT, Alloy, and Prolog. Alexandre Costa Dias created it at the University of Minho in 2021, extending OntoDL, under the guidance of Pedro Rangel Henriques and Cristiana Esteves Araújo.

This repository holds:

1. A reconstructed syntactic grammar, transcribed from the master's thesis
2. A Hugo documentation site for the language

It does **not** contain the compiler. The authors published a JAR, not the Java sources, and they did not attach a software license to that download. Use the official package:

```text
java -jar OntoDL.jar <targetfile>
```

Java 16 or newer is required. Get the JAR, template, and examples from the [official download page](https://epl.di.uminho.pt/~gepl/GEPL_DS/OntoDL/download.html).

## Credits

See [NOTICE.md](NOTICE.md) for the full attribution.

- **Author:** Alexandre Costa Dias
- **Advisors:** Pedro Rangel Henriques, Cristiana Esteves Araújo
- **Thesis:** [ONTODL+: an ontology description language and its compiler](https://hdl.handle.net/1822/81340) (University of Minho, 2021)
- **Project site:** [GEPL / OntoDL+](https://epl.di.uminho.pt/~gepl/GEPL_DS/OntoDL/)

## License

The contents of this repository are licensed under [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/). That follows the license of the thesis from which the grammar is adapted. Commercial use is not allowed.

The [Hugo Book](https://github.com/alex-shpak/hugo-book) theme is MIT-licensed and stays under that license.

## Grammar

The ANTLR 4 grammar is [grammar/OntoDLPlus.g4](grammar/OntoDLPlus.g4). It is a syntactic reconstruction: it has no semantic actions and no Java package. [grammar/NOTES.md](grammar/NOTES.md) records which thesis listings were used and which rules had to be inferred.

## Documentation site

The site is a Hugo project using the Book theme (Hugo 0.158 or newer), in English and European Portuguese. The root page picks Portuguese when the browser language is Portuguese (`pt`, `pt-PT`, `pt-BR`, …) and English otherwise. After cloning, load the theme submodule and serve:

```sh
git submodule update --init
hugo server
```

If `hugo version` reports an older build, use a current Homebrew install (`brew install hugo`). Preview at <http://localhost:1313/>.

Set `baseURL` in [hugo.yaml](hugo.yaml) when you publish the site.
