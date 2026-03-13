# Data-structure-practical-program-30# AVL Tree Deletion

class Node:
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None
        self.height = 1

def height(n):
    return n.height if n else 0

def getMin(node):
    while node.left:
        node = node.left
    return node

def delete(root, key):
    if not root:
        return root

    if key < root.key:
        root.left = delete(root.left, key)
    elif key > root.key:
        root.right = delete(root.right, key)
    else:
        if not root.left:
            return root.right
        elif not root.right:
            return root.left
        temp = getMin(root.right)
        root.key = temp.key
        root.right = delete(root.right, temp.key)

    return root

def inorder(root):
    if root:
        inorder(root.left)
        print(root.key, end=" ")
        inorder(root.right)

# Example
root = Node(30)
root.left = Node(20)
root.right = Node(40)
root.left.left = Node(10)
root.left.right = Node(25)

print("Before Deletion:")
inorder(root)

root = delete(root, 20)

print("\nAfter Deletion:")
inorder(root)
