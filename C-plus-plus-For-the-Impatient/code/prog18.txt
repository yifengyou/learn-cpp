#include <iostream>
#include <string>
#include <sstream>
#include <algorithm>
#include <vector>
using namespace std;

int main() {
     int n = 0;
     string inStr;            // Input string.
     vector<double>  xVec;    // Vector to contain numbers.
     cout << "Enter nums: ";
     getline(cin, inStr);     // Get line of input.
     stringstream ss(inStr);
     while (ss >> n, ss) {       // While there's another
           xVec.push_back(n);    //   num to read, add it
     }                           //   to the vector.
     sort(xVec.begin(), xVec.end());
     n = xVec.size();
     int n1 = xVec[n/2];         // Get middle 2 values.
     int n2 = xVec[(n - 1)/2];
     cout << "Median val. is: " << (n1 + n2)/2 << endl;
     cin.ignore();         // Wait for user to press ENTER.
     return 0;
}

