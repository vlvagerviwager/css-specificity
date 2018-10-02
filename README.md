# A platform integration developer works with CSS (professionally) for the first time: selector logic and specificity

_Originally written in 2016._

I’ve worked with CSS before and have done the brilliant CSS selector tutorial at http://flukeout.github.io/, but I am definitely not an expert. Coming from a product where UX was not a priority doesn’t help. Here’s what I’ve learned in my first week of being a MEAN (stack, not personality) web developer.

## Basic selector logic

a and b are CSS classes.

    .a.b = select an element with both classes on it
    .a, .b = select an element with a or b on it
    .a .b = select an element with class b, which is a descendant of an element with a
    .a > .b = select an element with class b, which is a direct descendant of an element with a

Elements which are direct descendants are exactly one level below, no more.

## Avoiding !important with CSS specificity

Putting !important at the end of CSS properties is bad. It brings the priority of that property to be the highest, i.e. it will override every other time that property is set, whether sensible or not. Arbitrarily overriding stuff will make your overall CSS messy and confusing. It’s useful for testing in developer tools, but don’t commit it.

How to not use important: wrap the class containing the property which is being overridden, by a class in a more specific parent element/a class with higher specificity (try to choose one without variables and other junk).

e.g. properties within b are being overridden by something or the other. a has high specificity:

.a {
  .b { … }
}

The above is equivalent to .a.b. Don’t worry about the enclosing class: only the styling in .b will be applied.

Why does this work? At the heart of it all is:

## Precedence of CSS selectors

The least complicated explanation I could find is the section Calculating CSS Specificity Value in https://css-tricks.com/specifics-on-css-specificity/.

TL;DR version of CSS selector precedence:

    Inline styling: there is no way to override this, except using !important, or maybe some jQuery/JS.
    #id
    class
    Native HTML tag/styling - e.g. <h1>, etc.
