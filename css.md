# American Specialty Health CSS / Sass Styleguide﻿

## Table of Contents
1. **[CSS](#css)**
	[ [Formatting](#1.1-formatting) ]
	[ [Property Ordering](#1.2-property-ordering) ]
	[ [Flexbox](#1.3-flexbox) ]
	[ [Do NOT Use](#1.4-do-not-use) ]
1. **[SCSS](#scss)**
	[ [Nesting](#2.1-nesting) ]
	[ [Variables](#2.2-variables) ]
	[ [Comments](#2.3-comments) ]

## CSS

### 1.1 Formatting
> Why? All of our styles should be formatted so that they are clean, concise, and easily readable by any developer on the team

* Put a space after the selector/before the opening brace `{` in rule declarations
* Class names should be lowerCamelCased
* When using multiple selectors for a style declaration, put each selector on its own line
* Each property goes a new line
* Put closing braces `}` of style declarations on a new line

**Bad**
```css
.className, .anotherClassName{ property: rule; another: rule }
.CrazyCase { property: rule; }
```

**Good**
```css
.className,
.anotherClassName {
    property: rule;
    another: rule;
}
.crazyCase { property: rule; }
```

### 1.2 Property Ordering
> Why? To keep our CSS properties in a consistent ordering scheme within the styles of every site

Properties should be ordered as follows:
    1. Box model (height, padding, border, etc.)
    2. Position properties (floats, display, position)
    3. Font properties (color, text-shadow, font-size)
    4. Misc (background, cursor, etc.)

**Bad**
```css
.selector {
    display: flex;
    color: #000;
    background: #e2e2e2;
    height: 2em;
    padding: 1em 0;
}
```

**Good**
```css
.selector {
    height: 2em;
    padding: 1em 0;
    display: flex;
    color: #000;
    background: #e2e2e2;
}
```

### 1.3 Flexbox
> Why? The use of flexbox is encouraged, however certain standards must be followed in order to maintain a consistent experience across all browsers (looking at you, IE10)

* Always use the flex shorthand over specifying `flex-shrink`, `flex-grow`, or `flex-basis` individually

### 1.4 DO NOT USE
> Why? The use of the following styles are not supported by screen readers and are therefore poor accessibility

* The content property - `content: 'Screen reader no see';`

## SCSS

### 2.1 Nesting
> Why? Deeply nested SCSS can get very messy very quickly. It is easy to lose track of selector hierarchy and maintain consistent, reusable SCSS if the styles are nested too deeply

* **Only use if necessary**
* Do not ever nest selectors more than three levels deep
* Place nested selectors after all other rule declarations, and make sure to put a line of whitespace in between the nested selector and the last rule declaration

**Bad**
```scss
.container {
    .nestedContainer {
        .anotherNestedContainer {
            font-weight: bold;
            .yetAnother {
                color: #fff;
            }
        }
        background: #e2e2e2;
    }
    font-family: 'Comic Sans MS', cursive, sans-serif;
}
```

**Good**
```scss
.container {
    font-family: 'Comic Sans MS', cursive, sans-serif;

    .nestedContainer {
        background: #e2e2e2;

        .anotherNestedContainer {
            font-weight: bold;
        }
    }
}

.anotherNestedContainer .yetAnother {
    color: #fff;
}
```

### 2.2 Variables
> Why? Variable naming convention and general usage should always be kept consistent so that anyone on the team can easily identify what the variable is intended to be used for

* Variable names should be `$lowerCamelCased`
* Shared variables should always be declared in the respective `/Base` variable partial, and overwritten in the site-specific variable partial of the same name
* Component-specific variables should be prefaced with an `_`, followed by the component name, and finally the variable name

**Example:**
- Declared within `/Base/partial/_var/componentName`
```scss
$_componentNameColor: #000;
```
- ...overwritten within `/site/partial/_var/componentName`
```scss
$_componentNameColor: $color1;
```

### 2.3 Comments

When commenting in sass be sure to use `//` version of comments. Comments written in this style are stripped out during the compilation process.

```scss
//Bad

 /*this comment will remain when the sass is compiled*/
$_componentNameColor: #000;

//Good

//this comment will be stripped out when compiled
$_componentNameColor: $color1;
```
