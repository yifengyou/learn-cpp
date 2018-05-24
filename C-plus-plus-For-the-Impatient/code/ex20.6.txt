// Exercise 20.6
// This exercise adds the following operators: exponent (^),
// arithmetic negation (~), test for equality and inequality (== and !=).
// Arithmetic negation is a unary operation and must be handled differently.

#include <iostream>
#include <string>
#include <cctype>
#include <regex>
#include <stack>
#include <cmath>         // MUST BE ADDED TO SUPPORT pow() FUNCT.

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
     string op_pattern("[~^+*/-]|(==)|(!=)");                // ADD TO OP PATTERN HERE.
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


// Process token function.
// THIS FUNCT. IS MODIFIED TO HANDLE ^, ~, !=, AND ==.
// SINCE THE MAIN FUNCTION LOOKS FOR "!=" AND "==" AS
// OPERATORS, WE ASSUME THAT THE FIRST CHARACTER FOR THESE
// OPS ARE "!" AND "="... IT ISN'T NECESSARY TO LOOK AT 
// SECOND CHARACTER.

void process_token(string s) {
     // If s contains any char that is NOT an op,
     //  consider it a number by default.
     if (s.find_first_not_of("=!~^+*/-") != s.npos) {      // ADD TO OP PATTERN HERE.
          st.push(atof(s.c_str()));
     } else if (s == "~") {                                // HANDLE UNARY ~.
          if (st.size() < 1 ) {
               cout << "Error: need an operand to use ~." << endl;
               return;
          }
          double op1 = st.top(); st.pop();
          st.push(op1 * -1);
     } else {
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
          case '^': st.push(pow(op1, op2)); break;  // HANDLE NEW OPS.
          case '=': st.push(op1 == op2); break;
          case '!': st.push(op1 != op2); break;
          }
     }
}

