Cheat sheet for the R language
==============================


- Installing packages

        install.packages('name of the package')

- i modulo n (modulus operator)

        i %% n

Packages
--------

Installing packages:

    install.packages('sp')

View version of installed packages:

    packageVersion('sp')
    packageDescription('sp')['Version']  # more verbose

    # Print version information about R and attached or loaded packages.
    sessionInfo()

Install package from tar file:

    R CMD INSTALL /path/to/file

Install package from its source directory:

    cd /path/to/project/source
    Rscript -e "install.packages('$PWD', repos=NULL, type='source')"

Print list of functions in a package:

    ls('package:achia')

Unload / detach library:

    detach('package:sp', unload=T)

R on Mac OS X
-------------

Installation path of R versions:

    /Library/Frameworks/R.framework/Versions

Creating packages
-----------------

Store a variable inside a package's environment:

    .AchiaEnv <- new.env()

    set.workdir <- function(path) {
      assign('WORKDIR', path, envir=.AchiaEnv)
    }

    get.workdir <- function() {
      get('WORKDIR', envir=.AchiaEnv)
    }
