#include <iostream>
using std::cout;
using std::cin;
using std::endl;

int main() {
     int lower_bound, upper_bound;  // Used in guessing.
     int n = 1;                     // This is the guess.
     int cmd = 1;                   // Menu command.
top_of_prog:
     lower_bound = 1;
     upper_bound = 50;
     cout << "Think of a number from 1 to 50." << endl;
     cout << "Then press ENTER.";
     cin.ignore();   // Wait for user to press ENTER.
     bool guess_again = true;
     do {
        n=static_cast<int>((lower_bound+upper_bound)/2.0);
        cout << "I guess " << n << "." << endl;
        cout << "Respond: 1=Correct!  2=Guess was too ";
        cout << "low!  3==Guess was too high! ENTER => ";
        cin >> cmd;
        if (cmd == 1) {
             cout << "Yay! I got it right!" << endl;
             guess_again = false;
        } else if (cmd == 3) {
             upper_bound = n - 1;
        } else {
             lower_bound = n + 1;
        }
     } while (guess_again);
     cout << "Play again? 1=Yes  2=No. ENTER: ";
     cin >> cmd;
     if (cmd == 1) goto top_of_prog;
     return 0;
}

