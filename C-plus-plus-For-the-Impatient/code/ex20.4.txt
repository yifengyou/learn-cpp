// Exercise 20.3.
// This exercise mdifies the sample application so that it can accept numeric
// expressions in any of several floating-point formats, such as "3.5E20".
// 

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

         // THE FOLLOWING STAMENTS CREATE PATTERNS CORRESPONDING TO
	 // THE DIFFERENT FLOATING POINT FORMATS. NOTE THAT THE MORE
	 // COMPLEX FORMATS MUST BE PLACED FIRST, OR THE REGEX
	 // ENGINE WILL SETTLE FOR THE SIMPLER FORMATS AND SKIP
	 // OVER CHARACTERS THAT DON'T FIT.

	 string num1 = "(-?[0-9]+E[0-9]+)";
	 string num2 = "(-?[0-9]+\\.[0-9]+E[0-9]+)";
 	 string num3 = "(-?[0-9]+(\\.[0-9]*)?)";
	 string num4 = "(-?\\.[0-9]+)";

	 string num_pattern(num1 + "|" + num2 + "|" + num3 + "|" + num4);

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

