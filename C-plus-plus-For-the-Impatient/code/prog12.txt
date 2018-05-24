#include <iostream>
#include <string>
#include <ctime>
using std::cout;
using std::cin;
using std::endl;
using std::string;

string input_str;  // Use for "Y or N?" input.

int main() {
  int a_year = 0, a_month = 0, a_day = 1;

  do {
     cout << "Enter a year from 1900 onward: ";
     cin >> a_year;
     cout << "Enter a month from 1 to 12: ";
     cin >> a_month;
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

