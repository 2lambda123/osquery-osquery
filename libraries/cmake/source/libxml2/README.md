# libxml2 library build notes

## Linux

### Linux Common

Make sure you are working in a clean source folder:

```bash
git reset --hard ; git clean -ffdx
```

Integrate the osquery-toolchain in the main `CMakeLists.txt` file (see the following file in osquery: `cmake/toolchain.cmake`). Then configure the project.

```bash
cmake \
  -S . \
  -B build \
  -DOSQUERY_TOOLCHAIN_SYSROOT=/usr/local/osquery-toolchain \
  -DBUILD_SHARED_LIBS=OFF \
  -DLIBXML2_WITH_C14N=ON \
  -DLIBXML2_WITH_CATALOG=OFF \
  -DLIBXML2_WITH_DEBUG=OFF \
  -DLIBXML2_WITH_FTP=OFF \
  -DLIBXML2_WITH_HTML=OFF \
  -DLIBXML2_WITH_HTTP=OFF \
  -DLIBXML2_WITH_ICONV=OFF \
  -DLIBXML2_WITH_ICU=OFF \
  -DLIBXML2_WITH_ISO8859X=OFF \
  -DLIBXML2_WITH_LEGACY=OFF \
  -DLIBXML2_WITH_LZMA=OFF \
  -DLIBXML2_WITH_MEM_DEBUG=OFF \
  -DLIBXML2_WITH_MODULES=OFF \
  -DLIBXML2_WITH_OUTPUT=ON \
  -DLIBXML2_WITH_PATTERN=ON \
  -DLIBXML2_WITH_PROGRAMS=OFF \
  -DLIBXML2_WITH_PUSH=ON \
  -DLIBXML2_WITH_PYTHON=OFF \
  -DLIBXML2_WITH_READER=ON \
  -DLIBXML2_WITH_REGEXPS=ON \
  -DLIBXML2_WITH_SAX1=OFF \
  -DLIBXML2_WITH_SCHEMAS=OFF \
  -DLIBXML2_WITH_SCHEMATRON=OFF \
  -DLIBXML2_WITH_TESTS=OFF \
  -DLIBXML2_WITH_THREADS=ON \
  -DLIBXML2_WITH_THREAD_ALLOC=OFF \
  -DLIBXML2_WITH_TLS=OFF \
  -DLIBXML2_WITH_TREE=ON \
  -DLIBXML2_WITH_VALID=OFF \
  -DLIBXML2_WITH_WRITER=ON \
  -DLIBXML2_WITH_XINCLUDE=OFF \
  -DLIBXML2_WITH_XPATH=ON \
  -DLIBXML2_WITH_XPTR=ON \
  -DLIBXML2_WITH_XPTR_LOCS=OFF \
  -DLIBXML2_WITH_ZLIB=ON \
  -DHAVE_VA_COPY:BOOL=ON
```

Build the project:

```bash
cmake \
  --build build \
  -j $(nproc)
```

## macOS

### macOS Common

Make sure you are working in a clean source folder:

```bash
git reset --hard ; git clean -ffdx
```

When building for macOS ARM, also pass the following parameter: `-DCMAKE_OSX_ARCHITECTURES=arm64`, or use `-DCMAKE_OSX_ARCHITECTURES=x86_64` for x86_64.

```bash
cmake \
  -S . \
  -B build \
  -DCMAKE_OSX_SYSROOT=/Applications/Xcode_15.0.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX14.2.sdk \
  -DCMAKE_OSX_DEPLOYMENT_TARGET=10.15 \
  -DBUILD_SHARED_LIBS=OFF \
  -DLIBXML2_WITH_C14N=ON \
  -DLIBXML2_WITH_CATALOG=OFF \
  -DLIBXML2_WITH_DEBUG=OFF \
  -DLIBXML2_WITH_FTP=OFF \
  -DLIBXML2_WITH_HTML=OFF \
  -DLIBXML2_WITH_HTTP=OFF \
  -DLIBXML2_WITH_ICONV=OFF \
  -DLIBXML2_WITH_ICU=OFF \
  -DLIBXML2_WITH_ISO8859X=OFF \
  -DLIBXML2_WITH_LEGACY=OFF \
  -DLIBXML2_WITH_LZMA=OFF \
  -DLIBXML2_WITH_MEM_DEBUG=OFF \
  -DLIBXML2_WITH_MODULES=OFF \
  -DLIBXML2_WITH_OUTPUT=ON \
  -DLIBXML2_WITH_PATTERN=ON \
  -DLIBXML2_WITH_PROGRAMS=OFF \
  -DLIBXML2_WITH_PUSH=ON \
  -DLIBXML2_WITH_PYTHON=OFF \
  -DLIBXML2_WITH_READER=ON \
  -DLIBXML2_WITH_REGEXPS=ON \
  -DLIBXML2_WITH_SAX1=OFF \
  -DLIBXML2_WITH_SCHEMAS=OFF \
  -DLIBXML2_WITH_SCHEMATRON=OFF \
  -DLIBXML2_WITH_TESTS=OFF \
  -DLIBXML2_WITH_THREADS=ON \
  -DLIBXML2_WITH_THREAD_ALLOC=OFF \
  -DLIBXML2_WITH_TLS=OFF \
  -DLIBXML2_WITH_TREE=ON \
  -DLIBXML2_WITH_VALID=OFF \
  -DLIBXML2_WITH_WRITER=ON \
  -DLIBXML2_WITH_XINCLUDE=OFF \
  -DLIBXML2_WITH_XPATH=ON \
  -DLIBXML2_WITH_XPTR=ON \
  -DLIBXML2_WITH_XPTR_LOCS=OFF \
  -DLIBXML2_WITH_ZLIB=ON
```

