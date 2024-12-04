# Miscellaneous

## cygwin update
`./setup-x86_64 -n -d -N -q --upgrade-also`

## msys2 update
`pacman -Syuu`

## vcpkg update

```
git pull
vcpkg update
vcpkg upgrade
vcpkg upgrade --no-dry-run
```

## Discard stderr
`Your_DOS_command 2> nul`

[Redirecting error messages from Command Prompt: STDERR/STDOUT](https://learn.microsoft.com/en-us/troubleshoot/developer/visualstudio/cpp/language-compilers/redirecting-error-command-prompt)

## Random number in C++
```cpp

import <random>;

/* ... */

std::random_device rd;  // Will be used to obtain a seed for the random number engine

std::mt19937 gen{rd()}; // Standard mersenne_twister_engine seeded with rd()

std::uniform_int_distribution<> distrib{0, 2}; // closed interval [0, 2]

distrib(gen);

```

## Measure execution time in C++
```cpp
import std;
//import <iostream>;
//import <chrono>;
//import <print>;

/* ... */

using namespace std::chrono;

auto start = high_resolution_clock::now();

/* do something */

auto stop = high_resolution_clock::now();

auto duration = duration_cast<microseconds>(stop - start);

// std::cout << "Time elapsed: " << duration.count() << " microseconds\n";

std::println("Time elapsed: {} microseconds", duration.count());
```

## vector of vector

```cpp
// 10 x 10 matrix with a default value, 1
std::vector<std::vector<int>> v(10, std::vector<int>(10, 1));
```

## 3D vector

```cpp
// 3 x 4 x 5 matrix with a default value, 0
std::vector<std::vector<std::vector<int>>> v(3, std::vector<std::vector<int>>(4, std::vector<int>(5)));
```


## Improve I/O performance

`std::ios_base::sync_with_stdio(false);`

## Structured binding

```cpp
for (auto [a, b] {std::pair{ 3, "foobar" }}; a; --a)
    std::println("{} {}", a, b);
```


## Boost TypeInfo

```cpp
#include <boost/type_index.hpp>
// ...
int a{};
using boost::typeindex::type_id_with_cvr;
std::println("{}", type_id_with_cvr<decltype(a)>().pretty_name());
// ...
```

## Type Aliases

```cpp
#include <cstdint>
#include <stdfloat> // C++23

using i8 = std::int8_t;
using i16 = std::int16_t;
using i32 = std::int32_t;
using i64 = std::int64_t;

using u8 = std::uint8_t;
using u16 = std::uint16_t;
using u32 = std::uint32_t;
using u64 = std::uint64_t;

using usize = std::size_t;
using ssize = std::ptrdiff_t;

using f16 = std::float16_t;
using f32 = std::float32_t;
using f64 = std::float64_t;
using f128 = std::float128_t;
using bf16 = std::bfloat16_t;
```

## cmake

```
cmake -GNinja -DCMAKE_CXX_COMPILER=/usr/local/bin/g++ -DCMAKE_BUILD_TYPE=Debug -B Debug
cmake --build Debug

cmake -GNinja -DCMAKE_CXX_COMPILER=/usr/local/bin/g++ -DCMAKE_BUILD_TYPE=Release -B Release
cmake --build Release

On Windows
cmake -B <dir>
cmake --build <dir> --config Release

vcpkg
CMake projects should use: "-DCMAKE_TOOLCHAIN_FILE=/path/to/vcpkg/scripts/buildsystems/vcpkg.cmake"
```

## CMakeLists.txt

```cmake
cmake_minimum_required(VERSION 3.26)

set(CMAKE_TOOLCHAIN_FILE "$ENV{HOME}/vcpkg/scripts/buildsystems/vcpkg.cmake")

project(cmake_test)

set(CMAKE_CXX_STANDARD 23)

add_executable(${PROJECT_NAME} main.cpp)

#set(CMAKE_PREFIX_PATH "C:/.../vcpkg/installed/x64-windows/share")
#include(/.../vcpkg/scripts/buildsystems/vcpkg.cmake)
find_package(fmt CONFIG REQUIRED)
target_link_libraries(${PROJECT_NAME} PRIVATE fmt::fmt)
```

## CMakeLists.txt for modules

```cmake
cmake_minimum_required(VERSION 3.28)
project(std_module_example CXX)

# Turning off extensions avoids and issue with the clang 16 compiler
# clang 17 and greater can avoid this setting
set(CMAKE_CXX_EXTENSIONS OFF)
# Set the version of C++ for the project
set(CMAKE_CXX_STANDARD 20)
# Create a library
add_library(foo)
# Add the module file to the library
target_sources(foo
  PUBLIC
    FILE_SET CXX_MODULES FILES
      foo.cxx
)
# Create an executable
add_executable(hello main.cxx)
# Link to the library foo
target_link_libraries(hello foo)
```

## namespace

```cpp
namespace rng = std::ranges;
namespace vw = std::views;
//namespace rv = std::ranges::views;
```

## Eigen

deprecate warning STL4042 for MSVC with /std:c++latest
```cpp
#define _SILENCE_CXX23_DENORM_DEPRECATION_WARNING
```

## Address Sanitizer Error: Container overflow

```
error LNK2038: mismatch detected for 'annotate_string': value '0' doesn't match value '1' in main.obj
error LNK2038: mismatch detected for 'annotate_vector': value '0' doesn't match value '1' in main.obj
```

### Workaround:

Properties - C/C++ - Command Line - Additional Options

`/D _DISABLE_VECTOR_ANNOTATION /D _DISABLE_STRING_ANNOTATION`

### Reference:

https://learn.microsoft.com/en-us/cpp/sanitizers/error-container-overflow?view=msvc-170

## Google benchmark in MSVC

```cpp
#pragma comment(lib, "shlwapi.lib")
```

## How to find out which process is locking a DLL

```
tasklist /m thelocked.dll
```

## Bash script

- Find and delete:

```bash
find . -type d -name "target" -exec rm -rf {} +
```

- Search `pattern` through all `.txt` files in the current directory:

```bash
grep "pattern" *.txt
```

- Search recursively through all `.txt` files:

```bash
grep -r --include="*.txt" "pattern" .
```

- Check the size of the current directory:

```bash
du -sh .
```
where

`-s`: Summarizes the total size of the directory rather than listing each file and subdirectory.

`-h`: Displays the size in a human-readable format (e.g., KB, MB, GB).

`.`: Refers to the current directory.


- Check the size of each directory within the current directory:

```bash
du -h --max-depth=1
```
