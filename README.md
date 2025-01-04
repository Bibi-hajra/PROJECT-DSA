
import matplotlib.pyplot as plt
import networkx as nx

class BinaryTree:
    def _init_(self, value):
        self.value = value
        self.left = None
        self.right = None

def add_node(graph, node, pos, x=0, y=0, level=1, width=1.5):
    """
    Recursively adds nodes to the graph for visualization.
    """
    if node is None:
        return

    graph.add_node(node.value, pos=(x, y))

    # Add left child
    if node.left is not None:
        graph.add_edge(node.value, node.left.value)
        add_node(graph, node.left, pos, x - width / level, y - 1, level + 1, width)

    # Add right child
    if node.right is not None:
        graph.add_edge(node.value, node.right.value)
        add_node(graph, node.right, pos, x + width / level, y - 1, level + 1, width)

def visualize_binary_tree(root):
    """
    Visualizes the binary tree using NetworkX and Matplotlib.
    """
    graph = nx.DiGraph()
    pos = {}

    # Build graph recursively
    add_node(graph, root, pos)

    # Extract positions for nodes
    pos = nx.get_node_attributes(graph, 'pos')

    # Plot the graph
    plt.figure(figsize=(10, 6))
    nx.draw(graph, pos, with_labels=True, node_size=1000, node_color="skyblue", font_size=10, font_weight="bold", arrows=False)
    plt.title("Binary Tree Visualization", size=16)
    plt.show()

# Example usage
if _name_ == "_main_":
    # Build a sample binary tree
    root = BinaryTree(1)
    root.left = BinaryTree(2)
    root.right = BinaryTree(3)
    root.left.left = BinaryTree(4)
    root.left.right = BinaryTree(5)
    root.right.left = BinaryTree(6)
    root.right.right = BinaryTree(7)

    # Visualize the binary tree
    visualize_binary_tree(root)
