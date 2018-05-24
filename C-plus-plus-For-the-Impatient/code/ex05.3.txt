// Exercise 05.3
// This version of the dice-odds program calculates the 
// profitability of playing the Field, which wins immediately on
// 2, 3, 4, 9, 10, 11, and 12; moreover, 2 and 12 pay double.
//
// Note that it's very easy to make a mistake and think this is
// a fair bet. The correct way to calculate is to assume that when
// a dollar is wagered, it has been spent. THEN look at the expected
// return on each number...
//
// If you lose, you don't get anything back. If you win, you get the
// original dollar you wagered plus another dollar, for a total of 2.
// If you win double (rolling a 2 or 12), you get the dollar you wagered,
// plus a payoff of two dollars, for a total return of 3 dollars.


#include <iostream>
using std::cout;
using std::cin;
using std::endl;

double calc_roll(int n);    // Function prototype

int dice_totals[11] = {1, 2, 3, 4, 5, 6, 5, 4, 3, 2, 1};

int main() {
     double prob_total = 0.0;  // Total probability of
                               //  player winning.
     for (int i = 2; i <= 12; ++i) {   // For each number,
          prob_total += calc_roll(i);  //   Find prob. of
     }                                 //   player winning.
     cout << "Here is your expected return for 1 dollar: ";
     cout << prob_total << endl;
     cout << "This is equivalent to having the following chance ";
     cout << "of winning: " << prob_total / 2;
     cin.ignore();  // Wait for user to press ENTER.
     return 0;
}

// Calc_roll: determine the mathematical EXPECTATION
// for each individual number: what can you expect to make
// by rolling this number? This figure is the total return
// multiplied by the probability of the roll.
//
// Note that we view the dollar as already being spent. If
// you win, then you get the dollar back, plus a winning of
// of either an additional $1, or, in the case of 2 and 12,
// TWO additional dollars.
//
double calc_roll(int n) {
     double d = dice_totals[n - 2];
     double prob_roll = d/36.0;
     
     switch(n) {
     case 2:
     case 12:               // Win your dollar back, plus 2 more.
          return prob_roll * 3;
          break;
     case 3:
     case 4:
     case 9:
     case 10:
     case 11:               // Win your dollar back, plus 1 more.
          return prob_roll * 2;
          break;
     default:
          return 0;
          break;
     }
}