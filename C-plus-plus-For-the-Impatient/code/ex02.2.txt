// Example 02.2
// This example adds a test to determine type that results
//  when an unsigned char is added to an int.


#include <iostream>
using std::cout;
using std::endl;

int main() {
     char c = 0;
     int si = 0;
     unsigned int ui = 0;
     double d = 0.0;
     unsigned char uc = 0;    // Here is the new decl.

     d = ui = si = c = uc;    // This avoids warning msg's.
     if (typeid(c + c) == typeid(int)) {
          cout << "type of (char + char) is int" << endl;
     }
     if (typeid(si + ui) == typeid(unsigned)) {
          cout << "type of (int + unsigned int) ";
          cout << "is unsigned" << endl;
     }
     if (typeid(si + d) == typeid(double)) {
        cout << "type of (int + double) is double" << endl;
     }

     // Here are the new statements.

     if (typeid(si + uc) == typeid(int)) {
        cout << "type of (si + uc) is int" << endl;
     } else if (typeid(si + uc) == typeid(unsigned int)) {
        cout << "type of (si + uc) is unsigned int" << endl;
     }

     cin.ingore();  // Wait for user to press ENTER.
     return 0;
}

