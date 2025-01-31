---
tags: algorithm, compress
---
```python
import heapq
from collections import Counter

# Node 클래스 정의
class Node:
    def __init__(self, char, freq):
        self.char = char
        self.freq = freq
        self.left = None
        self.right = None

    def __lt__(self, other):
        return self.freq < other.freq

# 문자 빈도 계산
text = "ABRACADABRA"
freq_map = Counter(text)

# 우선순위 큐 생성
priority_queue = [Node(char, freq) for char, freq in freq_map.items()]
heapq.heapify(priority_queue)

# 허프만 트리 생성
while len(priority_queue) > 1:
    left = heapq.heappop(priority_queue)
    right = heapq.heappop(priority_queue)
    
    merged = Node(None, left.freq + right.freq)
    merged.left = left
    merged.right = right
    
    heapq.heappush(priority_queue, merged)

# 코드 생성 함수
def generate_codes(root, current_code, huffman_codes):
    if root is None:
        return
    if root.char is not None:
        huffman_codes[root.char] = current_code
    generate_codes(root.left, current_code + "0", huffman_codes)
    generate_codes(root.right, current_code + "1", huffman_codes)

# 압축 함수
def compress(text, huffman_codes):
    return "".join(huffman_codes[char] for char in text)

# 트리 저장 함수
def serialize_tree(root):
    if root is None:
        return "None"
    return f"{root.char},{root.freq},{serialize_tree(root.left)},{serialize_tree(root.right)}"

# 복원 함수
def decompress(compressed_text, root):
    current = root
    original_text = ""
    for bit in compressed_text:
        if bit == "0":
            current = current.left
        else:
            current = current.right
        if current.char:
            original_text += current.char
            current = root
    return original_text

# 실행
huffman_codes = {}
generate_codes(priority_queue[0], "", huffman_codes)
compressed_text = compress(text, huffman_codes)
serialized_tree = serialize_tree(priority_queue[0])
original_text = decompress(compressed_text, priority_queue[0])

print("Original text:", text)
print("Compressed text:", compressed_text)
print("Decompressed text:", original_text)
```