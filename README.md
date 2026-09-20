# psp-argtable2

psp-argtable2 is a PlayStation Portable-specific maintenance fork of Argtable2.
It preserves the Argtable2 API while updating the code and build system for the
current PSPDEV toolchain.

This repository targets the PSP only. Legacy host-platform build support for
DOS/Windows, Watcom, MinGW, Solaris, AIX, and other historical environments has
been removed.

## Requirements

- PSPDEV with the PSP compiler toolchain installed
- CMake 3.20 or newer

The build expects the PSPDEV CMake toolchain file at:

```text
$PSPDEV/psp/share/pspdev.cmake
```

## Build

Configure and build with CMake:

```sh
cmake -S . -B build \
    -DCMAKE_TOOLCHAIN_FILE="$PSPDEV/psp/share/pspdev.cmake" \
    -DCMAKE_BUILD_TYPE=Release
cmake --build build --parallel
```

The static library is produced at:

```text
build/src/libargtable2.a
```

## Install

Configure an installation prefix for the PSP target, then install with CMake:

```sh
cmake -S . -B build \
    -DCMAKE_TOOLCHAIN_FILE="$PSPDEV/psp/share/pspdev.cmake" \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX="$PSPDEV/psp"
cmake --build build --parallel
cmake --install build
```

Installation provides:

```text
include/argtable2.h
lib/libargtable2.a
lib/pkgconfig/argtable2.pc
```

The pkg-config metadata is relocatable and resolves its include and library
directories relative to the installed `argtable2.pc` file.

## Validation builds

The test sources can be built as PSP executables to verify the public API and
linkage. They are not registered with CTest because they cannot be executed on
the host while cross-compiling for the PSP.

The programming examples are compile checks only. CMake builds them as object
files so their syntax, headers, and API usage are validated without producing
runnable example executables.

Enable both validation sets with:

```sh
cmake -S . -B build \
    -DCMAKE_TOOLCHAIN_FILE="$PSPDEV/psp/share/pspdev.cmake" \
    -DCMAKE_BUILD_TYPE=Release \
    -DARGTABLE2_BUILD_TESTS=ON \
    -DARGTABLE2_CHECK_EXAMPLES=ON
cmake --build build --parallel
```

The options may also be enabled independently:

- `ARGTABLE2_BUILD_TESTS` builds and links the PSP test executables.
- `ARGTABLE2_CHECK_EXAMPLES` compiles the programming examples without
  linking them into executables.

Both options are disabled by default and do not affect the installed library.

## CMake integration

A PSP CMake project may also include this source tree directly:

```cmake
add_subdirectory(path/to/psp-argtable2)
target_link_libraries(your_target PRIVATE argtable2)
```

The `argtable2` target exports the correct build-tree and install-tree include
directory.

## Source layout

- `src/` — Argtable2 library source and bundled GNU getopt implementation
- `example/` — programming examples, compile-checked but not built as runnable programs
- `tests/` — test programs that can be built and linked for the PSP
- `doc/` — upstream Argtable2 documentation

CMake is the supported build system for this PSP fork. The historical
Autotools, NMake, and platform-specific build files are no longer maintained or
included.

## License

Argtable2 is distributed under the GNU Library General Public License, version 2
or later. See `LICENSE.md`.

Original authors and contributors are listed in `AUTHORS.md`.
