// Exercise 07.1. This exercise uses the Pack_bool (packed Boolean) class in conjunction
// with the Sieve of Eratosthenes example at the end of Chapter 6. Note that the code
// taken from Chapter 6 must be revised to work with the methods of the Pack_bool class
// rather than trying to index it.

#include <iostream>
using std::cout;
using std::cin;
using std::endl;



// Packed Boolean class: creates a virtual Boolean array
// of dynamic length, storing each Boolean in one bit.
//
class Pack_bool {
private:
     int max_n;               // Number of bits.
     int nbytes;              // Number of bytes required.
     unsigned char *ptr;      // Pointer to the bit data.
public:
     Pack_bool(int max);      // Constructor – sets # bits.
     void set_bit(int n);
     void clear_bit(int n);
     bool get_bit(int n);
     void set_all_true() {
         for(int i = 0; i < nbytes; ++i) {ptr[i]=0xFF;}
     }
     void set_all_false() {
          for(int i = 0; i < nbytes; ++i) {ptr[i]=0x00;}
     }
};

// Constructor: divide max by 8 and round up
// to get number of byes to allocate.
//
Pack_bool::Pack_bool(int max) {
     max_n = max;
     nbytes = (max_n + 7) / 8;
     ptr = new unsigned char[nbytes];
}

// Set Bit member funct:
// Find the target bit and use bitwise OR to turn it on.
//
void Pack_bool::set_bit(int n) {
     int i = n / 8;
     int j = n % 8;
     ptr[i] = ptr[i] | (0x01 << j);   // Turn it on!
}

// Clear Bit member funct:
// Find the target bit and use combination of bitwise
// negation and bitwise AND to set it to zero.
//
void Pack_bool::clear_bit(int n) {
     int i = n / 8;
     int j = n % 8;
     ptr[i] = ptr[i] & ~(0x01 << j);
}

// Get Bit member funct:
// Find the target bit and use bitwise AND to get its value.
//
bool Pack_bool::get_bit(int n) {
     int i = n / 8;
     int j = n % 8;
     return (ptr[i] & (0x01 << j)) != 0;
}



void process_prime(Pack_bool &pb, int max_n, int n);

int main() {
     int max_n = 0;
     cout << "Calculate primes up to what number? ";
     cin >> max_n;
     Pack_bool pb(max_n);    // Invoke Pack_bool constr.
     pb.set_all_true();
     for (int i = 2; i <= max_n; ++i) {    // Find primes.
          if (pb.get_bit(i)) {
               process_prime(pb, max_n, i);
          }
     }
     cout << endl;
     cin.ignore();     // Consume last carriage return.
     cin.ignore();     // Wait for user to press ENTER.
     return 0;
}

// Process Prime function.
// Print the number n passed to the function, then
//   flag all the bits in the pb data structure
//   as false if they correspond to a multiple of n.
//
// Notice that the Pack_bool arg (pb) is passed by
// reference, as there is no need to make a copy of it.


void process_prime(Pack_bool &pb, int max_n, int n) {
     cout << n << "\t";
     for (int i = n + n; i <= max_n; i += n) {
          pb.clear_bit(i);
     }
}

