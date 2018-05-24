// Example 13.2
// This version of the application prints output in all uppercase
// letters. It uses the toupper() function to do this. (See Ch 12.)

#include <string>
#include <iostream>
#include <fstream>
#include <cctype>         // INCLUDE THIS HEADER FOR toupper().

using std::cout;         // Alternatively, you can use
using std::cin;          //   using namespace std;
using std::endl;
using std::string;
using std::ifstream;

#define VERT_LINES  25   // # of vertical lines per screen.

bool ask_more();         // Function used for pausing.

string convert_to_upper(string s);  //  CONV. FUNCTION

int main() {
     string fname;       // File name.
     string input_str;   // String used to hold file input.
     int n = 0;
     cout << "Enter file name: ";
     getline(cin, fname);
     ifstream file_in(fname);
     if (!file_in) {
          cout << "Could not open file." << endl;
     } else {
          while(!file_in.eof()) {
               getline(file_in, input_str);

               // CALL TO CONVERSION FUNCTION ADDED HERE.

               cout << convert_to_upper(input_str) << endl;

               ++n;
               if (n % (VERT_LINES - 2) == 0) {
                    if (!ask_more()) {
                         break;
                    }
               }
          } // End while
     } // End else clause
     cout << "Press ENTER to quit program.";
     cin.ignore();  // Wait for user to press ENTER.
     return 0;
}

// Ask More function:
// Pause and prompt the user as to whether to continue;
// Return true unless user wants to quit.
//
bool ask_more() {
     string input_str;
     cout << endl << "[PRESS ENTER for more, Q to quit]: ";
     getline(cin, input_str);
     if (input_str.size() > 0) {
          char c = input_str[0];
          if (c == 'Q' || c == 'q') {
               return false;
          }
     }
     return true;
}

// Convert to upper function
// This is added to make this exercise work.
// Declare an empty output string, and then concatenate characters
// from string argument after converting to uppercase.
//
string convert_to_upper(string s) {
     string output_str;
     for (int i = 0; i < s.length(); ++i) {
          output_str += toupper(s[i]);
     }
     return output_str;
}

