// Example 04_1.3
// This exercise modifies the sample app by keeping track
// of how many guesses were made.

#include <iostream>
#include <cstdlib>
#include <ctime>
using std::cin;
using std::cout;
using std::endl;

int main() {
      srand(time(NULL));       // Set random seed.
      bool play_more = true;
      int target = 0;
      int guess = 0;

      while (play_more) {     // While play_more is true...
            int target = 1 + rand() % 50;  // New target.

            int num_guesses = 0;  // NUMBER OF GUESSES.
  
            while (true) {
                cout << "Guess the number, or 0 to quit: ";
                cin >> guess;
                
                ++num_guesses;   // INCREMENT NUMBER OF GUESSES.

                if (guess == 0) {          // Time to quit.
                    play_more = false;
                    break;
                } else if (guess == target) {
                    cout << "CORRECT!!! Number is ";
                    cout << target << "! " << endl;

                    cout << "It only took you " << num_guesses;
                    cout << " guesses! ";

                    cout << "Let's play again!" << endl;
                    break;
                } else if (guess < target) {
                    cout << "Too low! Try again!" << endl;
                } else {
                    cout << "Too high! Try again!" << endl;
                }
            }  // End of inner while loop.
      }  // End of outer while loop.
      return 0;
}

