# [Graph](https://leetcode.com/explore/learn/card/graph/)
## Disjoint Set
**When merging, choose a common head**
### Implementation
- Store it as a root arrary

    ```
         0
        / \
       1   2
      / \ 
     3   4

    ```
    
    - Array value : [0,0,0,1,1] Parent Vertex

    - Array index : [0,1,2,3,4] Vertex

    **Root Node : value==index**

    **To change the parent of a children, we  change the root of the children**

- The ``find()`` function finds the root node of a given vertex. 

- The ``union()`` function unions two vertices and makes their root nodes the same. 

### Quick Find

- Pseudo Code

    -The array value is **Root Verex**, not parent.

```python
class UnionFind():
    root[];

    UnionFind(size):
        root = [0] * size;
        for i in [0,size):
            root[i] = i;

    int find(x):
        return root[x];
    
    void union(x,y):
        rootX = find(x);
        rootY = find(y);
        if (rootX != rootY):
            for i in [0, root.length):
                if (root[i] == rootY):
                    root[i] = rootX;
    
    bool connected(x,y):
        return find(x)==find(y);

```

```python
# UnionFind class
class UnionFind:
    def __init__(self, size):
        self.root = [i for i in range(size)]

    def find(self, x):
        return self.root[x]
		
    def union(self, x, y):
        rootX = self.find(x)
        rootY = self.find(y)
        if rootX != rootY:
            for i in range(len(self.root)):
                if self.root[i] == rootY:
                    self.root[i] = rootX

    def connected(self, x, y):
        return self.find(x) == self.find(y)


# Test Case
uf = UnionFind(10)
# 1-2-5-6-7 3-8-9 4
uf.union(1, 2)
uf.union(2, 5)
uf.union(5, 6)
uf.union(6, 7)
uf.union(3, 8)
uf.union(8, 9)
print(uf.connected(1, 5))  # true
print(uf.connected(5, 7))  # true
print(uf.connected(4, 9))  # false
# 1-2-5-6-7 3-8-9-4
uf.union(9, 4)
print(uf.connected(4, 9))  # true
```

- Time Complexity: 

    - UnionFind constructor: O(N)

    - find: O(1)

    - union: O(N)

    - connected: O(1)

### Quick Union

- The array value is **parent vertex**

- Find the root of the node and change its parent.

```python
# UnionFind class
class UnionFind:
    def __init__(self, size):
        self.root = [i for i in range(size)]

    def find(self, x):
        while (x != self.root[x]):
            x = self.root[x]
        return x
		
    def union(self, x, y):
        rootX = self.find(x)
        rootY = self.find(y)
        if rootX != rootY:
            self.root[rootY] = rootX
        

    def connected(self, x, y):
        return self.find(x) == self.find(y)


# Test Case
uf = UnionFind(10)
# 1-2-5-6-7 3-8-9 4
uf.union(1, 2)
uf.union(2, 5)
uf.union(5, 6)
uf.union(6, 7)
uf.union(3, 8)
uf.union(8, 9)
print(uf.connected(1, 5))  # true
print(uf.connected(5, 7))  # true
print(uf.connected(4, 9))  # false
# 1-2-5-6-7 3-8-9-4
uf.union(9, 4)
print(uf.connected(4, 9))  # true
```

- Time Complexity: 

    - UnionFind constructor: O(N)

    - find: O(N)

    - union: O(N)

    - connected: O(N)

### Union by rank

- 将height小的set合并到height大的tree

- 除非两个要合并的set height/rank一样高，否则rank不会变。一样高height+1

```python
class UnionFind:
    def __init__(self,size):
        self.root = [i for i in range(size)]
        self.rank = [1]*size

    def find(self,x):
        while(x != self.root[x]):
            x = self.root[x]
        return x

    def union(self,x,y):
        rootX = self.find(x)
        rootY = self.find(y)

        if(rootX != rootY):

            if self.rank[rootX] > self.rank[rootY]:
                self.root[rootY] = rootX 
            
            elif self.rank[rootX] < self.rank[rootY]:
                self.root[rootX] = rootY
            
            else:
                self.root[rootY] = rootX
                self.rank[rootX] += 1
    def connected(self,x,y):
        return self.find(x) == self.find(y)
```

- Time Complexity: 

    - UnionFind constructor: O(N)

    - find: O(logN)

    - union: O(logN)

    - connected: O(logN)
