---
layout: post
title: Huffman Text Compression in Python - Part 1
---

Around a week ago, I watched Tom Scott's video on Text Compression. He explained in a rough sort of way how Huffman encoded characters using mathematics.

I recommend watching the [video](https://www.youtube.com/watch?v=JsTptu56GM8&t=283s), and then looking here for a quick summary.

All characters are 8 bits long in ASCII. Huffman had a simple idea, give lesser bits to frequent digits and more bits to less frequent digits.
Now with this comes the problem of finding letters, i.e. lets say "a" was encoded to 10 and "b" was encoded to 1010. So when we come across the bits 101010 do we read them as ab, ba, aaa? So the solution to this was that either no character should have a repeating set of bits which is even a subset of another character, or the decoder should know when a letter has ended i.e. when traversing 101010, it should know that the 3rd digit is the start of a new character.
Huffman decided to go with latter and created a tree. He sorted the tree such that the minimun frequency elements were at the top and the lower frequency elements were at the bottom and each character must be a leaf node.

So you start from the top, if you move to the left, you add a 1 to your binary number or 0 if you move right and you keep doing this until you reach a character, and the binary string you get is the encoding for that character. Similarly you obtain encodings for each of the characters. And join the binary digits to form a long stream of bits which is the encoded and compressed version of the text.
For decoding, you start from the first binary digit in the compressed version and move left in the graph if its a 1 or right if its a 0. Keep repeating this until you reach a leaf node and you know that's the character that was there and then you start over from the top until you reach the end of the stream of bits.

Now to implement this in Python, I worked with my friend [Siddharth Shekhar (Sid)](https://github.com/Sid0518).

The repo for this code is hosted [here](https://github.com/kartikay-bagla/huffman-text-compression-in-python)

I decided on a more understandable approach whereas Sid went for the more efficient approach.

In this post, I'll explain my approach.

I initally created a class Node which would store data for each node in the tree.
```python
class Node:
    """Class for storing the character-value pairs in graph style i.e. with left and right nodes"""
    def __init__(self, val, freq):
        """Initializes the object with its value and frequency"""
        self.val = val
        self.freq = freq
        self.left = None
        self.right = None
```
"self.left" and "self.right" store which nodes are to its left and right.
I also added the less than operator for comparison between 2 nodes based on their frequencies.
```python
    def __lt__(self, other):
        try:
            return self.freq < other.freq
        except:
            return False

```

So after my nodes were completed, I needed a tree like structure to save them and sort them, so I decided to implement an extremely rudimentary version of Heap queues or Min Priority Queue. (I will update the sorting, pushing and popping algorithms for the Heap class when I dive into Heaps properly, but for now they're not very efficient. For now you can substitute the heap class with the heapq module if you want).

```python
class Heap:
    """An implementation of Min Heap queue or min priority queue"""
    def __init__(self, l = []):
        """Initializes the object with list l and sorts it"""
        self.l = l
        self.sort()
```

For sorting the queue, I just used a common sort instead of having different sorts for popping, pushing and pop push at once.
```python
    def _move_down(self, pos):
        """A recursive function for swapping parents with children"""
        item = self.l[pos]
        c1_pos = (pos + 1) * 2
        c2_pos = pos * 2 + 1
        try:
            c1 = self.l[c1_pos]
        except:
            try:
                c2 = self.l[c2_pos]
            except:
                return
            else:
                if item > c2:
                    self.l[pos], self.l[c2_pos] = self.l[c2_pos], self.l[pos]
                    pos = c2_pos
                    self._move_down(pos)
                    return
        else:
            c2 = self.l[c2_pos]
            if c1 > c2:
                if item > c2:
                    self.l[pos], self.l[c2_pos] = self.l[c2_pos], self.l[pos]
                    pos = c2_pos
                    self._move_down(pos)
                    return
            else:
                if item > c1:
                    self.l[pos], self.l[c1_pos] = self.l[c1_pos], self.l[pos]
                    pos = c1_pos
                    self._move_down(pos)
                
    def sort(self):
        """Sorts the heap queue"""
        if len(self.l)%2 == 0:
            if self.l == []:
                return
            ind = len(self.l)-1
            item = self.l[ind]
            parent_pos = ind//2
            parent = self.l[parent_pos]
            if item < parent:
                self.l[ind], self.l[parent_pos] = self.l[parent_pos], self.l[ind]
            ind = ind - 1
        else:
            ind = len(self.l) - 1
        for i in range(ind, -1, -2):
            if i%2 == 0:
                parent_pos = i//2 -1
            else:
                parent_pos = i//2
            if parent_pos < 0:
                break
            self._move_down(parent_pos)
```

And for pushing, I just appended an item to the list and sorted it again (I know, its not very efficient). For popping I popped the 0th element and sorted the list again.
```python
    def push(self, item):
        """Pushes an item into the heap and sorts it"""
        self.l.append(item)
        self.sort()

    def pop(self):
        """Pops the top item from the heap and sorts it"""
        first = self.l[0]
        last = self.l[-1]
        self.l[0], self.l[-1] = last, first
        first = self.l.pop()
        self.sort()
        return first
```

For the main file, I created a Huffman class which takes in the Input File, Output File and a Treefile (for the Huffman Tree)
```python
class Huffman:
    """An implementation of the Huffman Algorithm for text compression"""
    def __init__(self, out_path, in_path, g_path):
        """Takes the output path, input path and graph path for the input file, output file and the graph file"""
        self.out_path = out_path
        self.in_path = in_path
        self.g_path = g_path
        self.heap = []
        self.codes = {}
        self.reverse_mapping = {}
```

For encoding, I went with these steps:
1. Create a {char: frequency} pairs dictionary.
2. Make a heap from the dictionary by creates Nodes of all pairs and sort the heap.
3. Use the sorted heap to create a Huffman Tree.
4. Create a mapping(dictionary with {value: binary stream}) for all the characters.
5. Encode the text using the mapping
In python, you need to write bits to a file in groups of 8 (as integers), so we had to append 0s to the end of the binary stream. To keep track of the number os zeros appended, I inserted the number of zeros as 8 binary digits to the front of the file.
6. Pad the text with 0s
7. Create a bytearray from the binary stream
8. Write the byte array to the output file and save the tree.

So here's the code stepwise
1. Here's the code for step 1:
```python
    def freq_dict(self, text):
        """Takes a string text and returns a dictionary with the character-frequency pairs of all characters in the text"""
        freq = {}
        for char in text:
            if not char in freq:
                freq[char] = 0
            freq[char] += 1
        return freq
```

2. Here's the code for step 2:
```python
    def heap_list(self, freq):
        """Takes a character-frequency dictionary, converts them into Nodes and sorts them into a heap"""
        for key in freq:
            node = Node(key, freq[key])
            self.heap.append(node)
        self.heap = Heap(self.heap)
        self.heap.sort()
```

3. Here's the code for step 2:
```python
    def create_graph(self):
        """Creates a Huffman graph from self.heap"""
        while(len(self.heap.l) > 1):
            node1 = self.heap.pop()
            node2 = self.heap.pop()
            merged = Node(None, node1.freq + node2.freq)
            merged.left = node1
            merged.right = node2
            self.heap.push(merged)
```

4. Here's the code for step 2:
```python
    def _make_codes_recur(self, node, code):
        """Recursive function for mapping digits to characters"""
        if node == None:
            return
            
        if node.val != None:
            self.codes[node.val] = code
            self.reverse_mapping[code] = node.val
            return

        self._make_codes_recur(node.left, code + "0")
        self._make_codes_recur(node.right, code + "1")

    def make_code(self):
        """Creates the character-code and vice-versa dictionaries"""
        self.node = self.heap.pop()
        code = ""
        self._make_codes_recur(self.node, code)
```

5. Here's the code for step 2:
```python
    def encode_text(self, text):
        """Encodes the text using the coded values in self.codes"""
        encoded_text = ""
        for char in text:
            encoded_text += self.codes[char]
        return encoded_text
```

6. Here's the code for step 2:
```python
    def pad_text(self, text):
        """Pads the encoded text with 0's to make it complete bytes of data"""
        extra = 8 - len(text)%8
        for i in range(extra):
            text += "0"
        info = "{0:08b}".format(extra)
        text = info + text
        return text
```

7. Here's the code for step 2:
```python
    def byte_array(self, text):
        """Creates a byte array out of the padded text"""
        b = bytearray()
        for i in range(0, len(text), 8):
            byte = text[i:i+8]
            b.append(int(byte, 2))
        return b
```

8. Now I wrap all these functions in a nice little function called compress:
```python
    def compress(self):
        """Compresses the text from the input file to the output file and creates a graph used for decompression"""
        with open(self.in_path) as f, open(self.out_path, "wb") as o, open(self.g_path, "wb") as g:
            text = f.read().rstrip()
            freq = self.freq_dict(text)
            self.heap_list(freq)
            self.create_graph()
            self.make_code()
            encoded_text = self.encode_text(text)
            padded_encoded_text = self.pad_text(encoded_text)
            b = self.byte_array(padded_encoded_text)
            o.write(bytes(b))
            pickle.dump(self.node, g)
        print("Compressed")
```

Decompression follows a similar pattern
1. Depad the stream
```python
    def depad_text(self, bit_text):
        """Removes the padding from the binary text strings"""
        added_zeros = int(bit_text[:8], 2)
        return bit_text[8:-added_zeros]
```

2. Decode the text using the graph
```python
    def decode_text(self, depadded_text):
        """Moves through the graph to find characters from the depadded text"""
        decoded_text = ""
        main_node = self.node
        current_node = self.node
        for bit in depadded_text:
            if bit == "0":
                new_node = current_node.left
            elif bit == "1":
                new_node = current_node.right
            if new_node.val != None:
                decoded_text += new_node.val
                current_node = main_node
            else:
                current_node = new_node
        return decoded_text
```

3. I wrapped everything up in a nice function called decompress
```python
    def decompress(self):
        """Decompresses the data in the input file to the output file using the graph file as a table"""
        with open(self.in_path, "rb") as f, open(self.out_path, "w") as o, open(self.g_path, "rb") as g:
            self.node = pickle.load(g)
            bit_text = ""
            byte = f.read(1)
            while(byte != b""):
                
                byte = ord(byte)
                bits = bin(byte)[2:].rjust(8, "0")
                bit_text += bits
                byte = f.read(1)
            
            depadded_text = self.depad_text(bit_text)
            decoded_text = self.decode_text(depadded_text)
            o.write(decoded_text)
        print("Decompressed")
```

The repo for this code is hosted [here](https://github.com/kartikay-bagla/huffman-text-compression-in-python)