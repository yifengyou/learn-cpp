The problem with the regular-expression string shown in this exercise is that the dot (.) is not
preceeded by backslashes:

     [0-9]+(.[0-9]*)?

Consequently, the dot is interpreted to match ANY one character! It could, for example, match a
space or an operator, causing lines of input to be incorrectly read.

The dot in this case should be preceeded by a backslash:

     [0-9]+(\.[0-9]*)?

To be specified as a standard C++ string  (not a raw literal), you'd need to use two backslashes:

     "[0-9]+(\\.[0-9]*)?"