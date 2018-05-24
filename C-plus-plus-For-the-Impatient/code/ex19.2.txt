// Exercise 19.2
// This exercise modifies the sample app by weighting the dice;
// one die produces 3 twice as often as it should, and the other 
// produces 4 twice as often as it should.

#include <iostream>
#include <random>
#include <ctime>

using std::cout;            // Alternatively, you can use
using std::cin;             //  using namespace std;
using std::endl;
using std::default_random_engine;
using std::uniform_int_distribution;
using std:: bernoulli_distribution;    // ADD THIS DECLARATION.


void play_out_game(int point);
int roll_dice();

time_t seed = time(nullptr);
default_random_engine  eng(seed);
uniform_int_distribution<int>  dist(1, 6);
bernoulli_distribution         b_dist(0.14);  // DIST. USED FOR
                                              // BIASED ROLLING.
                                              // PRODUCES "TRUE" 14% OF TIME

int main() {
     int r = roll_dice();
     switch(r) {
     case 2:
     case 3:
     case 12:
         cout << "You lose!" << endl;
         break;
     case 7:
     case 11:
         cout << "You win!" << endl;
         break;
    default:
         play_out_game(r);
         break;
     }
     cout << "Press ENTER to exit game.";
     cin.ignore();   // Wait for user to press ENTER.
     return 0;
}

// Play Out Game function:
// Roll dice until 7 or the point is rolled.
void play_out_game (int point) {
     cout << "The point is now " << point << endl;
     while (true) {
          cout << "Press ENTER to roll... ";
          cin.ignore();   // Wait for user to press ENTER.
          int r = roll_dice();
          if (r == point) {
               cout << "You win!" << endl;
               return;
          } else if (r == 7) {
               cout << "You lose!" << endl;
               return;
          }
     }
}

// Roll Dice function.
// Roll two dice, print results, and return the total.
//
int roll_dice() {
     int n1 = 0, n2 = 0;  // Record dice rolls.

     // ROLL DICE: Use Bernoulli distribution (b_dist) to 
     // check weigting factor (0.14). if result is
     // "true", use the biased number (3 or 4). Otherwise,
     // roll a fair die.

     if (b_dist(eng)) {
         n1 = 3;
     } else {
         n1 = dist(eng);
     }
     if (b_dist(eng)) {
         n2 = 4;
     } else {   
         n2 = dist(eng);
     }

     cout << "Roll is: " << n1 << " " << n2 << ", ";
     cout << "for a total of " << n1 + n2 << "." << endl;
     return n1 + n2;
}

