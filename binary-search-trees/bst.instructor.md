# Instructor BST Solution

```python
class TreeNode:
    def __init__(self, key, val = None):
        if val == None:
            val = key

        self.key = key
        self.value = val
        self.left = None
        self.right = None        


class Tree:
    def __init__(self):
        self.root = None

    def add_helper(self, current_node, new_node):
        if new_node.key  < current_node.key:
            if not current_node.left:
                current_node.left = new_node
                return
            self.add_helper(current_node.left, new_node)
        else:
            if not current_node.right:
                current_node.right = new_node
                return
            self.add_helper(current_node.right, new_node)

    # Time Complexity: O(log n)
    # Space Complexity: O(log n) (recursive, the iterative solution is O(1)).
    def add(self, key, value = None):
        if not self.root:
            self.root = TreeNode(key, value)
        else:
            new_node = TreeNode(key, value)
            self.add_helper(self.root, new_node)

    # Time Complexity: O(log n)
    # Space Complexity: O(1)
    def find(self, key):
        current = self.root

        while current:
            if current.key == key:
                return current.value
            elif key < current.key:
                current = current.left
            else:
                current = current.right

        return None

    def inorder_helper(self, current_node, values):
        if not current_node:
            return values

        self.inorder_helper(current_node.left, values)
        values.append({ 
            "key": current_node.key,
            "value": current_node.value
        })
        self.inorder_helper(current_node.right, values)

        return values

    # Time Complexity: O(n)
    # Space Complexity: O(n)
    def inorder(self):
        values = []
        return self.inorder_helper(self.root, values)

    def preorder_helper(self, current_node, values):
        if not current_node:
            return values

        values.append({ 
            "key": current_node.key,
            "value": current_node.value
        })
        self.preorder_helper(current_node.left, values)        
        self.preorder_helper(current_node.right, values)

        return values

    # Time Complexity: O(n)
    # Space Complexity: O(n)
    def preorder(self):
        values = []
        return self.preorder_helper(self.root, values)

    def postorder_helper(self, current_node, values):
        if not current_node:
            return values

        self.postorder_helper(current_node.left, values)        
        self.postorder_helper(current_node.right, values)
        values.append({ 
            "key": current_node.key,
            "value": current_node.value
        })

        return values

    # Time Complexity: O(n)
    # Space Complexity: O(n)
    def postorder(self):
        values = []
        return self.postorder_helper(self.root, values)

    def height_helper(self, current_node):
        if not current_node:
            return 0

        return max(self.height_helper(current_node.left), self.height_helper(current_node.right)) + 1
    
    # Time Complexity: O(h) or O(n) if the tree is unbalanced and O(log n) if balanced
    # Space Complexity: O(h) or O(n) if the tree is unbalanced and O(log n) if balanced
    def height(self):
        return self.height_helper(self.root)


#   # Optional Method
#   # Time Complexity: O(n)
#   # Space Complexity: O(n)
    def bfs(self):
        values = []
        queue = []
        if self.root:
            queue.append(self.root)



        while len(queue) > 0:
            current_node = queue.pop(0)
            if current_node.left:
                queue.append(current_node.left)
            if current_node.right:
                queue.append(current_node.right)
            
            values.append({
                "key": current_node.key,
                "value": current_node.value,
            })


        return values

        


#   # Useful for printing
    def to_s(self):
        return f"{self.inorder()}"
```