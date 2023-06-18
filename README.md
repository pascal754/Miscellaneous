# Miscellaneous

## cygwin update
`./setup-x86_64 -n -d -N -q --upgrade-also`

## msys2 update
`pacman -Syuu`

## vcpkg update
`vcpkg update`

## Discard output
`Your DOS command 2> nul`

## Random number in C++
```cpp

import <random>;

/* ... */

std::random_device rd;  // Will be used to obtain a seed for the random number engine

std::mt19937 gen(rd()); // Standard mersenne_twister_engine seeded with rd()

std::uniform_int_distribution<> distrib(0, 2); // closed interval [0, 2]

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

`std::vector<std::vector<int>> v(10, std::vector<int>(10, 1));`

## 3D vector

`std::vector<std::vector<std::vector<int>>> v(3, std::vector<std::vector<int>>(4, std::vector<int>(5)));`


## Improve I/O performance

`std::ios_base::sync_with_stdio(false);`

## Structured binding

```
for (auto [a, b] {std::pair{ 3, "foobar" }}; a; --a)
    std::println("{} {}", a, b);
```
