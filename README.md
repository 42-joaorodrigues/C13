# C Piscine - C13 (Binary Trees)

![42 Badge](https://img.shields.io/badge/42-C13-brightgreen)
![C Badge](https://img.shields.io/badge/Language-C-blue)
![Status Badge](https://img.shields.io/badge/Status-Completed-success)

## What I Learned

Through this advanced C programming module at 42 School, I developed essential skills in data structures and algorithms:

- **Binary tree fundamentals** - Understanding tree structure, nodes, and hierarchical data organization
- **Tree traversal algorithms** - Implementing prefix (pre-order), infix (in-order), and suffix (post-order) traversals
- **Recursive programming** - Mastering recursive function design for tree operations
- **Dynamic memory management** - Creating and managing tree nodes with proper allocation/deallocation
- **Binary search tree operations** - Implementing insertion and search operations in sorted trees
- **Function pointers** - Using function pointers for flexible tree operations and callbacks
- **Level-order traversal** - Implementing breadth-first search and level-by-level processing
- **Tree metrics** - Calculating tree properties like depth and level count
- **Generic data handling** - Working with void pointers for type-agnostic tree implementations
- **Algorithm complexity** - Understanding time and space complexity of tree operations

This project strengthened my understanding of fundamental computer science concepts and recursive problem-solving techniques essential for advanced programming.

## About the Project

C13 focuses on binary tree implementation and manipulation. It covers the complete lifecycle of binary trees from creation to complex operations, providing a solid foundation in tree-based data structures.

The project implements a generic binary tree using the following structure:

```c
typedef struct s_btree
{
    struct s_btree  *left;
    struct s_btree  *right;
    void           *item;
} t_btree;
```

## Implementation Details

The project consists of 8 exercises, each building upon the previous ones:

### Exercise 00: btree_create_node
**Foundation - Node Creation**
- Allocates and initializes a new tree node
- Sets up the basic building block for all tree operations
- Handles memory allocation with proper error checking

```c
t_btree *btree_create_node(void *item);
```

### Exercise 01: btree_apply_prefix
**Pre-order Traversal**
- Implements depth-first traversal: Root → Left → Right
- Applies a function to each node in prefix order
- Demonstrates recursive tree navigation

```c
void btree_apply_prefix(t_btree *root, void (*applyf)(void *));
```

### Exercise 02: btree_apply_infix
**In-order Traversal**
- Implements depth-first traversal: Left → Root → Right
- Essential for processing binary search trees in sorted order
- Most commonly used traversal for sorted data retrieval

```c
void btree_apply_infix(t_btree *root, void (*applyf)(void *));
```

### Exercise 03: btree_apply_suffix
**Post-order Traversal**
- Implements depth-first traversal: Left → Right → Root
- Useful for operations requiring children processing before parents
- Critical for safe tree deletion and cleanup operations

```c
void btree_apply_suffix(t_btree *root, void (*applyf)(void *));
```

### Exercise 04: btree_insert_data
**Binary Search Tree Insertion**
- Maintains sorted tree property during insertion
- Uses comparison function for flexible data types
- Implements proper BST insertion algorithm

```c
void btree_insert_data(t_btree **root, void *item, int (*cmpf)(void *, void *));
```

### Exercise 05: btree_search_item
**Binary Search Tree Search**
- Efficiently locates elements in sorted trees
- Returns first matching element using infix traversal
- Demonstrates search optimization in tree structures

```c
void *btree_search_item(t_btree *root, void *data_ref, int (*cmpf)(void *, void *));
```

### Exercise 06: btree_level_count
**Tree Depth Calculation**
- Calculates the maximum depth/height of the tree
- Determines the longest path from root to leaf
- Essential metric for tree balance analysis

```c
int btree_level_count(t_btree *root);
```

### Exercise 07: btree_apply_by_level
**Level-order Traversal**
- Implements breadth-first tree traversal
- Processes nodes level by level from top to bottom
- Most complex exercise requiring queue-like behavior

```c
void btree_apply_by_level(t_btree *root, 
    void (*applyf)(void *item, int current_level, int is_first_elem));
```

## Key Algorithms Implemented

### Tree Traversal Methods
- **Pre-order (Prefix)**: Root → Left → Right
- **In-order (Infix)**: Left → Root → Right  
- **Post-order (Suffix)**: Left → Right → Root
- **Level-order**: Breadth-first, level by level

### Binary Search Tree Operations
- **Insertion**: Maintains sorted property
- **Search**: Efficient element location
- **Traversal**: In-order for sorted output

### Tree Analysis
- **Depth calculation**: Finding maximum tree height
- **Level processing**: Operating on nodes by depth level

## Usage Example

```c
#include "ft_btree.h"
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

void print_item(void *item)
{
    printf("%s ", (char *)item);
}

int string_compare(void *a, void *b)
{
    return strcmp((char *)a, (char *)b);
}

int main(void)
{
    t_btree *root = NULL;
    
    // Build a binary search tree
    btree_insert_data(&root, "dog", string_compare);
    btree_insert_data(&root, "cat", string_compare);
    btree_insert_data(&root, "elephant", string_compare);
    btree_insert_data(&root, "ant", string_compare);
    
    // Traverse in different orders
    printf("Prefix:  "); btree_apply_prefix(root, print_item);  printf("\n");
    printf("Infix:   "); btree_apply_infix(root, print_item);   printf("\n");
    printf("Suffix:  "); btree_apply_suffix(root, print_item);  printf("\n");
    
    // Search for an element
    void *found = btree_search_item(root, "cat", string_compare);
    printf("Found: %s\n", found ? (char *)found : "Not found");
    
    // Get tree depth
    printf("Tree depth: %d\n", btree_level_count(root));
    
    return (0);
}
```

## Technical Challenges Overcome

- **Memory management** - Proper allocation and prevention of memory leaks in recursive structures
- **Generic programming** - Using void pointers to create type-agnostic tree operations
- **Recursive algorithms** - Designing clean, efficient recursive functions for tree operations
- **Function pointers** - Implementing flexible callback mechanisms for tree traversal
- **Tree balancing awareness** - Understanding performance implications of tree structure
- **Level-order implementation** - Managing breadth-first traversal without built-in queue structures
- **Edge case handling** - Managing empty trees, single nodes, and malformed data
- **Comparison functions** - Implementing generic comparison mechanisms for different data types

## Project Structure

```
C13/
├── ex00/                    # btree_create_node
│   ├── btree_create_node.c
│   └── ft_btree.h
├── ex01/                    # btree_apply_prefix  
│   ├── btree_apply_prefix.c
│   └── ft_btree.h
├── ex02/                    # btree_apply_infix
│   ├── btree_apply_infix.c
│   └── ft_btree.h
├── ex03/                    # btree_apply_suffix
│   ├── btree_apply_suffix.c
│   └── ft_btree.h
├── ex04/                    # btree_insert_data
│   ├── btree_insert_data.c
│   └── ft_btree.h
├── ex05/                    # btree_search_item
│   ├── btree_search_item.c
│   └── ft_btree.h
├── ex06/                    # btree_level_count
│   ├── btree_level_count.c
│   └── ft_btree.h
├── ex07/                    # btree_apply_by_level
│   ├── btree_apply_by_level.c
│   └── ft_btree.h
└── en.subject.pdf          # Project requirements
```

## Compilation

Each exercise can be compiled individually:

```bash
# Example for exercise 00
cc -Wall -Wextra -Werror btree_create_node.c -o test

# For exercises using previous functions, include all necessary files
cc -Wall -Wextra -Werror ex00/btree_create_node.c ex04/btree_insert_data.c main.c -o test
```

## Algorithm Complexity

| Operation | Time Complexity | Space Complexity |
|-----------|----------------|------------------|
| Node Creation | O(1) | O(1) |
| Tree Traversal | O(n) | O(h) recursive stack |
| BST Insertion | O(h) average, O(n) worst | O(h) recursive stack |
| BST Search | O(h) average, O(n) worst | O(h) recursive stack |
| Level Count | O(n) | O(h) recursive stack |
| Level-order | O(n) | O(w) where w is max width |

*Where n = number of nodes, h = tree height, w = maximum width*

---

*This project was completed as part of the 42 School C Piscine, demonstrating proficiency in advanced data structures, recursive algorithms, and memory management in C.*

---

## License

This project is licensed under the [42 School License](https://42.fr/).
