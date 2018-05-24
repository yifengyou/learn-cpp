// Example 03.1.5
// This exercise prints for a string of digits and then 
// prints out their numeric value. The STL string type is
// used, so <string> must be included. 
//
// The size() member function is used to get length of the input. 
//
// For each digit entered, the process is to (1) double the amount
// (which starts at 0) and then (2) add 1 to it if the digit is 1.


#include <iostream>
#include <string>   // Remember to include <string>.

using std::cout;
using std::cin;
using std::endl;
using std::string;  // Remember that "string" is in std namespace.

int main() {

    int n = 0;
    unsigned long amt = 0;   // Amount to accumulate value in.
    string input_str;
    cout << "Enter string of digits: ";
    cin >> input_str;
    while (n < input_str.size()) {
         amt *= 2;                   // Double amt.
         if (input_str[n] == '1') {  // Then add 1 digit is 1.
              amt += 1;
         }
         ++n;
    }
    cout << "Amount is: " << amt;
    cout << endl;
    cin.ignore();  // Consume last carriage return.
    cin.ignore();  // Wait for user to press ENTER.
    return 0;
}

