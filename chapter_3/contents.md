# Chapter 3: Data Structures and Algorithms (DSA)

## Introduction

Data Structures and Algorithms (DSA) form the backbone of computer science and software engineering. They are essential for writing efficient, scalable, and maintainable code. This chapter will cover fundamental and advanced data structures, algorithm design techniques, and their implementation in multiple programming languages.

## Fundamental Data Structures

### 1. Arrays

Arrays are the simplest and most widely used data structures. They store elements of the same type in contiguous memory locations.

#### Implementation in Python:
```python
# Creating an array
arr = [1, 2, 3, 4, 5]

# Accessing elements
print(arr[0])  # Output: 1

# Modifying elements
arr[2] = 10
print(arr)  # Output: [1, 2, 10, 4, 5]
```

#### Time Complexity:
- Access: O(1)
- Search: O(n)
- Insertion: O(n)
- Deletion: O(n)

### 2. Linked Lists

Linked lists consist of nodes, where each node contains data and a reference (or link) to the next node in the sequence.

#### Implementation in C:
```c
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
};

struct Node* createNode(int data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = data;
    newNode->next = NULL;
    return newNode;
}

void printList(struct Node* head) {
    struct Node* temp = head;
    while (temp != NULL) {
        printf("%d -> ", temp->data);
        temp = temp->next;
    }
    printf("NULL\n");
}

int main() {
    struct Node* head = createNode(1);
    head->next = createNode(2);
    head->next->next = createNode(3);

    printList(head);
    return 0;
}
```

#### Time Complexity:
- Access: O(n)
- Search: O(n)
- Insertion: O(1) at the beginning, O(n) at the end
- Deletion: O(1) at the beginning, O(n) at the end

### 3. Stacks

Stacks follow the Last-In-First-Out (LIFO) principle. Elements are added and removed from the same end, called the top.

#### Implementation in Java:
```java
import java.util.Stack;

public class StackExample {
    public static void main(String[] args) {
        Stack<Integer> stack = new Stack<>();

        // Pushing elements
        stack.push(1);
        stack.push(2);
        stack.push(3);

        // Popping elements
        System.out.println(stack.pop());  // Output: 3
        System.out.println(stack.pop());  // Output: 2

        // Peeking at the top element
        System.out.println(stack.peek()); // Output: 1
    }
}
```

#### Time Complexity:
- Push: O(1)
- Pop: O(1)
- Peek: O(1)

### 4. Queues

Queues follow the First-In-First-Out (FIFO) principle. Elements are added at the rear and removed from the front.

#### Implementation in JavaScript:
```javascript
class Queue {
    constructor() {
        this.items = [];
    }

    enqueue(element) {
        this.items.push(element);
    }

    dequeue() {
        if (this.isEmpty()) {
            return "Queue is empty";
        }
        return this.items.shift();
    }

    front() {
        if (this.isEmpty()) {
            return "Queue is empty";
        }
        return this.items[0];
    }

    isEmpty() {
        return this.items.length === 0;
    }
}

// Usage
let queue = new Queue();
queue.enqueue(1);
queue.enqueue(2);
queue.enqueue(3);

console.log(queue.dequeue());  // Output: 1
console.log(queue.front());    // Output: 2
```

#### Time Complexity:
- Enqueue: O(1)
- Dequeue: O(1)
- Front: O(1)

### 5. Hash Tables

Hash tables provide fast insertion, deletion, and lookup operations by using a hash function to map keys to indices.

#### Implementation in Python:
```python
class HashTable:
    def __init__(self, size):
        self.size = size
        self.table = [[] for _ in range(self.size)]

    def hash_function(self, key):
        return hash(key) % self.size

    def insert(self, key, value):
        hash_index = self.hash_function(key)
        for item in self.table[hash_index]:
            if item[0] == key:
                item[1] = value
                return
        self.table[hash_index].append([key, value])

    def get(self, key):
        hash_index = self.hash_function(key)
        for item in self.table[hash_index]:
            if item[0] == key:
                return item[1]
        raise KeyError(key)

# Usage
ht = HashTable(10)
ht.insert("apple", 5)
ht.insert("banana", 7)

print(ht.get("apple"))   # Output: 5
print(ht.get("banana"))  # Output: 7
```

