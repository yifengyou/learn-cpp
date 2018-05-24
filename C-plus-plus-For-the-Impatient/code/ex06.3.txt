// Exercise 06.3
// This version of the sample app uses integers rather than the
// bool type. Although usually you'd never want to do this, this
// exercise does show the versatility of the int type and the fact
// that the bool type, at bottom, is an integer type.
//
// Note: some early versions of C did not support bool type and so
// required this kind of programming.

#include <iostream>
using std::cout;
using std::cin;
using std::endl;

// FUNCTION DECLARED WITH int* TYPE FOR FIRST ARG, NOT *bool.

void process_prime(int *p, int max_n, int n);

int main() {
     int max_n = 0;
     cout << "Calculate primes up to what number? ";
     cin >> max_n;

     // THIS NEXT STATEMENT CHANGED TO USE INT, NOT BOOL.

     int *p = new int[max_n + 1];    // Allocate array.

     for (int i = 2; i <= max_n; ++i) {    // Init array.
          p[i] = 1;     // INIT TO 1 RATHER THAN "true".
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
void process_prime(int *p, int max_n, int n) {
     cout << n << "\t";
     for (int i = n + n; i <= max_n; i += n) {
          p[i] = 0;   // SET TO 0 RATHER THAN "false".
     }
}

