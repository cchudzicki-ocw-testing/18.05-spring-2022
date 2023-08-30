---
content_type: page
description: This section provides R tutorial about random numbers.
draft: false
title: 'R Tutorial b: Random Numbers'
uid: caf11256-bc50-4551-95a6-70ae98b5918a
---
In order to run simulations of experiments with random outcomes we make use of R's ability to generate random numbers. More precisely it generates a 'pseudo-random' number, which behaves in many ways like a truly random number.

## The Function Sample(x, k, replace = TRUE)

`# sample(x,k) generates a random permutation of k objects from the vector x. That is, all k choices are different.`

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

`# You can't pick more than 5 different elements from a set of 5 things, so R gives an error.`    
`> sample(x, 6)`    
`Error in sample.int(length(x), size, replace, prob):`    
`cannot take a sample larger than the population when 'replace = FALSE'`

**Allowing repeated elements**       
`# Sometimes you want to allow repeats. For example when &nbsp;we roll a die repeatedly we expect to see numbers repeating. We can think of this as picking a random element from a set and then putting it back, i.e. replacing it, so it can be drawn again.`

`# In R we do this by setting the optional argument replace=TRUE`

`# Note that we get can get repeated values`    
`> y = sample(x, 3, replace=TRUE)`    
`> print(y)`    
`[1] 3 1 4 # Your answer may be different.`    
`> y = sample(x, 3, replace=TRUE)`    
`> print(y)`    
`[1] 4 5 4 # Your answer may be different.`    
`> y = sample(x, 3, replace=TRUE)`    
`> print(y)`    
`[1] 2 1 5 # Your answer may be different.`    
`> y = sample(x, 5, replace=TRUE)`    
`> print(y)`    
`[1] 5 1 5 1 4 # Your answer may be different.`    
`> y = sample(x, 5, replace=TRUE)`    
`> print(y)`    
`[1] 3 5 5 2 1 # Your answer may be different.`    
`> y = sample(x, 5, replace=TRUE)`    
`> print(y)`    
`[1] 4 2 3 2 1 # Your answer may be different.`

`# Now there is no problem asking for more than 5 things from a set of 5 elements.`    
`> y = sample(x, 12, replace=TRUE)`    
`> print(y)`    
`[1] 1 1 2 1 4 2 3 4 1 2 4 5 # Your answer may be different.`    
`> y = sample(x, 12, replace=TRUE)`    
`> print(y)`    
`[1] 3 2 5 1 4 2 4 1 4 5 3 1 # Your answer may be different.`

`# To generate an m x n array of random values we can use the function sample function followed by the matrix function.`

`# Let's simulate rolling a die.`    
`# We use 1:6 to make vector (1,2,3,4,5,6).`

`# Generate a 3 x 4 array of random dice rolls.`    
`> y = sample(1:6, 12, replace=TRUE)`    
`> z = matrix(y, nrow=3, ncol=4)`    
`> print(z)`    
`[,1] [,2] [,3] [,4]`    
`[1,] &nbsp; &nbsp;1 &nbsp; &nbsp;3 &nbsp; &nbsp;6 &nbsp; &nbsp;1`    
`[2,] &nbsp; &nbsp;2 &nbsp; &nbsp;2 &nbsp; &nbsp;3 &nbsp; &nbsp;6`    
`[3,] &nbsp; &nbsp;2 &nbsp; &nbsp;1 &nbsp; &nbsp;4 &nbsp; &nbsp;3`

`# Or we could make it a 2 x 6 array.`    
`> z = matrix(y, nrow=2, ncol=6)`    
`> print(z)`    
`[,1] [,2] [,3] [,4] [,5] [,6]`    
`[1,] &nbsp; &nbsp;1 &nbsp; &nbsp;2 &nbsp; &nbsp;2 &nbsp; &nbsp;6 &nbsp; &nbsp;4 &nbsp; &nbsp;6`    
`[2,] &nbsp; &nbsp;2 &nbsp; &nbsp;3 &nbsp; &nbsp;1 &nbsp; &nbsp;3 &nbsp; &nbsp;1 &nbsp; &nbsp;3`    
`# Your answer may be different.`  

