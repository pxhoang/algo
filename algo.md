
# Data structure and algorim

- [Data structure and algorim](#data-structure-and-algorim)
  - [Binary tree](#binary-tree)
    - [Preorder Tree Traversal – Iterative and Recursive](#preorder-tree-traversal--iterative-and-recursive)
    - [Inorder Tree Traversal – Iterative and Recursive](#inorder-tree-traversal--iterative-and-recursive)
    - [Postorder Tree Traversal – Iterative and Recursive](#postorder-tree-traversal--iterative-and-recursive)

## Binary tree

### Preorder Tree Traversal – Iterative and Recursive

- Push root to stack
- Pop a node from the stack and print it
- Push the right child of the popped node into the stack
- Push the left child of the popped node into the stack

### Inorder Tree Traversal – Iterative and Recursive

- Using one stack
- If the current node exists, push it into the stack (defer it) and move to its left child
- Otherwise, if the current node is null, pop an element from the stack, print it,
- And finally set the current node to its right child

### Postorder Tree Traversal – Iterative and Recursive

- Using 2 stacks
- Pop a node from the stack and push the data into the output stack
- Push the left and right child of the popped node into the stack

```cpp
#include <algorithm>
#include <deque>
#include <fstream>
#include <iostream>
#include <limits>
#include <queue>
#include <sstream>
#include <string>
#include <unordered_map>
#include <vector>
using namespace std;
#include <algorithm>
#include <stack>
#include <stdlib.h>

class Node {
public:
  Node *left;
  Node *right;
  int data;

public:
  Node();
  Node(int data);
  void insert(int data);
  void preorder_recursion(Node *root);
  void preorder_iterative(Node *root);
  void inorder_recursion(Node *root);
  void inorder_interative(Node *root);
  void postorder_recursion(Node *root);
  void postorder_interative(Node *root);
};

Node::Node(int data) : data(data) {
  left = nullptr;
  right = nullptr;
}

void Node::insert(int data) {
  Node *newNode = new Node(data);
  std::queue<Node *> queue;
  queue.push(this);

  while (!queue.empty()) {
    auto top = queue.front();
    queue.pop();

    if (top->left == nullptr) {
      top->left = newNode;
      return;
    }

    if (top->right == nullptr) {
      top->right = newNode;
      return;
    }

    if (top->left)
      queue.push(top->left);

    if (top->right)
      queue.push(top->right);
  }
}

void Node::preorder_recursion(Node *node) {
  if (node == nullptr)
    return;

  std::cout << node->data << " ";
  preorder_recursion(node->left);
  preorder_recursion(node->right);
}

void Node::preorder_iterative(Node *node) {
  std::stack<Node *> stack;
  stack.push(this);

  while (!stack.empty()) {
    auto top = stack.top();
    stack.pop();
    std::cout << top->data << " ";

    if (top->right)
      stack.push(top->right);

    if (top->left)
      stack.push(top->left);
  }
  std::cout << std::endl;
}

void Node::inorder_recursion(Node *node) {
  if (node == nullptr)
    return;

  inorder_recursion(node->left);
  std::cout << node->data << " ";
  inorder_recursion(node->right);
}

void Node::inorder_interative(Node *node) {
  std::stack<Node *> stack;
  Node *curr = node;

  while (!stack.empty() || curr != nullptr) {
    if (curr != nullptr) {
      stack.push(curr);
      curr = curr->left;
    } else {
      curr = stack.top();
      stack.pop();
      std::cout << curr->data << " ";
      curr = curr->right;
    }
  }

  std::cout << std::endl;
}

void Node::postorder_recursion(Node *node) {
  if (node == nullptr)
    return;

  postorder_recursion(node->left);
  postorder_recursion(node->right);
  std::cout << node->data << " ";
}

void Node::postorder_interative(Node *node) {
  std::stack<Node *> stack;
  std::stack<int> output;
  stack.push(node);

  while (!stack.empty()) {
    auto top = stack.top();
    stack.pop();
    output.push(top->data);

    if (top->left)
      stack.push(top->left);

    if (top->right)
      stack.push(top->right);
  }

  while (!output.empty()) {
    auto top = output.top();
    output.pop();
    std::cout << top << " ";
  }
  std::cout << std::endl;
}

int main() {
  Node node(1);
  node.insert(2);
  node.insert(3);
  node.insert(4);
  node.insert(5);

  node.preorder_recursion(&node);
  std::cout << std::endl;
  node.preorder_iterative(&node);

  node.inorder_recursion(&node);
  std::cout << std::endl;
  node.inorder_interative(&node);

  node.postorder_recursion(&node);
  std::cout << std::endl;
  node.postorder_interative(&node);

  return 0;
}
```
