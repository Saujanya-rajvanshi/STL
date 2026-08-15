# STL
## index
- [basic](#basic)
- [containers](#CONTAINERS)
- [iterators](#ITERATORS)
- [algorithm](#ALGORITHM)
- [function](#FUNCTION)

## basic
```
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

STL makes C++ powerful, fast, and easier to use.


STL
│
├── Containers   → store data
├── Iterators    → access data
├── Algorithms   → process data
└── Functions    → customize behavior

```

## CONTAINERS
Containers are STL components used to store and organize data in memory so that it can be accessed and modified efficiently.
They hold multiple elements of the same data type and manage memory automatically.

vector, list, stack, queue, deque, priority_queue, map, unordered_map, set 

- [vector](#VECTOR)
- [list](#LIST)
- [stack](#STACK)
- [queue](#QUEUE)
- [deque](#deque)
- [priority_queue](#priority_queue)
- [map](#map)
- [unordered_map](#unordered_map)
- [set](#SET)
- [difference](#STL-CONTAINERS--ADAPTORS-COMPARISON)
  
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
- [capacity and size](#capacity-and-size)
- [modifier](#modifier)
- [Element Access](#Element-Access)
  
---

## capacity and size
---
* `size()` → returns number of elements — [size](#size)
* `capacity()` → returns allocated storage — [capacity](#capacity)
* `empty()` → checks if vector is empty — [empty](#empty)
* `resize(n)` → changes size of vector — [resize](#resize)
* `reserve(n)` → reserves capacity — [reserve](#reserve)
* `shrink_to_fit()` → reduces capacity — [shrink_to_fit](#shrink_to_fit)
* `[]()` → vector index access — [bracket](#bracket)
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

[1][2][3][4]

[1][2][3][4][5][_][_][_]

```
👉 Doubling gives **fast push_back (amortized O(1))**
* when there is no more space left
* Allocate new memory , Copy into new memory, Insert
* the old copy gets deleted automaticaly
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
* **Changes size**
Adds elements (default-initialized) or removes elements
👉 It changes the **SIZE** of the vector, not primarily the capacity.
* Vector will contain exactly n elements
* Elements beyond index n-1  are removed
* **Capacity** usually remains the same 

```cpp
vec.resize(3);
    cout << "Size after resize: " << vec.size() << endl;
    cout << "Capacity after resize: " << vec.capacity() << endl;
```

##### resevse
👉 Changes **capacity** only
* No elements added/removed
* **Size unchanged**

```cpp
vec.reserve(10);
    cout << "Capacity after reserve: " << vec.capacity() << endl;
```

##### shrink_to_fit
👉 Reduces **capacity to size**
* Size unchanged
* Non-binding request (usually works) Non-binding = may obey
* It is a request, not a command

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

    cout << "val at idx 2 : " << vec[2] << " or " << vec.at(2) << endl;

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

#### push_back

👉 Adds element at end
* Size ↑, capacity may ↑

```cpp
vec.push_back(10);
```

---

#### pop_back

👉 Removes last element
* Size ↓, capacity same

```cpp
vec.pop_back();
```

---

#### emplace_back

* Adds element at end (faster than push_back for objects)
* 👉 can create inplace object
* Size ↑, capacity may ↑

```cpp
vec.emplace_back(20);
```

---

#### insert

👉 Inserts element at **given position**
* Shifts elements right

```cpp
vec.insert(vec.begin() + 1, 5);
```

---

#### erase

👉 **Removes** element at position
* Shifts elements left

```cpp
vec.erase(vec.begin() + 2);
```

---

#### clear
+
👉 Removes **all** elements
* Size = 0, **capacity unchanged**

```cpp
vec.clear();
```
---

#### assign
👉 assign() **removes all existing** elements of the vector and **fills** it with **new** elements.
* vec.assign(n, value);
* Size becomes n
* Elements become value
* Old elements are destroyed Replaces all elements with `n` copies of value
* Capacity may or may not change

```cpp
vec.assign(4, 7); // [7 7 7 7]
```
---

#### swap
👉swap() **exchanges** the contents of two vectors.
* Sizes swapped
* Capacities swapped
* Data swapped

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

### combined Code 

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

#### at()
👉 returns the data 
*If index is invalid: Throws std::out_of_range
* Program can be handled using try–catch
* **Safe** failure

```cpp
vec.at(2);
```

---

#### operator[]
👉 return the data 
* If index is invalid: No error
* May access garbage value
* May crash or corrupt memory
* **Dangerous**

```cpp
vec[2];
```

---

#### front()
+
👉 Access first element

```cpp
vec.front();
```

---

#### back()

👉 Access last element

```cpp
vec.back();
```

---

#### data()
👉 data() returns a pointer to the internal contiguous memory used by the vector.
* p points to the first element of the vector
* Same as &vec[0] (when vector is not empty)
* vector stores elements contiguously, so data() is safe.
```
[10][20][30][40]
  ↑
  p
```
* If vector is empty: data() may return nullptr
* Pointer becomes INVALID after: push_back(), emplace_back(), resize() (if reallocation happens)

```cpp
int* p = vec.data();
```
---

##  LIST 

A **list** is a **doubly linked list** provided by the STL that stores elements in **non-contiguous memory** and allows **fast insertion and deletion** at any position.
* std::list    :  	Doubly linked list
* std::forward_list     : 	Singly linked list

## **Key Points**

*  No random access
*  Dynamic size
*  Fast insertion & deletion
*  Elements NOT stored contiguously
*  Bidirectional traversal

**Example**

```cpp
list<int> l;
```

###### header file 
```cpp
#include <list>
```

---

## **List Functions (STL)**

- [capacity and size](#capacity-and-size)
- [modifier](#list-Modifier-and-size)
- [Element Access](#List-Element-Access)

---

### capacity and size

---
* `size()` → number of elements
* `empty()` → checks if list is empty
*  No `capacity()`
*  No `reserve()`
*  No `shrink_to_fit()`

---

---

#### Combined Code

```cpp
#include <iostream>
#include <list>
using namespace std;

int main() {
    list<int> l;

    cout << "Is empty? " << l.empty() << endl;

    l.push_back(1);
    l.push_back(2);
    l.push_back(3);

    cout << "List elements: ";
    for (int x : l)
        cout << x << " ";
    cout << endl;

    cout << "Size: " << l.size() << endl;

    return 0;
}
```

---

### list Modifier and size

* `push_back(x)` → insert at end
* `push_front(x)` → insert at beginning
* `pop_back()` → remove last
* `pop_front()` → remove first
* `emplace back / emplace front`
* `insert(pos, x)` → insert x at position
* `erase(pos)` → remove at position
* `remove(x)` → remove all x
* `clear()` → remove all elements
* `assign(n, x)` → fill list
* `swap(l)` → swap lists

---

#### Combined Code 

```cpp
#include <iostream>
#include <list>
using namespace std;

void printList(list<int> l) {
    for (int x : l)
        cout << x << " ";
    cout << endl;
}

int main() {
    list<int> l = {10, 20, 30};
    cout << "Initial list: ";
    printList(l);

    l.push_back(40);
    cout << "After push_back(40): ";
    printList(l);

    l.push_front(5);
    cout << "After push_front(5): ";
    printList(l);

    l.pop_back();
    cout << "After pop_back(): ";
    printList(l);

    l.pop_front();
    cout << "After pop_front(): ";
    printList(l);

    l.emplace_back(4);
    cout << "After emplace_back(4): ";
    printList(l);

    l.emplace_front(0);
    cout << "After emplace_front(0): ";
    printList(l);

    auto it = l.begin();
    l.insert(it, 15);
    cout << "After insert(15 at begin): ";
    printList(l);

    l.erase(l.begin());
    cout << "After erase(begin): ";
    printList(l);

    l.assign(3, 7);
    cout << "After assign(3,7): ";
    printList(l);

    list<int> l2 = {1, 2, 3};
    l.swap(l2);
    cout << "After swap with {1,2,3}: ";
    printList(l);

    return 0;
}
```

---

#### push_back / push_front

👉 Adds element at end / beginning

* Size ↑

```cpp
l.push_back(10);
l.push_front(5);
```

---

#### pop_back / pop_front

👉 Removes element from end / beginning

* Size ↓

```cpp
l.pop_back();
l.pop_front();
```

---

#### insert

👉 Inserts at given iterator position

* O(1) if iterator known

```cpp
l.insert(it, 20);
```

---

### erase

👉 Removes element at iterator

```cpp
l.erase(it);
```

---

#### remove

👉 Removes **all occurrences** of value

```cpp
l.remove(10);
```

---

#### clear

👉 Removes all elements

* Size = 0

```cpp
l.clear();
```

---

#### assign

👉 Replaces all elements
* Clears the list, All current nodes are deleted.
* Creates 4 new nodes, Each node stores the value 9.
* Links them as a doubly linked list

```cpp
l.assign(4, 9);
```

---

#### swap

👉 Swaps contents in **O(1)**

```cpp
l1.swap(l2);
```

---
### List Element Access

* `front()` → first element — front
* `back()` → last element — back
* `begin()` → iterator to first element — begin
* `end()` → iterator past the last element — end

⚠️ Important Difference from Vector
* No [] → linked lists do not support indexing.
* No at() → lists have no random access.
* No data() → elements are not stored contiguously in memory.

---

* **front / back**

```cpp
l.front();  // first element
l.back();   // last element
```




#### combined code

```cpp
#include <iostream>
#include <list>
using namespace std;

int main() {
    list<int> l = {10, 20, 30, 40};

    // Access using iterator (since no indexing)
    auto it = l.begin();
    advance(it, 1);   // move iterator to index 1
    cout << "Element at position 1: " << *it << endl;

    // front()
    cout << "front(): " << l.front() << endl;

    // back()
    cout << "back(): " << l.back() << endl;

    // Access first element using begin()
    cout << "begin(): " << *l.begin() << endl;

    return 0;
}
```



---



# STACK 

**Stack — Definition**

A **stack** is a **container adaptor** provided by STL that follows **LIFO**
(**Last In, First Out**) principle.

**Key points**

* LIFO order
* Insertion and deletion from **top only**
* No random access
* No iterators
* Built on another container (default: **deque**)
*  No iterators, No random access, Cannot access middle elements
* 👉 Only `top()` is accessible
* stack is NOT a container.
It is a container adaptor.
*👉 It uses another container internally to store elements.
```cpp
stack<int> st;          // uses deque by default
stack<int, vector<int>> st2;   // uses vector
```
* **Use Cases**  Function calls, Undo / Redo, Expression evaluation, Backtracking, DFS

**Example**
```cpp
stack<int> st;
```

---

##### Header File

```cpp
#include <stack>
```

---

### Stack Functions 

* `push(x)` → insert element
* `emplace(x)` → construct element
* `pop()` → remove top element
* `top()` → access top element
* `size()` → number of elements
* `empty()` → check if stack is empty
* `swap(st)` → swap stacks

---

### Stack Working (LIFO)

```
push(10)
push(20)
push(30)

TOP → 30
       20
       10
```

`pop()` removes **30**

---

### Combined Code

```cpp
#include <iostream>
#include <stack>
using namespace std;

int main() {
    stack<int> st;

    cout << "Is empty? " << st.empty() << endl;

    st.push(10);
    st.push(20);
    st.push(30);

    cout << "Top: " << st.top() << endl;
    cout << "Size: " << st.size() << endl;

    st.pop();

    cout << "Top after pop: " << st.top() << endl;

    return 0;
}
```


---

#### push()

👉 Inserts element at top

* **O(1)**

```cpp
st.push(10);
```

---

#### emplace()

👉 Constructs element directly at top

* Faster for objects
* **O(1)**

```cpp
st.emplace(20);
```

---

#### pop()

👉 Removes top element

* **O(1)**
*  Does NOT return value

```cpp
st.pop();
```

---

#### top()

👉 Access top element

* **O(1)**
*  Stack must not be empty

```cpp
st.top();
```

---

#### size()

👉 Returns number of elements

```cpp
st.size();
```

---

#### empty()

👉 Checks if stack is empty

* Returns `1` (true) or `0` (false)

```cpp
st.empty();
```

---

#### swap()

👉 Exchanges contents of two stacks

* **O(1)**

```cpp
st1.swap(st2);
```

---

# QUEUE 

**Queue — Definition**

A **queue** is a **container adaptor** provided by STL that follows **FIFO**
(**First In, First Out**) principle.

**Key points**

* FIFO order
* Insertion at **rear**
* Deletion from **front**
* No random access
* No iterators
* Built on another container (default: **deque**)
* No iterators, No random access, Cannot access middle elements
👉 Only `front()` and `back()` allowed
* Underlying Container
```cpp
queue<int> q;               // uses deque by default
queue<int, list<int>> q2;   // also possible
```
**Use Cases** Task scheduling, Breadth First Search (BFS), Producer–Consumer problem, Printing queues

---

**Example**

```cpp
queue<int> q;
```

---

##### Header File

```cpp
#include <queue>
```

### queue Working (LIFO)

```
push(10)
push(20)
push(30)

front → 10
        20
back  → 30
```

---


##### modifiers and size
---
* `push(x)` → insert element
* `emplace(x)` → construct element
* `pop()` → remove front element
* `front()` → access front element
* `back()` → access last element
* `size()` → number of elements
* `empty()` → check if empty
* `swap(q)` → swap queues

---

#### Combined Code

```cpp
#include <iostream>
#include <queue>
using namespace std;

int main() {
    queue<int> q;

    cout << "Is empty? " << q.empty() << endl;

    q.push(10);
    q.push(20);
    q.push(30);

    cout << "Front: " << q.front() << endl;
    cout << "Back: " << q.back() << endl;
    cout << "Size: " << q.size() << endl;

    q.pop();

    cout << "Front after pop: " << q.front() << endl;

    return 0;
}
```


---

#### push()

👉 Inserts element at **rear**

* **O(1)**

```cpp
q.push(10);
```

---

#### emplace()

👉 Constructs element directly at rear

* Faster for objects
* **O(1)**

```cpp
q.emplace(20);
```

---

#### pop()

👉 Removes **front** element

* **O(1)**
* Does NOT return value

```cpp
q.pop();
```

---

#### front()

👉 Access front element

* **O(1)**
* Queue must not be empty

```cpp
q.front();
```

---

#### back()

👉 Access last element

* **O(1)**

```cpp
q.back();
```

---

#### size()

👉 Returns number of elements

```cpp
q.size();
```

---

#### empty()

👉 Checks if queue is empty

```cpp
q.empty();
```

---

#### swap()

👉 Exchanges contents of two queues

* **O(1)**

```cpp
q1.swap(q2);
```

---


##### deque
---

# DEQUE 

**Deque (Double Ended Queue) — Definition**

A **deque** is a **dynamic container** provided by STL that allows **fast insertion and deletion at both front and back**.

**Key points**

* Fast random access — **O(1)**
* Dynamic size
* Insertion/removal at **both ends is O(1)**
* Elements stored in **multiple contiguous blocks** (not single block like vector)

**Example**

```cpp
deque<int> dq;
```

---
* [capacity and size](#capacity-and-size)
* [modifier](#modifier)
* [Element Access](#Element-Access)
---

### capacity and size

---

* `size()` → number of elements
* `empty()` → checks if deque is empty
* ❌ `capacity()` → **NOT available**
* ❌ `reserve()` → **NOT available**
* ❌ `shrink_to_fit()` → **NOT available**

---

#### Deque Growth 

* Deque does **NOT** have capacity like vector
* It grows by allocating **new blocks**
* No full reallocation of all elements

👉 This is why insertion at front is efficient

---

#### Combined Code

```cpp
#include <iostream>
#include <deque>
using namespace std;

int main() {
    deque<int> dq;

    cout << "Is empty? " << dq.empty() << endl;

    dq.push_back(1);
    dq.push_back(2);
    dq.push_back(3);

    cout << "Size: " << dq.size() << endl;

    return 0;
}
```

---

#### size()

```cpp
dq.size();
```

---

#### empty()

```cpp
dq.empty();
```

---

#### Modifier

* `push_back(x)` → insert at end
* `push_front(x)` → insert at front
* `pop_back()` → remove last element
* `pop_front()` → remove first element
* `emplace_back()` → construct at end
* `emplace_front()` → construct at front
* `insert(pos, x)` → insert at position
* `erase(pos)` → remove element
* `clear()` → remove all elements
* `assign(n, x)` → fill deque
* `swap(dq)` → swap deques

---

#### Combined Code

```cpp
#include <iostream>
#include <deque>
using namespace std;

int main() {
    deque<int> dq;

    dq.push_back(10);
    dq.push_front(5);

    dq.emplace_back(20);
    dq.emplace_front(1);

    cout << "Deque elements: ";
    for (int x : dq) cout << x << " ";
    cout << endl;

    dq.pop_back();
    dq.pop_front();

    cout << "After pop: ";
    for (int x : dq) cout << x << " ";
    cout << endl;

    return 0;
}
```

---

#### push_back / push_front

👉 Insert at end / front

* **O(1)**

```cpp
dq.push_back(10);
dq.push_front(5);
```

---

#### emplace_back / emplace_front

👉 Constructs element directly

* Faster for objects
* **O(1)**

```cpp
dq.emplace_back(20);
dq.emplace_front(1);
```

---

#### pop_back / pop_front

👉 Removes element from end / front

* **O(1)**

```cpp
dq.pop_back();
dq.pop_front();
```

---

#### insert

👉 Inserts at given position

* **O(n)** (elements shift)

```cpp
dq.insert(dq.begin() + 1, 100);
```

---

#### erase

👉 Removes element

* **O(n)**

```cpp
dq.erase(dq.begin() + 2);
```

---

#### clear

👉 Removes all elements

* Size = 0

```cpp
dq.clear();
```

---

#### assign

👉 Replaces all elements

```cpp
dq.assign(3, 7); // [7 7 7]
```

---

#### swap

👉 Exchanges contents of two deques

* **O(1)**

```cpp
dq1.swap(dq2);
```

---

### Element Access

* `at(i)` → bounds-checked
* `operator[]` → no check
* `front()` → first element
* `back()` → last element

---

#### Combined Code

```cpp
#include <iostream>
#include <deque>
using namespace std;

int main() {
    deque<int> dq = {10, 20, 30, 40};

    cout << dq.at(1) << endl;
    cout << dq[2] << endl;
    cout << dq.front() << endl;
    cout << dq.back() << endl;

    return 0;
}
```

---

#### at()

* Safe
* Throws exception if invalid

```cpp
dq.at(2);
```

---

#### operator[]

* Fast
* Unsafe

```cpp
dq[2];
```
---



##### priority_queue
---

# PRIORITY QUEUE 

**Priority Queue — Definition**

A **priority_queue** is a **container adaptor** provided by STL where **elements are processed based on priority**, not insertion order.

👉 By default, the **largest element has the highest priority**.

**Key points**

* Based on **Heap** data structure
* Default: **Max Heap**
* No iterators
* No random access
* Only **top element** is accessible
* No iterator, No random access, Cannot traverse elements 👉 Only `top()` is accessible
* Underlying Container
```cpp
priority_queue<int> pq;              // uses vector by default
priority_queue<int, deque<int>> pq2; // valid but uncommon
```
* **Use Cases** CPU scheduling, Dijkstra algorithm, Heap sort, Task scheduling, Event simulation

---

##### Header File

```cpp
#include <queue>
```

---

### Priority Queue Types

#### 1️⃣ Max Heap (Default)

```cpp
priority_queue<int> pq;
```

Top element = **largest**

---

#### 2️⃣ Min Heap

```cpp
priority_queue<int, vector<int>, greater<int>> pq;
```

Top element = **smallest**

---

### Priority Queue Functions (STL)

* `push(x)` → insert element
* `emplace(x)` → construct element
* `pop()` → remove highest priority element
* `top()` → access highest priority element
* `size()` → number of elements
* `empty()` → check if empty
* `swap(pq)` → swap priority queues

---

#### Working (Max Heap)

```
push(10)
push(40)
push(20)
push(30)

TOP → 40
```

`pop()` removes **40**

---

#### Combined Code (Max Heap)

```cpp
#include <iostream>
#include <queue>
using namespace std;

int main() {
    priority_queue<int> pq;

    pq.push(10);
    pq.push(40);
    pq.push(20);
    pq.push(30);

    cout << "Top: " << pq.top() << endl;
    cout << "Size: " << pq.size() << endl;

    pq.pop();

    cout << "Top after pop: " << pq.top() << endl;

    return 0;
}
```

---

#### Combined Code (Min Heap)

```cpp
#include <iostream>
#include <queue>
#include <vector>
using namespace std;

int main() {
    priority_queue<int, vector<int>, greater<int>> pq;

    pq.push(10);
    pq.push(40);
    pq.push(20);
    pq.push(30);

    cout << "Top (Min): " << pq.top() << endl;

    return 0;
}
```

---
---

#### push()

👉 Inserts element

* **O(log n)**

```cpp
pq.push(10);
```

---

#### emplace()

👉 Constructs element directly

* Faster for objects
* **O(log n)**

```cpp
pq.emplace(25);
```

---

#### pop()

👉 Removes highest priority element

* **O(log n)**
* Does NOT return value

```cpp
pq.pop();
```

---

#### top()

👉 Returns highest priority element

* **O(1)**
* Cannot modify element

```cpp
pq.top();
```

---

#### size()

👉 Returns number of elements

```cpp
pq.size();
```

---

#### empty()

👉 Checks if empty

```cpp
pq.empty();
```

---

#### swap()

👉 Exchanges contents of two priority queues

* **O(1)**

```cpp
pq1.swap(pq2);
```

---


###### map
---

# MAP 

* Stores **key–value pairs**
* **Keys are unique**
* Automatically **sorted by key**
* Implemented using **Red-Black Tree**

```cpp
map<int, string> mp;
```

---

#### Key Properties
* Keys are **unique**
* Stored in **sorted order**
* **Fast search, insert, delete → O(log n)**
* Allows **iteration in sorted order**
* No random indexing like array/vector

---

#### insert()

```cpp
mp.insert({1, "one"});
```

#### emplace()

```cpp
mp.emplace(2, "two");
```

#### operator[]

👉 Inserts key if not present

```cpp
mp[3] = "three";
```

⚠ If key doesn’t exist → default value is created

---

#### at()

👉 Access value (safe)
* Throws exception if key not present

```cpp
mp.at(1);
```
---

#### find()

👉 Returns iterator
* `end()` if key not found

```cpp
auto it = mp.find(2);
```
---

#### erase()

```cpp
mp.erase(2);          // by key
mp.erase(mp.begin()); // by iterator
```

---

#### size()

```cpp
mp.size();
```

---

#### empty()

```cpp
mp.empty();
```

---

#### clear()

```cpp
mp.clear();
```

---

#### count()

👉 Check key exists or not

```cpp
mp.count(2); // 0 or 1
```
---

###### unordered map
---
# UNORDERED_MAP 

**Unordered Map — Definition**

An **unordered_map** is an **associative container** that stores elements in **key–value pairs**, where **keys are unique**, but **elements are NOT stored in sorted order**.

**Key points**

* Stores **(key, value)** pairs
* **Keys are unique**
* No ordering
* Very fast lookup — **O(1) average**
* Implemented using **Hash Table**
* **Use Cases**
* Frequency counting, Fast lookup tables, Caching, Competitive programming
* No ordering, No `lower_bound()` / `upper_bound()`, Iteration order unpredictable

---

**Example**

```cpp
unordered_map<int, string> ump;
```

---

##### Header File

```cpp
#include <unordered_map>
```

---

#### Unordered Map Structure

```
Hash Table
Index → (Key, Value)

0 → (5, "E")
1 → (1, "A")
2 → (9, "I")
```

👉 Order is **unpredictable**

---

### Unordered Map Functions (STL)

#### Insertion / Update

* `insert({k, v})`
* `ump[k] = v`
* `emplace(k, v)`

#### Access

* `at(k)`
* `operator[]`

#### Remove

* `erase(k)`
* `clear()`

#### Search

* `find(k)`
* `count(k)`

#### Size

* `size()`
* `empty()`

#### Bucket / Hash Info

* `bucket_count()`
* `load_factor()`
* `rehash(n)`

---

### Combined Code

```cpp
#include <iostream>
#include <unordered_map>
using namespace std;

int main() {
    unordered_map<int, string> ump;

    ump[1] = "A";
    ump[2] = "B";
    ump[3] = "C";

    ump.insert({4, "D"});
    ump.emplace(5, "E");

    cout << "Unordered Map elements:\n";
    for (auto it : ump)
        cout << it.first << " -> " << it.second << endl;

    return 0;
}
```

---

### Insertion Methods

---

#### operator[]

👉 Inserts or updates value

* Creates key if missing
* **O(1) average**

```cpp
ump[2] = "B";
```

---

#### insert()

👉 Inserts key–value pair

* Does NOT update existing key

```cpp
ump.insert({3, "C"});
```

---

#### emplace()

👉 Constructs key–value directly

* Faster

```cpp
ump.emplace(4, "D");
```

---

### Access Methods

---

#### at()

* Safe
* Throws exception if key missing

```cpp
ump.at(2);
```

---

#### operator[]

* Easy
* Creates key if missing

```cpp
ump[2];
```

---

### Remove Elements

---

#### erase()

```cpp
ump.erase(3);
```

---

#### clear()

```cpp
ump.clear();
```

---

### Search Operations

---

#### find()

👉 Returns iterator

* If not found → `ump.end()`

```cpp
auto it = ump.find(2);
```

---

#### count()

👉 Returns `1` if key exists, else `0`

```cpp
ump.count(3);
```

---

### Bucket Concepts 

---

#### bucket_count()

👉 Number of buckets

```cpp
ump.bucket_count();
```

---

#### load_factor()

👉 Average elements per bucket

```cpp
ump.load_factor();
```

---

#### rehash(n)

👉 Increases number of buckets

```cpp
ump.rehash(20);
```

---

# SET 

**Set — Definition**

A **set** is an **associative container** that stores **unique elements** in **sorted order**.

**Key points**

* Stores **only keys** (no value)
* **All elements are unique**
* Automatically **sorted**
* Fast search, insert, delete — **O(log n)**
* Implemented using **Red-Black Tree**

**Example**

```cpp
set<int> s;
```

---

##### Header File

```cpp
#include <set>
```

---

### Set Structure

```
Elements (sorted)
10 20 30 40
```

Duplicates are **not allowed**

---

### Set Functions (STL)

### Insertion

* `insert(x)`
* `emplace(x)`

### Remove

* `erase(x)`
* `clear()`

### Search

* `find(x)`
* `count(x)`

### Size

* `size()`
* `empty()`

### Range Queries

* `lower_bound(x)`
* `upper_bound(x)`

### Others

* `swap(s)`

---

## Combined Code

```cpp
#include <iostream>
#include <set>
using namespace std;

int main() {
    set<int> s;

    s.insert(10);
    s.insert(20);
    s.insert(30);
    s.insert(20); // ignored

    s.emplace(40);

    cout << "Set elements:\n";
    for (int x : s)
        cout << x << " ";

    return 0;
}
```

---

## Insertion Methods

---

#### insert()

👉 Inserts element

* Duplicate ignored
* **O(log n)**

```cpp
s.insert(10);
```

---

#### emplace()

👉 Constructs element directly

* Faster
* **O(log n)**

```cpp
s.emplace(20);
```

---

## Remove Elements

---

#### erase()

```cpp
s.erase(20);
```

---

#### clear()

```cpp
s.clear();
```

---

### Search Operations

---

#### find()

👉 Returns iterator

* If not found → `s.end()`

```cpp
auto it = s.find(10);
```

---

#### count()

👉 Returns `1` if exists, else `0`

```cpp
s.count(10);
```

---

### Range Queries (IMPORTANT)

---

#### lower_bound(x)

👉 First element **≥ x**

```cpp
s.lower_bound(20);
```

---

#### upper_bound(x)

👉 First element **> x**

```cpp
s.upper_bound(20);
```
---



### difference 
---

## STL CONTAINERS & ADAPTORS COMPARISON

| **Feature / Container**  | **Vector**    | **List**                   | **Deque**               | **Stack**             | **Queue**             | **Priority Queue**    | **Map**          | **Unordered Map**     | **Set**              | **Unordered Set**  |
| ------------------------ | ------------- | -------------------------- | ----------------------- | --------------------- | --------------------- | --------------------- | ---------------- | --------------------- | -------------------- | ------------------ |
| **Type**                 | Container     | Container                  | Container               | Adaptor               | Adaptor               | Adaptor               | Associative      | Associative           | Associative          | Associative        |
| **Underlying Structure** | Dynamic array | Doubly linked list         | Segmented array         | Deque*                | Deque*                | Vector*               | Balanced BST     | Hash table            | Balanced BST         | Hash table         |
| **Memory**               | Contiguous    | Non-contiguous             | Multiple blocks         | Depends on underlying | Depends on underlying | Depends on underlying | Non-contiguous   | Non-contiguous        | Non-contiguous       | Non-contiguous     |
| **Random Access `[]`**   | ✔ O(1)        | ❌                          | ✔ O(1)                  | ❌                     | ❌                     | ❌                     | ✔† O(log n)      | ✔† O(1) avg           | ❌                    | ❌                  |
| **`at()`**               | ✔             | ❌                          | ✔                       | ❌                     | ❌                     | ❌                     | ✔†               | ✔†                    | ❌                    | ❌                  |
| **`front()`**            | ✔             | ✔                          | ✔                       | ❌                     | ✔                     | ❌                     | ❌                | ❌                     | ❌                    | ❌                  |
| **`back()`**             | ✔             | ✔                          | ✔                       | ❌                     | ✔                     | ❌                     | ❌                | ❌                     | ❌                    | ❌                  |
| **`top()`**              | ❌             | ❌                          | ❌                       | ✔                     | ❌                     | ✔                     | ❌                | ❌                     | ❌                    | ❌                  |
| **`push_back()`**        | ✔             | ✔                          | ✔                       | ❌                     | ❌                     | ❌                     | ❌                | ❌                     | ❌                    | ❌                  |
| **`push_front()`**       | ❌             | ✔                          | ✔                       | ❌                     | ❌                     | ❌                     | ❌                | ❌                     | ❌                    | ❌                  |
| **`pop_back()`**         | ✔             | ✔                          | ✔                       | ❌                     | ❌                     | ❌                     | ❌                | ❌                     | ❌                    | ❌                  |
| **`pop_front()`**        | ❌             | ✔                          | ✔                       | ❌                     | ✔                     | ❌                     | ❌                | ❌                     | ❌                    | ❌                  |
| **`push()`**             | ❌             | ❌                          | ❌                       | ✔                     | ✔                     | ✔                     | ❌                | ❌                     | ❌                    | ❌                  |
| **`pop()`**              | ❌             | ❌                          | ❌                       | ✔                     | ✔                     | ✔                     | ❌                | ❌                     | ❌                    | ❌                  |
| **`insert()`**           | ✔             | ✔                          | ✔                       | ❌                     | ❌                     | ❌                     | ✔                | ✔                     | ✔                    | ✔                  |
| **`erase()`**            | ✔             | ✔                          | ✔                       | ❌                     | ❌                     | ❌                     | ✔                | ✔                     | ✔                    | ✔                  |
| **`clear()`**            | ✔             | ✔                          | ✔                       | ✔                     | ✔                     | ✔                     | ✔                | ✔                     | ✔                    | ✔                  |
| **`swap()`**             | ✔             | ✔                          | ✔                       | ✔                     | ✔                     | ✔                     | ✔                | ✔                     | ✔                    | ✔                  |
| **`emplace()`**          | ✔             | ✔                          | ✔                       | ✔                     | ✔                     | ✔                     | ✔                | ✔                     | ✔                    | ✔                  |
| **`emplace_back()`**     | ✔             | ✔                          | ✔                       | ❌                     | ❌                     | ❌                     | ❌                | ❌                     | ❌                    | ❌                  |
| **`emplace_front()`**    | ❌             | ✔                          | ✔                       | ❌                     | ❌                     | ❌                     | ❌                | ❌                     | ❌                    | ❌                  |
| **Iterators**            | ✔             | ✔                          | ✔                       | ❌                     | ❌                     | ❌                     | ✔                | ✔                     | ✔                    | ✔                  |
| **`size()`**             | ✔             | ✔                          | ✔                       | ✔                     | ✔                     | ✔                     | ✔                | ✔                     | ✔                    | ✔                  |
| **`empty()`**            | ✔             | ✔                          | ✔                       | ✔                     | ✔                     | ✔                     | ✔                | ✔                     | ✔                    | ✔                  |
| **`capacity()`**         | ✔             | ❌                          | ❌                       | ❌                     | ❌                     | ❌                     | ❌                | ❌                     | ❌                    | ❌                  |
| **Sorted Automatically** | ❌             | ❌                          | ❌                       | ❌                     | ❌                     | ❌                     | ✔ keys           | ❌                     | ✔                    | ❌                  |
| **Unique Elements**      | ❌             | ❌                          | ❌                       | ❌                     | ❌                     | ❌                     | ✔ keys           | ✔ keys                | ✔                    | ✔                  |
| **Duplicates Allowed**   | ✔             | ✔                          | ✔                       | ✔                     | ✔                     | ✔                     | ✔ values         | ✔ values              | ❌                    | ❌                  |
| **Average Search**       | O(n)          | O(n)                       | O(n)                    | —                     | —                     | O(n)                  | O(log n)         | O(1)                  | O(log n)             | O(1)               |
| **Worst Search**         | O(n)          | O(n)                       | O(n)                    | —                     | —                     | O(n)                  | O(log n)         | O(n)                  | O(log n)             | O(n)               |
| **Typical Use**          | Dynamic array | Frequent insertion/erasure | Front + back operations | LIFO                  | FIFO                  | Priority-based access | Sorted key-value | Fast key-value lookup | Sorted unique values | Fast unique lookup |

### Important notes

* `*` **Stack, Queue and Priority Queue** are **container adaptors**. Their default underlying containers are `deque`, `deque`, and `vector` respectively.
* `†` For `map`/`unordered_map`, `operator[]` means **key lookup**, not positional random access. It does **not** mean `m[3]` accesses the 4th element.
* `list` insertion/erasure is **O(1) when you already have an iterator to the position**; finding that position can take O(n).
* `unordered_map` and `unordered_set` are **O(1) average, O(n) worst case** for lookup.
* `priority_queue::top()` is **O(1)**, while `push()` and `pop()` are **O(log n)**.
* `set` and `unordered_set` contain unique **elements**; `map` and `unordered_map` contain unique **keys**, but duplicate values are allowed.

These terms describe **how the STL data structure is designed and used**.

### 1. 📦 Container

A **container directly stores and manages a collection of elements**.

Examples:

```text
Vector
List
Deque
```

They directly hold elements:

```cpp
vector<int> v = {10, 20, 30};
```

You can generally insert, delete, iterate, and access their elements directly.

**Think:**

> Container = **I store the elements myself.**

### 2. 🧩 Container Adaptor

An **adaptor does not work like a general-purpose container**. It provides a **restricted interface** on top of another container.

Examples:

```text
Stack
Queue
Priority Queue
```

For example:

```cpp
stack<int> st;
```

You cannot do:

```cpp
st[2];        // ❌
st.begin();   // ❌
```

because a stack intentionally gives you only the operations needed for **LIFO**:

```cpp
st.push(10);
st.pop();
st.top();
```

Internally, a `stack` uses another container (by default, `deque`).

**Think:**

> Adaptor = **Take an existing container and restrict it to create a specific behavior.**

Examples:

```text
deque → Stack        → LIFO
deque → Queue        → FIFO
vector → Priority Queue → highest priority first
```

### 3. 🔗 Associative Container

Associative containers organize elements based on **keys/order or hashing**, rather than simply storing elements by position.

Examples:

```text
map
unordered_map
set
unordered_set
```

#### `map`

Stores:

```text
key → value
```

```cpp
map<int, string> m;

m[1] = "Apple";
m[2] = "Banana";
```

You access using the **key**, not a position.

```cpp
m[2]    // "Banana"
```

#### `set`

Stores **unique values**:

```cpp
set<int> s = {30, 10, 20};
```

It automatically sorts them:

```text
10 20 30
```

#### `unordered_map`

Stores key-value pairs but uses hashing:

```text
key → value
```

No sorted order, but average lookup is **O(1)**.

#### `unordered_set`

Stores unique elements using hashing:

```text
10
20
30
```

No guaranteed sorted order.

### 🧠 Simple way to remember

| Type            | Meaning                                                       | Examples                                       |
| --------------- | ------------------------------------------------------------- | ---------------------------------------------- |
| **Container**   | Directly stores elements                                      | `vector`, `list`, `deque`                      |
| **Adaptor**     | Gives a restricted interface/behavior using another container | `stack`, `queue`, `priority_queue`             |
| **Associative** | Organizes/searches using keys, ordering, or hashing           | `map`, `set`, `unordered_map`, `unordered_set` |

### The easiest mental picture

```text
                 STL
                  │
        ┌─────────┼──────────┐
        ↓         ↓          ↓
    Containers  Adaptors  Associative
        │         │          │
   vector       stack       map
   list         queue       set
   deque        priority    unordered_map
                queue       unordered_set
```

**One important point:** "Associative" doesn't mean all four work the same way. `map`/`set` are **ordered associative containers**, while `unordered_map`/`unordered_set` are **unordered associative containers based on hashing**.

---

# ITERATORS 

### What is an Iterator?

👉 An **object like a pointer** used to **traverse STL containers**

```cpp
vector<int> v;
auto it = v.begin();
```

### Types of Iterators

### begin() / end()

👉 Points to **first element** / **one past last**

```cpp
v.begin();
v.end();
```

Traversal:

```cpp
for(auto it = v.begin(); it != v.end(); it++)
    cout << *it << " ";
```

### rbegin() / rend()

👉 Reverse traversal

```cpp
v.rbegin();
v.rend();
```

### cbegin() / cend()

👉 **Read-only iterator**
❌ Cannot modify elements

```cpp
v.cbegin();
v.cend();
```

### Iterator Support by Containers

| Container      | Iterators |
| -------------- | --------- |
| vector         | ✔         |
| deque          | ✔         |
| list           | ✔         |
| map            | ✔         |
| set            | ✔         |
| unordered_map  | ✔         |
| stack          | ❌         |
| queue          | ❌         |
| priority_queue | ❌         |

### Iterator vs Pointer

| Iterator            | Pointer         |
| ------------------- | --------------- |
| STL specific        | Memory address  |
| Safer               | Unsafe          |
| Works on containers | Works on arrays |

---

#  ALGORITHM FUNCTIONS 

👉 Found in **`<algorithm>`**
👉 Work using **iterators**

---

## 🔹 Common Algorithms

### sort()

👉 Sorts elements

```cpp
sort(v.begin(), v.end());
```

✔ Random access required
❌ Not for list

---

### reverse()

👉 Reverses range

```cpp
reverse(v.begin(), v.end());
```

---

### find()

👉 Finds element

```cpp
auto it = find(v.begin(), v.end(), 5);
```

✔ Returns iterator
❌ Returns `end()` if not found

---

### count()

👉 Counts occurrences

```cpp
count(v.begin(), v.end(), 3);
```

---

### max_element() / min_element()

```cpp
*max_element(v.begin(), v.end());
*min_element(v.begin(), v.end());
```

---

### binary_search()

👉 Works on **sorted data only**

```cpp
binary_search(v.begin(), v.end(), 10);
```

---

### accumulate()

👉 Sum of elements (`<numeric>`)

```cpp
accumulate(v.begin(), v.end(), 0);
```

---

### all_of() / any_of() / none_of()

```cpp
all_of(v.begin(), v.end(), condition);
any_of(v.begin(), v.end(), condition);
none_of(v.begin(), v.end(), condition);
```

---

## 🔹 Algorithms vs Container Functions

| Algorithms         | Container Functions |
| ------------------ | ------------------- |
| Work via iterators | Work on container   |
| Generic            | Specific            |
| `<algorithm>`      | Member functions    |

---

## 🔹 Key Rules (VERY IMPORTANT)

✔ Algorithms **do not know containers**
✔ They only work with **iterator ranges**
✔ Containers decide **iterator type**

---

### ⭐ One-Line Summary

**Iterator** → Pointer-like object to access container
**Algorithm** → Function that works on iterator range

---
---

# FUNCTION

## 🔹 Functors — Definition

A **Functor (Function Object)** is an **object that behaves like a function**.
It is a **class or struct that overloads the `operator()`**.

👉 Used to **customize STL algorithms**

---

## Why Functors are needed?

* More powerful than normal functions
* Can store **state (data)**
* Faster than function pointers
* Used in **algorithms and containers**

---

## Syntax

```cpp
struct Functor {
    void operator()(int x) {
        cout << x << endl;
    }
};
```

Usage:

```cpp
Functor f;
f(10);   // behaves like function
```

---

## Types of Functors in STL

1. **Built-in Functors**
2. **User-defined Functors**
3. **Comparison Functors**

---

## 1️⃣ Built-in Functors

| Functor           | Meaning                   |
| ----------------- | ------------------------- |
| `greater<T>`      | descending order          |
| `less<T>`         | ascending order (default) |
| `equal_to<T>`     | equality check            |
| `not_equal_to<T>` | inequality check          |

---

### Example — `greater<int>`

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> v = {4, 1, 3, 2};

    sort(v.begin(), v.end(), greater<int>());

    for (int x : v)
        cout << x << " ";
}
```

📌 Output:

```
4 3 2 1
```

---

## 2️⃣ User-defined Functor

```cpp
#include <iostream>
#include <algorithm>
using namespace std;

struct Multiply {
    int operator()(int a, int b) {
        return a * b;
    }
};

int main() {
    Multiply m;
    cout << m(3, 4);   // 12
}
```

---

## 3️⃣ Comparison Functors (Very Important)

Used in:

* `sort()`
* `set`
* `map`
* `priority_queue`

---

### Example — Custom Sorting

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

struct Desc {
    bool operator()(int a, int b) {
        return a > b;
    }
};

int main() {
    vector<int> v = {2, 5, 1, 4};

    sort(v.begin(), v.end(), Desc());

    for (int x : v)
        cout << x << " ";
}
```

---

## Functors in Containers

### `priority_queue`

```cpp
priority_queue<int, vector<int>, greater<int>> pq;
```

✔ Makes **min heap**

---

### `set` / `map`

```cpp
set<int, greater<int>> s;
map<int, int, greater<int>> mp;
```

✔ Stores elements in **descending order**

---

## Functor vs Function Pointer

| Functor        | Function          |
| -------------- | ----------------- |
| Can store data | Cannot store data |
| Faster         | Slower            |
| Inlined        | Not inlined       |
| Object-based   | Pointer-based     |

---

## When to use Functors?

✔ Custom sorting
✔ Priority queues
✔ Sets / Maps ordering
✔ STL algorithms customization

---

> A functor is an object that acts like a function by overloading the `operator()` and is used to customize STL algorithms and containers.

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

