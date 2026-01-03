# STL
### index
- [basic](#basic)
- [containers](#containers)
- [algorithm](#algorithm)
- [iterators](#iterators)
- [function](#function)

### basic
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

## containers
vector, list, deque, set, map, unordered_map, stack, queue, priority_que
- [vector](#vector)
- [list](#list)
- [stack](#stack)
  
### vector 
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
  
##### push and pop
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

return 0;

}
```

##### size and capacity 
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

return 0;

}
```

##### emplace_back 
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

##### [ ] ( )
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

##### front and back 
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

##### vector begin and erase 
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

##### same number in table
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

#####  plus n on begin 

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

##### replacing an element by other

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

##### clear

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

##### loop with begin 
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

### list

##### push and pop 

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

##### pair
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

### stack

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




### queue

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

### Map
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

#### set
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

