// Exercise 19.4
// This exericse tests seven different random-generation engines by
// printing out the internal state of each one, so that you can
// compare them for amount of space each occupies in memory.
//

#include <iostream>
#include <random>
#include <ctime>

using namespace std;

int roll_dice();

time_t seed = static_cast<unsigned>(time(nullptr));

default_random_engine     dre(seed);
minstd_rand               mr(seed);
minstd_rand0              mr0(seed);
ranlux24_base             r24(seed);
mt19937                   mt(seed);
mt19937_64                mt64(seed);
knuth_b                   knu(seed);

uniform_int_distribution<int>   dist(1, 6);

int main() {
     cout << "Default random engine... (Press any key to continue)";
     cin.ignore();   // Wait for user to press ENTER.
     cout << dre << endl << endl;
	 
     cout << "minstd_rand engine... (Press any key to continue)";
     cin.ignore();   // Wait for user to press ENTER.
     cout << mr << endl << endl;
	 
     cout << "minstd_rand0 engine... (Press any key to continue)";
     cin.ignore();   // Wait for user to press ENTER.
     cout << mr0 << endl << endl;
	 
     cout << "ranlux24_base engine... (Press any key to continue)";
     cin.ignore();   // Wait for user to press ENTER.
     cout << r24 << endl << endl;
	 
     cout << "mt19937 engine... (Press any key to continue)";
     cin.ignore();   // Wait for user to press ENTER.
     cout << mt << endl << endl;
	 
     cout << "mt19937_64 random engine... (Press any key to continue)";
     cin.ignore();   // Wait for user to press ENTER.
     cout << mt64 << endl << endl;
	 
     cout << "Knuth engine... (Press any key to continue)";
     cin.ignore();   // Wait for user to press ENTER.
     cout << knu << endl << endl;

   
     cout << "Press any key to exit." << endl;
     cin.ignore();   // Wait for user to press ENTER.
     return 0;
}




