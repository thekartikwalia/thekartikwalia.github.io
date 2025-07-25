---
title: "Templates"
date: 2024-09-08 8:30:00 +0530
categories: [DSA, C++ Basics]
tags: [cpp, templates, generics]
math: true
---

## Templates 
- A template in C++ is a feature that allows for the creation of generic functions or classes.
- It enables the writing of code in a way that it can handle any data type without the need to rewrite the same code for different data types.
- Templates allow for the creation of reusable code that can operate on different data types.
- The variable datatype `T` will be determined at compile time.
- Templates makes the cases of Polymorphism very easy.

__Why Templates are Used__

1. __Code Reusability__ : Templates enable the creation of functions and classes that work with any data type. This promotes code reuse and eliminates the need to duplicate code for different data types.
2. __Flexibility__ : Templates provide flexibility by allowing the same code to be used with different data types, enhancing the adaptability and versatility of C++ programs.
3. __Type Safety__ : Despite being generic, templates in C++ maintain type safety. The compiler performs type checking during instantiation to ensure type correctness.
4. __Performance__ : Templates offer performance benefits by allowing the compiler to generate specialized code for each data type used, optimizing execution speed.

## Code Example - 1
```cpp
template <typename T>
template <class T>    // Alternate to above line of code

class Box {
public:
    T content;

    void setContent(T newContent) {
        content = newContent;
    }

    T getContent() {
        return content;
    }
};

int main() {
    Box<int> intBox;
    intBox.setContent(123);
    cout << intBox.getContent() << '\n';

    Box<string> stringBox;
    stringBox.setContent("Hello Templates");
    cout << stringBox.getContent() << '\n';

    return 0;
}
```

__Explanation__
- In this example, a class `Box` is defined using a template.
- The class `Box` has a member variable `content` of type `T`, and two member functions `setContent()` and `getContent()`.
- The `setContent` function sets the value of `content`, and the `getContent` function retrieves the value of `content`.
- The `main` function demonstrates the usage of the `Box` class with different data types (`int` and `std::string`).
- It creates instances of `Box` for `int` and `std::string`, sets their content, and then retrieves and prints the content.
## Code Example - 2
```cpp
template <typename T>
T max(T a, T b) {
    return (a > b) ? a : b;
}

int main() {
    cout << max(10, 5) << '\n';      // The compiler generates int max(int, int)
    cout << max(10.5, 20.5) << '\n'; // The compiler generates double max(double, double)
    return 0;
}
```

__Explanation__
- In this example, a template function `max` is defined, which takes two parameters of type `T` and returns the maximum of the two values.
- The `main` function demonstrates the usage of the `max` function with different data types (`int` and `double`).
- When `max` is called with integers (`max(10, 5)`), the compiler generates an instantiation of `max` for `int`.
- Similarly, when `max` is called with doubles (`max(10.5, 20.5)`), the compiler generates an instantiation of `max` for `double`.
- This shows how templates allow for the creation of generic functions that can work with different data types.