This document is based on https://ocaml-doc.github.io/odoc-parser/Odoc_parser/Loc/index.html

Locations in files.

This module concerns locations in source files, both points indicating a specific
    character and spans between two points.

## Basic types

<a id="point"></a>
Record type `point`

  - `line : int`
  - `column : int`

A specific character

<a id="span"></a>
Record type `span`

  - `file : string`
  - `start :` [point][]
  - `end_ :` [point][]

A range of characters between `start` and `end_` in a particular file

`val span :` [span][] `list ->` [span][]

`span spans` takes a list of spans and returns a single [span][] starting at the start of the first span and ending at the end of the final span

`val nudge_start : int ->` [span][] `->` [span][]

This adjusts only the column number, implicitly assuming that the offset does not move the location across a newline character.

## Located values

<!-- ##### Record type `+'a with_location` {#with_location} -->
<a id="with_location"></a>

  - `location :` [span][]
  - `value : 'a`

Describes values located at a particular span

`val at :` [span][] `list  -> 'a -> 'a` [with_location][]

Constructor for [with_location][]

`val value : 'a` [with_location][] `-> 'a`

Returns the location of ta located value

`val map : ( 'a -> b ) -> 'a` [with_location][] `-> 'b` [with_location][]

Map over a located value without changing its location

`val same : _` [with_location][] `-> 'b -> 'b` [with_location][]

`same x y` returns the value y wrapped in a [with_location][] whose location is that of `x`

[point]: #point
[span]: #span
[with_location]: #with_location
