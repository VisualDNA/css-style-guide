# .VisualDNA CSS Style Guide {

*A reasonable way of creating CSS Stylesheets*

## <a name='TOC'>Table of Contents</a>

1. [Tools](#tools)
1. [Frameworks](#frameworks)
1. [Files](#files)
1. [CSS rule declaration order](#cssorder)
1. [Properties declaration order](#cssorder2)
1. [Conventions](#conventions)
1. [License](#license)


## <a name='tools'>Tools</a>
In all our projects, we use **CSS pre-processors** and we generate the final CSS via Grunt (minification is done only on deployment), never on client side (LESSjs).

- **[SASS](http://sass-lang.com/)** We're using this preprocessor, moving away from our previous one, LESS. The file format is `.scss`, not `.sass`.

- **[Autoprefixer](https://github.com/ai/autoprefixer)** is used to add vendor prefixes to standard css. So use only standard CSS rules.
    ``` SCSS
    // Bad
    -webkit-box-shadow: 1px 1px 4px #333;
    -moz-box-shadow: 1px 1px 4px #333;
    -ms-box-shadow: 1px 1px 4px #333;
    box-shadow: 1px 1px 4px #333;

    //Good
    box-shadow: 1px 1px 4px #333;
    ```

    **[[⬆]](#TOC)**

- **[LESS](http://lesscss.org/)**: Some legacy projects still run on LESS. 




## <a name='frameworks'>Frameworks</a>

- **[Bootstrap](http://www.getbootstrap.com/)** We're still using some parts of this framework on our products. For the SASS version, please see [Bootstrap-sass](https://github.com/thomas-mcdonald/bootstrap-sass)

- Don't load multiple CSS stylesheets in your HTML, try to keep it to a minimum to prevent extra http calls.
    ``` HTML
    <!-- Bad -->
    <link href="/css/bootstrap.css" rel="stylesheet">
    <link href="/css/app.css" rel="stylesheet">

    <!-- Good -->
    <link href="/css/app.css" rel="stylesheet">
    ```

- Import only the needed parts of the framework to your .scss file. It is acceptable to comment-out the files not used to avoid importing theme.

    ``` SCSS
    // Bad (imports the whole set of css)
    @import 'bootstrap-sass/bootstrap';

    // Good
    @import "bootstrap-sass/variables";
    @import "bootstrap-sass/mixins";
    @import "bootstrap-sass/normalize";
    @import "bootstrap-sass/print";
    // @import "bootstrap-sass/print";
    ```
    **[[⬆]](#TOC)**

## <a name='files'>Files</a>

- Feel free to split the content in multiple files (in that case, use meaningful names for the files). 
- When the include files become too many, organize then in one or more subfolders (use meaningful and coherent names).
- Adopt an intelligent convention for the way files and folders are organized. _[TO BE DEFINED/DISCUSSED]_
- Don't forget to use a single output file, including all the other needed files in it.

- To comply with Sass convention, start with an underscore each file that shouldn't be converted to CSS.
    ```
    // Bad
    SCSS
        main.scss
        reset.scss
        mediaqueries.scss

    // Good
    SCSS
        main.scss
        _reset.scss
        _mediaqueries.scss
    ```

    **[[⬆]](#TOC)**


## <a name="cssorder">CSS rule declaration order</a>
- Inspired from this article from [CSS Tricks](http://css-tricks.com/sass-style-guide/)

- List @extend(s) first
    ``` SCSS
    .weather {
        @extends %module;
        ...
    }
    ```

- List @include(s) next
    ``` SCSS
    .weather {
        @extends %module;
        @include clearfix();
        ...
    }
    ```
- List regular styles next
    ``` SCSS
    .weather {
        @extends %module;
        @include clearfix();
        background: red;
        ...
    }
    ```

- Add nested selectors last
``` SCSS
    .weather {
        @extends %module;
        @include clearfix();
        background: red;
        a {
            color: yellow;
        }
    }
    ```

- Don't nest more than three rules!
    ``` SCSS
    .module {
        .header {
            .icon {
                // Don't nest anything more!
            }
        }
    }
    ```

- Write each selector and propertiy on its own line. It's acceptable to use one single line to improve readability or when there is only one selector and one property.
    ``` SCSS
    // Bad
    .error, .alert, .success { ... }
    .message { font-size: 12px; color: #000; background: #666; }
    .left { float: left; }

    // Good
    .error,
    .alert,
    .success {
        …
    }
    .message {
        font-size: 12px;
        color: #000;
        background: #666;
    }
    .left { float: left; }
    ```

    **[[⬆]](#TOC)**

## <a name='cssorder2'>Properties declaration order</a>

- Inspired from [Idiomatic CSS](https://github.com/necolas/idiomatic-css)
- Please define first positioning, then display model and everything else after

    ``` SCSS
    .selector {
        /* Positioning */
        position: absolute;
        z-index: 10;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;

        /* Display & Box Model */
        display: inline-block;
        overflow: hidden;
        box-sizing: border-box;
        width: 100px;
        height: 100px;
        padding: 10px;
        border: 10px solid #333;
        margin: 10px;

        /* Other */
        background: #000;
        color: #fff;
        font-family: sans-serif;
        font-size: 16px;
        text-align: right;
    }
    ```
- CR: actually in WHY we are using a slightly different order: first the positioning, then the dimensions of the element and at last (they are related!). always declare the properties in the clockwise order (top-right-bottom-left)

    ``` SCSS
    .selector {
        /* Positioning */
        position: absolute;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
        width: 100px;
        min-width: 0px;
        max-width: 100%;
        height: 100px;
        min-height: 0px;
        max-height: none;
        z-index: 10;
        margin: 0px auto;
        padding: 5px 10px 15px 10px;

        /* Display & Box Model */
        display: inline-block;
        float: none;
        overflow: hidden;
        box-sizing: border-box;

        /* List or Table styling */
        list-style: …
        table-layout: … 
        border-spacing: … 
        etc.

        /* Font styling */
        font-family: sans-serif;
        font-size: 16px;
        line-height: 1.2em;        
        font-weight: bold;
        font-style: italic;
        text-align: right;
        vertical-align: middle;
        text-transform: uppercase;
        text-decoration: none;
        white-space: nowrap;

        /* Box styling */
        background: #FFF url(../img/logo.png) no-repeat 0px 50%;
        background-size: 50% 50%;
        border: 10px solid #333;
        border-radius: 3px;
        box-shadow: 1px 1px 2px rgba(0,0,0,0.2);

        /* CSS3 and other properties */
        content: " ";
        opacity: 0.5;
        transition: …
        transform: …
        animation: …

    }
    ```

    **[[⬆]](#TOC)**

## <a name='conventions'>Conventions</a>

- **IDs vs. Classes**: as a general rule of thumb, we are using classes as identifiers, whenever possible. Use IDs only if required, only for top-level (and obviously unique) elements, and only if you know what you're doing.
- **!important**: it can be applied in very limited and specific situations. Use it only if you are at Level 3 of CSS knowledge.
- **Whitespace**: use 4 spaces per indentation level, so configure you editor accordingly. Use one level of indentation for each declaration.
- **Comments**: use `//` for generic comments (they are stripped on processing); never use `/* */` unless you need a comment to appear in the outputted CSS (legal declarations, licenses, etc.)
- **Sections**: you are invited to use comments (and ascii decorations) to break code into discrete and logical sections.
- **Namings**: adopt meaningful, readable and not-too-generic class names. Write them in lowercase with hyphens

    ``` SCSS
    // Bad
    .LukeSkywalker {

    }

    // Good
    .luke-skywalker {
    }
    ```

- To define multiple states of the same element, we're adopting the underscore _(up to discussion)__

    ``` SCSS
    // Bad
    .luke-skywalker-wounded {
    }
    .menu-open {
    }

    // Good
    .luke-skywlaker_wounded {
    }
    .menu_open {

    }
    ```

- **Formats**: 
  - Place the closing brace of a ruleset in the same column as the first character of the ruleset.
  - Separate each ruleset by a blank line.
  - Include a single space before the opening brace of a ruleset.

    ``` SCSS
    // Bad
    span{…}
    .primary{
        …
    }

    // Good
    span {…}
    .primary {
        …
    }
    ```

  - Include a single space after the colon of a declaration.

    ``` SCSS
    // Bad
    span { font-size:12px; }

    // Good
    span { font-size: 12px; }
    ```

- Use shorthand hexadecimal colours. In this way you increase readability and reduce the cognitive load
    ``` SCSS
    // Not bad, but require an extra cognitive effort to be interpreted
    .text { color: #000; }
    
    // Better
    .text { color: #000; }
    ```

- When a value has no magnitude, do not include the unit. Also border: 0; is preferred over border: none;
    ``` SCSS
    // This requires extra cognitive effort to be interpreted
    .text { padding: 0px; }
    
    // Better, both saves bytes but more importantly is abundantly clear that the developer meant no magnitude
    .text { padding: 0; }
    ```

- Don't use colour names. Whenever defined, use colour variables.
    ``` SCSS
    // Bad
    .alert { color: red; }
    .primary { background-color: #0B85DC; }
    
    // Good
    .alert { color: red; }
    .primary { background-color: @color-brand-base; }
    ```
- If you need to declare specific properties for specific browsers (IE, in 99.99% of the cases) use conditional comments to apply classes to the html tag for specific ies. This allows you to add classes at point of selector to keep the styles grouped for their vendors.

    **[[⬆]](#TOC)**
    
## <a name='license'>License</a>

The MIT License (MIT)

Copyright (c) 2013 VisualDNA

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.

**[[⬆]](#TOC)**

# }

