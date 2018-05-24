// Exercise 01.1.3
// This version of the program uses an additional variable
// named "number_of_items." It is set equal to 0 and
// incremented each another number is input by user.

#include <iostream>
using std::cout;
using std::cin;
using std::endl;

int main () {
     int sum = 0;
     int n = 1;
     int number_of_items = 0;
     cout << "Enter a list of numbers, terminated with 0 ";
     cout << "or non-digit." << endl << "Enter: ";
     while (n != 0) {   // While n is not zero...
          cin >> n;     //   Attempt to read next integer.
          if (!cin) {   //   If read failed, set n to 0.
               n = 0;
          } else {
               ++number_of_items;
          }
          sum = sum + n;
     }
     cout << "Total is: " << sum << endl;
     cout << "Number of items is: ";
     cout << number_of_items << endl;
     cout << "Press ENTER to exit.";
     cin.ignore();  // Consume carriage-return.
     cin.ignore();  // Pause for user to press ENTER.
     return 0;
}

