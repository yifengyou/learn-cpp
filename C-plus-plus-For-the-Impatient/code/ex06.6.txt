// Exercise 06.6
// Sample app rewritten to use a smart pointer (unique_ptr).
// Note that it is much easier to make a unique_ptr global, because
// it is problematic to pass as a function argument.
//
// Note also that to access an array, a unique ptr must be 
// declared as:
//
//    unique_ptr<bool []> p;

#include <iostream>
#include <memory>
using std::unique_ptr;
using std::cout;
using std::cin;
using std::endl;

void process_prime(int max_n, int n);

unique_ptr<bool []> p;

int main() {
     int max_n = 0;
     cout << "Calculate primes up to what number? ";
     cin >> max_n;

     p.reset(new bool[max_n + 1]);  // Allocate array.

     for (int i = 2; i <= max_n; ++i) {    // Init array.
          p[i] = true;
     }
     for (int i = 2; i <= max_n; ++i) {    // Find primes.
          if (p[i]) {
               process_prime(max_n, i);
          }
     }
     cout << endl;
     
     cin.ignore();     // Consume last carriage return.
     cin.ignore();     // Wait for user to press ENTER.
     return 0;
}

// Process Prime function.
// Print the number n passed to the function, then
//   flag all the elements in the Boolean array (p)
//   as false if they correspond to a multiple of n.
//   So, p[i] <= false if i is a multiple of n.

void process_prime(int max_n, int n) {
     cout << n << "\t";
     for (int i = n + n; i <= max_n; i += n) {
          p[i] = false;
     }
}

