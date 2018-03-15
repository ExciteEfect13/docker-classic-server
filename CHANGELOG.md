# Changelog

Items starting with `DEPRECATION` are important deprecation notices.

## (2018-03-14) (1.1.4)

### Bug fixes in 1.1.4

- Fixed missing Boost dependencies

## (2018-03-13) (1.1.3)

### Bug fixes in 1.1.3

- Fixed missing Boost filesystem dependency

## (2018-03-08) (1.1.2)

### Bug fixes in 1.1.2

- Fixed OpenSSL library to version 1.0

## (2018-03-08) (1.1.1)

### Bug fixes in 1.1.1

- Added MariaDB compatibility layer

## (2018-03-06) (1.1.0)

### New Features in 1.1.0

- Added Boost development headers

## (2018-02-26) (1.0.2)

### Maintenance in 1.0.2

- Fixed build.

## (2018-02-23) (1.0.1)

### Maintenance in 1.0.1

- Fixed build.

## (2018-02-23) (1.0.0)

### Maintenance in 1.0.0

- Upgrade to Debian 9 (Stretch)
- Upgrade to Clang 5.0 toolchain
- Upgrade MySQL client to MariaDB client

## (2018-01-23) 0.6.1

### Maintenance in 0.6.1

- Upgrade to [CMake 3.10.2][cmake].

## (2017-11-25) 0.6.0

### Maintenance in 0.6.0

- Upgrade to [CMake 3.10.0][cmake].

## (2017-11-14) 0.5.2

### Maintenance in 0.5.2

- Upgrade to [CMake 3.9.6][cmake].

## (2017-09-21) 0.5.1

### Maintenance in 0.5.1

- Upgrade to [CMake 3.9.3][cmake].

## (2017-07-21) 0.5.0

### Maintenance in 0.5.0

- Upgrade to [CMake 3.9.0][cmake].

## (2017-07-19) 0.4.0

### New Features 0.4.0

- Added support for [cppcheck][cppcheck].

### Maintenance in 0.4.0

- Only send status updates to Slack _if_ the build status changes.

## (2017-07-03) 0.3.0

### New Features in 0.3.0

- Added support for [Clang format][clang-format].

## (2017-06-27) 0.2.0

### New Features in 0.2.0

- Added support for [CLang Tidy][clang-tidy].
- Added support for [Lua][lua].

## (2017-06-26) Release 0.1.0

### New Features in 0.1.0

- Added [CLang 4.0][llvm-apt].
- Added [CMake 3.8.2][cmake] support.

[llvm-apt]: http://apt.llvm.org/
[cmake]: https://cmake.org/
[lua]: http://lua.org/
[clang-tidy]: http://clang.llvm.org/extra/clang-tidy/
[clang-format]: http://clang.llvm.org/docs/ClangFormat.html
[cppcheck]: https://sourceforge.net/projects/cppcheck/
