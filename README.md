# STL
## index
- [basic](#basic)
- [containers](#CONTAINERS)
- [algorithm](#ALGORITHM)
- [iterators](#iterators)
- [function](#function)

## basic
```cpp
STL (Standard Template Library)
The STL is a collection of generic classes and functions in C++ that provide ready-made data structures and algorithms.

Main components of STL

1. Containers: store data
    Examples: vector, list, deque, set, map, unordered_map, stack, queue, priority_queue

2. Algorithms: perform operations on data
    Examples: sort, find, reverse, count, max_element, min_element

3. Iterators: access container elements
    Examples: begin(), end(), rbegin(), rend()

4. Function objects (Functors): objects that act like functions
    Examples: greater<>, less<>

Advantages of STL
  Reusable and efficient
  Reduces code length
  Well-tested and optimized

👉 STL makes C++ powerful, fast, and easier to use.
```

## CONTAINERS
Containers (STL) — Definition

Containers are STL components used to store and organize data in memory so that it can be accessed and modified efficiently.
They hold multiple elements of the same data type and manage memory automatically.

vector, list, stack, queue, priority_queue, deque, map, unordered_map, set 

- [vector](#VECTOR)
- [list](#LIST)
- [stack](#STACK)
- [queue](#QUEUE)
- [map](#MAP)
- [set](#SET)
  
## VECTOR 

**Vector (STL) — Definition**

A **vector** is a **dynamic array** provided by the STL that stores elements in **contiguous memory** and can **grow or shrink automatically** at runtime.

**Key points**

* Fast random access — **O(1)**
* Dynamic size
* Elements stored continuously in memory

**Example:**

```cpp
vector<int> v;
```

---

## **Vector Functions (STL)**

### 🍀 Capacity & Size
- [capacity and size](#capacity-and-size)
---

### 🍀 Modifiers
- [modifier](#modifier)
---

### 🍀 Element Access
- [Element Access](#Element-Access)
---

### 🍀 Iterators
- [Iterators](#Iterators)
---

### 🍀 Common STL Algorithms used with vector
- [Common STL Algorithms used with vector](#Common-STL-Algorithms-used-with-vector)
  
---

## capacity and size
---
* `size()` → returns number of elements — [size](#size)
* `capacity()` → returns allocated storage — [capacity](#capacity)
* `empty()` → checks if vector is empty — [empty](#empty)
* `resize(n)` → changes size of vector — [resize](#resize)
* `reserve(n)` → reserves capacity — [reserve](#reserve)
* `shrink_to_fit()` → reduces capacity — [shrink_to_fit](#shrink_to_fit)
* `[]()` → — [bracket](#bracket)
---
---
#### STL `vector` growth 

* `size` = used boxes
* `capacity` = total boxes
* When full → **capacity doubles**

```
1  →  2  →  4  →  8  →  16 ...
[_]

[1][2]

[1][2][3][_]

[1][2][3][4][5][_][_][_]
```

👉 Doubling gives **fast push_back (amortized O(1))**

---

#### combined code 

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> vec;

    // empty()
    cout << "Is vector empty? " << vec.empty() << endl;

    vec.push_back(1);
    vec.push_back(2);
    vec.push_back(3);
    vec.push_back(4);
    vec.push_back(5);

    // size and capacity
    cout << "Size: " << vec.size() << endl;
    cout << "Capacity: " << vec.capacity() << endl;

    // resize(n)
    vec.resize(3);
    cout << "Size after resize: " << vec.size() << endl;
    cout << "Capacity after resize: " << vec.capacity() << endl;

    // reserve(n)
    vec.reserve(10);
    cout << "Capacity after reserve: " << vec.capacity() << endl;

    // shrink_to_fit()
    vec.shrink_to_fit();
    cout << "Capacity after shrink_to_fit: " << vec.capacity() << endl;

    return 0;
}
```
##### size 
```cpp
cout << "Size: " << vec.size() << endl;
```

##### capacity 
```cpp
cout << "Capacity: " << vec.capacity() << endl;
```

##### empty
```cpp
cout << "Is vector empty? " << vec.empty() << endl;
```

##### resize
Changes size
Adds elements (default-initialized) or removes elements
Capacity may increase

```cpp
vec.resize(3);
    cout << "Size after resize: " << vec.size() << endl;
    cout << "Capacity after resize: " << vec.capacity() << endl;
```

##### reverse
Changes capacity only
No elements added/removed
Size unchanged

```cpp
vec.reserve(10);
    cout << "Capacity after reserve: " << vec.capacity() << endl;
```

##### shrink_to_fit
Reduces capacity to size
Size unchanged
Non-binding request (usually works)

```cpp
vec.shrink_to_fit();
    cout << "Capacity after shrink_to_fit: " << vec.capacity() << endl;
```

#### bracket
```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
    vector<int> vec; //0
    vec.push_back(1);
    vec.push_back(2);
    vec.push_back(3);
    vec.push_back(4);
    vec.push_back(5);
    cout << vec.size() << endl; //3
    cout << vec.capacity() << endl; //4

    cout << "val at idx 2" << vec [2] << or << vec.at(2) << endl;

return 0;

}

```

## Modifier

* `push_back(x)` → insert element at end — [push_back](#push_back)
* `pop_back()` → remove last element — [pop_back](#pop_back)
* `emplace_back()` → insert last element — [emplace_back](#emplace_back)
* `insert(pos, x)` → insert at position — [insert](#insert)
* `erase(pos)` → remove element — [erase](#erase)
* `clear()` → remove all elements — [clear](#clear)
* `assign(n, x)` → fill vector — [assign](#assign)
* `swap(v)` → swap vectors — [swap](#swap)

#### combined code 
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> vec;

    // push_back()
    vec.push_back(10);
    vec.push_back(20);
    vec.push_back(30);

    // emplace_back()
    vec.emplace_back(40);

    cout << "Vector elements: ";
    for (int x : vec) cout << x << " ";
    cout << endl;

    // pop_back()
    vec.pop_back();

    cout << "After pop_back: ";
    for (int x : vec) cout << x << " ";
    cout << endl;

    // insert()
    vec.insert(vec.begin() + 1, 15);

    cout << "After insert: ";
    for (int x : vec) cout << x << " ";
    cout << endl;

    // erase()
    vec.erase(vec.begin() + 2);

    cout << "After erase: ";
    for (int x : vec) cout << x << " ";
    cout << endl;

    // assign()
    vec.assign(3, 7);

    cout << "After assign: ";
    for (int x : vec) cout << x << " ";
    cout << endl;

    // clear()
    vec.clear();
    cout << "Size after clear: " << vec.size() << endl;

    // swap()
    vector<int> vec2 = {1, 2, 3};
    vec.swap(vec2);

    cout << "After swap, vec elements: ";
    for (int x : vec) cout << x << " ";
    cout << endl;

    return 0;
}
```
---

### push_back

Adds element at end
Size ↑, capacity may ↑

```cpp
vec.push_back(10);
```

---

### pop_back

Removes last element
Size ↓, capacity same

```cpp
vec.pop_back();
```

---

### emplace_back

* Adds element at end (faster than push_back for objects)
* can create inplace object

```cpp
vec.emplace_back(20);
```

---

### insert

Inserts element at given position
Shifts elements right

```cpp
vec.insert(vec.begin() + 1, 5);
```

---

### erase

Removes element at position
Shifts elements left

```cpp
vec.erase(vec.begin() + 2);
```

---

### clear

Removes all elements
Size = 0, capacity unchanged

```cpp
vec.clear();
```

---

### assign

Replaces all elements with `n` copies of value

```cpp
vec.assign(4, 7); // [7 7 7 7]
```

---

### swap

Swaps contents of two vectors (O(1))

```cpp
vec1.swap(vec2);
```

---

---

## Element Access

* **at(i)** → bounds-checked access — `at`
* **operator[]** → direct access (no check) — `[]`
* **front()** → first element — `front`
* **back()** → last element — `back`
* **data()** → pointer to internal array — `data`

---

## combined Code 

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> vec = {10, 20, 30, 40};

    // at()
    cout << "at(1): " << vec.at(1) << endl;

    // operator[]
    cout << "operator[2]: " << vec[2] << endl;

    // front()
    cout << "front(): " << vec.front() << endl;

    // back()
    cout << "back(): " << vec.back() << endl;

    // data()
    int* ptr = vec.data();
    cout << "data()[0]: " << ptr[0] << endl;

    return 0;
}
```

---

### at()

✔ Bounds-checked
❌ Throws exception if index invalid

```cpp
vec.at(2);
```

---

### operator[]

✔ Faster
❌ No bounds checking

```cpp
vec[2];
```

---

### front()

✔ Access first element

```cpp
vec.front();
```

---

### back()

✔ Access last element

```cpp
vec.back();
```

---

### data()

✔ Returns pointer to internal array
✔ Useful for C-style arrays

```cpp
int* p = vec.data();
```

---
---

## Iterators 

* **begin() / end()** → forward iterators — `begin`, `end`
* **rbegin() / rend()** → reverse iterators — `rbegin`, `rend`
* **cbegin() / cend()** → constant iterators — `cbegin`, `cend`

---

## 🔹 Combined Code 

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> vec = {10, 20, 30, 40};

    // begin() / end()
    cout << "Forward: ";
    for (auto it = vec.begin(); it != vec.end(); it++)
        cout << *it << " ";
    cout << endl;

    // rbegin() / rend()
    cout << "Reverse: ";
    for (auto it = vec.rbegin(); it != vec.rend(); it++)
        cout << *it << " ";
    cout << endl;

    // cbegin() / cend()
    cout << "Constant: ";
    for (auto it = vec.cbegin(); it != vec.cend(); it++)
        cout << *it << " ";
    cout << endl;

    return 0;
}
```

---

### begin() / end()

✔ Points to first element
✔ `end()` → points **after last element**

```cpp
vec.begin();
vec.end();
```

---

### rbegin() / rend()

✔ Reverse traversal
✔ `rbegin()` → last element
✔ `rend()` → before first element

```cpp
vec.rbegin();
vec.rend();
```

---

### cbegin() / cend()

✔ Read-only iterator
❌ Cannot modify values

```cpp
vec.cbegin();
vec.cend();
```
---

---

## Common STL Algorithms used with vector

**sort()** → sorts elements — `sort`
**reverse()** → reverses order — `reverse`
**find()** → searches element — `find`

---

## 🔹 Combined Code (Algorithms)

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> v = {40, 10, 30, 20};

    // sort()
    sort(v.begin(), v.end());
    cout << "After sort: ";
    for (int x : v) cout << x << " ";
    cout << endl;

    // reverse()
    reverse(v.begin(), v.end());
    cout << "After reverse: ";
    for (int x : v) cout << x << " ";
    cout << endl;

    // find()
    int key = 30;
    auto it = find(v.begin(), v.end(), key);

    if (it != v.end())
        cout << "Found " << key << " at index "
             << it - v.begin() << endl;
    else
        cout << "Not found" << endl;

    return 0;
}
```

---

## 🔹 Quick Notes (Algorithm-wise)

### sort()

✔ Sorts in ascending order (default)
✔ Time: **O(n log n)**

```cpp
sort(v.begin(), v.end());
```

---

### reverse()

✔ Reverses vector order
✔ Time: **O(n)**

```cpp
reverse(v.begin(), v.end());
```

---

### find()

✔ Linear search
✔ Returns iterator
✔ If not found → `v.end()`

```cpp
find(v.begin(), v.end(), x);
```

---































- [push and pop](#push-and-pop)
- [size and capacity](#size-and-capacity)
- [emplace_back](#emplace_back)
- [() []](#(-)-[-])
- [front and back ](#front-and-back)
- [vector begin and erase](#vector-begin-and-erase)
- [same number in table](#same-number-in-table)
- [plus n on begin](#plus-n-on-begin)
- [replacing an element by other](#replacing-an-element-by-other)
- [clear](#clear)
- [loop with begin](#loop-with-begin)


    
#### emplace_back 
```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
    vector<int> vec; //0
    vec.push_back(1);
    vec.push_back(2);
    vec.push_back(3);
    vec.push_back(4);
    vec.push_back(5);
    vec.emplace_back(6);
    
    
    for(int val: vec) {
        cout << val << " ";
        
    }
    cout << endl;

return 0;

}
```

#### front and back 
```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
    vector<int> vec; //0
    vec.push_back(1);
    vec.push_back(2);
    vec.push_back(3);
    vec.push_back(4);
    vec.push_back(5);
    vec.emplace_back(6);
    
    vec.pop_back();
    for(int val: vec) {
        cout << val << " ";
        
    }
    cout << endl;
    
    cout << "front" << vec.front() << endl;
    cout << "back" << vec.back() << endl;

return 0;

}
```

#### vector begin and erase 
```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
    vector<int> vec = {1, 2, 3, 4, 5};
    vec.erase (vec.begin());
    for(int val: vec) {
        cout << val << " ";
    }
    cout << endl;
    
return 0;

}
```

#### same number in table
```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
    vector<int> vec(10,-2); //dynamic programming tabular data 
    
    vec.pop_back();
    for(int val: vec) {
        cout << val << " ";
        
    }
    cout << endl;

return 0;

}
```

####  plus n on begin 

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
    vector<int> vec = {1, 2, 3, 4, 5};
    vec.erase (vec.begin() + 2 );
    for(int val: vec) {
        cout << val << " ";
    }
    cout << endl;
    
return 0;

}
```

#### replacing an element by other

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
    vector<int> vec = {1, 2, 3, 4, 5};
    vec.erase (vec.begin() + 2 );
    for(int val: vec) {
        cout << val << " ";
    }
    cout << endl;
    
return 0;

}
```

#### clear

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
    vector<int> vec = {1, 2, 3, 4, 5};
    
    vec.clear();
    
    for(int val: vec) {
        cout << val << " ";
    }
    cout << endl;
    
    cout << "is empty: "<< vec.empty() << endl;
    
return 0;

}
```

#### loop with begin 
```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
    vector<int> vec = {1, 2, 3, 4, 5};
    
    for(vector<int>:: reverse_iterator it=vec.rbegin(); it != vec.rend(); it++) {
        cout << *(it) << " ";
    }
    
    cout << endl;
    
return 0;

}
```

### LIST
- [push and pop](#push-and-pop)
- [pair](#pair)


#### push and pop 

```cpp
#include <iostream>
#include <list>

using namespace std;

int main() {
    list<int> l; //0
    l.push_back(1);
    l.push_back(2);
    l.push_back(3);
    l.push_back(4);
    l.push_back(5);
    
    l.emplace_back(6);
    
    l.pop_back();
    
    for(int val: l) {
        cout << val << " ";
        
    }
    cout << endl;
    
    cout << "front" << l.front() << endl;
    cout << "back" << l.back() << endl;

return 0;

}
```

#### pair
```cpp
#include <iostream>
#include <list>


using namespace std;

int main() {
    pair<int, pair<char, int>> p = {1, {'a', 3}};
    
    cout << p.first << endl;
    cout << p.second.first << endl;

return 0;

}
```

```cpp
#include <iostream>
#include <list>
#include <vector>
#include <deque>

using namespace std;

int main() {
    vector<pair<int, int>> vec = {{1, 2}, {2, 3}, {3, 4}};
   // vec.push_back(4, 54); //insert
    vec.emplace_back(4, 5); //in-place objects create
    for(auto p: vec) {
        cout << p.first <<" "<< p.second << endl;
    }

return 0;

}
```

### STACK

```cpp

#include <iostream>
#include <stack>

using namespace std;
int main() {
    stack<int> s;
    s.push(1);
    s.push (2);
    s.push(3);
    stack<int> s2;
    s2.swap(s);
    while(!s.empty()) {
        cout << s.top() << "";
        s.pop();
    }
    cout << endl;
    
return 0;

}

```

```cpp
#include <iostream>
#include <stack>

using namespace std;
int main() {
    stack<int> s;
    s.push(1);
    s.push (2);
    s.push(3);
    stack<int> s2;
    s2.swap(s);
    
    cout << endl;
    
    cout << "s.size: " << s.size() << endl;
    cout << "s2.size: " << s2.size() << endl;
    
return 0;

}

```


### QUEUE

```cpp
#include <iostream>
#include <queue>

using namespace std;

int main(){
    queue<int> q;
    q.push(1);
    q.push(2);
    q.push(3);
    while(!q.empty()) {
        cout << q.front() <<" ";
        q.pop();
    }
    cout << endl;

return 0;

}
```


### MAP
```cpp
#include <iostream>
#include <map>

using namespace std;

int main() {
    map<string, int> m;
    m["tv"] = 100;
    m["laptop"] = 100;
    m["headphones"] = 50;
    m["tablet"] = 120;
    m["watch"] = 50;
    for(auto p: m) {
        cout << p.first << " " << p.second << endl;
    }
    return 0;
}

```

```cpp

#include <iostream>
#include <map>

using namespace std;

int main() {
    map<string, int> m;
    m["tv"] = 100;
    m["laptop"] = 100;
    m["headphones"] = 50;
    m["tablet"] = 120;
    m["watch"] = 50;
    for(auto p: m) {
        cout << p.first << " " << p.second << endl;
    }
    
    m.emplace("camera", 25);
    
    for(auto p: m) {
        cout << p.first << " " << p.second << endl;
    }
    
    cout <<< "count = " << m.count("laptop") << endl;
    
    return 0;
}

```
```cpp
#include <iostream>
#include <map>

using namespace std;

int main() {
    map<string, int> m;
    m["tv"] = 100;
    m["laptop"] = 100;
    m["headphones"] = 50;
    m["tablet"] = 120;
    m["watch"] = 50;
    for(auto p: m) {
        cout << p.first << " " << p.second << endl;
    }
    
    m.emplace("camera", 25);
    
    m.erase("tv");

    for(auto p: m) {
        cout << p.first << " " << p.second << endl;
    }
        if (m.find("camera") != m.end()) {
            cout << "found\n";
            
        }else {
            cout << "not found";
        }
    
    
    return 0;
}
```
```cpp
#include <iostream>
#include <map>

using namespace std;

int main() {
    map<string, int> m;
    m["tv"] = 100;
    m["laptop"] = 100;
    m["headphones"] = 50;
    m["tablet"] = 120;
    m["watch"] = 50;
    for(auto p: m) {
        cout << p.first << " " << p.second << endl;
    }
    
    m.emplace("camera", 25);
    
    m.erase(m.find("tv"));
    
    for(auto p: m) {
        cout << p.first <<" "<< p.second << endl;
    }
    
    
    return 0;
}
```

##### multimap
```cpp
#include <iostream>
#include <map>

using namespace std;

int main() {
    multimap<string, int> m;
    
    m.emplace("tv", 100);
    m.emplace("tv", 100);
    m.emplace("tv", 100);
    m.emplace("tv", 100);
    
    m.erase(m.find("tv"));
    
    for(auto p: m) {
        cout << p.first << " " << p.second << endl;
    }

return 0;


}
```

```cpp
#include <iostream>
#include <algorithm>  

using namespace std;

int main() {
    int arr[5] = {3, 5, 1, 8, 2};

    sort(arr, arr + 5);  

    for (int val : arr) {
        cout << val << " ";  
    }

    cout << endl;

    return 0;
}

```

#### SET
```cpp
#include <iostream>
#include <map>
#include <set>
using namespace std;

int main() {
    set<int> s;
    s.insert(1);
    s.insert(2);
    s.insert(3);
    s.insert(4);
    s.insert(5);
    for(auto val: s) {
        cout << val << " ";
        cout << endl;
    }

return 0;


}
```

```cpp
#include <iostream>
#include <map>
#include <set>
using namespace std;

int main() {
    set<int> s;
    s.insert(1);
    s.insert(2);
    s.insert(3);
    s.insert(4);
    s.insert(5);
    
    
    cout << "lower bound = " << *(s.lower_bound (4)) << endl; //4
    
    for(auto val: s) {
        cout << val << " ";
        cout << endl;
    }

return 0;
}
```

### ALGORITHM
Algorithms (STL) — Definition

Algorithms are STL functions used to perform operations on data stored in containers, such as searching, sorting, counting, or modifying elements.
They work with iterators and are independent of container type.

Examples: sort, find, reverse, count, max_element

#### sorting
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int main() {
vector<int> vec = {3, 5, 1, 8, 2};

sort(vec.begin(), vec.end(), greater<int>());

for(int val : vec) {
    cout << val << " ";
};

cout << endl;
return 0;
};
```

###### sorting in pair
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int main() {
    vector<pair<int, int>> vec = {{3, 1}, {2, 1}, {7, 1}, {5, 2}};

    sort(vec.begin(), vec.end());

    for(auto p : vec) {
        cout << p.first << " " << p.second << endl;
    };


return 0;
};
```

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;
bool comparator(pair<int,int> p1,pair<int,int> p2){
    if(p1.second < p2.second) return true;
    if(p1.second > p2.second) return false;
    
    if(p1.first < p2.first) return true;
    else return false ;
}



int main() {
    vector<int> vec = {1, 2, 3, 4, 5};
    
    reverse (vec.begin(), vec.end());
for(auto val : vec) {
    cout << val<< endl;
}

return 0;
};
```

##### next permutations 
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;
bool comparator(pair<int,int> p1,pair<int,int> p2){
    if(p1.second < p2.second) return true;
    if(p1.second > p2.second) return false;
    
    if(p1.first < p2.first) return true;
    else return false ;
}



int main() {
    string s = "abc";
    next_permutation (s.begin(), s.end());
    
    cout << s << endl;

return 0;
};
```
##### prev permutations 
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;
bool comparator(pair<int,int> p1,pair<int,int> p2){
    if(p1.second < p2.second) return true;
    if(p1.second > p2.second) return false;
    
    if(p1.first < p2.first) return true;
    else return false ;
}



int main() {
    string s = "abc";
    prev_permutation (s.begin(), s.end());
    
    cout << s << endl;

return 0;
};
```


```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;
bool comparator(pair<int,int> p1,pair<int,int> p2){
    if(p1.second < p2.second) return true;
    if(p1.second > p2.second) return false;
int main() {
    vector<int> vec = {1,2,3,4,5};
    
    cout << *(max_element(vec.begin(),vec.end()) )<< endl;
    cout << *(min_element(vec.begin(),vec.end()) )<< endl;
    cout << binary_search(vec.begin(),vec.end(),4) << endl;
return 0;
};
```

#### builtin count sets 
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int main() {
    int n = 15;
    
    cout << __builtin_popcount(n) << endl ;
    
return 0;
};
```

