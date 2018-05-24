The Sieve program is more efficient for a number of reasons,
not least of which is that the Sieve doesn't require the computation of
square roots.

In general, though, the Sieve is more efficient because once a 
prime number is found, subsequent composite numbers are eliminated as
a result; all these numbers never need to be looked at again. For 
example, since 2 is prime, all even numbers larger than 2 are quickly
struck from consideration for prime-ness. Moreover, as the algorithm
proceeds, composite numbers become more dense, so it becomes
increasingly common to simply skip over numbers after looking at a
Boolean value. So, over time, the efficiency of the Sieve increases.

With the "brute force" approach, each individual number has to be 
checked by using a prime-number-detection scheme. This requires a 
for loop inside a forloop.

This analysis, however, assumes that you want to detect the
prime-ness of ALL numbers between 2 and N. If you want only want to
check one individual number for being a prime, the brute force approach
may potentially be faster.