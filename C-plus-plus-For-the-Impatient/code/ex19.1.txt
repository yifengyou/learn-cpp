// Exercise 19.1
// This version of the sample app replays the dice game, and keeps a running total
// of wins and losses.

#include <iostream>
#include <random>
#include <ctime>
#include <string>

using std::cout;            // Alternatively, you can use
using std::cin;             //  using namespace std;
using std::endl;
using std::string;
using std::default_random_engine;
using std::uniform_int_distribution;

int play_out_game(int point);
int start_game();
int roll_dice();

time_t seed = time(nullptr);
default_random_engine  eng(seed);
uniform_int_distribution<int>  dist(1, 6);

int main() {

     int nwins = 0;    // Number of wins
     int nlose = 0;    // Number of losses.
     string input_str;

     while (true) {
          if (start_game() == 1) {
               ++nwins;
          } else {
               ++nlose;
          }
          cout << "Number of wins:   " << nwins << endl;
          cout << "NUmber of losses: " << nlose << endl;
          cout << "Play again? (Y or N) ";
          getline(cin, input_str);     
          if (input_str != "Y" && input_str != "y") {
               break;
          }
     }
}

// Play the game:
// return 1 for win, 0 for loss
//
int start_game() {
     int rv = 0;          // Holds return value.
     int r = roll_dice();
     switch(r) {
     case 2:
     case 3:
     case 12:
         cout << "You lose!" << endl;
         return 0;
     case 7:
     case 11:
         cout << "You win!" << endl;
         return 1;
     default:
         return play_out_game(r);
     }
}

// Play Out Game function:
// Roll dice until 7 or the point is rolled.
// In this version, return 1 for win, 0 for loss.
//
int play_out_game (int point) {
     cout << "The point is now " << point << endl;
     while (true) {
          cout << "Press ENTER to roll... ";
          cin.ignore();   // Wait for user to press ENTER.
          int r = roll_dice();
          if (r == point) {
               cout << "You win!" << endl;
               return 1;
          } else if (r == 7) {
               cout << "You lose!" << endl;
               return 0;
          }
     }
}

// Roll Dice function.
// Roll two dice, print results, and return the total.
int roll_dice() {
     int n1 = dist(eng);     // Roll a die (1 to 6).
     int n2 = dist(eng);     // Roll another.
     cout << "Roll is: " << n1 << " " << n2 << ", ";
     cout << "for a total of " << n1 + n2 << "." << endl;
     return n1 + n2;
}