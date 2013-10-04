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
In all our projects, we use **CSS pre-processors** and we generate the final CSS via Grunt (minification is done only on deployment). 

We are largely using **LESS**, because of its simplicity. Nonetheless, we are evaluating if moving away and adopting **Sass** as our standard CSS preprocessing language (more powerful, becoming a standard de-facto, easy to find documentation or sample code). For this reason, all the examples below will be in SCSS, when not differently reported.

- **[LESS](http://lesscss.org/)**: currently the preprocessor used in large part of our projects.
- **[Sass](http://sass-lang.com/)** used in some secondary/experimental/explorative projects. The syntax (and file format) we use is `.scss`, not `.sass`.

- **[Autoprefixer](https://github.com/ai/autoprefixer)** is used in some projects to automatically add vendor prefixes to standard CSS. Notice: it can't generalize all the different implementations for advanced/experimental CSS3 properties (transforms, animations, flexbox, etc.); for this reason we are still relying on mixins for this scope.
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
    .message { font-size: 12px; color: #000000; background: #666666; }
    .left { float: left; }

    // Good
    .error,
    .alert,
    .success {
   		…
  	}
    .message {
   		font-size: 12px;
  		color: #000000;
  		background: #666666;
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

    **[[⬆]](#TOC)**

## <a name='conventions'>Conventions</a>

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

- Prepend a space before the opening brace.
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

- Don't spare on bites: use full hexadecimal color, declare specifically measures, ect. In this way you increase readability and expecially reduce the cognitive load
    ``` SCSS
    // Not bad, but require an extra cognitive effort to be interpreted
    .text { color: #000; }
    .intro { padding: 0; }
    
    // Better
    .text { color: #000000; }
    .intro { padding: 0px; }
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

