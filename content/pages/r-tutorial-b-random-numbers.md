---
content_type: page
description: This section provides R tutorial about random numbers.
draft: false
title: 'R Tutorial b: Random Numbers'
uid: caf11256-bc50-4551-95a6-70ae98b5918a
---
In order to run simulations of experiments with random outcomes we make use of R's ability to generate random numbers. More precisely it generates a 'pseudo-random' number, which behaves in many ways like a truly random number.

## The Function Sample(x, k, replace = TRUE)

\# sample(x,k) generates a random permutation of k objects from the vector x. That is, all k choices are different.

`# start with a vector x with 5 elements.`   
`> x = 1:5`   
`> print(x)`   
`[1] 1 2 3 4 5`

`# randomly sample 3 of the elements of x.`   
`> y = sample(x, 3)`   
`> print(y)`   
`[1] 2 5 1 # Your answer may be different.`   
`> y = sample(x, 3)`   
`> print(y)`   
`[1] 3 1 4 # Your answer may be different.`   
`> sample(x, 3)`   
`> print(y)`   
`[1] 1 2 5 # Your answer may be different.`   
`# Note every element is chosen at most once.`

`# randomly sampling 5 elements of x is a permutation of all 5 elements.`   
`> y = sample(x, 5)`   
`> print(y)`   
`[1] 1 3 2 5 4 # Your answer may be different.`   
`> y = sample(x, 5)`   
`> print(y)`   
`[1] 2 3 1 4 5 # Your answer may be different.`

\# You can't pick more than 5 different elements from a set of 5 things, so R gives an error.    
\> sample(x, 6)    
Error in sample.int(length(x), size, replace, prob):     
cannot take a sample larger than the population when 'replace = FALSE'

**Allowing repeated elements**    
\# Sometimes you want to allow repeats. For example when  we roll a die repeatedly we expect to see numbers repeating. We can think of this as picking a random element from a set and then putting it back, i.e. replacing it, so it can be drawn again.

\# In R we do this by setting the optional argument replace=TRUE

\# Note that we get can get repeated values    
\> y = sample(x, 3, replace=TRUE)    
\> print(y)    
\[1\] 3 1 4 # Your answer may be different.    
\> y = sample(x, 3, replace=TRUE)    
\> print(y)    
\[1\] 4 5 4 # Your answer may be different.    
\> y = sample(x, 3, replace=TRUE)    
\> print(y)    
\[1\] 2 1 5 # Your answer may be different.    
\> y = sample(x, 5, replace=TRUE)    
\> print(y)    
\[1\] 5 1 5 1 4 # Your answer may be different.    
\> y = sample(x, 5, replace=TRUE)    
\> print(y)    
\[1\] 3 5 5 2 1 # Your answer may be different.    
\> y = sample(x, 5, replace=TRUE)    
\> print(y)    
\[1\] 4 2 3 2 1 # Your answer may be different.

\# Now there is no problem asking for more than 5 things from a set of 5 elements.    
\> y = sample(x, 12, replace=TRUE)    
\> print(y)    
\[1\] 1 1 2 1 4 2 3 4 1 2 4 5 # Your answer may be different.    
\> y = sample(x, 12, replace=TRUE)    
\> print(y)    
\[1\] 3 2 5 1 4 2 4 1 4 5 3 1 # Your answer may be different.

\# To generate an m x n array of random values we can use the function sample function followed by the matrix function.

\# Let's simulate rolling a die.     
\# We use 1:6 to make vector (1,2,3,4,5,6).

\# Generate a 3 x 4 array of random dice rolls.    
\> y = sample(1:6, 12, replace=TRUE)    
\> z = matrix(y, nrow=3, ncol=4)    
\> print(z)    
    \[,1\] \[,2\] \[,3\] \[,4\]    
\[1,\]    1    3    6    1    
\[2,\]    2    2    3    6    
\[3,\]    2    1    4    3

\# Or we could make it a 2 x 6 array.    
\> z = matrix(y, nrow=2, ncol=6)    
\> print(z)    
    \[,1\] \[,2\] \[,3\] \[,4\] \[,5\] \[,6\]    
\[1,\]    1    2    2    6    4    6    
\[2,\]    2    3    1    3    1    3    
\# Your answer may be different.  

## Simulation

\# First      

### One More Simulation

\# Goal: