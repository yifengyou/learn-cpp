// Exercise 06.4
// This version of the sample app reports the total number
// of primes found.

#include <iostream>
using std::cout;
using std::cin;
using std::endl;

void process_prime(bool *p, int max_n, int n);

int num_of_primes = 0;  // ADD THIS GLOBAL VAR DECL.

int main() {
     int max_n = 0;
     cout << "Calculate primes up to what number? ";
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
     cout << "Total number of primes found is: ";
     cout << num_of_primes << endl;

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

void process_prime(bool *p, int max_n, int n) {

     ++num_of_primes;  // INCREMENT GLOBAL VAR.

     cout << n << "\t";
     for (int i = n + n; i <= max_n; i += n) {
          p[i] = false;
     }
}

