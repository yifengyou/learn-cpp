// Exercise 04_1.2
// This version of the program reprompts user for input
// if a non-numeric value is input.

#include <iostream>
using std::cout;
using std::cin;
using std::endl;

int main() {
   int lower_bound, upper_bound;  // Used in guessing.
   int n = 1;                     // This is the guess.
   int cmd = 1;                   // Menu command.

// do-while syntax inserted to eliminate need for goto.

   do {
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

           // HERE IS THE NEW INPUT CODE:
            
           while (!(cin >> cmd)) {
                cin.clear();  // Clear error flags.
                cin.sync();   // Discard chars in buffer.
                cout << "Invalid input. Re-enter. " << endl;
           } 

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

       // HERE IS THE NEW INPUT CODE:
            
       while (!(cin >> cmd)) {
            cin.clear();  // Clear error flags.
            cin.sync();   // Discard chars in buffer.
            cout << "Invalid input. Re-enter. " << endl;
       }

   } while (cmd == 1);  // Cycle if cmd "1" entered.
   return 0;
}

