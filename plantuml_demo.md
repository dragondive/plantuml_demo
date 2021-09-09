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
uml_diagrams:
  - sequence diagram
@endyaml
```

## UML Diagrams

PlantUML draws beautiful UML diagrams from simple textual descriptions. This document gives a demo of the following types of UML diagrams:
* Sequence Diagram

### Sequence Diagram

The below sequence diagram describes a workflow of a software developer working on an issue. This illustrates a few features:
* A few different participant types
* Encompassing participants in a box
* Autonumbering of steps
* Using divider to split a diagram into logical sections
* Grouping steps
* Delay between steps
* Label on steps
* Different arrow types

Refer the [documentation](https://plantuml.com/sequence-diagram) for the full set of features and configuration options.

The example also introduces the following features:
* The `as` keyword to define an object alias
* Adding hyperlinks into the diagram

```plantuml
@startuml
title **Sequence Diagram Example**\n\n

actor Developer as Dev
actor Reviewers

box Development Infrastructure
  participant "Build\nServer" as Build
  collections "[[https://github.com/dragondive/hebi/issues Tracker]]" as Tracker
  database "[[https://github.com/dragondive/hebi Repository]]" as Repository
end box

autonumber
== Initial Setup ==
Dev -> Repository : clone repository

== Development ==
Dev -> Tracker : assign issue to self
Dev -> Dev : work towards solution

... some days later ...
Dev -> Build : submit build job
note left: when solution is ready
Build --> Dev : build successful
note left: dotted arrows indicate\ncomputer-triggered steps

== Review ==
Dev ->  Reviewers : [[https://github.com/dragondive/hebi/compare submit pull request]]
alt approved
  Reviewers -> Dev : approve changes
else rejected
  loop
    Dev <- Reviewers : review comments
    Dev -> Reviewers : submit changes
  end loop
end alt
== Release ==
Dev -> Build : submit for pre-release check
Build --> Repository : merge changes
note left: build failure scenario\nomitted to reduce clutter.
Repository --> Tracker : close issue
note right: for simplicity, assume\nno merge conflicts.
@enduml
```
