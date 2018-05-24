// Exercise 12.1
// Expands further on the sample app by accepting month input 
// in the form of a 3-letter abbreviation for a month ("Jan") 
// as well as spelled-out name.

#include <iostream>
#include <string>
#include <ctime>
using std::cout;
using std::cin;
using std::endl;
using std::string;

string input_str;  // Use for input.

int get_month_num(string s);    // Convert-month-name-to-num function.

int main() {
  int a_year = 0, a_month = 0, a_day = 1;

  do {
     cout << "Enter a year from 1900 onward: ";
     cin >> a_year;

     cout << "Enter the name of the month or 3-letter abbreviation: ";
     cin >> input_str;
     a_month = get_month_num(input_str);
 
     cout << "Enter a day of the month, from 1 to 31: ";
     cin >> a_day;

     tm theday;              // Fill out tm structure.
     theday.tm_mday = a_day;
     theday.tm_mon = a_month - 1;
     theday.tm_year = a_year - 1900;
     theday.tm_hour = 12;    // Let's just go with noon.
     theday.tm_min = 0;
     theday.tm_sec = 0;

     time_t this_time = mktime(&theday);  // Get data.
     if (this_time != -1) {               // If date valid,
         char date_str[256];
         char format_str[] = "The day is %A, %d %B, %Y.";
         strftime(date_str, 256, format_str, &theday);
         cout << date_str << endl;
     }  else {
          cout << "Sorry. Invalid date." << endl;
     }
     cout << "I'm an excellent driver... ";
     cout << "Do again? (Enter Y or N.)";
     cin >> input_str;
     if (input_str[0] != 'Y' && input_str[0] != 'y') {
           break;
     }
  } while(true);
  return 0;
}

// Get Month Number Function.
// Accepts the name of a month.
// Note thta number returned is from  1 to 12; the
// program subtracts 1 from this later to convert to
// 0 to 11.

int get_month_num(string s) {
     if (s == "January" || s == "Jan")
          return 1;
     if (s == "Feburary" || s == "Feb")
          return 2;
     if (s == "March" || s == "Mar")
          return 3;
     if (s == "April" || s == "Apr")
          return 4;
     if (s == "May")
          return 5;
     if (s == "June" || s == "Jun")
          return 6;
     if (s == "July" || s == "Jul")
          return 7;
     if (s == "August" || s == "Aug")
          return 8;
     if (s == "September" || s == "Sep")
          return 9;
     if (s == "October" || s == "Oct")
          return 10;
     if (s == "November" || s == "Nov")
          return 11;
     if (s == "December" || s == "Dec")
          return 12;
     
     return 0;  // Default to an out of range number.
                // (Will be converted to -1.)
}
