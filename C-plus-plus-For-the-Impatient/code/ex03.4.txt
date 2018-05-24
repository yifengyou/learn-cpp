// Example 03.1.4
// This version of the program prints bits in reverse order.
// Instead of comparing test_num to a bit mask (0x8000), it
// prints 1 or 0 depending on whether or not test_num is odd;
// then test_num is shifted 1 to the right. 


#include <iostream>
using std::cout;
using std::cin;
using std::endl;

int main() {
    int n = 0;                      // Loop variable.
    unsigned short  test_num = 0;   // Number to print.
    cout << "Enter a number: ";
    cin >> test_num;
    while (n++ < sizeof(test_num) * 8) {

        // The next two lines are modified from the example.

        cout << test_num % 2;   // Print 1 if test_num is odd.        
        test_num >>= 1;         // Shift test_num right.

        if (n % 4 == 0) {       // After every four digits,
             cout << " ";       //  print a space.
        }
    }
    cout << endl;
    cin.ignore();  // Consume last carriage return.
    cin.ignore();  // Wait for user to press ENTER.
    return 0;
}

