// Example 03.1.3
// This version of the program is rewritten to use "for".
//
// Note that the modular test (%) must now test for n % 4 = 3,
// because n is not incremented until the end of the loop!


#include <iostream>
using std::cout;
using std::cin;
using std::endl;

int main() {
    unsigned short  test_num = 0;   // Number to print.
    unsigned mask = 0x8000;         // Bit mask.
    cout << "Enter a number: ";
    cin >> test_num;
    for (int n = 0; n < sizeof(test_num) * 8; ++n) {
        cout << ((test_num & mask) != 0);  // Print 1 or 0.
        mask >>= 1;             // Then shift right.
        if (n % 4 == 3) {       // After every four digits,
             cout << " ";       //  print a space.
        }
    }
    cout << endl;
    cin.ignore();  // Consume last carriage return.
    cin.ignore();  // Wait for user to press ENTER.
    return 0;
}
