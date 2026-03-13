# Class 6: R Functions
Allyson Cauffiel (PID:A19113278)

- [Background](#background)
- [A first function](#a-first-function)
- [A second function](#a-second-function)

## Background

Functions are at the heart of using R. Everything we do involves calling
using functions. (from data input, analysis, to results output).

All functions in R have at least 3 things:

1.  A **name**, the thing you use to call a function.
2.  One or more input **arguments** that are comma separated.
3.  The **body**, lines of code between curly brackets {} that does the
    work of the function.

## A first function

Let’s write a silly wee function to add some numbers:

``` r
add <- function(x) {
  x + 1
}
```

Let’s try it out

``` r
add(100)
```

    [1] 101

Will this work

``` r
add( c(100, 200, 300) )
```

    [1] 101 201 301

Modify to be more useful

``` r
add <- function(x, y = 1) {
  x + y
}
```

``` r
add(100, 10)
```

    [1] 110

Will this still work?

``` r
add(100)
```

    [1] 101

``` r
plot(1:10, col= "blue", type = "b")
```

![](Class06_files/figure-commonmark/unnamed-chunk-7-1.png)

``` r
log(10, base = 10)
```

    [1] 1

> **N.B.** Input arguments can be either **required** or **optional**.
> The later have a fall-back default that is specified in the function
> code with an equals sign.

``` r
#add(100, 200, 300)
```

## A second function

All functions in R look like this:

    name <- function(arg) {
      body
    }

The `sample()` function in R …

``` r
sample(1:10, 4)
```

    [1] 3 2 6 4

> Q. Return 12 numbers picked randomly from the input 1:10

``` r
sample(1:10, 12, replace = TRUE)
```

     [1] 4 8 3 1 6 8 9 6 4 7 1 2

> Q. Write the code to generate a 12 nucleotide long DNA sequence?

``` r
bases <- c("A", "T","G","C")
sample(bases, 12, replace = TRUE)
```

     [1] "T" "A" "C" "T" "C" "G" "G" "G" "A" "G" "T" "A"

> Q. Write a first version function called `generate_dna()` that
> generates a user specified length `n` random DNA sequence.

``` r
generate_dna <- function(n=12) {
  bases <- c("A","T","G","C")
  sample( bases, size=n, replace = TRUE)
} 
```

> Q. Modify your function to return a FASTA like sequence so rather than
> \[1\] “A” “C” “C” “A” “C” “G” “C” “T” “A” “C” “C” “G” we want “GCAAT”

``` r
generate_dna <- function(n=12) {
  bases <- c("A","T","G","C")
  dna <- sample( bases, size=n, replace = TRUE) 
  paste(dna, collapse="")

} 
generate_dna()
```

    [1] "TCATCCCTTTGC"

> Q. Give the user an option to return FASTA format output sequence

``` r
generate_dna <- function(n=12, FASTA = TRUE) {
  bases <- c("A","T","G","C")
  dna <- sample( bases, size=n, replace = TRUE) 
  
  if(FASTA){
  dna <- paste(dna, collapse="")
  cat("hello")
  } else { 
    cat("...is it me you are looking for...")
  }
  
  return(dna)
} 
generate_dna(20, FASTA = TRUE)
```

    hello

    [1] "TCAACAAGACTAGACGTAGT"

> Q. Write a function called `generate_protein()` that generates a user
> specified length protein sequence in FASTA like format?

``` r
generate_protein <- function(n=12, FASTA = TRUE) {
  aa <- c("A", "R", "N", "D", "C",
"Q", "E", "G", "H", "I",
"L", "K", "M", "F", "P",
"S", "T", "W", "Y", "V")
  protein <- sample(aa, siz=n, replace =TRUE)
  paste(protein, collapse = "")
}
generate_protein(6)
```

    [1] "CGNEFG"

> Q. Use your new `generate_protein()` function to. generate sequences
> between length 6 and 12 amino-acids in length and check if any of
> these are unique in nature (i.e. found in the NR database at NCBI)

``` r
generate_protein(9)
```

    [1] "DPWYRPSKQ"

``` r
generate_protein(10)
```

    [1] "LHVPTKQFRG"

``` r
generate_protein(12)
```

    [1] "DLKQHHFNKPTQ"

or we could do a `for()` loop:

``` r
for(i in 6:12) {
  cat(">", i, "\n", sep = "")
  cat( generate_protein(i), "\n")
}
```

    >6
    RCLEIY 
    >7
    VASQTCH 
    >8
    FILHGGWF 
    >9
    TWTAMATIF 
    >10
    IISMFLPKDK 
    >11
    CMPGHRQCVHS 
    >12
    WNRWISSFCQND 
