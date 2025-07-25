---
layout: post
title: "Algorithmic Design & Custom Data Structures"
date: 2024-10-08
categories: dsa
math: true
tags: [algorithm-design, data-structure, median, mode, variance, multiset, map, struct, precomputation]
---

## Algorithmic Design
Algorithmic design involves the systematic creation and optimization of algorithms to solve specific computational problems. In the context of the given problem, the objective is to design an efficient algorithm to handle a series of queries related to student records.

Each query specifies an operation, such as adding a student with a given name and marks, erasing entries for a specific student, erasing all entries for a student, or printing the first entry of marks for a given student.

A well-designed algorithm should consider the efficiency of operations, minimizing time and space complexities. Utilizing appropriate data structures, such as hash tables or associative containers, can facilitate quick access and modification of student records. The algorithm must gracefully handle cases where entries do not exist for a given student.

Additionally, an optimal solution should strive for simplicity and maintainability, ensuring ease of understanding and maintenance as the algorithm evolves or scales to larger datasets.

---

## Question 1 : Basics
__Design a Data structure with following functions__ : 
- insert(int x) : Inserts value `x`
- erase(int x) : Erases 1 occurrence of `x` (given `x` definitely exists at least once)
- erase_all(int x) : Erases all occurrences of `x` 
- get_sum() : Returns sum of all entries present
- get_min() : Returns minimum of all entries present
- get_distinct() : Returns number of distinct entries amongst all entries present

Try using something called as _Frequency Map_
Keep in mind following points 
- Map is sorted by Keys
- Entries in Map can be erased using Keys
- Accessing entry in Map is $O(\log N)$
```cpp
#include <bits/stdc++.h>
using namespace std;

struct myBag {
	int curr_sum;
	map<int, int> freq;    // {entry, frequency}

	// Constructor 
	myBag() {
		curr_sum = 0;
	}

	void insert(int x) {
		freq[x]++;
		curr_sum += x;
	}

	void erase(int x) {
		freq[x]--;
		// Delete entry when frequency becomes 0 (issue with get_min & get_distinct)
		if(freq[x] == 0) {
			freq.erase(x);
		}
		curr_sum -= x;
	}

	void erase_all(int x) {
		curr_sum -= freq[x] * x;    // Remove element from sum frequency times
		freq.erase(x);
	}

	int get_sum() {
		return curr_sum;
	}

	int get_min() {
		return freq.begin()->first;    // (*freq.begin()).first
	}

	int get_distinct() {
		return freq.size();
	}
};

int main() { 
	mybag x; 
	x.insert(2); 
	x.insert(5); 
	cout << x.get_sum() << '\n'; 

	return 0;
}
```
Not using Unordered map because it's worst case accessing time complexity can go to $O(N)$, only average case is $O(1)$

__NOTE__ : In 1 sec time limit, $O(N\log^{2} N)$ may pass but $O(N\log^{3}N)$ never passes

---

## Question 2 : Nesting of Structs
__Design a Dashboard with following functions__ : 
- ingest(name, score) : Inserts score (per ball) of Cricket Player with given name
- get_details(name) : Shows details (Sum, Mean, Variance and SD) of Player with given name

