# .VisualDNA CSS Style Guide {

*A reasonable way of creating CSS Stylesheets*

## <a name='TOC'>Table of Contents</a>

1. [Tools](#tools)
1. [Frameworks](#frameworks)
1. [Files](#files)
1. [CSS rule declaration order](#cssorder)
1. [Properties declaration order](#cssorder2)
1. [Class definitions](#classnames)
1. [License](#license)

## <a name='tools'>Tools</a>
- In any case, we compile css during deployment. Don't use tools like LESSjs to build the css client-side.

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

## <a name='frameworks'>Frameworks</a>

- **[Bootstrap](http://www.getbootstrap.com/)** We're still using some parts of this framework on our products. For the SASS version, please see [Bootstrap-sass](https://github.com/thomas-mcdonald/bootstrap-sass)

- Don't load multiple css stylesheets, try to keep it to a minimum to prevent extra http calls.
    ``` html
    <!-- Bad -->
    <link href="/css/bootstrap.css" rel="stylesheet">
    <link href="/css/app.css" rel="stylesheet">

    <!-- Good -->
    <link href="/css/app.css" rel="stylesheet">
    ```

- Please import all the needed parts to your .scss file

    ``` SCSS
    // Bad (imports the whole set of css)
    @import 'bootstrap-sass/bootstrap';

    // Good
    @import "bootstrap-sass/variables";
    @import "bootstrap-sass/mixins";
    @import "bootstrap-sass/normalize";
    @import "bootstrap-sass/print";
    ```
    **[[⬆]](#TOC)**

## <a name='files'>Files</a>

- Feel free to split the content in multiple files.
- Start with an underscore each file that shouldn't be converted to css.
    ```
    // Bad
    scss
        main.scss
        reset.scss
        mediaqueries.scss

    // Good
    scss
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

    **[[⬆]](#TOC)**

## <a name='classnames'>Class definitions</a>

- We write all the class names in lowercase with hyphens

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

- Multiple classes, write one class per line

    ``` SCSS
    // Bad
    .luke-skywalker, .han-solo, .princess-leia {

    }

    // Good
    .luke-skywalker,
    .han-solo,
    .princess-leia {

    }
    ```

- Single line rules, use them only when one property is defined

    ``` SCSS
    // Bad
    .luke-skywalker { box-sizing: border-box; padding: 10px; }

    // Good
    div { box-sizing: border-box; }
    .luke-skywalker { padding: 10x; }

    ```
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

