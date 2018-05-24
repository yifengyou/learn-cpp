// Ex 06.7
// This version of the sample app tests for insufficient memory
// by first using the nothrow keyword. Use of this keyword causes
// the value returned by "new" to be null if memory is insufficient
// and no bad_alloc exception to be thrown.

#include <iostream>

#include <new>       // NEW DIRECTIVES REQUIRED.
using std::nothrow;

using std::cout;
using std::cin;
using std::endl;

void process_prime(bool *p, int max_n, int n);

int main() {
     int max_n = 0;
     cout << "Calculate primes up to what number? ";
     cin >> max_n;
     bool *p = new (nothrow) bool[max_n + 1];  // NOTHROW.

     if (!p) {
          cout << "Insufficient memory." << endl;
          return -1;
     }
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
void process_prime(bool *p, int max_n, int n) {
     cout << n << "\t";
     for (int i = n + n; i <= max_n; i += n) {
          p[i] = false;
     }
}

