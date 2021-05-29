# YAIC
Yet Another Imgui Console
Header only C++ Imgui console, with support for stdout redirection unto itself.

## Usage
myCustomConsole.hpp
```
#pragma once
#include <functional>
#include "console.hpp"

struct customType{
  int someVar;
};

using namespace std::placeholders;
#define BIND(name) _commandList.emplace(std::make_pair<std::string, std::function<void(std::stringstream args, customType data)>>(#name, std::bind(&myCustomConsole::name, this, _1, _2)))

class myCustomConsole : public console<customType>{
	public:
		myCustomConsole(bool redir = false): console(redir){
			BIND(customCommand1);
    		}
	private:
		void customCommand1(std::stringstream args, customType data){
			doWhatev(data.someVar);
		}
};
```
Then just initialize an object myCustomConsole wherever you want, and call its myCustomConsoleObject.show(data) method inside an ImGui context.

![Sample image](https://github.com/theKlanc/YAIC/blob/master/sample.jpg?raw=true)
