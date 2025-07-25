---
title: Game DP (Form 5)
date: 2024-01-16 10:00:00 +0530
categories: [DSA, Dynamic Programming]
tags: [game dp, grundy number, game theory, win/lose dp, xor dp, subtraction game]
math: true
mermaid: true
pin: false
---

## Form 5 - Game DP
### **Transition**

$$DP(Config) \rightarrow W/L$$ 

This state represents whether the current configuration (`Config`) results in a winning ($W$) or losing ($L$) position for the current player.

The key idea is to evaluate whether the current configuration can **force the opponent into a losing state**:

- If there exists any move from the current configuration that transitions to a losing state for the opponent, the current state is winning ($W$).
- Conversely, if all possible moves lead to winning states for the opponent, the current state is losing ($L$).

In the base case, if no moves are possible from the current configuration, it is considered a losing state.

### **Identifying Game DP Problems**

1. _Impartial Games_  
    These are games where **both players have the same set of rules** and the outcome depends solely on the current configuration and the available moves.  
    Example: Nim game, Grundy numbers, or any problem where players alternate turns to reduce a configuration until no moves are left.
    
2. _Configuration-Based Decision Making_  
    Problems that require evaluating the **current board state or scenario** and determining the best move for the player.  
    Example: Tic-tac-toe, chess-like problems, or minimizing/maximizing results based on optimal play.
    
3. _Forcing Strategy_  
    Problems where the goal is to **force the opponent into a guaranteed losing state** fall naturally into the Game DP framework.

### **Thinking about Transitions in Game DP**

- Start by assuming the **current state is losing** for the player.
    - If there are no valid moves, the state is losing.
- For each possible move from the current configuration, evaluate the resulting state:
    - If even **one resulting state** is losing for the opponent, the current state is winning for the player.
    - Otherwise, if **all resulting states** are winning for the opponent, the current state remains losing.

This approach builds transitions recursively by evaluating all possible configurations the player can reach. The final answer depends on systematically applying the above rules to determine the outcome for every possible state.

By combining these ideas, you can model problems like **Nim**, **Grundy numbers**, and other combinatorial games effectively using Game DP.

---

## Example-1 : Subtraction Game 
Vivek and Abhishek are playing a game of chips, taking turns alternatively. Initially, there are $x$ chips on table. On each turn, a player can pick up $2^m$ chips such that $m \geq 0$ and $x \geq 2^m$. A player loses the game if he has no chips to pick from the table.

Given that Vivek starts the game, Predict the winner of the game.

Constraints: $1 \leq T \leq 10^6$ and $0 \leq x \leq 2 \times 10^5$

**Approach-1: Game DP**

The game revolves around forcing the opponent into a losing state by choosing moves strategically. Each move involves removing chips in powers of 2 (1, 2, 4, 8, etc.) from the total chips available.

If you're in a state with `X` chips, you evaluate whether there exists any move that leaves the opponent in a losing position. The approach focuses on *evaluating each possible configuration of chips* after a move to determine if the current player can guarantee a win.

1. *Losing State Identification* 
    A state is considered losing if no matter what move the current player makes, the opponent can always transition to a winning state.
    
2. *Winning State Identification*
    If there exists any move that forces the opponent into a losing state, then the current configuration becomes a winning state.
    
3. *Recursive Thought Process*  
    At each state, assume the current player loses by default. Then, evaluate all valid moves:
    
    - If a move exists that transitions to a losing state for the opponent, the current state becomes winning.
    - Otherwise, it remains losing.

**Code-1 (Based on Game DP)**
```cpp
#include<bits/stdc++.h>
using namespace std;

#define int long long 

int dp[200001];

int rec(int x) {
    // pruning
    // base case
    if(x == 0) {    // If no chip is left, current player is gonna lose
        return 0;
    }
    
    // cache check 
    if(dp[x] != -1) {
        return dp[x];
    }
    
    // transition
    int ans = 0;    // assuming current player is in losing state 
    for(int m=0; (1 << m)<=x; m++) {
        // If any move leads to losing state for opponent, then current player is gonna win
        if(rec(x-(1 << m)) == 0) {
            ans = 1;    
            break;
        }
    }
    
    // save and return
    return (dp[x] = ans);
}

void solve() {
    int x;
    cin >> x;
    
    // Recurrence Meaning:
    // rec(x) : Whether current player is gonna win or lose, as per current configuration
    if(rec(x)) cout << "Vivek\n";    // Assuming current player is "Vivek"
    else cout << "Abhishek\n";
}

signed main() {
    ios_base::sync_with_stdio(0);
    cin.tie(0); cout.tie(0);
    
	// Values filled in the dp array doesn't depends on test cases
    memset(dp, -1, sizeof(dp));
    
    int _t; cin >> _t; while(_t--)
    solve();
    return 0;
}
```

*Input & Output*
```cpp
// Input
5
0 
2
12783
1001
33

// Output
Abhishek
Vivek
Abhishek
Vivek
Abhishek
```

**NOTE**
Values filled in the Dp array doesn't depends on test cases

**Approach-2: Pattern Observation**
We can modify the `solve()` function like below, to see what actually the code is doing
```cpp
void solve() {
    // Recurrence Meaning:
    // rec(x) : Whether current player is gonna win or lose, as per current configuration
    for(int i=0; i<=10; i++) {
        cout << i << " " << rec(i) << '\n';
    }
}
```

*Input & Output*
```cpp
// Input
1

// Output
0 0
1 1
2 1
3 0
4 1
5 1
6 0
7 1
8 1
9 0
10 1
```
We can clearly observe the pattern of `011` being repeated.

**Code-2 (Based on Observed Pattern)**
```cpp
#include<bits/stdc++.h>
using namespace std;

#define int long long 

void solve() {
    int x;
    cin >> x;
    
    if(x % 3) cout << "Vivek\n";    // Assuming current player is "Vivek"
    else cout << "Abhishek\n";
}

signed main() {
    ios_base::sync_with_stdio(0);
    cin.tie(0); cout.tie(0);
    
    int _t; cin >> _t; while(_t--)
    solve();
    return 0;
}
```

*Input & Output*
```cpp
// Input
5
0 
2
12783
1001
33

// Output
Abhishek
Vivek
Abhishek
Vivek
Abhishek
```