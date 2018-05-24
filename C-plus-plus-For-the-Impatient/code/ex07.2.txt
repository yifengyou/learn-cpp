// Exercise 07.2. 
// This declaration of the Pack_bool class includes a destructor; this destructor should
// free memory pointed to by ptr.




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

     ~Pack_bool() {           // DESTRUCTOR ADDED.
           delete [] ptr;
     }

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


