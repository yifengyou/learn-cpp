#include <iostream>
#include <string>
#include <sstream>
#include <list>

using std::string;        // Alternatively, you can use
using std::stringstream;  //  using namespace std.
using std::list;
using std::cout;
using std::cin;
using std::endl;

list<double> numList;

double get_nth_item(int n);

int main() {
     string input_str;
     cout << "Enter a series of numbers: ";
     getline(cin, input_str);
     stringstream ss(input_str);
     double x = 0.0;
     while (ss >> x) {
          numList.push_back(x);
     }
     numList.sort();
     int n1 = numList.size()/2;
     int n2 = (numList.size() - 1)/2;
     cout << "Median value is: ";
     cout <<  (get_nth_item(n1) + get_nth_item(n2)) / 2;
     cout << endl;
     cout << "Press ENTER to exit.";
     cin.ignore();
     return 0;
}

double get_nth_item(int n) {
     list<double>::iterator it = numList.begin();
     while(n-- > 0) {
          ++it;
     }
     return *it;
}

