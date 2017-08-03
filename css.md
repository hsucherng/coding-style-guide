# CSS

- [Class Types](#class-types)
    - [Component Classes](#component-classes)
    - [Local Classes](#local-classes)
    - [Modifier Classes](#modifier-classes)
    - [Utility Classes](#utility-classes)
    - [JavaScript Classes](#javascript-classes)
        - [Selection Classes](#selection-classes)
        - [State Classes](#state-classes)
    - [Component Classes vs Local Classes](#component-classes-vs-local-classes)
    - [Utility Classes vs inline styles](#utility-classes-vs-inline-styles)
    - [Utility Classes vs other classes](#utility-classes-vs-other-classes)

## Class Types

By default, CSS classes have very little restrictions on how they can be named, formatted, styled, and so on. It's very lenient and easy to get into, but it's somewhat daunting to scale this up to handle a website that has hundreds of pages.

In efforts to tackle that, I separate my classes into three distinct "types", in order to allow me to easily distinguish them.

### Component Classes

Component Classes are global classes that consistently provide a set of expected, predictable style.

Component Class names should have these properties:

- Fully lowercase, with hyphens linking multiple words.
- Use generic words, so as to allow them to be used naturally throughout the entire site.

Examples of Component Classes:

- `.button` — any element that uses this class is expected to look like a button.
- `.page-banner` — any element that uses this class is expected to look like a page banner.
- `.media` — a common component used to display an image together with some text. Can be used for comments, author profile, search results, and more.

### Local Classes

Local Classes are restricted classes that are intended to be used for a specific page or section only. These classes can be used on their own, or can be used to complement Component Classes.

Local Class names should have these properties:

- Every word should be capitalised, with hyphens linking multiple words.
- Use specific words or names, to limit their scope down to its intended area.

Examples of Local Classes:

- `.Address-Form` — a kind of form used specifically for addresses, e.g. shipping and billing address forms.
- `.Flash-Sale-Item` — an item catered specifically for flash sales.

:exclamation: **Keep Local Classes as specific as possible.** Local Classes are not supposed to be reusable over a large number of pages, and that is intentional, because that minimises their impact and allows us to adjust their styles without worrying about other pages being affected. Code that is easy to delete is code that is easy to maintain.

### Modifier Classes

Modifier Classes are dependent classes that are used to add onto or tweak the styles of a specific base class. These are classes that do nothing on their own; they must always be associated with a base class.

Modifier Class names should have these properties:

- Begin with two dashes.
- Follow the same formatting as its base class:
    - If this is a modifier for a Component Class, then it should be fully lowercase, with hyphens linking multiple words.
    - If this is a modifier for a Local Class, every word should be capitalised, with hyphens linking multiple words.

Examples of Modifier Classes:

- `.--black` as a modifier for `.button` to create a button with a black-coloured theme.
- `.--Delivery` as a modifier for `.Address-Form` to distinguish a Delivery Address Form from other Address Forms.

### Utility Classes

Utility Classes are global classes that consistently provide a single, specific style. They work almost like inline styles, except they have lower specificity, terse naming, and better functionality.

Utility Class names are inspired single-handedly from [shed.css](http://tedconf.github.io/shed-css/), which follows this naming scheme: `A:B@C`, where:

- `A` is one or more letters representing a style property name, e.g. `d` for `display`.
- `B` is highly dependent on what `A` is, and can either be:
    - One or more letters, this time representing the style value name, e.g. `i` for inline, `ib` for `inline-block`.
    - One or more digits representing a certain scale of size or dimension.
- `C` is two letters representing the media query to be used for the class, e.g. `sm`. This portion is optional and can be removed together with the `@` symbol if it doesn't need to have a media query.

There are a number of concepts involved with Utility Classes, so it is best to read more about it in its [documentation](#/).

### JavaScript Classes

There are inevitably classes that are made to be used with JavaScript, so it would be helpful to be able to easily distinguish them as well.

#### Selection Classes

Sometimes, for a much finer control on what elements to select, we can introduce a class that is made specifically for JavaScript selection. Hence its name: Selection Classes.

These classes should *never* have any styles associated with them. Their purpose is solely for use with JavaScript.

To clearly distinguish these classes, their names should start with the letters `js`.

Examples:

- `.js-popup-toggler` for elements that need to toggle a popup.
- `.js-masonry-item` for elements that need to be initialised into a Masonry layout.

#### State Classes

These are essentially Modifier Classes, but are toggled through JavaScript.

To clearly distinguish these classes, use one of these specific keywords — `is` or `has` — while maintaining the same format as Modifier Classes.

Examples:

- `.--has-error` as a state for `.field` to show that the input field did not pass validation.
- `.--is-disabled` as a state for `.button` to show that it shouldn't be interacted with.
- `.--Submitted` as a state for `.Address-Form` to show that it has been submitted.

### Component Classes vs Local Classes

The most important factor to consider is always **where** and **how often** do I imagine myself using the class:

- If I expect to use the class *multiple times* on *multiple pages* throughout the entire site, I will treat as a Component Class.
- If I expect to use the class *once or twice only* on *one or two pages only*, I will treat it as a Local Class.

### Utility Classes vs inline styles

Utility Classes are a step above inline styles because:

1. Utility Classes are much more terse, to the point of being unreadable to people who've never seen this kind of naming scheme before: `w:10` vs `width: 100%`, `d:ib` vs `display: inline-block`.
2. A certain amount of consistency can still be maintained, through a scale system. For example, the default font-size scale through Utility Classes is `f:1`. If we want a slightly smaller size, rather than thinking of a very specific size to use — and whether it'd be consistent with the rest of the site — we can just bump down the digit by a fraction, to `f:.9`.
3. Utility Classes can be setup for use with media queries, making them responsive-viable. Inline styles can't be used with media queries at all.

### Utility Classes vs other classes

I typically use Utility Classes in replacement of creating a whole new class just to set one specific property. Another way to look at this is: in situations where I feel very tempted to stoop down to inline styles, I will use Utility Classes instead.

However, in the first place, depending on how elaborate the Utility Classes are setup, it is very much possible to style an entire page using just Utility Classes. So why don't I just do that?

My main argument against using solely Utility Classes is because of the thought process that I have to get into. If I want to style an element as a button, I do not want to think of how to piece together a whole bunch of different Utility Classes to get it to look like a button — I just want to style it as a button. That's where Component Classes fit in — just use the `.button` class, and I can expect the element to look like a button.

The above can be resolved through a templating layer, but I have yet to figure out how to set that layer up, and since the final generated HTML files end up being riddled with Utility Classes anyway, I worry on how the back-end developers would integrate the HTML into their project.