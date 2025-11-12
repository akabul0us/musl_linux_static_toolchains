### Pre-built GCC toolchains from [musl.cc](https://musl.cc/), with the following libraries prebuilt as static libraries:

- [hwloc](https://github.com/open-mpi/hwloc)
- [OpenSSL](https://github.com/openssl/openssl)
- [libssh2](https://libssh2.org/)
- [libnl](https://github.com/thom311/libnl)
- [libpcre2](https://github.com/PCRE2Project) and [libpcre](https://sourceforge.net/projects/pcre/files/)
- [zlib](https://zlib.net/)
- [libmpfr](https://www.mpfr.org/)
- [libxxhash](https://github.com/Cyan4973/xxHash)
- [libgmp](https://gmplib.org/)
- [libncurses](https://invisible-island.net/ncurses) - _both libncurses and libncursesw (for wide characters) build from the same source, both have been included_

### How To Use

_(Optional)_ Keep your toolchains organized by storing them in a dedicated place, for example /opt/toolchains

`mkdir -p /opt/toolchains`

Clone the branch you wish to target, e.g. for the mipsel toolchain, run:

`git clone -b mipsel https://github.com/akabul0us/musl_linux_static_toolchains /opt/toolchains/mipsel-linux-muslsf-cross`

Append the toolchain's bin/ directory to your $PATH variable

`export PATH=/opt/toolchains/mipsel-linux-muslsf-cross/bin:$PATH`

Configure the program you wish to build _(note: this is assuming that the program you wish to cross compile uses a GNU-style configure script and GNU Makefile. Not all programs have the exact same options in their configuration scripts. Always read documentation)_

`CC=mipsel-linux-muslsf-gcc CXX=mipsel-linux-muslsf-g++ LD=mipsel-linux-muslsf-ld CFLAGS="-static -fPIC -I/opt/toolchains/mipsel-linux-muslsf-cross/include -L/opt/toolchains/mipsel-linux-muslsf-cross/lib" LDFLAGS="-static -L/opt/toolchains/mipsel-linux-muslsf-cross/lib" CXXFLAGS="-static -fPIC -I/opt/toolchains/mipsel-linux-muslsf-cross/include -L/opt/toolchains/mipsel-linux-muslsf-cross/lib" ./configure --prefix=/opt/toolchains/mipsel-linux-muslsf-cross --host=mipsel-linux-muslsf --build=x86_64-linux-gnu --enable-static --disable-shared`

Run `make` using all available processor cores

`make -j$(nproc --all)`

Enjoy your static-PIE compiled binaries
