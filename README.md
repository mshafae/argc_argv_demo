# Argc & Argv Demo

All programs have an entry point. In C++, [the entry point to our program is the main function](https://en.wikipedia.org/wiki/Entry_point#C_and_C.2B.2B).

```c++
#include <iostream>

using namespace std;

int main(int argc, char const *argv[]) {
  cout << "Hello World!\n"
  return 0;
}
```

In this hello world program, the main function has the prototype `int main(int argc, char const *argv[])`. This means that the function's name is `main`, it's return type is `int`, and it has a named and typed parameter list. 

The parameter list is `(int argc, char const *argv[])`. There are two parameters. We can also call the parameters arguments. The first parameter is named `argc` and it is an `int` type. The second parameter is named `argv` and it is a `char const* []` type.

It may appear that `argv` is very complicated yet it is just a list of words. If you type in the command `./argc_argv_demo cat dog rhino bird sheep`, then `argv` will be created by the operating system and initialized for you to contain the list of words "cat", "dog", "rhino", "bird", "sheep". This means that `argv` will have 5 items in it and they will be numbered from 0 through 4. (Remember in C++, we start counting from 0.)

To access something that is entered on the command line, we just need to walk from the start of the list at location 0 all the way to the end. The way we know the length of `argv` is by using `argc`. The variable `argc` is a count of how many strings (or words) are stored in `argv`.

With some practice, you can write programs that will read in arguments from the command line.

# How to Build

This example program has a [Makefile](https://en.wikipedia.org/wiki/Makefile) which you may use to build the program `argc_argv_demo`. The Makefile has the following targets:

* all: builds the project
* clean: removes object and dependency files
* spotless: removes everything the clean target removes and all binaries
* format: outputs a [`diff`](https://en.wikipedia.org/wiki/Diff) showing where your formatting differes from the [Google C++ style guide](https://google.github.io/styleguide/cppguide.html)
* tidy: output of the [linter](https://en.wikipedia.org/wiki/Lint_(software)) to give you tips on how to improve your code
* headercheck: check to make sure your files have the appropriate header

To build the program use the `make` command. The Makefile's default target is to build `all`.

# Example Output

Below is an example of what to expect when using the program `argc_argv_demo`.

```
$ make
set -e; clang++ -MM -g -Wall -pipe -std=c++14  argc_argv_demo.cc \
	| sed 's/\(argc_argv_demo\)\.o[ :]*/\1.o argc_argv_demo.d : /g' > argc_argv_demo.d; \
	[ -s argc_argv_demo.d ] || rm -f argc_argv_demo.d
clang++ -g -Wall -pipe -std=c++14  -c argc_argv_demo.cc
clang++ -g -Wall -pipe -std=c++14 -o argc_argv_demo argc_argv_demo.o 
$ ./argc_argv_demo 
The command that was executed is: "./argc_argv_demo"
The argument count (argc) is 1
Argv stores the command line arguments as strings...
argv[0] is "./argc_argv_demo"
$ ./argc_argv_demo cat dog rhino bird sheep
The command that was executed is: "./argc_argv_demo cat dog rhino bird sheep"
The argument count (argc) is 6
Argv stores the command line arguments as strings...
argv[0] is "./argc_argv_demo"
argv[1] is "cat"
argv[2] is "dog"
argv[3] is "rhino"
argv[4] is "bird"
argv[5] is "sheep"
$ ./argc_argv_demo cat blue 1.123 orange 4 yellow 0.123 red -4.87
The command that was executed is: "./argc_argv_demo cat blue 1.123 orange 4 yellow 0.123 red -4.87"
The argument count (argc) is 10
Argv stores the command line arguments as strings...
argv[0] is "./argc_argv_demo"
argv[1] is "cat"
argv[2] is "blue"
argv[3] is "1.123"
argv[4] is "orange"
argv[5] is "4"
argv[6] is "yellow"
argv[7] is "0.123"
argv[8] is "red"
argv[9] is "-4.87"
$ 
```