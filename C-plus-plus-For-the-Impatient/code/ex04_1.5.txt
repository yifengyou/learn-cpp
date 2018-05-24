// Example 04_1.5
// This exercise calculates number of guesses required to
// guess from 1 to n, applying formula
// 
//   answer = ceil(log_base_2(n + 1))
//
// To calculate log_base_2, use log(n + 1)/log(2).


#include <iostream>
#include <math>

using std::cin;
using std::cout;
using std::endl;

int main() {
    int n;

    cout << "Enter number of possible values: ";
    cin >> n;
    double x = ceil(log(n + 1) / log(2));
    cout << static_cast<int>(x);
    cout << " guesses required." << endl;
      
    cin.ignore();  // Consume last carriage return.
    cin.ignore();  // Wait for user to press ENTER.
    return 0;
}

