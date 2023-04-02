## Numeric Limits

!!! note
    Below demonstrates the limits of all the numeric primitive types in c++ and therefore can     help in chosing which would work best for certain scernarios.

```c
#include <iostream>
#include <cstdint>
#include <limits>


template<typename T>
std::string typeStr(){
    std::string pf(__PRETTY_FUNCTION__);
    auto tEqualPos = pf.rfind("T = ");
    auto closeBracPos = pf.rfind("]");
    if(tEqualPos != std::string::npos &&
            closeBracPos != std::string::npos &&
            closeBracPos > tEqualPos){
        return pf.substr(tEqualPos + 4, closeBracPos - 4 - tEqualPos);
    }else{
        return "indeterminate";
    }
}

int main(int argc, char* argv[]){
    std::cout << "Unsigned integers (only numbers >= 0)" << std::endl;
    std::cout << "               uint8_t low: " << static_cast<uint16_t>(std::numeric_limits<uint8_t>::lowest()) << std::endl;
    std::cout << "               uint8_t min: " << static_cast<uint16_t>(std::numeric_limits<uint8_t>::min()) << std::endl;
    std::cout << "               uint8_t max: " << static_cast<uint16_t>(std::numeric_limits<uint8_t>::max()) << std::endl;
    std::cout << "            sizeof uint8_t: " << sizeof (uint8_t) << std::endl;
    std::cout << "    actual type of uint8_t: " << typeStr<uint8_t>() << std::endl << std::endl;
    std::cout << "              uint16_t low: " << std::numeric_limits<uint16_t>::lowest() << std::endl;
    std::cout << "              uint16_t min: " << std::numeric_limits<uint16_t>::min() << std::endl;
    std::cout << "              uint16_t max: " << std::numeric_limits<uint16_t>::max() << std::endl;
    std::cout << "           sizeof uint16_t: " << sizeof (uint16_t) << std::endl;
    std::cout << "   actual type of uint16_t: " << typeStr<uint16_t>() << std::endl << std::endl;
    std::cout << "              uint32_t low: " << std::numeric_limits<uint32_t>::lowest() << std::endl;
    std::cout << "              uint32_t min: " << std::numeric_limits<uint32_t>::min() << std::endl;
    std::cout << "              uint32_t max: " << std::numeric_limits<uint32_t>::max() << std::endl;
    std::cout << "           sizeof uint32_t: " << sizeof (uint32_t) << std::endl;
    std::cout << "   actual type of uint32_t: " << typeStr<uint32_t>() << std::endl << std::endl;
    std::cout << "                  uint min: " << std::numeric_limits<uint>::lowest() << std::endl;
    std::cout << "                  uint min: " << std::numeric_limits<uint>::min() << std::endl;
    std::cout << "                  uint max: " << std::numeric_limits<uint>::max() << std::endl;
    std::cout << "               sizeof uint: " << sizeof (uint) << std::endl;
    std::cout << "       actual type of uint: " << typeStr<uint>() << std::endl << std::endl;
    std::cout << "              uint64_t low: " << std::numeric_limits<uint64_t>::lowest() << std::endl;
    std::cout << "              uint64_t min: " << std::numeric_limits<uint64_t>::min() << std::endl;
    std::cout << "              uint64_t max: " << std::numeric_limits<uint64_t>::max() << std::endl;
    std::cout << "           sizeof uint64_t: " << sizeof (uint64_t) << std::endl;
    std::cout << "   actual type of uint64_t: " << typeStr<uint64_t>() << std::endl << std::endl;
    std::cout << "                size_t low: " << std::numeric_limits<size_t>::lowest() << std::endl;
    std::cout << "                size_t min: " << std::numeric_limits<size_t>::min() << std::endl;
    std::cout << "                size_t max: " << std::numeric_limits<size_t>::max() << std::endl;
    std::cout << "             sizeof size_t: " << sizeof (size_t) << std::endl;
    std::cout << "     actual type of size_t: " << typeStr<size_t>() << std::endl << std::endl;
    std::cout << "Signed Integers" << std::endl;
    std::cout << "                int8_t low: " << static_cast<int16_t>(std::numeric_limits<int8_t>::lowest()) << std::endl;
    std::cout << "                int8_t min: " << static_cast<int16_t>(std::numeric_limits<int8_t>::min()) << std::endl;
    std::cout << "                int8_t max: " << static_cast<int16_t>(std::numeric_limits<int8_t>::max()) << std::endl;
    std::cout << "             sizeof int8_t: " << sizeof (int8_t) << std::endl;
    std::cout << "     actual type of int8_t: " << typeStr<int8_t>() << std::endl << std::endl;
    std::cout << "               int16_t low: " << std::numeric_limits<int16_t>::lowest() << std::endl;
    std::cout << "               int16_t min: " << std::numeric_limits<int16_t>::min() << std::endl;
    std::cout << "               int16_t max: " << std::numeric_limits<int16_t>::max() << std::endl;
    std::cout << "            sizeof int16_t: " << sizeof (int16_t) << std::endl;
    std::cout << "    actual type of int16_t: " << typeStr<int16_t>() << std::endl << std::endl;
    std::cout << "               int32_t min: " << std::numeric_limits<int32_t>::lowest() << std::endl;
    std::cout << "               int32_t min: " << std::numeric_limits<int32_t>::min() << std::endl;
    std::cout << "               int32_t max: " << std::numeric_limits<int32_t>::max() << std::endl;
    std::cout << "            sizeof int32_t: " << sizeof (int32_t) << std::endl;
    std::cout << "    actual type of int32_t: " << typeStr<int32_t>() << std::endl << std::endl;
    std::cout << "                   int min: " << std::numeric_limits<int>::lowest() << std::endl;
    std::cout << "                   int min: " << std::numeric_limits<int>::min() << std::endl;
    std::cout << "                   int max: " << std::numeric_limits<int>::max() << std::endl;
    std::cout << "                sizeof int: " << sizeof (int) << std::endl;
    std::cout << "        actual type of int: " << typeStr<int>() << std::endl << std::endl;
    std::cout << "               int64_t low: " << std::numeric_limits<int64_t>::lowest() << std::endl;
    std::cout << "               int64_t min: " << std::numeric_limits<int64_t>::min() << std::endl;
    std::cout << "               int64_t max: " << std::numeric_limits<int64_t>::max() << std::endl;
    std::cout << "            sizeof int64_t: " << sizeof (int64_t) << std::endl;
    std::cout << "    actual type of int64_t: " << typeStr<int64_t>() << std::endl << std::endl;
    std::cout << "Floating Point Numbers" << std::endl;
    std::cout << "                 float low: " << std::numeric_limits<float>::lowest() << std::endl;
    std::cout << "                 float min: " << std::numeric_limits<float>::min() << std::endl;
    std::cout << "                 float max: " << std::numeric_limits<float>::max() << std::endl;
    std::cout << "              sizeof float: " << sizeof (float) << std::endl;
    std::cout << "      actual type of float: " << typeStr<float>() << std::endl << std::endl;
    std::cout << "                double low: " << std::numeric_limits<double>::lowest() << std::endl;
    std::cout << "                double min: " << std::numeric_limits<double>::min() << std::endl;
    std::cout << "                double max: " << std::numeric_limits<double>::max() << std::endl;
    std::cout << "             sizeof double: " << sizeof (double) << std::endl;
    std::cout << "     actual type of double: " << typeStr<double>() << std::endl << std::endl;
    std::cout << "           long double low: " << std::numeric_limits<long double>::lowest() << std::endl;
    std::cout << "           long double min: " << std::numeric_limits<long double>::min() << std::endl;
    std::cout << "           long double max: " << std::numeric_limits<long double>::max() << std::endl;
    std::cout << "        sizeof long double: " << sizeof (long double) << std::endl;
    std::cout << "actual type of long double: " << typeStr<long double>() << std::endl << std::endl;
    return 0;

}
```

