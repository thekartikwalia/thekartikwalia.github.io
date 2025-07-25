---
title: Segment Tree Framework
date: 2025-02-09 8:00:00 +0530
categories: [DSA, Segment Tree]
tags: [segment tree, range query, point update, merge logic, data structures]
math: true
mermaid: true
pin: false
---

```cpp
#include <bits/stdc++.h>
using namespace std;

#define int long long 

// Node structure to store segment tree information
struct node {
    // Define necessary properties
    node() {
        // Initialise identity element
    }
};

// Merge function: Defines how two nodes combine
node merge(node &a, node &b) {
    node ans;
    // Define merge logic
    return ans;
}

// Segment tree array (typically 4*N size)
const int N = 200200;
node t[4 * N];

// Build function: Constructs segment tree from input array
void build(int id, int l, int r, vector<int>& arr) {
    if (l == r) {
        // Initialise leaf node
        return;
    }
    int mid = (l + r) / 2;
    build(2 * id, l, mid, arr);
    build(2 * id + 1, mid + 1, r, arr);
    t[id] = merge(t[2 * id], t[2 * id + 1]);
}

// Point update function: Updates a single position
void update(int id, int l, int r, int pos, /* update parameters */) {
    if (pos < l || r < pos) {
        return;
    }
    if (l == r) {
        // Apply update
        return;
    }
    int mid = (l + r) / 2;
    update(2 * id, l, mid, pos, /* update parameters */);
    update(2 * id + 1, mid + 1, r, pos, /* update parameters */);
    t[id] = merge(t[2 * id], t[2 * id + 1]);
}

// Range query function: Queries over [lq, rq]
node query(int id, int l, int r, int lq, int rq) {
    if (rq < l || r < lq) {  
        return node();  // Return identity element
    }
    if (lq <= l && r <= rq) {
        return t[id];
    }
    int mid = (l + r) / 2;
    return merge(query(2 * id, l, mid, lq, rq), query(2 * id + 1, mid + 1, r, lq, rq));
}

void solve() {
    int n, q;
    cin >> n >> q;
    vector<int> arr(n);
    for (int i = 0; i < n; i++) cin >> arr[i];
    
    build(1, 0, n - 1, arr);
    
    while (q--) {
        int type;
        cin >> type;
        if (type == 1) { 
            int pos;
            cin >> pos;
            pos--;  // Convert to 0-based index
            update(1, 0, n - 1, pos, /* update parameters */);
        } else {
            int l, r;
            cin >> l >> r;
            l--, r--;  // Convert to 0-based index
            cout << query(1, 0, n - 1, l, r) << '\n';
        }
    }
}

signed main() {
    ios_base::sync_with_stdio(0);
    cin.tie(0); cout.tie(0);
    
    // int _t; cin >> _t; while(_t--)
    solve();
    return 0;
}
```