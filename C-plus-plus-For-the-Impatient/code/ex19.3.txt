// Exercise 19.3
// This exericse tests seven different random-generation engines by
// checking how many microsecs each takes to roll 220,000 dice.
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
     time_t t1, t2;
	 int n = 0;

     // Default random engine
     t1 = clock();
     for (int i = 0; i < 220000; ++i) {
          n = dist(dre);
     }
     t2 = clock();
     cout << "default random engine took " << t2 - t1 << " mss." << endl;

     // minstd_rand engine
     t1 = clock();
     for (int i = 0; i < 220000; ++i) {
          n = dist(mr);
     }
     t2 = clock();
     cout << "minstd_rand engine took    " << t2 - t1 << " mss." << endl;

     // minstd_rand0 engine
     t1 = clock();
     for (int i = 0; i < 220000; ++i) {
          n = dist(mr0);
     }
     t2 = clock();
     cout << "minstd_rand0 engine took   " << t2 - t1 << " mss." << endl;

     // randlux24_base engine
     t1 = clock();
     for (int i = 0; i < 220000; ++i) {
          n = dist(r24);
     }
     t2 = clock(); 
     cout << "randlux24_base engine took " << t2 - t1 << " mss." << endl;    

	 // mt19937 engine
     t1 = clock();
     for (int i = 0; i < 220000; ++i) {
          n = dist(mt);
     }
     t2 = clock();
     cout << "mt19937 engine took        " << t2 - t1 << " mss." << endl;

     // mt19937_64 engine
     t1 = clock();
     for (int i = 0; i < 220000; ++i) {
          n = dist(mt64);
     }
     t2 = clock();
     cout << "mt19937_64 engine took     " << t2 - t1 << " mss." << endl;

     // Knuth engine
     t1 = clock();
     for (int i = 0; i < 220000; ++i) {
          n = dist(knu);
     }
     t2 = clock();
     cout << "Knuth engine took          " << t2 - t1 << " mss." << endl;

     cout << "Press any key to exit." << endl;
     cin.ignore();   // Wait for user to press ENTER.
     return 0;
}


