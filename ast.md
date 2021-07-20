This document is based on https://ocaml-doc.github.io/odoc-parser/Odoc_parser/Ast/index.html

Abstract syntax tree representing ocamldoc comments

This is a syntactic representation of ocamldoc comments. See The [manual][] for a detailed description of the syntax understood. Note that there is no attempt at semantic analysis, and hence these types are capable of representing values that will be rejected by further stages, for example, invalid references or headings that are out of range.

<a id="with_location"></a>
`type 'a with location = 'a` <a href="loc.md#with_location">Loc.with_location</a>

<a id="style"></a>
Variant type `style`

  - `` `Bold``
  - `` `Italic``
  - `` `Emphasis ``
  - `` `Superscript``
  - `` `Subscript``

<a id="reference_kind"></a>
Variant type `reference_kind`

  - `` `Simple ``
  - `` `With_text ``

References in doc comments can be of two kinds: `{!Simple}` or `{{!ref}With_text}`

<a id="inline_element"></a>
Variant type `inline_element`

  - `` `Space of string ``
  - `` `Word of string ``
  - `` `Code_span of string ``
  - `` `Raw_markup of string option * string ``
  - `` `Styled of`` [style][] `*` [inline_element][] [with_location][] `list`
  - `` `Reference of `` [reference_kind][] `*` `string` [with_location][] `*` [inline_element][] [with_location][] `list`
  - `` `Link of string `` `*` [inline_element][] [with_location][] `list`

Inline elements are equivalent to what would be found in a `span` in HTML. Mostly these are straightforward. The `` `Reference `` constructor takes a triple whose second element is the reference itself, and the third the replacement text. Similarly the `` `Link `` constructor has the link itself as first parameter and the second is the replacement text.

<a id="nested_block_element"></a>
Variant type `nestable_block_element`

  - `` `Paragraph of `` [inline_element][] [with_location][] `list`
  - `` `Code_block of string `` [with_location][] `list`
  - `` `Verbatim of string ``
  - `` Modules of stirng`` [with_location][] `list`
  - `` `List of [ `Unordered | `Ordered ] * [ `Light | `Heavy ] * `` [nested_block_element][] [with_location] `list list`

Some block elements may be nested within lists or tags, but not all. The `` `List `` constructor has a parameter of type `` [`Light | `Heavy] ``. This corresponds to the syntactic constructor used (see the [manual][] ).

[manual]: https://ocaml.org/releases/4.12/htmlman/ocamldoc.html
[style]: #style
[with_location]: #with_location
[inline_element]: #inline_element
[reference_kind]: #reference_kind
[nested_block_element]: #nested_block_element
