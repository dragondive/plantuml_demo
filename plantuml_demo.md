# PlantUML demo ... and other useful stuff

## Data Visualization

PlantUML can _also_ be used to visualize data written in various data representation formats. This document gives a demo of visualization for the following formats:
* YAML: YAML Ain't Markup Language

### YAML Data Visualization

The below demo has the table of contents of this document written in YAML. To create a visual representation with PlantUML, enclose the YAML data within `@startyaml` and `@endyaml`. This YAML data visualization is one of the PlantUML demos, making it an example of self-reference. :grin:

_Note_: PlantUML's YAML support is limited. It doesn't recognize several valid YAML constructs. For example, it considers [YAML's homepage](https://yaml.org/), written in YAML, as invalid YAML.

Refer the [documentation](https://plantuml.com/yaml) for the full set of features and configuration options.

The example also introduces the following features:
* Writing comments in the plantuml description using `/' '/`

```plantuml
@startyaml

<style>
yamlDiagram {
  node {
	FontName Consolas
	FontSize 20
  }
}
</style>

**table_of_contents**:  " " /' workaround: space here to avoid dummy link '/
data_visualization:
  yaml_data : table_of_contents (this!)
@endyaml
```
