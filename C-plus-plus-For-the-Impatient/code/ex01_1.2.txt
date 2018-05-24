// Exercise 01.1.2
// This version of the program tests the expression "cin >> n""
// directly; the value returned is the value of the stream cin.
// This test true while numeric input is valid; it tests false
// as soon as non-numeric input is entered.

#include <iostream>
using std::cout;
using std::cin;
using std::endl;

int main () {
     int sum = 0;
     int n = 1;
     cout << "Enter a list of numbers, terminated with 0 ";
     cout << "or non-digit." << endl << "Enter: ";
     while (cin >> n) {   // While numeric input is valid,
          sum = sum + n;  // Add to sum
     }
     cout << "Total is: " << sum << endl;
     cout << "Press ENTER to exit.";

     cin.clear();         // Flush buffer and restore cin.
     cin.sync();          

     cin.ignore();  // Pause for user to press ENTER.
     return 0;
}

