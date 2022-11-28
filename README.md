# Hypre

## 1. Abstract

This document provides the specifications and the formal definition for the 
Hypre language.

## 2. Introduction

Hypre is an HTML preprocessor markup language. It provides an easy and fast way
to write HTML via a simpler and cleaner syntax. You can think about it as a mix
of Markdown and HAML. Here an example:

``` HTML
# Hypre # 
= Hypre is an HTML preprocessor markup language =
$section #main {
    = { .truth } It provides an easy and fast way to write HTML =
    $div: $p: $span: Via a simpler and cleaner ** { .enjoy } syntax **
}
---
<h1>Hypre</h1>
<p>Hypre is an HTML preprocessor markup language</p>
<section id="main">
    <p class="truth">It provides an easy and fast way to write HTML</p>
    <div>
        <p>
            <span>Via a simpler and cleaner <strong class="enjoy">syntax</strong></span>
        </p>
    </div>
</section>
```

## 3. Conventions

In all examples in this document white spaces (also called whitespaces) and 
line breaks (also called linebreaks) always matters and sometimes, to be more
clear about the behavior, they are expressed explicitly with a point symbol `‧`
for a single whitespace, and with a leftwards symbol `↩` for a single line 
break. Each example is divided into two sections by three dashes `---`, the 
first section is the Hypre syntax and the second part is generated HTML.

Shorthands notations uses spaces after the opening symbol and before the
closing symbol for block elements (`#‧foo‧#`), meanwhile for inline elements
no spaces are added (`*foo*`).

## 3. Comments

Comments are portions of text that is parsed but does not generate HTML code.
Everything after the exact sequence `/*` and before the exact sequence `*/`
is considered a comment.

``` HTML
/* foo */
---
```

Comment con be on multiple lines:

``` HTML
/* foo
bar
baz */
---
```

## 5. Plain text

TODO

## 7. Attributes

Hypre attributes are an alternative notation to express HTML attributes. There
are four types of attributes: class, id, named attribute and boolean attribute.

Named and boolean attributes are expressed just like regular HTML
attributes, meanwhile classes can be expressed with a dot `.` before the class 
name and ids can be expressed with an hash sign `#` before the id value.
Just like HTML each element can have a single id and multiple classes. Classes
are keep in the original order.

| Attribute         | Hypre      | HTML            | 
| ----------------- | ---------- | --------------- |
| class             | .foo .bar  | class="foo bar" |
| id                | #foo       | id="foo"        |
| named attribute   | foo="bar"  | foo="bar"       |
| boolean attribute | foo        | foo             |

## 7. Elements

Hypre provides three types of notations to generate HTML elements: the standard
notation, the shorthand notation and the special notatiion.

### 7.1 Standard notation

The standard notation let's you generate any HTML elements. All tags are 
expressed by adding a dollar sign `$` in front of the tag name: `div` becomes
`$div`, `p` becomes `$p`.

The opening and closing tags can be expressed in two
different way: if the content of the element spans over multiple lines then
the opening and closing tags are replaced by braces `{` `}`. Elements declared
using the multi line standard notation are called multi line elements.

If the content of the element is in a single line the opening tag is replaced 
by a colon `:` and the closing tag can be omitted. Elements declare using the 
single line standard notation are called single line elements.

#### Multi lines standard notation:

``` HTML
$div { foo }
---
<div>foo</div>
```

#### Single line standard notation:

``` HTML
$div: foo
---
<div>foo</div>
```

#### Structure

| identifier | tag | attributes | opening | content | closing |
| ---------  | --- | ---------- | ------- | ------- | ------- |
| $          | tag | attributes | {       | content | }       |
| $          | tag | attributes | :       | content |         |

### 7.1.1 Attributes

Both multi lines and single lines standard elements can have HTML attributes
and they must be expressed before the opening tag:

``` HTML
$div .foo { bar }
$div .baz: qux
---
<div class="foo">bar</div>
<div class="baz">qux</div>
```

### 7.1.2 Nested elements

Nested elements can be expressed by adding an element inside braces for the
multi line notation:

``` HTML
$div { 
    $p { foo }
}
---
<div><p>foo</p></div>
```

And after the colon for the single line notation:

``` HTML
$div: $p: foo
---
<div><p>foo</p></div>
```

### 7.2 Shorthand notation

The shorthand notation is an alternative notation used to easily generate some 
of the most common elements. It uses dedicated symbol to open and close the 
element, but does not require the tag name, for example: 

``` HTML
## foo ##
---
<h1>foo</h1>
```

### 7.2.1 Attributes

Attributes in the shorthand notations are expressed between braces `{ }` and as
first thing after the opening symbol:

``` HTML
## { .foo #bar } baz ##
---
<h2 class="foo" id="bar">baz</h2>
```

### 7.2.2 Nested elements

In the shorthand notation elements can be nested by nesting an element inside
the content of another one, for example:

``` HTML
= foo *baz* =
---
<p><strong>foo</strong></p>
```

Also standard notation can used inside shorthand elements:

``` HTML
= foo $span { bar } =
---
<p><span>foo</span></p>
```

### 7.2.3 Structure

| opening | attributes opening | attributes | attributes closing | content | closing |
| ------- | ------------------ | ---------- | ------------------ | ------- | ------- |
| #       | {                  | attributes | }                  | content | #       |

### 7.2.4 Reference

#### Headings

``` HTML
# foo #
## bar ##
### baz ###
#### qux ####
---
<h1>foo</h1>
<h2>bar</h2>
<h3>baz</h3>
<h4>qux</h4>
```

#### Paragraph

``` HTML
= foo =
---
<p>foo</p>
```

#### Blockquote

``` HTML
> foo <
---
<blockquote>foo</blockquote>
```

#### Strong

``` HTML
*foo*
---
<strong>foo</strong>
```

#### Emphasis

``` HTML
_foo_
---
<em>foo</em>
```

#### Strikethrough

``` HTML
~foo~
---
<s>foo</s>
```

#### Code

``` HTML
`foo`
---
<code>foo</code>
```

### 7.3 Special notations

Special notations are a set of custom notations used to generate common used
HTML, like lists and tables. Each special notation has its own rules.

### 7.3.1 Links

TODO

### 7.3.2 Images

TODO

### 7.3.3 Lists

TODO

### 7.3.2 Tables

TODO