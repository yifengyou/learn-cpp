// Exercise 16.4.
// This exercise calculates standard deviation for a set of numbers.
// (It also calculates min, max, and average along with median, as
// was done for Exercise 16.2.)

#include <iostream>
#include <string>
#include <sstream>
#include <list>

#include <cmath>          // NECESSARY TO SUPPORT sqrt().

using std::string;        // Alternatively, you can use
using std::stringstream;  //  using namespace std.
using std::list;
using std::cout;
using std::cin;
using std::endl;

list<double> numList;

double get_nth_item(int n);

double calc_std_dev(double avg);     // CALCULATE STANDARD DEVIATION
                                     // (given the average as input!)

int main() {
     double total = 0.0;   // KEEP TRACK OF TOTAL (NEED FOR AVG.)
     double minx = 0.0;    // TRACK MINIUMUM VALUE ENTERED.
     double maxx = 0.0;    // TRACK MAX VALUE ENTERED.

     string input_str;
     cout << "Enter a series of numbers: ";
     getline(cin, input_str);
     stringstream ss(input_str);
     double x = 0.0;
     while (ss >> x) {
          numList.push_back(x);
          total += x;
          if (numList.size() == 1) { // FIGURE MIN AND MAX
               minx = maxx = x;
          } else if (x < minx) {
               minx = x;
          } else if (x > maxx) {
               maxx = x;
          }
     }
     numList.sort();
     int n1 = numList.size()/2;
     int n2 = (numList.size() - 1)/2;
     cout << "Median value is: ";
     cout <<  (get_nth_item(n1) + get_nth_item(n2)) / 2;
     cout << endl;

     // THESE STATEMENTS REPORT AVG, MIN, & MAX... PLUS STD. DEV.

     double avg = total/numList.size();
     cout << "Average is: " << avg << endl;
     cout << "Standard deviation is: " << calc_std_dev(avg) << endl;
     cout << "Minimum value is: " << minx << endl;
     cout << "Maximum value is: " << maxx << endl;

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


// CALCULATE STANDARD DEVIATION:
// This is much easier to calculate if average (avg.) is already known,
// so that this function doesn't have to iterate through the list twice.
//
double calc_std_dev(double avg) {
     double sum = 0.0;
     list<double>::iterator it;

     // For each item, add the square of deviation from avg. to sum.

     for (it = numList.begin(); it != numList.end(); ++it) {
           double x = *it - avg;
           sum += x * x;
     }

     // Now, divide this sum by the number of items, and return the
     // square root of the result:
 
     return sqrt(sum/numList.size());
}