#### Time Complexity (average case):
- Insertion: O(1)
- Deletion: O(1)
- Lookup: O(1)

## Advanced Data Structures

### 1. Trees

Trees are hierarchical data structures consisting of nodes connected by edges. Common types include binary trees, binary search trees, and balanced trees (e.g., AVL trees, Red-Black trees).

#### Binary Search Tree Implementation in C++:
```cpp
#include <iostream>

struct Node {
    int data;
    Node* left;
    Node* right;

    Node(int value) : data(value), left(nullptr), right(nullptr) {}
};

class BinarySearchTree {
private:
    Node* root;

    Node* insert(Node* node, int value) {
        if (node == nullptr) {
            return new Node(value);
        }

        if (value < node->data) {
            node->left = insert(node->left, value);
        } else if (value > node->data) {
            node->right = insert(node->right, value);
        }

        return node;
    }

    void inorder(Node* node) {
        if (node == nullptr) return;

        inorder(node->left);
        std::cout << node->data << " ";
        inorder(node->right);
    }

public:
    BinarySearchTree() : root(nullptr) {}

    void insert(int value) {
        root = insert(root, value);
    }

    void printInorder() {
        inorder(root);
        std::cout << std::endl;
    }
};

int main() {
    BinarySearchTree bst;
    bst.insert(5);
    bst.insert(3);
    bst.insert(7);
    bst.insert(1);
    bst.insert(9);

    bst.printInorder();  // Output: 1 3 5 7 9
    return 0;
}
```

#### Time Complexity (for balanced BST):
- Insertion: O(log n)
- Deletion: O(log n)
- Search: O(log n)

### 2. Graphs

Graphs consist of vertices (or nodes) connected by edges. They can be directed or undirected, weighted or unweighted.

#### Graph Implementation in Python:
```python
class Graph:
    def __init__(self):
        self.graph = {}

    def add_edge(self, u, v):
        if u not in self.graph:
            self.graph[u] = []
        self.graph[u].append(v)

    def bfs(self, start):
        visited = set()
        queue = [start]
        visited.add(start)

        while queue:
            vertex = queue.pop(0)
            print(vertex, end=" ")

            for neighbor in self.graph.get(vertex, []):
                if neighbor not in visited:
                    visited.add(neighbor)
                    queue.append(neighbor)

# Usage
g = Graph()
g.add_edge(0, 1)
g.add_edge(0, 2)
g.add_edge(1, 2)
g.add_edge(2, 0)
g.add_edge(2, 3)
g.add_edge(3, 3)

print("BFS starting from vertex 2:")
g.bfs(2)  # Output: 2 0 3 1
```

#### Time Complexity:
- BFS: O(V + E), where V is the number of vertices and E is the number of edges

### 3. Heaps

Heaps are specialized tree-based data structures that satisfy the heap property. They are commonly used to implement priority queues.

#### Max Heap Implementation in Java:
```java
import java.util.ArrayList;

public class MaxHeap {
    private ArrayList<Integer> heap;

    public MaxHeap() {
        heap = new ArrayList<>();
    }

    private int parent(int i) {
        return (i - 1) / 2;
    }

    private int leftChild(int i) {
        return 2 * i + 1;
    }

    private int rightChild(int i) {
        return 2 * i + 2;
    }

    private void swap(int i, int j) {
        int temp = heap.get(i);
        heap.set(i, heap.get(j));
        heap.set(j, temp);
    }

    public void insert(int key) {
        heap.add(key);
        int i = heap.size() - 1;
        while (i > 0 && heap.get(parent(i)) < heap.get(i)) {
            swap(i, parent(i));
            i = parent(i);
        }
    }

    public int extractMax() {
        if (heap.isEmpty()) {
            throw new IllegalStateException("Heap is empty");
        }

        int max = heap.get(0);
        int lastElement = heap.remove(heap.size() - 1);

        if (!heap.isEmpty()) {
            heap.set(0, lastElement);
            heapify(0);
        }

        return max;
    }

    private void heapify(int i) {
        int largest = i;
        int left = leftChild(i);
        int right = rightChild(i);

        if (left < heap.size() && heap.get(left) > heap.get(largest)) {
            largest = left;
        }

        if (right < heap.size() && heap.get(right) > heap.get(largest)) {
            largest = right;
        }

        if (largest != i) {
            swap(i, largest);
            heapify(largest);
        }
    }

    public static void main(String[] args) {
        MaxHeap maxHeap = new MaxHeap();
        maxHeap.insert(3);
        maxHeap.insert(1);
        maxHeap.insert(4);
        maxHeap.insert(1);
        maxHeap.insert(5);

        System.out.println(maxHeap.extractMax());  // Output: 5
        System.out.println(maxHeap.extractMax());  // Output: 4
    }
}
```

