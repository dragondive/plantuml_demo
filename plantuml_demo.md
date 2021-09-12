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
uml_diagrams:
    - sequence diagram
    - class diagram
common_features:
    - colours
    - openiconic
    - fonts
    - zoom
@endyaml
```

## UML Diagrams

PlantUML draws beautiful UML diagrams from simple textual descriptions. This document gives a demo of the following types of UML diagrams:

* Sequence Diagram
* Class Diagram

### Sequence Diagram

The below sequence diagram describes a workflow of a software developer working on an issue. This demo illustrates a few features:

* A few different participant types
* Encompassing participants in a box
* Autonumbering of steps
* Using divider to split a diagram into logical sections
* Grouping steps
* Delay between steps
* Different arrow types

Refer the [documentation](https://plantuml.com/sequence-diagram) for the full set of features and configuration options.

The demo also introduces the following common features:

* Specifying a title for the diagram
* Defining an object instance using the `as` keyword
* Adding hyperlinks into the diagram
* Placing notes on entities

```plantuml
@startuml
title **Sequence Diagram Demo**\n\n

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
note right: dotted arrows indicate\ncomputer-triggered steps

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

### Class Diagram

The below class diagram describes the relationships between the chess piece types. This demo illustrates a few features:

* Defining an abstract class
* Adding methods and attributes to a class
* Describing access specifiers of the class members
* Describing inheritance relationship between classes
* Hiding sections from the class

