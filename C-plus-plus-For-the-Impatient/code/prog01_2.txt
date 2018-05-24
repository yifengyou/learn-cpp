#include <iostream>
using std::cout;
using std::cin;
using std::endl;

int main() {
     int n = 0;
     double prev1 = 1.0;
     double prev2 = 1.0;
     double current = 0.0;
     cout << "How many Fib. nums to generate? ";
     cin >> n;              // Get input
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

