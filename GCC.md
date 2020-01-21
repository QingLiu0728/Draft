## Usage of GCC

-o: rename the output file, default is a.out
-g: generate debug information

-w: no warning signal
-Wall: all warning signal

-O0: not optimize (for faster compile speed)
-O / -O1:
-O2:
-O3

-shared: build shared library
-static: build static library

-l<name>: link lib<name>.a lib, located at default fold or inside -L<folder>
e.g. -lm means find the libm.a library in the default library folder(/usr/lib).


-L<folder>: library folder

-I<folder>: header folder, the default is /usr/include/



https://www.runoob.com/w3cnote/cpp-static-library-and-dynamic-library.html

