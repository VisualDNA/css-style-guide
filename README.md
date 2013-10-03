# .VisualDNA CSS Style Guide {

*A reasonable way of creating CSS Stylesheets*

## <a name='TOC'>Table of Contents</a>

1. [Tools](#tools)
1. [Frameworks](#frameworks)
1. [Files](#files)
1. [CSS rule declaration order](#cssorder)

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

- Create a main.scss file, put everything else inside a folder
- Create one .scss file per page / section.

## <a name="cssorder">CSS rule declaration order</a>

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