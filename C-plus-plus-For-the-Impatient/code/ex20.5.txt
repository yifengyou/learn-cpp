// Exercise 20.5
// This version of the sample app detects and recovers from incorrect
// syntax in evaluation; when an operator is entered when there are
// less than two operands on stack, it reports the error and continues.

#include <iostream>
#include <string>
#include <cctype>
#include <regex>
#include <stack>

using std::cout;         // Alternatively, you can use
using std::cin;          //  using namespace std;
using std::endl;
using std::string;
using std::regex;
using std::sregex_iterator;
using std::stack;

void process_token(string s);
stack<double> st;

int main() {
     string instr; 
     string num_pattern("-?[0-9]+(\\.[0-9]*)?");
     string op_pattern("[+*/-]");
     regex re(num_pattern + "|" + op_pattern);
     while (true) {
         cout << "Enter expression (or ENTER to exit): ";
         getline(cin, instr);
         if (instr.length() == 0) { break; }
         sregex_iterator it(instr.begin(), instr.end(), re);
         sregex_iterator it_end;
         for (;it != it_end; ++it) {
              process_token(it->str());
         }
         if (!st.empty()) {
              cout << "The value is: " << st.top() << endl;
         }
     };
     return 0;
}

void process_token(string s) {
     // If s contains any char that is NOT an op,
     //  consider it a number by default.
     if (s.find_first_not_of("+*/-") != s.npos) {
          st.push(atof(s.c_str()));
     } else {

          // THIS IF STATEMENT IS ADDED TO DETECT ERROR CONDITION

          if (st.size() < 2) {
               cout << "Error: insufficient number of operands." << endl;
               return;
          }

          double op2 = st.top(); st.pop();
          double op1 = st.top(); st.pop();
          switch(s[0]) {
          case '+': st.push(op1 + op2); break;
          case '-': st.push(op1 - op2); break;
          case '*': st.push(op1 * op2); break;
          case '/': st.push(op1 / op2); break;
          }
     }
}
