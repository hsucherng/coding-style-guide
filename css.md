# CSS





- [BEM Methodology](#bem-methodology)
    - [Making it a little more DRY](#making-it-a-little-more-dry)
- [Class Types](#class-types)
    - [Component Classes](#component-classes)
    - [Local Classes](#local-classes)
    - [Utility Classes](#utility-classes)
    - [JavaScript Classes](#javascript-classes)
        - [Selection Classes](#selection-classes)
        - [State Classes](#state-classes)
    - [Component Classes vs Local Classes](#component-classes-vs-local-classes)
    - [Utility Classes vs inline styles](#utility-classes-vs-inline-styles)
    - [Utility Classes vs other classes](#utility-classes-vs-other-classes)
- [Inheritance](#inheritance)
- [Indentation](#indentation)
- [Inline Styles](#inline-styles)
- [Specificity](#specificity)





## BEM Methodology

BEM stands for _**B**lock, **E**lement, **M**odifier_, and it is a methodology that I often use, with [one main difference highlighted in a section further below](#making-it-a-little-more-dry).

The standard BEM convention is as follows:

```css
/* Block */
.button {}

/* Element that is associated with the block */
.button__icon {}

/* Modifier that changes the style of the block */
.button--black {}
.button--large {}
```

BEM makes our classes much more clearer and predictable. Just by glancing at the HTML below, we can immediately identify which classes are related to each other, and which aren't:

```html
<a href="#/" class="button button--black">
    This is a black button with a global right arrow icon

    <span class="button__icon">
        <i class="icon-font icon-font--arrow-right"></i>
    </span>
</a>
```

There are many resources on the web that discuss about BEM, some of which are listed below.

- BEM Methodology: [Quick Start](https://en.bem.info/methodology/quick-start/)
- CSS Wizardry: [MindBEMding - getting your head 'round BEM syntax](https://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)
- CSS-Tricks: [BEM 101](https://css-tricks.com/bem-101/)

### Making it a little more DRY

As an effort to reduce repetition, I personally drop the block name from the modifier class:

```css
/* Standard BEM-style modifier */
.button--black {}

/* My style of modifier */
.button.--black {}
```

```html
<!-- Standard BEM-style modifier -->
<a href="#/" class="button button--black"></a>

<!-- My style of modifier -->
<a href="#/" class="button --black"></a>
```





## Class Types

On top of the [BEM methodology](#bem-methodology), I also further categorise my classes into several distinct "types", in order to allow me to easily distinguish them.

### Component Classes

Component Classes are global classes that consistently provide a set of expected, predictable style.

Component Class names should have these properties:

- Fully lowercased, and using hyphens to link multiple words: `.button`, `.popup`, `.bullet-list`
- Apply the same formatting to its modifiers: `.--large`, `.--with-icon`
- Use generic words, so as to allow them to be used naturally throughout the entire site

### Local Classes

Local Classes are restricted classes that are intended to be used for a specific page or section only. These classes can be used on their own, or can be used to complement Component Classes.

Local Class names should have these properties:

- Every word should be capitalised, and using hyphens to link multiple words: `.Registration`, `.Checkout-Form`
- Apply the same formatting to its modifiers: `.--Complete`, `.--Invalid-Details`
- Use specific words or names, to limit their scope down to its intended area.

:exclamation: **Keep Local Classes as specific as possible.** Local Classes are not supposed to be reusable over a large number of pages, and that is intentional, because that minimises their impact and allows us to adjust their styles without worrying about other pages being affected. Code that is easy to delete is code that is easy to maintain.

### Utility Classes

Utility Classes are global classes that consistently provide a single, specific style. They function almost like inline styles, except with terse naming, lower specificity, and responsive compatibility.

Utility Class names are inspired single-handedly from [shed.css](http://tedconf.github.io/shed-css/), which follows this naming scheme: `LETTER(S):(VALUE)@(MEDIA)`.

Read more about Utility Classes [here](css-utility-classes.md).

### JavaScript Classes

There are inevitably classes that are made to be used with JavaScript, so it would be helpful to be able to easily distinguish them as well.

#### Selection Classes

Sometimes, for a much finer control on what elements to select, we can introduce a class that is made specifically for JavaScript selection.

To clearly distinguish these classes, their names should start with the letters `js`. Since their sole purpose is for JavaScript, there must be **no** styles associated with these classes.

Examples:

- `.js-popup-toggler` for elements that need to toggle a popup.
- `.js-masonry-item` for elements that need to be initialised into a Masonry layout.

:exclamation: **Consider using data attributes instead of Selection Classes,** reason being that it's more flexible, as it's possible to pass in a value to modify the behaviour of our JavaScript.

#### State Classes

These are essentially modifier classes, but are toggled through JavaScript.

To clearly distinguish these classes, use one of these specific keywords — `is` or `has` — while maintaining the same format as the Component or Local Class that it's associated with. The keyword doesn't have to be used as the first word of the class — as long as it's used in any part of the class, it should be recognised as a State Class.

Examples:

- `.--has-error` as a state for `.field` to show that the input field did not pass validation.
- `.--is-disabled` as a state for `.button` to show that it shouldn't be interacted with.
- `.--popup-is-shown` as a state for `body` to hide the page's scrollbar when a popup is shown.
- `.--Is-Submitted` as a state for `.Address-Form` to show that it has been submitted.


### Component Classes vs Local Classes

The most important factor to consider is always **where** and **how often** do I imagine myself using the class:

- If I expect to use the class *multiple times* on *multiple pages* throughout the entire site, I will set it up as a Component Class.
- If I expect to use the class *once or twice only* on *one or two pages only*, I will set it up as a Local Class.

### Utility Classes vs inline styles

Utility Classes are a step above inline styles because:

- They are more terse: `display: inline-block` is greatly shortened to `d:ib`.
- Their specificity is much lower than inline styles, forcing us to be much more considerate and deliberate with their use.
- They can be used in a responsive manner. For example, `d:ib@sm` turns the element into an inline-block element only in the `sm` viewport and above.

### Utility Classes vs other classes

I typically use Utility Classes in replacement of creating a whole new class just to set one specific property. Another way to look at this is: in situations where I feel very tempted to stoop down to inline styles, I will use Utility Classes instead.

However, in the first place, depending on how elaborate the Utility Classes are setup, it is very much possible to style an entire page using just Utility Classes. So why don't I just do that?

My main argument against using solely Utility Classes is because of the thought process that I have to get into. If I want to style an element as a button, I do not want to think of how to piece together a whole bunch of different Utility Classes to get it to look like a button — I just want to style it as a button. That's where Component Classes fit in — just use the `.button` class, and I can expect the element to look like a button.

The above can be resolved through a templating layer, but I have yet to figure out how to set that layer up, and since the final generated HTML files end up being riddled with Utility Classes anyway, I worry on how other developers would integrate the HTML into their project.





## Inheritance

In CSS, there are a number of styles that are automatically inherited from its ancestors. This allows us to set a certain style on a large block, and have all of its child elements inherit that style.

The properties that are commonly inherited are related to text, so `color`, `line-height`, `text-align`, and finally anything that starts with `font`.

Inheritance is great for reducing repetition and maintaining consistency. For example, instead of explicitly setting `font-size: 18px` on each of the block's child elements, consider setting that property on the block itself, then leverage inheritance from there.

Always be aware of what properties would be inherited from the element's context. Then, think hard and decide clearly on whether to explicitly control a property, or whether to let it inherit from its parent. For example, to ensure buttons are sized consistently throughout the site, we will most likely want to explicitly set its font-size. But when it comes to the line-height of a general section, we will likely want to set it once on its parent only, and allow all its child elements to inherit, to keep the line-height consistent.





## Indentation

Indentation in CSS has zero impact on the resulting outcome; instead, I use it together with the [BEM methodology](#bem-methodology) to further emphasise the parent-child relation between classes inside a block:

```css
.button {
    /* Button styles*/
}
    .button__label {
        /* Button label styles */
    }
        .button__label-icon {
            /* Button label icon styles */
        }

@media (min-width: 481px) {
    .button {
        /* Responsive button styles */
    }
        .button__label-icon {
            /* Responsive button label icon styles */
        }
}
```

With this, we can clearly see the hierarchy without having to check the HTML markup.

Note that the indentation levels are relative within its own scope, and do not carry over between blocks; notice that `.button__label-icon` is indented two levels deeper than `.button` in the first block, but inside the @media block, it is only indented one level deeper than the `.button` in the same block.





## Inline Styles

Inline styles are generally frowned upon, and so they see very little use. But that doesn't they do not have their own legitimate uses:

1. I use it to markup styles that need to be overwritten by a back-end templating layer. For example, in banners, `color` and `background-image` are usually unique to each banner, and so I set those properties inline.
2. I use it to markup styles that are unique to its contents. For example, in a page that has multiple articles that each have a unique `background-image`, I will set that property inline.
3. I use it to preset properties that are controlled through JavaScript. For example, for an error message that is hidden through `display: none` by default, and is shown and hidden using jQuery's `.show()` and `.hide()` methods — when I want to override the error message's default hidden state, I will set `display: block` inline.

Otherwise, majority of the styles should be set through CSS, using mainly classes only.




## Specificity

The general practice is to keep specificity as low as possible, to allow ourselves the flexibility and the leeway of being able to easily override styles when needed.

To keep specificity as low as possible, we should follow these points as much as possible:

- Use classes only, and if possible, stick to a single class only.
- Avoid IDs.
- Avoid inline styles.
- Avoid nesting selectors.
- `!important` is forbidden — if it's used, it is expected to be accompanied by comments explaining why it's being used.

Also, the [BEM Methodology](#bem-methodology) helps tremendously with keeping specificity low.