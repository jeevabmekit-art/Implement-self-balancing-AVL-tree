AVL Tree (Self-Balancing Binary Search Tree)
📌 Overview
This project implements an AVL Tree, a self-balancing Binary Search Tree that maintains its height to ensure efficient operations.
The tree automatically balances itself after every insertion using rotations.
🧠 What is an AVL Tree?
An AVL Tree is a BST where the balance factor of every node is between -1 and +1.
⚖️ Balance Factor

Balance Factor = Height(Left Subtree) - Height(Right Subtree)
Value
Status
-1, 0, +1
Balanced ✅
< -1 or > +1
Unbalanced ❌
🔄 Rotations in AVL Tree
1️⃣ Right Rotation (LL Case)

Before Rotation:        After Rotation:

      z                      y
     /                      / \
    y          →           x   z
   /                          /
  x                          T3
2️⃣ Left Rotation (RR Case)

Before Rotation:        After Rotation:

  z                         y
   \                       / \
    y        →            z   x
     \                     \
      x                     T2
3️⃣ Left-Right Rotation (LR Case)

Step 1: Left Rotate
Step 2: Right Rotate
4️⃣ Right-Left Rotation (RL Case)

Step 1: Right Rotate
Step 2: Left Rotate
⚙️ Features
✅ Self-balancing BST
✅ Supports insertion
✅ Automatic rotations
✅ Efficient traversal
🚀 Time Complexity
Operation
Complexity
Search
O(log n)
Insert
O(log n)
Delete
O(log n)
💻 Implementation (Java)
Java
class AVLNode {
    int key, height;
    AVLNode left, right;

    AVLNode(int d) {
        key = d;
        height = 1;
    }
}

public class AVLTree {

    AVLNode root;

    int height(AVLNode N) {
        return (N == null) ? 0 : N.height;
    }

    int max(int a, int b) {
        return (a > b) ? a : b;
    }

    AVLNode rightRotate(AVLNode y) {
        AVLNode x = y.left;
        AVLNode T2 = x.right;

        x.right = y;
        y.left = T2;

        y.height = max(height(y.left), height(y.right)) + 1;
        x.height = max(height(x.left), height(x.right)) + 1;

        return x;
    }

    AVLNode leftRotate(AVLNode x) {
        AVLNode y = x.right;
        AVLNode T2 = y.left;

        y.left = x;
        x.right = T2;

        x.height = max(height(x.left), height(x.right)) + 1;
        y.height = max(height(y.left), height(y.right)) + 1;

        return y;
    }

    int getBalance(AVLNode N) {
        return (N == null) ? 0 : height(N.left) - height(N.right);
    }

    AVLNode insert(AVLNode node, int key) {
        if (node == null)
            return new AVLNode(key);

        if (key < node.key)
            node.left = insert(node.left, key);
        else if (key > node.key)
            node.right = insert(node.right, key);
        else
            return node;

        node.height = 1 + max(height(node.left), height(node.right));

        int balance = getBalance(node);

        // LL
        if (balance > 1 && key < node.left.key)
            return rightRotate(node);

        // RR
        if (balance < -1 && key > node.right.key)
            return leftRotate(node);

        // LR
        if (balance > 1 && key > node.left.key) {
            node.left = leftRotate(node.left);
            return rightRotate(node);
        }

        // RL
        if (balance < -1 && key < node.right.key) {
            node.right = rightRotate(node.right);
            return leftRotate(node);
        }

        return node;
    }

    void preOrder(AVLNode node) {
        if (node != null) {
            System.out.print(node.key + " ");
            preOrder(node.left);
            preOrder(node.right);
        }
    }

    public static void main(String[] args) {
        AVLTree tree = new AVLTree();

        tree.root = tree.insert(tree.root, 10);
        tree.root = tree.insert(tree.root, 20);
        tree.root = tree.insert(tree.root, 30);
        tree.root = tree.insert(tree.root, 40);
        tree.root = tree.insert(tree.root, 50);
        tree.root = tree.insert(tree.root, 25);

        System.out.println("Preorder traversal:");
        tree.preOrder(tree.root);
    }
}
▶️ Usage
🔧 Compile & Run
Bash
javac AVLTree.java
java AVLTree
📌 Sample Output

Preorder traversal:
30 20 10 25 40 50
📂 Project Structure

AVL-Tree/
│── AVLTree.java
│── README.md
📖 Applications
Database indexing
Memory management
Searching systems
Real-time applications
🏁 Conclusion
AVL Tree ensures that the tree remains balanced after every operation, providing fast and reliable performance compared to a normal Binary Search Tree.
