// Exercise 16.3
// This version of the sample app deals with the situation in which the user
// enters no data. There are a number of different ways to handle. (You could,
// for example, reprompt the user.) This solution takes the approach of just
// ending gracefully.

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

     // THESE NEXT 5 LINES ARE THE ONES NEEDED FOR THIS EXERCISE...

     if (numList.empty()) {
          cout << "No numbers were entered. Press ENTER to exit." << endl;
               cin.ignore();
          return -1;
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
