// Exercise 09.1
// This version of the sample app adds the ability to detect
// long and unsigned long types.

#include <iostream>
#include <string>

using std::cout;
using std::cin;
using std::endl;
using std::string;

template<typename T1, typename T2>
string return_type(T1 a, T2 b) {
     if (typeid(a + b) == typeid(int))
          return "int";
     if (typeid(a + b) == typeid(unsigned))
          return "unsigned";
     if (typeid(a + b) == typeid(float))
          return "float";
     if (typeid(a + b) == typeid(double))
          return "double";
     if (typeid(a + b) == typeid(char))
          return "char";

// NEW TESTS ADDED HERE.

     if (typeid(a + b) == typeid(long))
          return "long";
     if (typeid(a + b) == typeid(unsigned long))
          return "unsigned long";

     return "other";
}

int main() {
     char ch = 'a';
     int si = 0;
     unsigned ui= 0;
     double x = 0.0;
     float flt = 0.0F;

     cout << "ch + si => " << return_type(ch, si) << endl;
     cout << "si + si => " << return_type(si, si) << endl;
     cout << "si + ui => " << return_type(si, ui) << endl;
     cout << "si + x  => " << return_type(si, x) << endl;
     cout << "x + flt => " << return_type(x, flt) << endl;

     long sl = 0;

     cout << "si + sl => " << return_type(si, sl) << endl;
     cout << "ui + sl => " << return_type(ui, sl) << endl;
     cin.ignore();   // Wait for user to press ENTER.
     return 0;
}