Build the project:

```bash
cmake \
  --build build \
  -j $(nproc)
```

## Windows

### Windows Common

Make sure you are working in a clean source folder:

```cmd
git reset --hard ; git clean -ffdx
```

It may be necessary to keep the osquery source code and zlib library compiled around,
because if the configuration doesn't find zlib, then we will need to pass to CMake the zlib library and include paths ourselves.

Configure the project:

```cmd
cmake ^
  -S . ^
  -B build ^
  -G "Visual Studio 16 2019" ^
  -DBUILD_SHARED_LIBS=OFF ^
  -DLIBXML2_WITH_C14N=ON ^
  -DLIBXML2_WITH_CATALOG=OFF ^
  -DLIBXML2_WITH_DEBUG=OFF ^
  -DLIBXML2_WITH_FTP=OFF ^
  -DLIBXML2_WITH_HTML=OFF ^
  -DLIBXML2_WITH_HTTP=OFF ^
  -DLIBXML2_WITH_ICONV=OFF ^
  -DLIBXML2_WITH_ICU=OFF ^
  -DLIBXML2_WITH_ISO8859X=OFF ^
  -DLIBXML2_WITH_LEGACY=OFF ^
  -DLIBXML2_WITH_LZMA=OFF ^
  -DLIBXML2_WITH_MEM_DEBUG=OFF ^
  -DLIBXML2_WITH_MODULES=OFF ^
  -DLIBXML2_WITH_OUTPUT=ON ^
  -DLIBXML2_WITH_PATTERN=ON ^
  -DLIBXML2_WITH_PROGRAMS=OFF ^
  -DLIBXML2_WITH_PUSH=ON ^
  -DLIBXML2_WITH_PYTHON=OFF ^
  -DLIBXML2_WITH_READER=ON ^
  -DLIBXML2_WITH_REGEXPS=ON ^
  -DLIBXML2_WITH_SAX1=OFF ^
  -DLIBXML2_WITH_SCHEMAS=OFF ^
  -DLIBXML2_WITH_SCHEMATRON=OFF ^
  -DLIBXML2_WITH_TESTS=OFF ^
  -DLIBXML2_WITH_THREADS=ON ^
  -DLIBXML2_WITH_THREAD_ALLOC=OFF ^
  -DLIBXML2_WITH_TLS=OFF ^
  -DLIBXML2_WITH_TREE=ON ^
  -DLIBXML2_WITH_VALID=OFF ^
  -DLIBXML2_WITH_WRITER=ON ^
  -DLIBXML2_WITH_XINCLUDE=OFF ^
  -DLIBXML2_WITH_XPATH=ON ^
  -DLIBXML2_WITH_XPTR=ON ^
  -DLIBXML2_WITH_XPTR_LOCS=OFF ^
  -DLIBXML2_WITH_ZLIB=ON ^
```

For Windows ARM64, when configuring from Window x86, add
```
-A ARM64
```

And optionally
```cmd
  -DZLIB_LIBRARY="<path to thirdparty_zlib.lib>" ^
  -DZLIB_INCLUDE_DIR="<path to osquery source>\libraries\cmake\source\zlib\src"
```

Build the project:

```cmd
cmake ^
  --build build ^
  --config Release
```

NOTE: If necessary, convert the config.h and xmlversion.h line endings from CRLF to LF

## Common to All Platforms

Copy the generated config files:

`build/config.h` -> `config/<os>/<arch>/`
`build/libxml/xmlversion.h` -> `version/<os>/<arch>/libxml/`
