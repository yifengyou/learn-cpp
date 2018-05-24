// Exercise 15.2
// This exercise modifies the sample application by performing
// case-insenstive comparisons on strings.

#include <iostream>
#include <fstream>
#include <string>
#include <vector>
#include <cctype>           // ADD THIS INCLUDE

using std::cout;            // Alternatively, you can use
using std::cin;             //  "using namespace std;"
using std::endl;
using std::ifstream;
using std::ofstream;
using std::string;
using std::vector;

vector<string> str_vec;        // Holds lines of text.
vector<string>::iterator it;   // Iterator into str_vec.

void insert_string(string s);       // Inserts strings in alpha
                                    //   order.
int comp_str(string s1, string s2); // Case-insensitive compare funct.

int main() {
     string ifname;
     string ofname;
     string input_str;
     cout << "Enter name of input file: ";
     getline(cin, ifname);
     ifstream file_in(ifname);
     if (!file_in) {
          cout << "File could not be opened." << endl;
          system("PAUSE");
          return -1;
     }
     cout << "Enter name of output file: ";
     getline(cin, ofname);
     ofstream file_out(ofname);
     if (!file_out) {
          cout << "File could not be opened." << endl;
          system("PAUSE");
          return -1;
     }
     // Read in lines of text and insert into str_vec.
     while(!file_in.eof()) {
          getline(file_in, input_str);
          insert_string(input_str);
     }
     // Write out contents of str_vec to file_out.
     for(it = str_vec.begin(); it != str_vec.end(); ++it) {
          file_out << *it << endl;
     }
     cout << "Alphabetizing complete." << endl;
     cout << "Press ENTER to exit.";
     cin.ignore();  // Wait for user to press ENTER.
     return 0;
}

// Insert String function.
// Search for proper insertion spot according to alpha
//   order; then insert the string.
//
void insert_string(string s) {
      it = str_vec.begin();
      while(it != str_vec.end() && comp_str(s, *it) > 0)
           ++it;
      str_vec.insert(it, s);
}


// Case-insensitive string comparison function.
// Works by first converting temp strings to all lowercase.
// Fnct returns 1, 0, -1, depending on whether first string
// is later in the order, equal, or earlier in alpha order.
//
int comp_str(string s1, string s2) {
     string temp1, temp2;
     for (int i = 0; i < s1.length(); ++i) {
          temp1 += toupper(s1[i]);
     }
     for (int i = 0; i < s2.length(); ++i) {
          temp2 += toupper(s2[i]);
     }
     if (temp1 < temp2) return -1;
     else if (temp1 == temp2) return 0;
     else return 1;
}

     