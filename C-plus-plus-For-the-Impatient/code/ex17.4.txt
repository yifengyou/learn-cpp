// Exercise 17.4
// This exercise modifies the sample app by telling the answer
// when he or she quits early. It also offers replay option.

#include <set>
#include <string>
#include <cctype>     // is_alpha() needed for purging.
#include <iostream>
#include <fstream>
#include <cstdlib>    // Include these 2 headers to support
#include <ctime>      //   srand, rand, time functs.

using std::set;       // Alternatively, you can use
using std::string;    //  using namespace std;
using std::ifstream;
using std::cout;
using std::cin;
using std::endl;

set<string> word_set;            // Word database.

string select_nth_word(int n);   // Iterate thru the set.
void purge_word(string &s);      // Get rid of non-letters.
void play_the_game(const string &target);

int main() {
     string fname;               // Name of text file.
     string a_word;              // Word to guess.

     cout << "Input name of a file to pick a word from: ";
     getline(cin, fname);
     ifstream file_in(fname);
     if (! file_in) {
          cout << "Could not open file." << endl;
          system("PAUSE");
          return 1;
     }
     while(file_in >> a_word) {
          word_set.insert(a_word);
     }

     // PUT GAME-PLAY STMTS INTO A LOOP

     while (true) {                 
          srand(static_cast<unsigned>(time(NULL)));
          int n = rand() % word_set.size();
          a_word = select_nth_word(n);
          purge_word(a_word);
          play_the_game(a_word);

          // QUERY USER AS TO WHETHER TO REPLAY GAME.          

          string input_str;
          cout << "Play again? Y or N: ";
          getline(cin, input_str);
          if (input_str != "Y" && input_str != "y") {
                break;
          }
     }
     
     return 0;  // JUST EXIT.
}

string select_nth_word(int n) {
     set<string>::iterator it;
     it = word_set.begin();
     while (n-- > 0) {
          ++it;
     }
     return *it;
}

void purge_word(string &s) {
     for (unsigned i = 0; i < s.size(); ++i) {
          if (!isalpha(s[i])) {
               s.erase(i);
          }
     }
     if (s.size() == 0) {
          s = "unknown";
     }
}

void play_the_game(const string &target) {
     string my_guess;
     while(true) {
          cout << "Enter your guess or press ENTER to exit: ";
          getline(cin, my_guess);
          if (my_guess.size() == 0) {

               // HERE IS THE NEW CODE...

               cout << "Oh! Too bad you want to quit! You gave up so easily!" << endl;
               cout << "The correct answer is: " << target << endl;
               return;

          } else if (my_guess < target) {
               cout << "Secret word is later in alpha order.";
          } else if (my_guess > target) {
               cout<<"Secret word is earlier in alpha order.";
          } else {
               cout << "That's it exactly! YOU WIN!" << endl;
               return;
          }
          cout << " Guess again." << endl;
     }
}

