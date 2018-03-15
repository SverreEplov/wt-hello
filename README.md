# wt-hello

WT Hello world using conan package

Works on OS X and Ubuntu, fails miserably on Windows 

In conanfile.txt there is a imports directive which copies all dynamic libraries to a "lib" folder, så by having this folder in dynamic library search path the executable can be run

"example" in bin folder is executed as: 

LD_LIBRARY_PATH=../lib ./example --docroot . --http-address 0.0.0.0 --http-port 9090