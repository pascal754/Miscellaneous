# Miscellaneous

## cygwin update
`./setup-x86_64 -n -d -N -q --upgrade-also`

## msys2 update
`pacman -Syuu`

## vcpkg update
`vcpkg update`

## discard output
`Your DOS command 2> nul`

## random number in C++
```cpp

import <random>;

/* ... */

std::random_device rd;  // Will be used to obtain a seed for the random number engine

std::mt19937 gen(rd()); // Standard mersenne_twister_engine seeded with rd()

std::uniform_int_distribution<> distrib(0, 2); // closed interval [0, 2]

distrib(gen);

```
