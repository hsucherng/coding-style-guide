# Utility Classes





- [Introduction](#introduction)
- [Setup](#setup)
    - [Customisation](#customisation)
- [Class Name Format](#class-name-format)
- [Class List](#class-list)
- [Customisation](#customisation)





## Introduction

Utility Classes are global classes that consistently provide a single, specific style. They function almost like inline styles, except that:

- They are more terse: `display: inline-block` is greatly shortened to `d:ib`.
- Their specificity is much lower than inline styles, forcing us to be much more considerate and deliberate with their use.
- They can be used in a responsive manner. For example, `d:ib@sm` turns the element into an inline-block element only in the `sm` viewport and above.





## Setup

The mixin that generates the utility classes holds all the booleans that will determine what classes are generated in the output. On a brand new project, all utilities should be turned off by being set to `false`, in order to minimise bloat.

Only turn them on when you've determined that you really need that set of utility classes, as once it's turned on, it becomes very unlikely that it can ever be turned off.

### Customisation

Certain utility classes have values that depend solely on its associated variable. For example: the values for `color` will depend solely on the `$colors` variable. Do check these out and customise as needed.





## Class Name Format

Utility Class names are inspired single-handedly from [shed.css](http://tedconf.github.io/shed-css/), which follows this naming scheme:

`LETTER(S):VALUE@MEDIA`

- `LETTER(S)` correspond to the property that it represents. Majority of the time it's the initials of the property name: `bgc` for `background-color`, `c` for `color`, `ta` for `text-align`, and so on.
- `VALUE` is just as it sounds, and is highly dependent on what style is being set. On the whole, it generally breaks into the following:
    - `NUMBER`
        - This is a simplified, arbitrary scaling system that is used for margins, paddings and other sizes. The base number is `1`; it goes *up* by `1` per level, but goes *down* by `0.1` per level. A sample range of this would be `0.8`, `0.9`, `1`, `2`, and `3`.
        - An exception to this is `fw` (`font-weight`), which uses three digits that correspond to the intended weight: `400` for normal, `500` for medium, `600` for semibold, and so on.
    - `LETTER(S)`
        - The letter(s) in this position correspond to the value that it represents: in the case of `ta` (`text-align`), it can have a value of `l`, `c` and `r`, which are `left`, `center` and `right` respectively.
    - `WORD`
        - For certain properties such as those related to colors, we will need to use a proper word that corresponds to one of the keywords setup in its related variable.
- `MEDIA` - this should be a media query to apply the utility class in, e.g. `xs`, `sm`, `lg`. This is optional, and not all utility classes can be appended with a media query.



## Class List

The best way to see what classes are available is to inspect the mixin itself, as we will also need to make sure that the classes are enabled before they can be used. Nevertheless, here's the list of all possible utility classes:

- `bgc:WORD` - Background-color. `WORD` should correspond to a keyword inside the `$colors` variable.
- `bdc:WORD` - Border-color. `WORD` should correspond to a keyword inside the `$colors` variable.
- `b:NUMBER@MEDIA` - Bottom. If the negative equivalent is enabled, you can use it by putting a dash in front of the `NUMBER`.
- `c:WORD` - Color. `WORD` should correspond to a keyword inside the `$colors` variable.
- `cl:LETTER` - Clear.
- `cf` - Clearfix.
- `d:LETTER(S)@MEDIA` - Display.
- `ff:WORD` - Font-family. `WORD` should correspond to a keyword inside the `$font-families` variable.
- `fs:NUMBER@MEDIA` - Font-size. See the `$font-sizes` variable on what numbers are available for use, and what size they correspond to.
    - You can also use `em` instead, e.g. `fs:1.25em`. See the `$font-sizes-em` variable on what ratios are available for use.
- `fs:LETTER` - Font-style.
- `fw:NUMBER` - Font-weight. `NUMBER` here should be the three digit value of the intended weight.
- `fl:LETTER@MEDIA` - Float.
- `l:NUMBER@MEDIA` - Left. If the negative equivalent is enabled, you can use it by putting a dash in front of the `NUMBER`.
- `m:NUMBER@MEDIA` - Margin. If the negative equivalent is enabled, you can use it by putting a dash in front of the `NUMBER`.
- `mt:NUMBER@MEDIA` - Margin-top. If the negative equivalent is enabled, you can use it by putting a dash in front of the `NUMBER`.
- `mr:NUMBER@MEDIA` - Margin-right. If the negative equivalent is enabled, you can use it by putting a dash in front of the `NUMBER`.
- `mb:NUMBER@MEDIA` - Margin-bottom. If the negative equivalent is enabled, you can use it by putting a dash in front of the `NUMBER`.
- `ml:NUMBER@MEDIA` - Margin-left. If the negative equivalent is enabled, you can use it by putting a dash in front of the `NUMBER`.
- `mx:NUMBER@MEDIA` - Margin-left and margin-right. If the negative equivalent is enabled, you can use it by putting a dash in front of the `NUMBER`.
- `my:NUMBER@MEDIA` - Margin-top and margin-bottom. If the negative equivalent is enabled, you can use it by putting a dash in front of the `NUMBER`.
- `p:NUMBER@MEDIA` - Padding.
- `pt:NUMBER@MEDIA` - Padding-top.
- `pr:NUMBER@MEDIA` - Padding-right.
- `pb:NUMBER@MEDIA` - Padding-bottom.
- `pl:NUMBER@MEDIA` - Padding-left.
- `px:NUMBER@MEDIA` - Padding-left and padding-right.
- `py:NUMBER@MEDIA` - Padding-top and padding-bottom.
- `p:LETTER@MEDIA` - Position.
- `r:NUMBER@MEDIA` - Right. If the negative equivalent is enabled, you can use it by putting a dash in front of the `NUMBER`.
- `ta:LETTER@MEDIA` - Text-align.
- `td:LETTER` - Text-decoration.
- `t:NUMBER@MEDIA` - Top. If the negative equivalent is enabled, you can use it by putting a dash in front of the `NUMBER`.
- `va:LETTER` - Vertical-align.
- `ws:nw` - `white-space: nowrap`.
- `w:WORD@MEDIA` - Width. `WORD` should correspond to a keyword inside the `$widths` variable.