#include <iostream>
#include <fstream>
#include <string>
#include <vector>

using std::cout;            // Alternatively, you can use
using std::cin;             //  "using namespace std;"
using std::endl;
using std::ifstream;
using std::ofstream;
using std::string;
using std::vector;

vector<string> str_vec;        // Holds lines of text.
vector<string>::iterator it;   // Iterator into str_vec.
void insert_string(string s);  // Inserts strings in alpha
                               //   order.
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
void insert_string(string s) {
       it = str_vec.begin();
       while(it != str_vec.end() && s > *it)
            ++it;
       str_vec.insert(it, s);
}

