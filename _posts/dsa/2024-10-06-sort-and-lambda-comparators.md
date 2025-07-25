---
title: "sort() and Lambda Comparators"
date: 2024-10-06 13:40:00 +0530
categories: [DSA]
tags: [cpp, stl, sort, comparator, lambda]
math: true
---

## sort()
The `sort()` function in C++ STL is a powerful algorithm used to sort elements in a range (such as arrays or containers like `vector`, `deque`, etc.). It is a part of the `<algorithm>` header, and it's highly efficient, typically implemented using the __Introsort__ algorithm, which is a hybrid sorting algorithm combining Quick Sort, Heap Sort, and Insertion Sort (because these 3 don't require extra spaces).

__Function Prototype__
```cpp
void sort(RandomIt first, RandomIt last);
```
- _first_ : Iterator pointing to the beginning of the range 
- _last_ : Iterator pointing to the end of the range (the position one past the last element)

## Key Points about `sort()`
1. __Random Access Iterators__ : `sort()` requires the iterators to be random access (e.g., for `vector`, `array`, `deque`). Containers like `list` and `forward_list` that do not provide random access iterators cannot use `sort()`.
2. __Default Sorting (Ascending order)__ : By default, `sort()` sorts elements in ascending order based on the `<` operator.
   - For integers, strings, floating-point numbers, etc., it uses the built-in comparison operators.
   - For custom data types, you need to overload the `<` operator or provide a custom comparator.
1. __Time Complexity__ : Average-case and worst-case time complexity is __O(NlogN)__, where __N__ is the number of elements to be sorted.
2. __Custom Comparators__ : You can provide a custom comparator (a function or a function object) to define the sorting criterion. This is useful when you want to sort in descending order or use custom rules for sorting.

## Examples of using `sort()`
__Sorting in Ascending Order__
```cpp
sort(v.begin(), v.end());    // Sorting an vector
sort(v, v + n);    // Sorting an array
```
__Partial Sorting (using `sort()` on a Range)__
```cpp
// Sort elements from idnex 1 to 4 (excluding index 4)
sort(v.begin() + 1, v.begin() + 4);
```
__Sorting with Custom Comparator (User-defined Objects)__
```cpp
struct Person {
	string name;
	int age;
}

// Custom comparator to sort by age 
bool compareByAge(const Person &a, const Person &b) {
	return a.age < b.age;    // Sort in ascending order of age
}

int main() {
	vector<Person> people = { {"Kartik", 21}, {"Cat", 19}, {"Mayank", 31}, {"Mohit", 18} };

	// Sort people by age 
	sort(people.begin(), people.end(), compareByAge);

	return 0;
}
```

__NOTE__ : Comparator should be written in a way that it returns True in case `a` lies before `b`

## Lambda Expressions 
In C++11 and Later, you can create a comparator __inline__ using __lambda expressions__. This makes it easier to write short, simple comparators without needing to define a separate function. Lambda expressions provide a concise way to create anonymous functions directly at the place where you need them.

__NOTE__
If your function returns _true_ for both `(x, y)` and `(y, x)`, you'll get runtime error TLE, because the algorithm tries to place x before y and y before x (contradiction). So, never use `=` in expressions while writing comparator functions (or Lambda Expressions).

## Syntax of Lambda Expressions 
A Lambda expression has the following general form:
```cpp
[ capture ] ( parameters ) -> return_type {body}
```
- __Capture__ : Specifies which variables from thee surrounding scope should be accessible in the lambda.
  Common captures include:
  - `[ ]` (no capture)
  - `[=]` (capture all variables by value)
  - `[&]` (capture all variables by reference)
  - `[x]` (capture only `x` by value), `[&x]` (capture only `x` by reference) 
- __Parameters__ : The function arguments (optional)
- __Return Type__ : Can be inferred (optional)
- __Body__ : The function body (code to execute)

## Examples of using Lambda Expressions
__Sorting Custom Objects with a Lambda Comparator__
```cpp
struct Person {
	string name;
	int age;
}

int main() {
	vector<Person> people = { {"Kartik", 21}, {"Cat", 19}, {"Mayank", 31}, {"Mohit", 18} };

	// Sort people by age using a lambda expression
	sort(people.begin(), people.end(), [](const Person &a, const Person &b){
		return a.age < b.age;    // Sort in ascending order of age
	});

	return 0;
}
```
__Sorting by Multiple Criteria using a Lambda__
```cpp
struct Person {
	string name;
	int age;
}

int main() {
	vector<Person> people = { {"Kartik", 21}, {"Cat", 19}, {"Mayank", 31}, {"Mohit", 18} };

	// Sort people by age using a lambda expression
	sort(people.begin(), people.end(), [](const Person &a, const Person &b){
		if(a.age == b.age) {
			return a.name < b.name;    // If ages are equal, sort by name
		}
		return a.age < b.age;    // Sort in ascending order of age
	});

	return 0;
}
```

## Advantages of using Lambda Functions for Comparators 
1. __Conciseness__ : Inline lambda functions eliminate the need to write separate comparator functions, making your code more compact and readable.
2. __Ease of Use__ : For simple comparators, lambdas are quick to write and don't require additional function definitions.
3. __Clarity__ : The sorting logic is placed where it is used, improving the code's readability by keeping relevant parts close together.

## Sort using Overloading `<` Operator
__Method-1__
In `a < b`, `<` will act like operator and `b` will be the argument
```cpp
struct Student {
	string name;
	double height;

	// Sort in Decreasing order of height ('o' represents 'b')
	bool operator<(const Student& o) const {
		return height > o.height;
	}
};
```
__Method-2__
```cpp
struct Student {
	string name;
	double height;
};

// Sort in Decreasing order of height
bool operator<(const Student& a, const Student& b) {
	return a.height > b.height;
};
```