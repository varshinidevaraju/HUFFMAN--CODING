# Huffman-Coding
### Aim
To implement Huffman coding to compress the data using Python.

### Software Required
Anaconda - Python 3.7

### Algorithm:
#### Step1:
Calculate the frequency of each character in the input string.
#### Step2:
Create a priority queue (min-heap) to store nodes based on character frequencies.
#### Step3:
Build the Huffman tree by repeatedly combining the two nodes with the lowest frequencies until only one node remains.
#### Step4:
Generate the Huffman codes by traversing the tree and assigning binary codes ('0' for left, '1' for right).
#### Step5:
Print the Huffman codes for each character in the input string.

### Program:
```
import heapq
from collections import defaultdict
string = input("Enter a string to encode: ")
class NodeTree(object):
    def __init__(self, char, freq):
        self.char = char  # Character in the input string
        self.freq = freq  # Frequency of the character
        self.left = None   # Left child
        self.right = None  # Right child
    def __lt__(self, other):
        return self.freq < other.freq
def huffman_code_tree(node, left=True, binString=''):
    if node is None:
        return {}
    if node.char is not None:
        return {node.char: binString}
    huffman_codes = {}
    huffman_codes.update(huffman_code_tree(node.left, left=True, binString=binString + '0'))
    huffman_codes.update(huffman_code_tree(node.right, left=False, binString=binString + '1'))
    return huffman_codes
freq = defaultdict(int)
for char in string:
    freq[char] += 1
heap = []
for char, freq_value in freq.items():
    heapq.heappush(heap, NodeTree(char, freq_value))
while len(heap) > 1:
    left = heapq.heappop(heap)
    right = heapq.heappop(heap)
    merged = NodeTree(None, left.freq + right.freq)
    merged.left = left
    merged.right = right
    heapq.heappush(heap, merged)
root = heap[0]
huffmanCode = huffman_code_tree(root)
print(" Char | Huffman code ")
print("----------------------")
for char, code in huffmanCode.items():
    print(f" {char}  | {code}")
```

### Output:
#### Print the characters and its huffmancode
![image](https://github.com/user-attachments/assets/5d100793-cebc-4d44-8697-98363622a0bf)


![image](https://github.com/user-attachments/assets/40f9739c-6b0f-4421-8905-f714a99906f5)

### Result
Thus the huffman coding was implemented to compress the data using python programming.