Will the data of 2 Players ever interact with each other ?
No, that's why use 2 structs
```cpp
#include <bits/stdc++.h>
using namespace std;

struct Player_details {
	int cur_sum;
	int cur_cnt;    // Tracks number of balls played
	int cur_sq_sum;    // Tracks sum of squares of score

	// Constructor
	Player_Details() {
		cur_sum = 0;
		cur_cnt = 0;
		cur_sq_sum = 0;
	}

	void insert(int x) {
		cur_sum += x;
		cur_sq_sum += x*x;
		cur_cnt++;
	}

	// Converts cur_sum into double, to avoid integer division in get_mean()
	double get_sum() {
		return cur_sum;
	}

	double get_mean() {
		return get_sum()/cur_cnt;    // double(cur_sum)/cur_cnt
	}

	// Var(X) = E(X^2) - E(X)^2
	double get_var() {
		double mean_sq_sum = (double)cur_sq_sum/cur_cnt;
		double mean = get_mean();
		return mean_sq_sum - (mean * mean);
	}

	// SD(X) = Var(X)^0.5
	double get_sd() {
		int var = get_var();
		return sqrt(var);
	}

	map<string, double> get_details() {
		map<string, double> details;
		details["mean"] = get_mean();
		details["sum"] = get_sum();
		details["variance"] = get_var();
		details["standard deviation"] = get_sd();
		return details;
	}
};

struct Dashboard {
	map<string, Player_details> mp;    // {name, details}

	void ingest(string player, int score) {
		map[player].insert(score);
	}

	map<string, double> get_details(string player) {
		return map[player].get_details();
	}
};

int main() { 
	Dashboard mydash; 
	mydash.ingest("virat",6); 
	mydash.ingest("dhoni",2); 
	mydash.ingest("virat",0); 
	
	auto data = mydash.get_details("virat"); 
	for(auto v:data){ 
		cout << v.first << " " << v.second << '\n'; 
	} 

	return 0;
}
```
__NOTE__ : For learning about industry level good coding practices, refer [C++ Style Guide](https://google.github.io/styleguide/cppguide.html)

---

## Question 3 : Running Mean, Median and Mode
__Mean__, often referred to as the average, is a fundamental measure of central tendency that represents the sum of all values divided by the total number of observations.

__Median__ is the middle value of a dataset when arranged in ascending order. For datasets with an even number of observations, the median is typically calculated as the average of the two middle values.

__Variance__ measures the spread or dispersion of a dataset by calculating the average of the squared differences between each data point and the mean.

__Mode__ is the value that appears most frequently in a dataset.

__Design a Data structure with following functions__ : 
- insert(int x) : Inserts value `x`
- erase(int x) : Erases value `x` (given `x` definitely exists at least once)
- get_mean() : Returns mean of all values present
- get_variance() : Returns variance of all values present 
- get_median() : Returns median of all values present
- get_mode() : Returns mode of all values present (if frequency is same, consider highest valued one)

__Handling the Median__

The median is the value that separates the higher half from the lower half of a dataset. To efficiently maintain and compute the median during insertions and deletions,  `myBag` structure uses 2 `multiset`

- `smaller` : This multiset contains the smaller half of the numbers.
- `larger` : This multiset contains the larger half of the numbers.

$\underline{\textit{Insertion of an Element}}$

When an element $x$ is inserted into the `myBag`, the following steps are followed :

1. _Insert into the Appropriate Multiset_
    - If the `smaller` set is empty, insert $x$ directly into `smaller`.
    - If `smaller` is not empty, determine where $x$ should go:
        - Compare $x$ with the maximum of `smaller` (which is `*s_last`, where `s_last` is the last element of the `smaller` multiset).
        - If $x$ is less than or equal to the maximum of `smaller`, it goes into `smaller`.
        - If $x$ is greater, it goes into `larger`.
3. _Balance the Sets_
   After inserting $x$, call the `balance_sl()` function to ensure the sizes of `smaller` and `larger` remain balanced:
    - The sizes can differ by at most 1.
    - If `smaller` has more than one extra element compared to `larger`, transfer the largest element from `smaller` to `larger`.
    - If `larger` has more elements than `smaller`, transfer the smallest element from `larger` to `smaller`.

$\underline{\textit{Removal of an Element}}$

When an element $x$ is erased, the process is as follows :
1. _Remove from the Appropriate Multiset_:
   Determine whether $x$ is in `smaller` or `larger`:
	- If `larger` is empty, it implies $x$ must be in `smaller`. Remove it from `smaller`.
    - If $x$ is less than or equal to the maximum of `smaller`, remove it from `smaller`.
    - Otherwise, remove it from `larger`.
2. _Balance the Sets_:
   After removing $x$, call the `balance_sl()` function to ensure the sizes remain balanced.

$\underline{\textit{Retrieving the Median}}$

The median can be computed efficiently based on the sizes of `smaller` and `larger`:
- If the total number of elements (`t_size`) is odd, the median is the maximum of `smaller`, which can be accessed as `*(smaller.rbegin())`
- If the total number of elements is even, the median is the average of the maximum of `smaller` and the minimum of `larger`. 

__Handling the Mode__

The mode is calculated by maintaining a frequency count of each element in the `freq` map. The `modeCalc` multiset is structured as pairs of frequency and value, allowing you to keep track of how many times each number appears.

$\underline{\textit{Mode Handling Logic}}$
- _Insert Operation_:
    
    - Before inserting a new element, if it already exists, we remove its previous frequency from `modeCalc` using `modeCalc.erase({freq[x], x});`.
    - We increment the frequency of the element in `freq`, and then insert the updated frequency into `modeCalc`.
    - This ensures that `modeCalc` always contains the most recent frequencies, allowing you to quickly retrieve the current mode.
- _Erase Operation_:
    
    - Similarly, when erasing an element, we first remove its frequency from `modeCalc`.
    - We decrement its frequency in `freq`, and if it's still greater than zero, we insert the updated frequency back into `modeCalc`.
    - If the frequency reaches zero, the element is removed from `freq`, ensuring that `modeCalc` only contains valid entries.


```cpp
#include <bits/stdc++.h>
using namespace std;

struct myBag {
	// Mean & Variance
	int cur_sum;
	int cur_sq_sum;
	int cur_cnt;

	// Median
	multiset<int> smaller;
	multiset<int> larger;
	int s_size;
	int l_size;
	
	// Mode
	map<int, int> freq;    // {value: frequency}
	multiset<pair<int, int>> modeCalc;    // {frequency, value}
	// In modeCalc, every pair is unique bcoz every element has 1 frequency assigned

	myBag() {
		cur_sum = 0;
		cur_cnt = 0;
		cur_sq_sum = 0;
		s_size = 0;
		l_size = 0;
	}

	void balance_sl() {    // O(logN)
		int d_size = s_size - l_size;
		if(d_size != 0 && d_size != 1) {
			if(d_size > 0) {
				auto s_last = prev(smaller.end());
				int transfer_val = *s_last;
				smaller.erase(s_last);
				s_size--;
				larger.insert(transfer_val);
				l_size++;
			}
			else {
				auto l_first = larger.begin();
				int transfer_val = *l_first;
				larger.erase(l_first);
				l_size--;
				smaller.insert(transfer_val);
				s_size++;
			} 
		}
	}

	void insert(int x) {    // O(logN)
		// Mean & Variance
		cur_sum += x;
		cur_sq_sum += x*x;
		cur_cnt++;
		
		// Mode
		if(freq[x] > 0) modeCalc.erase({freq[x], x});    // Every pair is unique
		freq[x]++;
		modeCalc.insert({freq[x], x});

		// Median
		if(smaller.empty()) {
			smaller.insert(x);
			s_size++;
		} else {
			auto s_last = prev(smaller.end());
			if(x <= *s_last) {
				smaller.insert(x);
				s_size++;
			}
			else {
				larger.insert(x);
				l_size++;
			}
			balance_sl();
		}
	}

	void erase(int x) {    // O(logN)
		// Mean & Variance
		cur_sum -= x;
		cur_sq_sum -= x*x;
		cur_cnt--;
		
		// Mode
		modeCalc.erase({freq[x], x});
		freq[x]--;
		if(freq[x] == 0) freq.erase(x);
		if(freq[x] > 0) modeCalc.insert({freq[x], x});

		// Median
		if(larger.empty()) {
			auto it = smaller.find(x);
			smaller.erase(it);
			s_size--;
		} else {
			auto s_last = prev(smaller.end());
			if(x <= *s_last) {
				auto it = smaller.find(x);
				smaller.erase(it);
				s_size--;
			} else {
				auto it = larger.find(x);
				larger.erase(it);
				l_size--;
			}
			balance_sl();
		}
	}

	double get_mean() {    // O(1)
		return double(cur_sum)/cur_cnt;    // (1.0 * cur_sum)/cur_cnt
	}

	// Var(X) = E(X^2) - (E(X))^2
	double get_variance() {    // O(1)
		double mean = get_mean();
		double mean_sq_sum = double(cur_sq_sum)/cur_cnt;
		return mean_sq_sum - (mean * mean);
	}

	double get_median() {    // O(logN) (logN->Balance + 1->Accessing)
		int t_size = s_size + l_size;
		if(t_size % 2) return *(smaller.rbegin());
		else {
			double val_1 = *(smaller.rbegin());
			double val_2 = *(larger.begin());
			return (val_1+val_2)/2;    // (*(smaller.rbegin()) + *(larger.begin()))/2.0
		}
	}

	double get_mode() {    // O(logN)
		return modeCalc.rbegin()->second;
	}
};

int main() { 
	myBag x; 
	x.insert(2); 
	x.insert(5); 
	x.insert(8);

	cout << "Before erase" << '\n';
	cout << "Mean : " << x.get_mean() << '\n'; 
	cout << "Variance : " << x.get_variance() << '\n'; 
	cout << "Median : " << x.get_median() << '\n'; 
	cout << "Mode : " << x.get_mode() << '\n'; 
	
	x.erase(5);
	cout << '\n';
	
	cout << "After erase" << '\n';
	cout << "Mean : " << x.get_mean() << '\n'; 
	cout << "Variance : " << x.get_variance() << '\n'; 
	cout << "Median : " << x.get_median() << '\n'; 
	cout << "Mode : " << x.get_mode() << '\n'; 
	
	return 0; 
}
```
Output
```
Before erase
Mean : 5
Variance : 6
Median : 5
Mode : 8

After erase
Mean : 5
Variance : 9
Median : 5
Mode : 8
```

__NOTE__
Don't use `count()` to count the number of occurrence because it's linear in number of occurrence, it's not a $O(\log N)$ function. But `find()` is $O(\log N)$