```sh
Compile Command:
g++-5 -std=c++14 main.cpp -o exampleCpp
Execution Call:
./exampleCpp
Output:
Unsigned integers (only numbers >= 0)
               uint8_t low: 0
               uint8_t min: 0
               uint8_t max: 255
            sizeof uint8_t: 1
    actual type of uint8_t: unsigned char; std::string = std::basic_string<char>

              uint16_t low: 0
              uint16_t min: 0
              uint16_t max: 65535
           sizeof uint16_t: 2
   actual type of uint16_t: short unsigned int; std::string = std::basic_string<char>

              uint32_t low: 0
              uint32_t min: 0
              uint32_t max: 4294967295
           sizeof uint32_t: 4
   actual type of uint32_t: unsigned int; std::string = std::basic_string<char>

                  uint min: 0
                  uint min: 0
                  uint max: 4294967295
               sizeof uint: 4
       actual type of uint: unsigned int; std::string = std::basic_string<char>

              uint64_t low: 0
              uint64_t min: 0
              uint64_t max: 18446744073709551615
           sizeof uint64_t: 8
   actual type of uint64_t: long unsigned int; std::string = std::basic_string<char>

                size_t low: 0
                size_t min: 0
                size_t max: 18446744073709551615
             sizeof size_t: 8
     actual type of size_t: long unsigned int; std::string = std::basic_string<char>

Signed Integers
                int8_t low: -128
                int8_t min: -128
                int8_t max: 127
             sizeof int8_t: 1
     actual type of int8_t: signed char; std::string = std::basic_string<char>

               int16_t low: -32768
               int16_t min: -32768
               int16_t max: 32767
            sizeof int16_t: 2
    actual type of int16_t: short int; std::string = std::basic_string<char>

               int32_t min: -2147483648
               int32_t min: -2147483648
               int32_t max: 2147483647
            sizeof int32_t: 4
    actual type of int32_t: int; std::string = std::basic_string<char>

                   int min: -2147483648
                   int min: -2147483648
                   int max: 2147483647
                sizeof int: 4
        actual type of int: int; std::string = std::basic_string<char>

               int64_t low: -9223372036854775808
               int64_t min: -9223372036854775808
               int64_t max: 9223372036854775807
            sizeof int64_t: 8
    actual type of int64_t: long int; std::string = std::basic_string<char>

Floating Point Numbers
                 float low: -3.40282e+38
                 float min: 1.17549e-38
                 float max: 3.40282e+38
              sizeof float: 4
      actual type of float: float; std::string = std::basic_string<char>

                double low: -1.79769e+308
                double min: 2.22507e-308
                double max: 1.79769e+308
             sizeof double: 8
     actual type of double: double; std::string = std::basic_string<char>

           long double low: -1.18973e+4932
           long double min: 3.3621e-4932
           long double max: 1.18973e+4932
        sizeof long double: 16
actual type of long double: long double; std::string = std::basic_string<char>

```