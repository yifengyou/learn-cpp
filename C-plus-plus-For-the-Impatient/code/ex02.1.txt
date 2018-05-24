// Example 02.1
// This example adds a test to determine type that results when
//  two vars of type float are added together.


#include <iostream>
using std::cout;
using std::endl;

int main() {
     char c = 0;
     int si = 0;
     unsigned int ui = 0;
     double d = 0.0;
     float f = 0.0;      // Here is the new decl.

     d = f = ui = si = c;    // This avoids warning msg's.
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

     if (typeid(f + f) == typeid(double)) {
        cout << "type of (float + float) is double" << endl;
     } else if (typeid(f + f) == typeid(float)) {
        cout << "type of (float + float) is float" << endl;
     }

     cin.ingore();  // Wait for user to press ENTER.
     return 0;
}

