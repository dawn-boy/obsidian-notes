## Setting up `vcpkg` to install c++ libs
#### 1. Install `vcpkg`
```sh
git clone https://github.com/microsoft/vcpkg.git
cd vcpkg
./bootstrap-vcpkg.sh   
```
#### 2. update `vcpkg` packages
```sh
vcpkg update
vcpkg upgrade --no-dry-run
```
#### 3. Install `crow` lib
```sh
vcpkg install crow
```
#### 4. Integrate the package
```sh
vcpkg integrate install
```

### Make a `CMakeLists.txt`
```cmake
cmake_minimum_required(VERSION 3.15)
project(crow_app)

set(CMAKE_CXX_STANDARD 17)

find_package(Crow CONFIG REQUIRED)

add_executable(crow_app main.cpp)
target_link_libraries(crow_app PRIVATE Crow::Crow)
```

### Finally build and run
```sh
mkdir build
cd build
cmake ..
make
./crow_app
```