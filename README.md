# cpp_option_parser

## Simple C++ option parser
+ This library can be used in any command line software for an easy option parsing.
Accessed in code with [] operator, the options of the command line are encoded in string objects. Further conversion in integer or floating values can be made. This choice simplifies the code and make it python like.  

+ Each option is represented by both a small and a long name, and also has a description and a default value. The short name is recognised on command line when preceded by a -, the long name with a --. 

+ Note : If an option is required and no default value can be set, just precise it in the description and put a "" or a "?" as default value in the option declaration.

## Use example
Here is a short code to illustrate how to use library.

```c++

// C++ OPTION PARSER TOOL

#include <iostream>
#include "optionParser.hpp"

using namespace std;



int main(int argc, char* argv[]){

    // create a OptionParser with options
    op::OptionParser opt;
    opt.add_option("h", "help", "shows option help"); // no default value means boolean options, which default value is false
    opt.add_option("w", "window_size", "window's size", "256" );
    opt.add_option("r", "rate", "learning rate", "0.01" );
    opt.add_option("m", "mode", "learning mode", "random" );

    // parse the options and verify that all went well. If not, errors and help will be shown
    bool correct_parsing = opt.parse_options(argc, argv);
    
    if(!correct_parsing){
        return EXIT_FAILURE;
    }

    cout << opt["rate"] << endl;
    cout << opt["w"] << endl;
    cout << opt["h"] << endl;
    
    // you have to convert yourself arguments if needed. This gives you full control over your options
    int window_size     =  op::str2int(opt["w"]);
    float learning_rate =  op::str2float(opt["r"]);
    bool has_help       =  op::str2bool(opt["h"]);

    // show help
    if(has_help) opt.show_help();
    
    return 0;
}

```
