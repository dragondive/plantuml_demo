# PlantUML demo ... and other useful stuff

## Data Visualization

PlantUML can _also_ be used to visualize data written in various data representation formats. This document gives a demo of visualization for the following formats:

* YAML: YAML Ain't Markup Language

### YAML Data Visualization

The below demo has the table of contents of this document written in YAML. To create a visual representation with PlantUML, enclose the YAML data within `@startyaml` and `@endyaml`. This YAML data visualization is one of the PlantUML demos, making it an example of self-reference. :grin:

_Note_: PlantUML's YAML support is limited. It doesn't recognize several valid YAML constructs. For example, it considers [YAML's homepage](https://yaml.org/), written in YAML, as invalid YAML.

Refer the [documentation](https://plantuml.com/yaml) for the full set of features and configuration options.

The demo also introduces the following common features:

* Customizing the diagram using `<style>`
* Single line comment using `'`
    * Should be placed on its own separate line, otherwise it is parsed as continuation of the preceding text (unlike `//` comments of C, C++, and Java)
* Multiline comment using `/' ... '/`
    * Can be used anywhere, including on a line having the diagram description
* Use of the lightweight markup language creole

```plantuml
@startyaml
<style>
yamlDiagram {
    node {
        ' use a constant width font because that's what developers do.
        FontName Consolas
        FontSize 20
    }
}
</style>

/'TODO:
It would be cool to hyperlink the entries in the table_of_contents to the
respective section in the document. Not only would it further accentuate the
[Medium Awareness](https://tvtropes.org/pmwiki/pmwiki.php/Main/MediumAwareness)
of this yaml document, but also augment the
[Anachronic Order](https://tvtropes.org/pmwiki/pmwiki.php/Main/AnachronicOrder)
of the outer markdown document.
'/

**table_of_contents**: ""  /' workaround: empty string here to avoid dummy link '/
data_visualization:
    yaml_data : table_of_contents //(this!)//
@endyaml
```
