# .VisualDNA CSS Style Guide {

*A reasonable way of creating CSS Stylesheets*

## <a name='TOC'>Table of Contents</a>

1. [Tools](#tools)
2. [Frameworks](#frameworks)

## <a name='tools'>Tools</a>
- **SASS** We're using this preprocessor, moving away from our previous one, LESS


## <a name='frameworks'>Frameworks</a>

- **Bootstrap** We're still using some parts of this framework on our products. For the SASS version, please see [Bootstrap-sass](https://github.com/thomas-mcdonald/bootstrap-sass)

- Please import all the needed parts to your own file:

    ``` css
    // Bad (imports the whole set of css)
    @import 'bootstra-sass/bootstrap';

    // Good
