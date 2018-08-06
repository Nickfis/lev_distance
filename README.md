# Implementation of Levenshtein Distance in Python

This project was done as a group work during the first trimester in my Data Science Master's degree at Barcelona Graduate School of Economics. The code can be found in the jupyter notebook and a more extensive write-up in the pdf. 

### What is the goal?
Given strings X and Y, the proposed algorithm needs to be able to calculate the amount of
minimum modifications needed to turn string X into string Y. Furthermore it needs to choose the best
option between the possible edit modifications and log which edits were performed. The amount of needed
modification is called the edit distance between the two strings. Since we are searching for an optimal
algorithm we have to find a way of storing all the alternative costs and compare them to choose the minimum.
This problem has a wide variety of possible applications, starting with spellchecking for autocorrect to analyzing the DNA genom.

### Using recursion to solve the problem

In order to solve this problem we will turn it into a number of smaller subproblems and first of all take look at the first index of the strings X and Y. Since they need to be equal in the end, we know that they will have the same length and match all characters in each position. Therefore we start by looking at X[0] and Y[0] and consider the possible routes to take if they do not match:

#### I Substitution

By replacing the first character of the string Y we do one modification. After doing this both strings start with the same character, so we will need to compute the edit distance for X[1,...,n] and
Y[1,...,m] characters. The final result would therefore be the cost of the substitution of X[0] plus the edit distance of the remaining substrings. 

#### II Insertion

We could also match the first index of both strings by inserting the first character of Y to the beginning of X. The cost for this solution would be the cost of the insertion plus the edit distance of the original string X and Y[1,...,m]. 

#### III Deletion 
Analog to the insertion,when deleting, we only get rid of the first character in X (X[0]). In this case after the modification we have to compute the remaining edit distance between X[1,...,m] and the original string Y and add the cost of the deletion for the optimal solution.

Using dynamic programming we can reduce the time to compute the optimal solution, since by storing the
already computed values in a matrix, with index i for X and index j for Y, we will not recurrently solve every subproblem again. By solving every one of the subproblems by choosing the option with the minimum cost we will eventually choose the minimum solution for every step and reach the optimal solution for the overall problem.
