# Guess The Pokemon


## Problem Statement:

Have you heard the new trending game? GUESS THE POKEMON!!! Please come try out our vast database of pokemons.

## Solution

The website displays a text input. Entering a guess gives us a verdict on whether our answers were right or wrong. Downloading the ZIP file also contains a Data Base file, from which we can figure out is SQL. 

We can use SQL injection in order to trick the website into thinking we guessed correctly. An input you may try is `' OR 1=1 --`, but we are greeted with an error saying "**no quotes or backslashes:)**".

We can get around this by using a different OR statement that doesn't utilize any quotes or backslashes: 
`105 OR 1=1`

Doing so will yield the flag.


![Image](./guesspoke.png)

## Answer

`LITCTF{flagr3l4t3dt0pok3m0n0rsom3th1ng1dk}`