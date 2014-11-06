Cheat sheet for the R language
==============================

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

Scripting
---------

Use this first line for R scripts:

    #!/usr/bin/env Rscript

Ask for user input in Rscript:

    cat('\n[Press Enter]\n')
    foo <- scan("stdin", character(), n=1, nlines=1, quiet=TRUE)

Getting help
------------

Get help about any R function or structure:

    # documentation of the `rle` function
    ?rle

    # documentation of the `read.csv` function
    ?read.csv

Objects in memory
-----------------

    # list objects in memory
    ls()

    # delete objects from memory
    rm('variablename')

    # delete all objects
    rm(list = ls())

Navigating in the filesystem
----------------------------

    # current working directory
    getwd()

    # change to another directory
    setwd('/path/to/somewhere/else')

Extracting subsets from data frames
-----------------------------------

    # these are the same
    subset(airquality, Month == 5)
    subset(airquality, airquality[,'Month'] == 5)
    subset(airquality, airquality[,5] == 5)

Misc
----

Modulo operator:

    # 5 mod 3 is 2
    # 3 mod 5 is 3
    i %% n