## Simulation

`# First let's simulate rolling 1 die 3 times and checking if one of the rolls was a 6.`

`# First we use sample to generate 3 samples from 1:6`   
`> x = sample(1:6, 3, replace=TRUE)`   
`> print(x)`   
`[1] 6 4 1 &nbsp;# Your answer may be different.`

`# To check if any of the 3 rolls are 6 we use the following command. It returns a vector of TRUE or FALSE depending on whether that entry of x is 6 or not. Note the use of the double equal sign. We can't use a single equal sign because that would mean 'set the value of x to 6'. Compare the result with the value of x above.`   
`> print(x == 6)`   
`[1] &nbsp;TRUE FALSE FALSE`   
`# Your answer may be different.`

`# &nbsp;We can also see which elements of x are less than 6`   
`> print(x < 6)`   
`[1] FALSE &nbsp;TRUE &nbsp;TRUE`   
`# Your answer may be different.`

`# &nbsp;Now let's roll the die 1000 times and see what fraction of the rolls give 6. We expect that about 1/6 of them will be.`

`# Simulate 1000 rolls`   
`> x = sample(1:6, 1000, replace=TRUE)`   
`# Your answer may be different.`

`# x == 6 gives a vector of TRUE or FALSE. R is clever, when we sum the vector: each TRUE counts as 1 and each FALSE counts as 0. So the sum is the number of TRUE's. In this case that means the number of 6's, which happens to be 168.`   
`> s = sum(x == 6)`   
`> print(s)`   
`[1] 168 &nbsp; # Your answer may be different.`

`# Divide by 1000 to get the fraction of 6's.`   
`> a = sum(x == 6)/1000`   
`> print(a)`   
`[1] 0.168 &nbsp; # Your answer may be different.`

`# Compare that with the theoretical value of 1/6.`   
`> print(1/6)`   
`[1] 0.1666667`   
`# Not bad!`

`# Now let's estimate the probability of getting at least one 6 in 4 rolls.`

`# Goal: estimate the probability of getting at least one 6 in 4 rolls.`   
`# Experiment: roll 1 die 4 times and check for a 6.`   
`# Repeat the experiment 10 times and see what fraction of times this happens.`

`# So you can see all the commands at once, we'll show them all and then explain them later. For commenting, we'll put a command number before each '>'.`   
`1. > x = matrix(sample(1:6, 4*10, replace=TRUE), nrow=4, ncol=10)`   
`2. > print(x)`   
`[,1] [,2] [,3] [,4] [,5] [,6] [,7] [,8] [,9] [,10]`   
`[1,] &nbsp; &nbsp;5 &nbsp; &nbsp;6 &nbsp; &nbsp;1 &nbsp; &nbsp;1 &nbsp; &nbsp;3 &nbsp; &nbsp;6 &nbsp; &nbsp;1 &nbsp; &nbsp;4 &nbsp; &nbsp;6 &nbsp; &nbsp; 1`   
`[2,] &nbsp; &nbsp;3 &nbsp; &nbsp;6 &nbsp; &nbsp;6 &nbsp; &nbsp;4 &nbsp; &nbsp;3 &nbsp; &nbsp;2 &nbsp; &nbsp;2 &nbsp; &nbsp;1 &nbsp; &nbsp;6 &nbsp; &nbsp; 5`   
`[3,] &nbsp; &nbsp;2 &nbsp; &nbsp;3 &nbsp; &nbsp;5 &nbsp; &nbsp;2 &nbsp; &nbsp;5 &nbsp; &nbsp;3 &nbsp; &nbsp;4 &nbsp; &nbsp;6 &nbsp; &nbsp;2 &nbsp; &nbsp; 5`   
`[4,] &nbsp; &nbsp;2 &nbsp; &nbsp;6 &nbsp; &nbsp;6 &nbsp; &nbsp;5 &nbsp; &nbsp;5 &nbsp; &nbsp;3 &nbsp; &nbsp;1 &nbsp; &nbsp;4 &nbsp; &nbsp;5 &nbsp; &nbsp; 3`   
`# Your answer may be different.`

