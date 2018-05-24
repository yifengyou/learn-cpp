// Exercise 17.1.
// This version of the sample app performs case-insensitve comparisions,
// by calling a function to do such comparisons.

#include <set>
#include <string>
#include <cctype>     // is_alpha() needed for purging.
#include <iostream>
#include <fstream>
#include <cstdlib>    // Include these 2 headers to support
#include <ctime>      //   srand, rand, time functs.

#include <cctype>     // ADD TO SUPPORT toupper.

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

int comp_str(string s1, string s2);   // CASE-INSENSITIVE COMP FUNCT.

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
     srand(static_cast<unsigned>(time(NULL)));
     int n = rand() % word_set.size();
     a_word = select_nth_word(n);
     purge_word(a_word);
     play_the_game(a_word);
     cout << endl;
     cin.ignore();   // Wait for user to press ENTER.
     return 0;
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
               return;          
          } 

          // USE RESULTS OF CASE-INSENSITIVE STR COMPARISON

          int n = comp_str(my_guess, target);
          if (n < 0) {
               cout << "Secret word is later in alpha order.";
          } else if (n > 0) {
               cout<< "Secret word is earlier in alpha order.";
          } else {
               cout << "That's it exactly! YOU WIN!" << endl;
               return;
          }
          cout << " Guess again." << endl;
     }
}


// Case-insensitive compare-string function.
// Return -1, 0, or 1 depending on whether first string
// is before, equal, or later in alpha order.
// This function ignores case by converting both arguments
// to all-uppercase and then comparing.
//
int comp_str(string s1, string s2) {
     string temp1;
     string temp2;
     for (int i = 0; i < s1.size(); ++i) {
          temp1 += toupper(s1[i]);
     }
     for (int i = 0; i < s2.size(); ++i) {
          temp2 += toupper(s2[i]);
     }
     if (temp1 < temp2) return -1;
     if (temp1 > temp2) return 1;
     return 0;
}
