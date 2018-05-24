If you play the game optimally, the max. number of guesses you
should ever have to make is given by the formula:

    log-base-2(n + 1)

in which n is the number of target values. After taking this value,
round upward to the nearest integer.

The complete formula is therefore:

    ceil(log-base-2(n + 1))

So, if n is 50, the max. number of guesses you should have to make
is ceil(log-base-2(52)), which is equal to the log-base-2 of
64 (the next higher power of 2), which is 6.