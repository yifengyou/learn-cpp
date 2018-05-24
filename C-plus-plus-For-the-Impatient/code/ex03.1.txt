// Example 03.1.1
// This version of the program replaces "mask = mask >> 1"
// with "mask >>= 1".


#include <iostream>
using std::cout;
using std::cin;
using std::endl;

int main() {
    int n = 0;                      // Loop variable.
    unsigned short  test_num = 0;   // Number to print.
    unsigned mask = 0x8000;         // Bit mask.
    cout << "Enter a number: ";
    cin >> test_num;
    while (n++ < sizeof(test_num) * 8) {
        cout << ((test_num & mask) != 0);  // Print 1 or 0.
        mask >>= 1;             // Then shift right.
        if (n % 4 == 0) {       // After every four digits,
             cout << " ";       //  print a space.
        }
    }
    cout << endl;
    cin.ignore();  // Consume last carriage return.
    cin.ignore();  // Wait for user to press ENTER.
    return 0;
}

