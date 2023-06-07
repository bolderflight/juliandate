[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

![Bolder Flight Systems Logo](img/logo-words_75.png) &nbsp; &nbsp; ![Arduino Logo](img/arduino_logo_75.png)

# Julian Date
This library converts from year, month, day and hour, minute, second to a Julian date. This library is compatible with Arduino and CMake build systems.
   * [License](LICENSE.md)
   * [Changelog](CHANGELOG.md)
   * [Contributing guide](CONTRIBUTING.md)

# Installation

## Arduino
Use the Arduino Library Manager to install this library or clone to your Arduino/libraries folder. This library is added as:

```C++
#include "juliandate.h"
```

An example Arduino executable is located at *examples/arduino/juliandate_ex/juliandate_ex.ino*. Teensy 3.x, 4.x, and LC devices are used for testing under Arduino and this library should be compatible with other Arduino devices.

## CMake
CMake is used to build this library, which is exported as a library target called *juliandate*. The header is added as:

```C++
#include "juliandate.h"
```

The library can be also be compiled stand-alone using the CMake idiom of creating a *build* directory and then, from within that directory issuing:

```
cmake ..
make
```

This will build the library, an example executable called *juliandate_example*, and an executable for testing using the Google Test framework, called *juliandate_test*. The example executable source files are located at *examples/cmake/juliandate_ex.cc*.

# Namespace
This library is within the namespace *bfs*.

# Functions

**double juliandate(const int16_t yyyy, const int8_t mm, const int8_t dd, const int8_t h, const int8_t m, const int8_t s)** Given the UTC year, month, day, hour, minute, and second, computes and returns the Julian date.

```C++
/* Julian date on 2023-5-30 13:23:10 UTC, 2460095.0577546292916 */
std::cout << std::setprecision(20) << bfs::juliandate(2023, 5, 30, 13, 23, 10) << std::endl;
```

**double juliandate(const int16_t yyyy, const int8_t mm, const int8_t dd)** Given the UTC year, month, and day, computes and returns the Julian date.

```C++
/* Julian date on 2023-5-30 0:0:0 UTC, 2460094.5 */
Serial.println(bfs::juliandate(2023, 5, 30));
```
