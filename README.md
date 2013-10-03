# .VisualDNA CSS Style Guide {

*A reasonable way of creating CSS Stylesheets*

## <a name='TOC'>Table of Contents</a>

1. [Tools](#tools)
2. [Frameworks](#frameworks)

## <a name='tools'>Tools</a>
- **SASS** We're using this preprocessor, moving away from our previous one, LESS


## <a name='frameworks'>Frameworks</a>

- **Bootstrap** We're still using some parts of this framework on our products. For the SASS version, please see [Bootstrap-sass](https://github.com/thomas-mcdonald/bootstrap-sass)

- Don't load multiple css stylesheets, try to keep it to a minimum to prevent extra http calls.
    ``` html
    <!-- Bad -->
    <link href="/css/bootstrap.css" rel="stylesheet">
    <link href="/css/app.css" rel="stylesheet">

    <!-- Good -->
    <link href="/css/app.css" rel="stylesheet">

- Please import all the needed parts to your own file:

    ``` css
    // Bad (imports the whole set of css)
    @import 'bootstra-sass/bootstrap';

    // Good
    @import "sass-bootstrap/variables";
    @import "sass-bootstrap/mixins";
    @import "sass-bootstrap/normalize";
    @import "sass-bootstrap/print";
    ```
