// Exercise 15.4
// This version of the sample app uses a list container rather than a vector.
//

#include <iostream>
#include <fstream>
#include <string>
#include <list>             // ADD THIS INCLUDE

using std::cout;            // Alternatively, you can use
using std::cin;             //  "using namespace std;"
using std::endl;
using std::ifstream;
using std::ofstream;
using std::string;

using std::list;            // ADD THIS.

list<string> str_list;      // CREATE LIST CONTAINER AND ITERATOR.
list<string>::iterator it;

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
          str_list.push_back(input_str);  // PUSH ONTO LIST
     }

     str_list.sort();                     // SORT THE LIST

     // Write out contents of str_vec to file_out. USE LIST VARS

     for(it = str_list.begin(); it != str_list.end(); ++it) {
          file_out << *it << endl;
     }
     cout << "Alphabetizing complete." << endl;
     cout << "Press ENTER to exit.";
     cin.ignore();  // Wait for user to press ENTER.
     return 0;
}

