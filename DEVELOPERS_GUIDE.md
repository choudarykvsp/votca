
# Developers Guide

 The page is designed to give new developers general guidelines for
 implementing code consistent with the VOTCA and c++ style and standard.

## Resources

 A good starting point is to take a look at the c++ standard. Though the code
 has not always consistently followed the c++ standard we now make an
 effort to really enforce it and follow best practices.

 - [Best Practices1](https://www.gitbook.com/book/lefticus/cpp-best-practices/details)
 - [Best Practices2](https://google.github.io/styleguide/cppguide.html)

## Testing

 Each repository contains a src folder. Within the src folder exists a 
 library folder: libtools, libcsg etc... and a tools folder. A tests folder
 should also exist in the src folder. If it does not you should create one.

 For every new object and algorithm created there should exist a test. We
 use the Boost libraries testing framework. Good documentation can be found 
 here:

 - [Boost link](https://www.ibm.com/developerworks/aix/library/au-ctools1_boost/)
 
 We will outline the general workflow here using the vec object in 
 votca::tools. This object only has a header file it is in:
 tools/include/votca/tools/vec.h
 
 Determine if a tests folder has already been created or not in /src if it
 has not take a look at what was done in the votca-tools repo. 

 1. Create a test file in [tools/src/tests/](https://github.com/votca/tools/tree/master/src/tests)test_vec.cc 
    must have the same name as what appears in the foreach in the 
    CMakeLists.txt file. And place the following contents

```  
#define BOOST_TEST_MAIN

#define BOOST_TEST_MODULE vec_test
#include <boost/test/unit_test.hpp>
#include <exception>

#include <votca/tools/vec.h>

using namespace std;
using namespace votca::tools;

BOOST_AUTO_TEST_SUITE(vec_test)


BOOST_AUTO_TEST_CASE(test1){
  vecv;
  BOOST_CHECK_EQUAL(...);
  BOOST_CHECK_EQUAL(...);
  :
}
BOOST_AUTO_TEST_CASE(test2){
  vecv;
  BOOST_CHECK_EQUAL(...);
  BOOST_CHECK_EQUAL(...);
  :
}
:
BOOST_AUTO_TEST_SUITE_END()
```
 
Replace the '...' and ':' with the appropriate syntax. 
For more info on which boost test macros to use refer to the boost documentation

 2. To compile and test the code create a folder tools/build and run the following
    commands: 

```
cmake -DENABLE_TESTING=ON ../
make 
make test
```

Ensure you have an up to date version of cmake or use cmake3 

## CPP Codeing Style Guide

 VOTCA uses the clang formatter to automatically ensure consistent style.
 The style is essentially the same, as what is used by google, with the 
 exception that types and = are aligned to make the code more readable. 
 Have a look at `.clang-format file` in the
 [main votca repository](https://github.com/votca/votca/blob/master/.clang-format) for details.


To run the clang-format function on file.cc  

```
clang-format -i -style=file file.cc
```

'-i' ensures it will make change to file.cc, omitting the '-i' will display the
     changes without implementing them.
'-style=file' ensures the format is read from the .clang-format file otherwise 
     it will use a default style guide. 




