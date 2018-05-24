// Exercise 16.1
// This version of the sample application fills out a list,
// sorts it, and then copies the contents to a vector by using
// the appropriate constructor. From there, it is an easy matter
// to index into the vector.

#include <iostream>
#include <string>
#include <sstream>
#include <list>
#include <vector>

using std::string;        // Alternatively, you can use
using std::stringstream;  //  using namespace std.
using std::list;
using std::cout;
using std::cin;
using std::endl;
using std::vector;

list<double> numList;

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

     vector<double> numVec(numList.begin(), numList.end());

     int n1 = numList.size()/2;
     int n2 = (numList.size() - 1)/2;
     cout << "Median value is: ";
     cout <<  (numVec[n1] + numVec[n2]) / 2;
     cout << endl;
     cout << "Press ENTER to exit.";
     cin.ignore();
     return 0;
}

