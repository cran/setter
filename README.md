[![Project Status: Active - The project has reached a stable, usable state and is being actively developed.](http://www.repostatus.org/badges/0.1.0/active.svg)](http://www.repostatus.org/#active)
[![Build Status](https://semaphoreci.com/api/v1/richierocks/setter/branches/master/badge.svg)](https://semaphoreci.com/richierocks/setter)
[![Build status](https://ci.appveyor.com/api/projects/status/vtihvx16tsl1xngc?svg=true)](https://ci.appveyor.com/project/richierocks/setter)

# setter: Mutators That Work With Pipes

Mutators to set attributes of variables, that work well in a pipe (much like `stats::setNames`).

## Installation

To install the development version, you first need the *devtools* package.

```{r}
install.packages("devtools")
```

Then you can install the *setter* package using

```{r}
library(devtools)
install_bitbucket("richierocks/setter")
```

# Functionality

`set_*` functions change an attribute, then return their first input, allowing you to chain them together.  For example, to turn a vector into a matrix, you could do

```{r}
m <- 1:12 %>%
  set_dim(3:4) %>%
  set_dimnames(list(letters[1:3], LETTERS[1:4])) 
##   A B C  D
## a 1 4 7 10
## b 2 5 8 11
## c 3 6 9 12
```

To copy attributes from one variable to another, use a `copy_*` function.

```{r}
month.abb %>%
  copy_dim(x) %>%
  copy_dimnames(x)
##   A     B     C     D    
## a "Jan" "Apr" "Jul" "Oct"
## b "Feb" "May" "Aug" "Nov"
## c "Mar" "Jun" "Sep" "Dec"
```
`set_*` and `copy_*` functions are available for the following attributes: `names`, `colnames`, `rownames`, `dimnames`, `class`, `dim`, `length`.

There are also  `set_attributes` and `copy_attributes` for setting/copying arbitrary attributes.  Here's the previous example thrice more. `copy_all_attributes` and `copy_most_attributes` provide a shortcut for copying all the outputs, the latter using `base::mostattributes<-` to take special care with `dim`, `names` and `dimnames`.

```{r}
month.abb %>%
  copy_attributes(x, c("dim", "dimnames"))
month.abb %>%
  copy_all_attributes(x) 
month.abb %>%
  copy_most_attributes(x) # special care with dim, names, dimnames
```

  
