// Example 03.1.6
// This exercise does the same thing as ex03.5, except that
// it skips over blank spaces in the input. To do that, it has
// to test specifically for blank spaces; it does not double
// the accumulated amount unless a digit is entered.
//
// Note that getilne() function must be used to get an entire
// line of input, blanks included.

#include <iostream>
#include <string>    // Remember to include <string>.

using std::cout;
using std::cin;
using std::endl;
using std::string;    // Remember that "string" is in std namespace.

int main() {

    int n = 0;
    unsigned long amt = 0;   // Amount to accumulate value in.
    string input_str;
    cout << "Enter string of digits: ";

    getline(cin, input_str); // Get entire line of input.
    
    while (n < input_str.size()) {
         int dig = input_str[n];     // Get digit.
         if (dig == '1' || dig == '0') {
              amt *= 2;              // Double amt if digit is 0 or 1.
         }
         if (dig == '1') {           // Then add 1 if digit is 1.
              amt += 1;
         }
         ++n;
    }
    cout << "Amount is: " << amt;
    cout << endl;

    cin.ignore();  // Wait for user to press ENTER.
    return 0;
}

