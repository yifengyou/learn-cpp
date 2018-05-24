// Exercise 05.2
// This version of the dice-odds program calculates of winning
// by betting on the "Don't Pass" bar. The bet is that the
// dice roller loses... however, rolls of 12 are considered
// ties. So, this program (1) counts rolls of 12 as "half a win"
// and (2) subtracts total probability from 1.0, because we are
// betting AGAINST the shooter.
//
// Note: the resulting probability, 0.493182, is just slightly
// better than the regular bet, a win probability of 0.492929.


#include <iostream>
using std::cout;
using std::cin;

double calc_roll(int n);    // Function prototype

int dice_totals[11] = {1, 2, 3, 4, 5, 6, 5, 4, 3, 2, 1};

int main() {
     double prob_total = 0.0;  // Total probability of
                               //  player winning.
     for (int i = 2; i <= 12; ++i) {   // For each number,
          prob_total += calc_roll(i);  //   Find prob. of
     }                                 //   shooter winning.
     cout << "Probability of winning on Don't Pass Bar: ";

     cout << 1.0 - prob_total;  // Probability of shooter LOSING

     cin.ignore();  // Wait for user to press ENTER.
     return 0;
}

// Calc_roll: return the probability of shooter rolling n AND
// going on to win the game. (In the case of 7 or 11,
// this is just the probability of rolling the number.)
//
// However, in this version of the program, a roll of 12 is
// a tie and so is considered half a win.
//
double calc_roll(int n) {
     double d = dice_totals[n - 2];
     double prob_roll = d/36.0;
     
     switch(n) {
     case 2:
     case 3:                   // Instant loser.
          return 0;
          break;
     case 12:                  // It's a tie; count as half a win.
          return prob_roll / 2.0;
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
