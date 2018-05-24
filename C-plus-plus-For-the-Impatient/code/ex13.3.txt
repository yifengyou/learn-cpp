// Exercise 13.3
// This version of the application continues in a loop,
// exiting only when the user presses ENTER (enters a
// zero length string).
//

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

     while(true) {       // DO UNTIL BREAK
        cout << "Enter file name, or press ENTER to exit: ";
        getline(cin, fname);
        if (fname.length() == 0) // BREAK ON EMPTY STRING.
             break;
        ifstream file_in(fname);
        if (!file_in) {
             cout << "Could not open file." << endl;
        } else {
             while(!file_in.eof()) {
                  getline(file_in, input_str);
                  cout << input_str << endl;
                  ++n;
                  if (n % (VERT_LINES - 2) == 0) {
                       if (!ask_more()) {
                            break;
                       }
                  }
              } // End while
         } // End else clause
     } // End outer while

//     EXIT SEQUENCE COMMENTED OUT, NOT REALLY NECESSARY.
//     cout << "Press ENTER to quit program.";
//     cin.ignore();  // Wait for user to press ENTER.
  
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

