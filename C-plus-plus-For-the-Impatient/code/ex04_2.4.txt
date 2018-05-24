// Exercise 04_1.4
// This version of the game detects logically invalid input
// on the part of the end user and then restarts the game
// in that situation. The logic is: if lower_bound is 
// higher than upper_bound or upper_bound is lower than
// lower_bound, then there has been a mistake.

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
           cin >> cmd;
           if (cmd == 1) {
               cout << "Yay! I got it right!" << endl;
               guess_again = false;
           } else if (cmd == 3) {
               upper_bound = n - 1;
           } else {
               lower_bound = n + 1;
           }

           // NEW LINES OF CODE ADDED HERE:

           if (upper_bound < lower_bound || lower_bound > upper_bound) {
               cout << "You gave incorrect information at some point! ";
               cout << "I'm cancelling this game." << endl;
               guess_again = false;
           } 

       } while (guess_again);
       cout << "Play again? 1=Yes  2=No. ENTER: ";
       cin >> cmd;
   } while (cmd == 1);  // Cycle if cmd "1" entered.
   return 0;
}

