# OutOfTreeLLVMPass

Template for creating an out of tree llvm pass that can be built with pre-compiled llvm binaries or from llvm source.

## Setup the build system

### llvm sources

Clone this repository and the llvm source next to each other and create a build folder. 
Run cmake from within the build folder:
```
git clone https://github.com/TG908/OutOfTreeLLVMPass.git
git clone https://github.com/llvm/llvm-project.git
mkdir build
cd build
cmake -DPATH_TO_LLVM=../llvm-project/llvm ../OutOfTreeLLVMPass
```

### pre-compiled llvm

Clone this repoitory and install or download a pre-compiled version of llvm for your system. The example uses macOS and llvm 9.0.0.
Run cmake from within the build folder.
```
git clone https://github.com/TG908/OutOfTreeLLVMPass.git
wget http://releases.llvm.org/9.0.0/clang+llvm-9.0.0-x86_64-darwin-apple.tar.xz
tar xzf clang+llvm-9.0.0-x86_64-darwin-apple.tar.xz
mkdir build
cd build
cmake -DPATH_TO_LLVM=../clang+llvm-9.0.0-x86_64-darwin-apple ../OutOfTreeLLVMPass
```

## Build the pass

```
cmake --build .
```

## Run the pass

Make sure to provide some bitcode or LLVM IR in `hello.bc` / `hello.ll`. If your are not using macOS make sure to adapt the file ending for the compiled module to `.so` or `.dll`.

### llvm source

```
./llvm-build/bin/opt -load OutOfTreeLLVMPass.dylib -hello < hello.ll > /dev/null

```

### pre-compiled llvm

```
../clang+llvm-9.0.0-x86_64-darwin-apple/bin/opt -load OutOfTreeLLVMPass.dylib -hello < hello.ll > /dev/null

```

