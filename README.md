# bstree
bstree with easy to find any nodes within a given interval

class Node():

    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None

    def append(self, value):
        if value <self.value:
            if self.left is None:
                self.left = Node(value)
            else:
                self.left.append(value)
        else:
            if self.right is None:
                self.right = Node(value)
            else:
                self.right.append(value)
                
    def ordered_list(self):
        if self.left is None and self.right is None:
            return [self.value]
        if self.left is not None and self.right is None:
            return self.left.ordered_list() + [self.value]
        if self.left is None and self.right is not None:
            return [self.value] + self.right.ordered_list()
        if self.left is not None and self.right is not None:
            return self.left.ordered_list() + [self.value] + self.right.ordered_list()
        
    def ordered_list_limits(self, lower, upper):
        order_list = self.ordered_list()
        order_list_limit_lower = None
        order_list_limit = None
        
        for i in range(0, len(order_list)):
            if order_list[i] <= lower:
                order_list_limit_lower = order_list[i+1:]

        for i in range(0, len(order_list_limit_lower)):
            if order_list_limit_lower[i] >= upper:
                order_list_limit = order_list_limit_lower[:i-1]
        return order_list_limit

class BinarySearchTree():

    def __init__(self):
        self.root = None

    def append(self, value):
        if self.root is None:
            self.root = Node(value)
        else:
            self.root.append(value)

    def ordered_list(self):
        if self.root is None:
            return []
        else:
            return self.root.ordered_list()

    def ordered_list_limits(self, lower, upper):
        if self.root is None:
            return []
        else:
            return self.root.ordered_list_limits(lower, upper)
if __name__ == "__main__":
    tree = BinarySearchTree()
    tree.append(50)
    tree.append(17)
    tree.append(12)
    tree.append(9)
    tree.append(14)
    tree.append(23)
    tree.append(19)
    tree.append(72)
    tree.append(54)
    tree.append(67)
    tree.append(76)
    print(tree.ordered_list())
    print(tree.ordered_list_limits(14, 70))
