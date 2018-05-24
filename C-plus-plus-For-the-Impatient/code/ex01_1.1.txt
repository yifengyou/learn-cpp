// Exercise 1.1.1
// This program is the same as the program in the book but is
// rewritten to use double type instead of int for the variable in
// which to store input; also var is renamed from n to x.

#include <iostream>
using std::cout;
using std::cin;
using std::endl;

int main () {
     double sum = 0.0;
     double x = 1.0;
     cout << "Enter a list of numbers, terminated with 0 ";
     cout << "or non-digit." << endl << "Enter: ";
     while (x != 0.0) {   // While n is not zero...
          cin >> x;       //   Attempt to read next integer.
          if (!cin) {     //   If read failed, set n to 0.
               x = 0.0;
          }
          sum = sum + x;
     }

     cout << "Total is: " << sum << endl;
     cout << "Press ENTER to exit.";
     cin.ignore();  // Consume carriage return.
     cin.ignore();  // Pause for user to press ENTER.
     return 0;
}

