// Exercise 13.1
// This version of the application reprompts user until a 
// valid file name is entered.

#include <string>
#include <iostream>
#include <fstream>

using std::cout;         // Alternatively, you can use
using std::cin;          //   using namespace std;
using std::endl;
using std::string;
using std::ifstream;

#define VERT_LINES  25   // # of vertical lines per screen.

bool ask_more();         // Function used for pausing.

int main() {
     string fname;       // File name.
     string input_str;   // String used to hold file input.
     int n = 0;

     ifstream file_in;   // THIS VAR MUST NOW BE DECLARED SEPARATELY

     // INPUT STMT NOW REPLACED WITH A LOOP

     while (true) {
          cout << "Enter file name: ";
          getline(cin, fname);
          file_in.open(fname);
          if (file_in)
               break;
          cout << "could not open file. Re-enter." << endl;
     }

     while(!file_in.eof()) {
          getline(file_in, input_str);
          cout << input_str << endl;
          ++n;
          if (n % (VERT_LINES - 2) == 0) {
               if (!ask_more()) {
                    break;
               }
          }
     }

     cout << "Press ENTER to quit program.";
     cin.ignore();  // Wait for user to press ENTER.
     return 0;
}

// Ask More function:
// Pause and prompt the user as to whether to continue;
// Return true unless user wants to quit.
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

