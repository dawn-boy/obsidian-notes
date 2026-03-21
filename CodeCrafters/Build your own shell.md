```c++
#include <iostream>
#include <string>

int main(){
	std::cout << std::unitbuf;
	std::cout << std::unitbuf;

	std::cout << "$ ";

	std::string input;
	std::getline(std::cin, input);

	std::cout << input << ": command not found" << std::endl;
}
```

`std::unitbuf` is an I/O stream manipulator which tells C++ to flush the output buffer after every insertion