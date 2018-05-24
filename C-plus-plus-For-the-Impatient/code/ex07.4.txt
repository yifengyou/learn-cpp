// Exercise 17.4.
// This version of the Pack_bool class performs a no-op (no operation)
// the user of the class attempts to access a bit value that is
// out of range.


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
     void resize(int n);
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
     if (n < 0 || n >= max_n) {  // NO-OP
         return;
     }
     int i = n / 8;
     int j = n % 8;

     ptr[i] |= (0x01 << j);      // Turn it on! (COMBINED |= OP USED.)
}

// Clear Bit member funct:
// Find the target bit and use combination of bitwise
// negation and bitwise AND to set it to zero.
//
void Pack_bool::clear_bit(int n) {
     if (n < 0 || n >= max_n) {  // NO-OP
         return;
     }
     int i = n / 8;
     int j = n % 8;
     ptr[i] &= ~(0x01 << j);     // Turn it off! (COMBINED &= USED.)
}

// Get Bit member funct:
// Find the target bit and use bitwise AND to get its value.
//
bool Pack_bool::get_bit(int n) {
     if (n < 0 || n >= max_n) {  // NO-OP
         return 0;
     }
     int i = n / 8;
     int j = n % 8;
     return (ptr[i] & (0x01 << j)) != 0;
}


//
//
void resize(int n) {
     

}
