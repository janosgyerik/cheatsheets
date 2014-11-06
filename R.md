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