`3. > y = (x==6)`   
`4. > print(y)`   
`[,1] &nbsp;[,2] &nbsp;[,3] &nbsp;[,4] &nbsp;[,5] &nbsp;[,6] &nbsp;[,7] &nbsp;[,8] &nbsp;[,9] [,10]`   
`[1,] FALSE &nbsp;TRUE FALSE FALSE FALSE &nbsp;TRUE FALSE FALSE &nbsp;TRUE FALSE`   
`[2,] FALSE &nbsp;TRUE &nbsp;TRUE FALSE FALSE FALSE FALSE FALSE &nbsp;TRUE FALSE`   
`[3,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE &nbsp;TRUE FALSE FALSE`   
`[4,] FALSE &nbsp;TRUE &nbsp;TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE`   
`# Your answer may be different.`

`5. > z = colSums(y)`   
`6. > print(z)`   
`[1] 0 3 2 0 0 1 0 1 2 0`   
`# Your answer may be different.`

`7. > print(z > 0)`   
`[1] FALSE &nbsp;TRUE &nbsp;TRUE FALSE FALSE &nbsp;TRUE FALSE &nbsp;TRUE &nbsp;TRUE FALSE`   
`8. > s = sum(z > 0)`   
`9. > print(s)`   
`[1] 5 &nbsp; # Your answer may be different.`

`10. > m = mean(z > 0)`   
`11. > print(m)`   
`[1] 0.5 # Your answer may be different.`

`# Command 1: Generate a 4 by 10 random array. Each column represents one experimental trial of 4 rolls. The 10 columns represent the 10 trials.`

`# Command 2: Display x`

`# Command 3: See which of the rolls are 6's. Note the double equals to check which rolls were 6. The result y is an array of TRUE or FALSE. You can check that it picks out the 6's.`

`# Command 4: Display y`

`# Command 5: Sum each of the columns. The result is then number of 6's in each trial (column).`

`# Command 6: Display z`

`# Command 7: If the column sum is greater than 0 there was at least one TRUE in the column, that is at least one 6. This command prints a vector of TRUE or FALSE representing &nbsp;whether or not the experiment yielded a 6.`

`# command 8: sum the vector in command 7 to get the number of trials that yielded a 6. We see that 5 out of 10 trials did. (This is random. Your answer may be different.)`

`# Command 9: Display s`

`# command 10: The mean function is just the sum divided by the number of trials. This is just 5/10 = .5. Half the trials yielded a 10.`

`# command 11: Display the mean`

`# Let's repeat this but with 1000 trials instead of 10. Without all the comments it's pretty short.`   
`> x = matrix(sample(1:6, 4*1000, replace=TRUE), nrow=4, ncol=1000)`   
`> y = (x==6)`   
`> z = colSums(y)`   
`> print(sum(z > 0))`   
`[1] 525`   
`> print(mean(z>0))`   
`[1] 0.525`

`Our estimate of the probability of at least one 6 in 4 rolls is .525. This is pretty close to the theoretical value of .518.`

`The dim() function`   
`# We can always check that x has 4 rows and 1000 columns using the dim() function.`   
`> print(dim(x))`   
`[1] &nbsp; &nbsp;4 1000`     

### One More Simulation

`# Goal: estimate the probability of getting a sum of 7 when rolling two dice.`  
`1. > ntrials = 10000`  
`2. > x = matrix(sample(1:6, 2*ntrials, replace=TRUE), nrow=2, ncol=ntrials)`  
`3. > y = colSums(x)`  
`4. > print(mean(y == 7))`  
`[1] 0.1658`

`# Command 1: We assign the number of trials to the variable ntrials. Writing code like this makes it easier to modify later. If we want to change the number of trials to 7 we just have to change this one line of code.`  
`# Command 2: we create 10000 columns with 2 rows. That is, we run 10000 experiments of rolling 2 dice.`  
`# Command 3: we sum each of the columns, i.e., we sum the two dice.`  
`# Command 4: we find the fraction of sums that are 7.`

`# Note, this is essentially the exact answer of 1/6.`

Exercise: Try to estimate the probability of two sixes when rolling two dice.