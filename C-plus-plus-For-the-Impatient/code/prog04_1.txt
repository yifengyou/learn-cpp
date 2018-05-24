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
            while (true) {
                cout << "Guess the number, or 0 to quit: ";
                cin >> guess;
                if (guess == 0) {          // Time to quit.
                    play_more = false;
                    break;
                } else if (guess == target) {
                    cout << "CORRECT!!! Number is ";
                    cout << target << "! " << endl;
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

