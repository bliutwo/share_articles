# Inconsistency constructing std::string from C-string vs. from another std::string

**Why does the `std::string` constructor produce different output depending *only* on what kind of string it is constructed from?**

For example, consider the following C++ code:

```cpp
#include <iostream>
#include <string>

int main() {
    char cstyle[] = "01234567";
    std::string std = "01234567";
    std::cout << std::string(cstyle, 4) << std::endl;
    std::cout << std::string(std, 4) << std::endl;
    return 0;
}
```

which produces the following output:

```
0123
4567
```


I would expect them both to produce `0123`, or both to produce `4567`, but I wouldn't expect one to produce `0123` and the other to produce `4567`.

**Why this inconsistency?**

**EDIT**: This question isn't about which default constructor is called, or whether they do different things. They *do* different things, and different constructors *are* called. **This question *is* about *why* they don't do the same thing.** In other words, this is more of a philosophical question than a technical question.
