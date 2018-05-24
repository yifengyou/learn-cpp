// Exercise 01.2.2.
// This version of the program introduces a while loop to test
// number input through cin. If The input is not valid, cin
// will test false. In that case, n is set to 0 (to ensure the
// while loop will continue), the cin error flags are cleared,
// and the end user is prompted again.


#include <iostream>
using std::cout;
using std::cin;
using std::endl;

int main() {
     int n = 0;
     double prev1 = 1.0;
     double prev2 = 1.0;
     double current = 0.0;

     while (n == 0 ) {
          cout << "How many Fib. nums to generate? ";
          if (!(cin >> n)) {
               n = 0;
               cin.clear();  // Clear error flags.
               cin.sync();   // Disard chars in buffer.
               cout << "Invalid input. Re-enter. " << endl;
          }
     }

     cout.precision(15);    // Set 15 digits of precision.
     while (n > 0) {        // While n is greater than 0...
          current = prev1 + prev2;
          prev2 = prev1;
          prev1 = current;
          cout << current << "\t";
          cout << "ratio = " << prev1/prev2 << endl;
          --n;             // Subtract 1 from n.
     }
     cout << endl;
     cout << "Press ENTER to exit.";
     cin.ignore();  // Consume carriage-return.
     cin.ignore();  // Pause for user to press ENTER.
     return 0;
}

