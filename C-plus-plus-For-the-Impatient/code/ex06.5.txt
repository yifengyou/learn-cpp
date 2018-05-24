// Exercise 06.5
// This version of the sample app lists the primes only for a
// specific range, in which the user specifies both the lower
// and upper bounds... Program is almost the same; the same
// calculations have to be done; but a number is not printed if
// it is less than the lower bound specified by the user.

#include <iostream>
using std::cout;
using std::cin;
using std::endl;

void process_prime(bool *p, int max_n, int n);

int min_n = 0;

int main() {
     int max_n = 0;
     cout << "List primes beginning with what number? ";
     cin >> min_n;
     cout << "Up to what number? ";
     cin >> max_n;
     bool *p = new bool[max_n + 1];    // Allocate array.
     for (int i = 2; i <= max_n; ++i) {    // Init array.
          p[i] = true;
     }
     for (int i = 2; i <= max_n; ++i) {    // Find primes.
          if (p[i]) {
               process_prime(p, max_n, i);
          }
     }
     cout << endl;
     delete [] p;      // Not absolutely necessary, but
                       //   a good idea.
     cin.ignore();     // Consume last carriage return.
     cin.ignore();     // Wait for user to press ENTER.
     return 0;
}

// Process Prime function.
// Print the number n passed to the function, then
//   flag all the elements in the Boolean array (p)
//   as false if they correspond to a multiple of n.
//   So, p[i] <= false if i is a multiple of n.
//
void process_prime(bool *p, int max_n, int n) {
     if (n >= min_n) {
          cout << n << "\t";
     }
     for (int i = n + n; i <= max_n; i += n) {
          p[i] = false;
     }
}

