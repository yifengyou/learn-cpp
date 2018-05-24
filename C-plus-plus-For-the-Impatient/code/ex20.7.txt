// Exercise 20.7
// This exercise primarily adds symbol-table capability (conveniently
// processed with a map container). It also preserves some of the
// capabilities added in previous exercises.
// Adding the symbol table enables processing of assignments, such as:
//
//   amount 3.5 =
//
// This input assigns the value 3.5 to a symbol named "amount". The
// next line of input then prints the result "7":
//
//   amount 2 *

#include <iostream>
#include <string>
#include <cctype>
#include <regex>
#include <stack>
#include <map>
#include <cmath>         // MUST BE ADDED TO SUPPORT pow().
#include <cctype>        // MUST BE ADDED TO SUPPORT isalpha().

using std::cout;         // Alternatively, you can use
using std::cin;          //  using namespace std;
using std::endl;
using std::string;
using std::regex;
using std::sregex_iterator;
using std::stack;
using std::map;          // ADDED TO SUPPORT MAP TEMPLATE.

struct tok {             // TOKENS MUST CONTAIN VALUE AND/OR
	double val;        //    SYMBOL NAME
	string name;
};


void process_token(string s);

stack<tok> st;                    // REVISED STACK FOR TOKENS.

map<string, double> symbol_map;   // SYMBOL TABLE.

int main() {
     string instr; 

// IN REG. EXPRESSION PATTERN, ADD SUPPORT FOR RECOGINITION OF
// SYMBOLS; FIRST CHAR. IS A LETTER; REMAINDER OF SYMBOL NAME
// IS A LETTER OR DIGIT.

     string num_pattern("-?[0-9]+(\\.[0-9]*)?");
     string op_pattern("[~^+*/-]|(==)|(!=)|=");
     string symbol_pattern("[a-zA-Z][a-zA-Z0-9]*");
     regex re(num_pattern + "|" + op_pattern + "|" + symbol_pattern);
     while (true) {
          while (!st.empty()) {                   // CLEAR I/O STACK
               st.pop();
          }
          cout << "Enter expression (or ENTER to exit): ";
          getline(cin, instr);
          if (instr.length() == 0) {
               break;
          }
          sregex_iterator it(instr.begin(), instr.end(), re);
          sregex_iterator it_end;
          for (;it != it_end; ++it) {
               string s = it->str();
               if (isalpha(s[0])) {               // READ A SYMBOL
                    tok t;
                    t.val = symbol_map[s];
                    t.name = s;
                    st.push(t);
               } else {
                    process_token(s);
               }
          }
          if (!st.empty()) {
              cout << "The value is: " << st.top().val << endl;
          }
     };
     return 0;
}


// Process token function.
// 

void process_token(string s) {
     if (isdigit(s[0])) {                        // HANDLE NUMBER.
          tok t;
          t.val = atof(s.c_str());
          st.push(t);
     } else if (s == "=") {                      // HANDLE ASSIGNMENT.
          if (st.size() < 2) {
               cout << "Error: insufficient number of operands." << endl;
               return;
          }
          double x = st.top().val; st.pop();
          string nm = st.top().name; st.pop();
          if (!nm.empty()) {        // CARRY OUT ASSIGNMENT ONLY IF
               symbol_map[nm] = x;  //  LEFT OP CONTAINS A SYMBOL.
          }
     } else if (s == "~") {                      // HANDLE UNARY ~.
          if (st.size() < 1 ) {
               cout << "Error: need an operand to use ~." << endl;
               return;
          }
          tok t;
          double op1 = st.top().val; st.pop();
          t.val = op1 * -1;
          st.push(t);
     } else {                                    // HANDLE OTHER OPS.
          if (st.size() < 2) {
               cout << "Error: insufficient number of operands." << endl;
               return;
          }
          tok t;
          double op2 = st.top().val; st.pop();
          double op1 = st.top().val; st.pop();
          switch(s[0]) {
          case '+': t.val = op1 + op2; st.push(t); break;
          case '-': t.val = op1 - op2; st.push(t); break;
          case '*': t.val = op1 * op2; st.push(t); break;
          case '/': t.val = op1 / op2; st.push(t); break;
          case '^': t.val = pow(op1, op2); st.push(t); break;
          case '=': t.val = (op1 == op2); st.push(t); break; // case ==
          case '!': t.val = (op1 != op2); st.push(t); break; // case !=
          }
     }
}
