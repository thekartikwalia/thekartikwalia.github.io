---
title: "Conditional Statements"
date: 2024-09-05 10:00:00 +0530
categories: [DSA]
tags: [cpp, conditionals, basics]
---

## The If-Else If statement:
This is used when multiple statements need to be executed depending on different conditions.

Look at the following template code to understand.
```cpp
if (/* condition 1 */) {
	/* code */
}
else if(/* condition 2 */) {
	/* code */
}

// more else if blocks 

// more else if blocks 
else {
	/* code */
}
```
Here, the program will first check __condition 1__. If it evaluates to __true__, then the code inside the first if block would be executed and then the program will directly jump to the code after the else {} block.

If __condition 1__ evaluates to __false__, it will check __condition 2__. If that condition evaluates to __true__, then the code inside else-if would be executed, and then the program will jump to the code after the else {} block.

Similarly, the same thing will happen for all else-if statements. If none of the if/else-if conditions evaluates to true, then the else {} block of code is executed.

## Nested If-Statements 
When several if-else blocks can be used within other if-else constructs. To get a better understanding, think about the inside if-else conditions as separate codes. They don't interfere with the working of the outside if-else conditions. They just get executed only if the block they are written in is getting executed.

Look at the following template code to understand.
```cpp
if (/* condition */) {
	/* code */
	if (/* condition */) {
		/* code */
	}
}
else {
	/* code */
}
```

![Nested If-Statements.jpeg](/assets/img/dsa/nested-if-statements.jpeg)

Nested If-Else statements can be effectively used in programming to check multiple conditions sequentially, where each condition depends on the previous one's.