#### Time Complexity:
- Insertion: O(log n)
- Extract Max/Min: O(log n)

## Algorithm Design Techniques

### 1. Divide and Conquer

Divide and Conquer is an algorithm design paradigm that works by recursively breaking down a problem into smaller subproblems until these become simple enough to be solved directly.

#### Example: Merge Sort
```python
def merge_sort(arr):
    if len(arr) <= 1:
        return arr

    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])

    return merge(left, right)

def merge(left, right):
    result = []
    i, j = 0, 0

    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1

    result.extend(left[i:])
    result.extend(right[j:])
    return result

# Usage
arr = [38, 27, 43, 3, 9, 82, 10]
sorted_arr = merge_sort(arr)
print(sorted_arr)  # Output: [3, 9, 10, 27, 38, 43, 82]
```

### 2. Dynamic Programming

Dynamic Programming is a method for solving complex problems by breaking them down into simpler subproblems. It is applicable when subproblems overlap and have optimal substructure.

#### Example: Fibonacci Sequence
```java
public class Fibonacci {
    public static int fibonacci(int n) {
        if (n <= 1) {
            return n;
        }

        int[] dp = new int[n + 1];
        dp[0] = 0;
        dp[1] = 1;

        for (int i = 2; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }

        return dp[n];
    }

    public static void main(String[] args) {
        System.out.println(fibonacci(10));  // Output: 55
    }
}
```

### 3. Greedy Algorithms

Greedy algorithms make locally optimal choices at each step with the hope of finding a global optimum.

#### Example: Coin Change Problem
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> coinChange(vector<int>& coins, int amount) {
    sort(coins.rbegin(), coins.rend());
    vector<int> result;

    for (int coin : coins) {
        while (amount >= coin) {
            result.push_back(coin);
            amount -= coin;
        }
    }

    if (amount == 0) {
        return result;
    } else {
        return vector<int>();  // No solution
    }
}

int main() {
    vector<int> coins = {25, 10, 5, 1};
    int amount = 67;

    vector<int> change = coinChange(coins, amount);

    if (!change.empty()) {
        cout << "Coins used: ";
        for (int coin : change) {
            cout << coin << " ";
        }
        cout << endl;
    } else {
        cout << "No solution found." << endl;
    }

    return 0;
}
```

## Time and Space Complexity Analysis

Understanding time and space complexity is crucial for analyzing and optimizing algorithms. We use Big O notation to describe the upper bound of an algorithm's growth rate.

Common time complexities:
- O(1): Constant time
- O(log n): Logarithmic time
- O(n): Linear time
- O(n log n): Linearithmic time
- O(n^2): Quadratic time
- O(2^n): Exponential time

Space complexity refers to the amount of memory an algorithm uses relative to the input size.

Example analysis:
```python
def linear_search(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i
    return -1

# Time complexity: O(n) - we may need to search through all elements
# Space complexity: O(1) - we only use a constant amount of extra space
```

## Conclusion

This chapter has covered fundamental and advanced data structures, along with key algorithm design techniques. Understanding these concepts is crucial for writing efficient and scalable code. As you progress through your programming journey, continue to practice implementing these data structures and algorithms in various languages to solidify your understanding and improve your problem-solving skills.