Refer the [documentation](https://plantuml.com/class-diagram) for the full set of features and configuration options.

The demo also introduces the following common features:

* The preprocessor directive `!include` to include contents of another file
* Defining a sprite and using it in the diagram
* Using unicode characters in the diagram

```plantuml
@startuml
title **Class Diagram Demo**\n\n

!include sprites/chess_king.puml /' load sprite from file '/
!include sprites/chess_pawn.puml
!include sprites/chess_bishop_rook.puml  /' load file having multiple sprites '/

sprite $chess_piece_colour {  /' define sprite directly in the description '/
    FFFFFFFFFFFFFFFFFF
    F00000000FFFFFFFFF
    F00000000FFFFFFFFF
    F00000000FFFFFFFFF
    F00000000FFFFFFFFF
    F00000000FFFFFFFFF
    F00000000FFFFFFFFF
    F00000000FFFFFFFFF
    F00000000FFFFFFFFF
    FFFFFFFFFFFFFFFFFF
}

abstract class Piece {
    - rank: enum
    - file: enum
    - colour <$chess_piece_colour> : enum
    + move()
    + capture()
    # is_valid_move(starting_square, destination_square): bool
}

class "<$pawn,scale=0.4,color=Black> Pawn" as Pawn { /' include the sprite in class name '/
    - en_passant: bool
    + promote()
}

note left of Pawn::en_passant
    can this pawn
    be captured
    en passant
end note

class "<$king,scale=.4,color=green> King" as King { /' change the sprite color '/
    - in_check: bool
    + castle()
}

class "<size:40><color:red>♕</color></size> Queen" as Queen /' use unicode character in class name '/
class "<size:40>&#9816;</size> Knight" as Knight /' use unicode value in class name'/
class "<$bishop,scale=.5,color=Black> Bishop" as Bishop
class "<$rook,scale=.5,color=Black> Rook" as Rook

Piece <|-- Pawn
Piece <|-- Knight
Piece <|-- Bishop
Piece <|-- Rook
Piece <|-- King
Bishop <|-- Queen
Rook <|-- Queen

hide Queen members
@enduml
```

## Common Features

This section includes demo of the common features that apply to all or multiple diagram types:

* Colours
* OpenIconic
* Fonts
* Zoom

### Colours

The colour can be configured for almost all the entities that appear in PlantUML diagrams. The colour can be specified by its hexadecimal RGB value.

#### Named Colours

PlantUML also defines names for some common colours. These names can be also be used to specify the colour. The `colors` command prints the palette of all the named colours.

```plantuml
@startuml
colors
@enduml
```

#### Similar Colours

The `colors` command can also be called with an argument, which is either a named colour or a hexadecimal RGB colour value. It prints the palette of named colours similar to the specified colour.

```plantuml
@startuml
colors Yellow
@enduml
```

```plantuml
@startuml
colors #ffb36a
@enduml
```

#### Demo

This demo shows the use of various colours in a sequence diagram and a class diagram.

```plantuml
@startuml
title **Sequence Diagram Demo**\n\n

actor Developer as Dev  #Tomato
actor Reviewers

box Development Infrastructure #LightGreen
    participant "Build\nServer" as Build #Azure
    collections "[[https://github.com/dragondive/hebi/issues Tracker]]" as Tracker #PowderBlue
    database "[[https://github.com/dragondive/hebi Repository]]" as Repository #Plum
end box

autonumber 2
...
== Development ==
Dev -[#404032]> Tracker : assign issue to self
Dev -> Dev : work towards solution

... some days later ...
Dev -> Build : submit build job
note left #PeachPuff : when solution is ready
Build --> Dev : build successful
note right: dotted arrows indicate\ncomputer-triggered steps

== Review ==
Dev ->  Reviewers : [[https://github.com/dragondive/hebi/compare submit pull request]]
alt #MediumSpringGreen approved
    Reviewers -> Dev : approve changes
else #LightSalmon rejected
    loop #AntiqueWhite
        Dev <- Reviewers : review comments
        Dev -> Reviewers : submit changes
    end loop
end alt
...

@enduml
```

<br><br>

```plantuml
@startuml
title **Class Diagram Demo**\n\n
!include sprites/chess_king.puml /' load sprite from file '/
!include sprites/chess_pawn.puml
!include sprites/chess_bishop_rook.puml  /' load file having multiple sprites '/

sprite $chess_piece_colour {  /' define sprite directly in the description '/
    FFFFFFFFFFFFFFFFFF
    F00000000FFFFFFFFF
    F00000000FFFFFFFFF
    F00000000FFFFFFFFF
    F00000000FFFFFFFFF
    F00000000FFFFFFFFF
    F00000000FFFFFFFFF
    F00000000FFFFFFFFF
    F00000000FFFFFFFFF
    FFFFFFFFFFFFFFFFFF
}

abstract class Piece #WhiteSmoke {
    - rank: enum
    - file: enum
    - colour <$chess_piece_colour> : enum
    + move()
    + capture()
    # is_valid_move(starting_square, destination_square): bool
}

class "<$pawn,scale=0.4,color=Black> Pawn" as Pawn #D0D0FF { /' include the sprite in class name '/
    - en_passant: bool
    + promote()
}

note left of Pawn::en_passant
    can this pawn
    be captured
    en passant
end note

class "<$king,scale=.4,color=green> King" as King { /' change the sprite color '/
    - in_check: bool
    + castle()
}

class "<size:40><color:red>♕</color></size> Queen" as Queen #Gold /' use unicode character in class name '/
class "<size:40>&#9816;</size> Knight" as Knight /' use unicode value in class name'/
class "<$bishop,scale=.5,color=Black> Bishop" as Bishop
class "<$rook,scale=.5,color=Black> Rook" as Rook

Piece <|-- Pawn
Piece <|-[#Green]- Knight
Piece <|-- Bishop
Piece <|-- Rook
Piece <|-[#Indigo]- King
Bishop <|-- Queen
Rook <|-- Queen

hide Queen members
@enduml
```

### OpenIconic

The open source icon set OpenIconic can be used in diagrams using the syntax `<&icon_name>`. The `listopeniconic` command lists the available icons.

```plantuml
@startuml
listopeniconic
@enduml
```

#### Demo

```plantuml
@startuml

:<size:32>**Developers <&monitor><&tablet><&phone> of the world <&globe>, unite! <&people><&people>**</size> ;
@enduml
```

### Fonts

The font can be configured for almost all the text that appears in PlantUML diagrams. The `listfonts` command lists all the fonts available on the system.

```plantuml
@startuml
listfonts
@enduml
```

#### Demo

This demo shows the customization of font used in a sequence diagram.

The demo also introduces the following common features:

* Customizing the diagram using the `skinparam` command

```plantuml
@startuml
skinparam DefaultFontName Courier New
skinparam DefaultFontSize 16
"Brian Kernighan" -> Developers : main( ) {\n        printf(“hello, world”);\n}
note right : [[https://ozanerhansha.medium.com/on-the-origin-of-hello-world-61bfe98196d5 On the Origin of "Hello, World!"]]
@enduml
```

### Zoom

The generated image can be zoomed in or out by specifying a scaling factor.

This demo shows the use of `scale` command to enlarge the image.

The demo also introduces the following common features:

* PlantUML's preprocessor functionalities

```plantuml
@startuml
/' computes the factorial of the given integer. '/
!function $factorial($n)
    /' Return value of this function is memoized because it uses recursion. PlantUML preprocessor doesn't provide dictionary or array data structure, hence a "hack" simulates a dictionary. For every input integer, a variable is created with the stringized integer as its name, and the return value is assigned to it. Thus, the variable's name serves as the "key". '/
    !if %variable_exists(%string($n))
        !return %get_variable_value(%string($n))
    !endif

    !if $n == 0
        !$value = 1
    !else
        !$value = $n * $factorial($n - 1)
    !endif

    %set_variable_value(%string($n), $value)
    !return $value
!endfunction

!procedure $factorial_question_answer_sequence(\
        $starting_number = 0,\
        $ending_number = 12,\
        $color_number_in_question = blue,\
        $color_number_in_answer = green)
    skinparam SequenceMessageAlignment direction
    !$number = $starting_number
    !while $number <= $ending_number
        Question -> Answer : What is factorial of <color:$color_number_in_question>**$number**</color>?
        Question <- Answer : Factorial of <color:$color_number_in_question>**$number**</color> is <color:$color_number_in_answer>**$factorial($number)**</color>.
        |||
        !$number = $number + 1
    !endwhile
!endprocedure

scale 1.5 /' zooms the generated diagram per specified scaling factor '/
$factorial_question_answer_sequence(\
    $color_number_in_answer = darkviolet, $color_number_in_question = red\
)
@enduml
```
