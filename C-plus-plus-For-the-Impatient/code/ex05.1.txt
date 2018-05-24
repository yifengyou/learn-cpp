// Exercise 05.1
// This version of the dice-odds program calculates the odds
// of winning at craps, but replaces the call to make_point
// with the expression d/(d + 6.0).


#include <iostream>
using std::cout;
using std::cin;

double calc_roll(int n);    // Function prototypes
double make_point(int n);

int dice_totals[11] = {1, 2, 3, 4, 5, 6, 5, 4, 3, 2, 1};

int main() {
     double prob_total = 0.0;  // Total probability of
                               //  player winning.
     for (int i = 2; i <= 12; ++i) {   // For each number,
          prob_total += calc_roll(i);  //   Find prob. of
     }                                 //   player winning.
     cout << "Total probability of winning: ";
     cout << prob_total;
     cin.ignore();  // Wait for user to press ENTER.
     return 0;
}

// Calc_roll: return the probability of rolling n AND
// going on to win the game. (In the case of 7 or 11,
// this is just the probability of rolling the number.)
//
double calc_roll(int n) {
     double d = dice_totals[n - 2];
     double prob_roll = d/36.0;
     
     switch(n) {
     case 2:
     case 3:
     case 12:                  // Instant loser.
          return 0;
          break;
     case 7:
     case 11:                  // Instant winner.
          return prob_roll;
          break;
     default:
          return prob_roll * d/(d + 6.0);
          break;
     }
}


