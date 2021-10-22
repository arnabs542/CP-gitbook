# --->Tree

## Notes:

* **DFS vs BFS:: How to Pick One?**
  1. Extra Space can be one factor (Explained below)
  2. **Depth First Traversals** are typically recursive and recursive code requires **function call overheads**.
  3. The most important points is, BFS starts visiting nodes from root while DFS starts visiting nodes from leaves. So if our problem is to search something that is more likely to\*\* closer to root,\*\* we would prefer **BFS**. And if the target node is **close to a leaf**, we would prefer **DFS**.
* **Rooting A Tree**: is like picking up the tree by a specific node and having all the edges point downwards
  * Res: [https://towardsdatascience.com/graph-theory-rooting-a-tree-fb2287b09779](https://towardsdatascience.com/graph-theory-rooting-a-tree-fb2287b09779)
* Node:

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None
...
root = TreeNode(x)
```

* ffs

## 1. Regular Tree Problems

* [x] \*\*\*\*[**Inorder Successor in Binary Search Tree**](https://www.geeksforgeeks.org/inorder-successor-in-binary-search-tree/) ✅💪
* [x] 501\. [Find Mode in Binary Search Tree](https://leetcode.com/problems/find-mode-in-binary-search-tree/) | MindTickle!
* [x] 236\. [Find LCA in Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/) | **DnQ** | Standard ✅✅
* [x] Distance b/w 2 nodes in Tree: **`dist(a,b) = depth(a) + depth(b) - 2*depth(c) ; where c = lca(a,b)`**
* [x] LCA of N-ary tree ([article](https://medium.com/@sahilawasthi9560460170/lowest-common-ancestor-of-n-ary-tree-107fa772a939))
* [x] 1367.[ Linked List in Binary Tree](https://leetcode.com/problems/linked-list-in-binary-tree/)

{% tabs %}
{% tab title="InO_Succ✅" %}
```python
# Method 1: (Uses Parent Pointer) 
'''
1. If right subtree of node is not NULL, then succ lies in right subtree. 
    => Go to right subtree and return the node with minimum key value in the right subtree.
2. If right sbtree of node is NULL, then succ is one of the ancestors. 
    => Travel up using the parent pointer until you see a node which is
       left child of its parent. The parent of such a node is the succ.
'''
class Node:
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

    def inOrderSuccessor(n):
     
        # Step 1 of the above algorithm
        if n.right is not None:
            return minValue(n.right)
     
        # Step 2 of the above algorithm
        p = n.parent
        while( p is not None):
            #if n != p.right :
            if n == p.left :
                break
            n = p
            p = p.parent
        return p
     
    def minValue(node):
        current = node
     
        # loop down to find the leftmost leaf
        while(current is not None):
            if current.left is None:
                break
            current = current.left
     
        return current


# Method 2: w/o parent pointer
'''
1. If right subtree of node is not NULL, then succ lies in right subtree. 
    => {same as above}
2. If right sbtree of node is NULL, then succ is one of the ancestors. 
    => Travel down the tree, if a node’s data is greater than root’s data
      then go right side, otherwise, go to left side.
'''
class Node:
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None
 
def inOrderSuccessor(root, n):
     
    # Step 1 of the above algorithm
    if n.right is not None:
        return minValue(n.right)
 
    # Step 2 of the above algorithm
    succ=Node(None)
     
    while( root):
        if(root.data<n.data):
            root=root.right
        elif(root.data>n.data):
            succ=root
            root=root.left
        else:
            break
    return succ
 
def minValue(node):
    current = node
 
    # loop down to find the leftmost leaf
    while(current is not None):
        if current.left is None:
            break
        current = current.left
 
    return current
 
```
{% endtab %}

{% tab title="501" %}
```python
#1. O(N) space ==================================================
    cnts = collections.Counter()
    self.maxx = 0
    
    def helper(node):
        # nonlocal maxx
        if not node:
            return
        cnts[node.val] += 1
        self.maxx = max(self.maxx, cnts[node.val])
        helper(node.left)
        helper(node.right)
        
    helper(root)
    return [k for k,v in cnts.items() if v == self.maxx]

    #2. O(1) Space ===================================================
    prev,count=0,0
    ans=[]
    c=0
    def inorder(root):
        nonlocal prev,count,c,ans
        if root:
            inorder(root.left)
            if prev==root.val:
                count+=1
            else:
                prev=root.val
                count=1
            if count>c:
                c=count
                ans=[root.val]
            elif count==c:
                ans.append(root.val)
            inorder(root.right)
    inorder(root)
    return(ans)
```
{% endtab %}

{% tab title="236.lca✅" %}
```python
def lca(root,p,q) -> 'TreeNode':
        # found p and q?
        if not root or root == p or root == q:
            return root
    
        left = lca(root.left,p,q)
        right = lca(root.right,p,q)
        
        # p and q appears in left and right respectively, then their ancestor is root
        if left is not None and right is not None:
            return root
        
        # p and q not in left, then it must be in right, otherwise left
        if left is None:
            return right
        
        if right is None:
            return left
```
{% endtab %}

{% tab title="1367." %}
```python
def isSubPath(self, head: Optional[ListNode], root: Optional[TreeNode]) -> bool:

    def dfs(head, root):
        if not head: return True
        if not root: return False
        return root.val == head.val and (dfs(head.next, root.left) or dfs(head.next, root.right))
    if not head: return True
    if not root: return False
    return dfs(head, root) or self.isSubPath(head, root.left) or self.isSubPath(head, root.right)

'''
Time O(N * min(L,H))
Space O(H)
where N = tree size, H = tree height, L = list length.
'''
```
{% endtab %}
{% endtabs %}

![LCA of N-ary Tree](../../.gitbook/assets/screenshot-2021-09-10-at-1.56.31-pm.png)

## 2. DP on Trees ✅ : // does the job in O(N)

* [CF tutorial](https://codeforces.com/blog/entry/20935?locale=en)

### 2.1 Trivial Questions

* [x] **BOOK#1: Number of nodes in subtree**

![](../../.gitbook/assets/screenshot-2021-09-10-at-12.43.41-pm.png)

* [x] **BOOK#2: Counting the number of paths till node X**

![](../../.gitbook/assets/screenshot-2021-09-10-at-1.13.22-pm.png)

* [x] **CF#1**: [Find max coins s.t. no two adjacent edges get collected](https://codeforces.com/blog/entry/20935?locale=en)
  * Do **`dfs()`** & build our dp1 & dp2

![CF#1](../../.gitbook/assets/screenshot-2021-09-12-at-2.07.09-am.png)

* [x] CSES:[ Tree Diameter](https://cses.fi/problemset/task/1131) ✅✅ | Basic level Tree DP | AdityaVerma | [KartikArora- N-ary tree](https://www.youtube.com/watch?v=qNObsKl0GGY\&list=PLb3g_Z8nEv1j_BC-fmZWHFe6jmU_zv-8s\&index=3\&ab_channel=KartikArora)
* [x] CSES: [Tree Distances I](https://cses.fi/problemset/task/1132) | aka. **`All Longest Paths`** | Same code as TreeDiameter=> use 2 dfs to get endpoints of dia ==> dfs b/w them | [underrated amazing video by HiteshTripathi](https://www.youtube.com/watch?v=Rnv4qvoxsTo\&ab_channel=HiteshTripathi) 🚀✅✅🚀 | **must_do**
* [x] LC: [Diameter of N-ary tree](http://leetcode.libaoj.in/diameter-of-n-ary-tree.html) | `TreeDistances I 's` code works here too

{% tabs %}
{% tab title="template" %}
```python
def f(node):
    #1. Base Condition
        if node is None: return 0
    #-----------------
    #2. HYPOTHESIS :: Recursive call on left & right 
        lr = f(node->left)
        rr = f(node-right)
    #------------------
    #3. INDUCTION :: Take decision & return it
         opt1 = g(lr,rr)    # case when 'node' cant be part of final ans
         opt2 = h()         # case when 'node cant be part of final ans
         
         return max(opt1, opt2)
```
{% endtab %}

{% tab title="CF#1." %}
```cpp
/ =====================================Complexity is O(N).

vector<int> adj[N];
int dp1[N],dp2[N];        //functions as defined above

//p is parent of node x
void dfs(int x, int p){

    //for storing sums of dp1 and max(dp1, dp2) for all children of V
    int sum1=0, sum2=0;

    //traverse over all children
    for(auto y: adj[x]){
        if(y == p) continue;
        dfs(y, x);        // ===> now we have calculated dp1[y] & dp2[y]
        sum1 += dp2[y];
        sum2 += max(dp1[y], dp2[y]);
    }

    dp1[x] = C[x] + sum1;
    dp2[x] = sum2;
}

int main(){
    int n;
    cin >> n;

    for(int i=1; i<n; i++){
    cin >> u >> v;
        adj[u].push_back(v);
        adj[v].push_back(u);
    }

    dfs(1, 0);
    int ans = max(dp1[1], dp2[1]);
    cout << ans << endl;
}
```
{% endtab %}

{% tab title="TreeDiameter" %}
```python
---------------------- works only for binary tree

def recurse(x):
    if not x: 
        return 0
    ldia = recurse(x.left)
    rdia = recurse(x.right)

    self.result = max(self.result, ldia+rdia)  # this is the dia of node x
    return 1 + max(ldia,rdia)  # passes this to its parent

self.result = 0
recurse(root)
return self.result    
    
------------------------- for n-arry tree
int n, ans;
vector<int> adj[MAX];
int d[MAX];
 
 void dfs(int u = 1, int p = -1){
     for(auto v:adj[u]){
         if(v==p)continue;
         dfs(v,u);
         ans = max(ans, d[u]+d[v]+1); # max v1--u--v2 
         d[u] = max(d[u],1+d[v]) # max v---u ::max depth of node u(i.e. longest path in its subtree)
     }
 }
 
int main() {
    cin >> n;
    for(int i=1;i<n;i++)
    {
        int u,v;
        cin >> u >> v;
        adj[u].push_back(v);
        adj[v].push_back(u);
    }
    dfs(1,-1);
    cout<<ans;
}
```
{% endtab %}

{% tab title="TreeDistance I" %}
```python
from collections import defaultdict

G = [[1,2],[2,3],[2,4],[3,5],[4,6]]
N = 6
adj = defaultdict(list)

for x,y in G:
    adj[x].append(y)
    adj[y].append(x)

def dfs(x,p,d):
    vis.add(x)
    par[x] = p
    dists[x] = d
    for y in adj[x]:
        if y not in vis and y != p:
            dfs(y,x,d+1)
            
#=================== DFS#1: getting one end of diameter: ndoe1
par = [-1]*(N+1)
dists = [0]*(N+1)
vis = set()

dfs(1,-1,0)     # start dfs from any arbitraily rooted node
node1 = -1
max_dist = float('-inf')

for i in range(1,N+1):
    if max_dist < dists[i]:
        node1 = i
        max_dist = dists[i]

print('node1 = ', node1)

#=================== DFS#1: getting the other end of diameter: ndoe2
par = [-1]*(N+1)
dists = [0]*(N+1)
vis = set()

dfs(node1,-1,0) # start dfs from tree rooted @node1
node2 = -1
max_dist = float('-inf')

for i in range(1,N+1):
    if max_dist < dists[i]:
        node2 = i
        max_dist = dists[i]

print('node2 = ', node2)

# node1 & node2 mil gye
# ab unse dfs call karo aur dists calculate karo

dists = [0]*(N+1)
vis = set()

dfs(node1,-1,0)
d1 = dists[::]

dists = [0]*(N+1)
vis = set()

dfs(node2,-1,0)
d2 = dists[::]

print(d1)
print(d2)
print(f'========> Tree Diameter = {d1[node2]}')

print('======== Now printing max longest paths for all nodes =========')
for i in range(1,N+1):
    print(f' Node: {i} => {max(d1[i],d2[i])}')
```
{% endtab %}

{% tab title="MaxPathSum" %}
```python
# From any node to any node
def solve(node):
    if node is null: return 0
    
    lsum = solve(node.left)
    rsum = solve(node.right)
    
    opt1 = max(node.val,                    # path startes from node
                node.val + max(lsum,rsum))  # 'node' is in beech-mei of path
    opt2 = max(node.val , lsum+rsum+node.val)
    return max(opt1, opt2)            
```
{% endtab %}

{% tab title="MaxLeafPathSum" %}
```python
# From Leaf node to leaf node
def solve(node):
    if node is None: return 0
    
    lsum = solve(node.left)
    rsum = solve(node.right)
    
    opt1 = node.val + max(lsum,rsum)  # 'node' is in beech-mei of path
    # path can start from node only if its a leaf node
    if node.left is None and node.right is None:
        opt1 = max(node.val, opt1)
        
    opt2 = max(lsum+rsum+node.val)
    return max(opt1, opt2) 
```
{% endtab %}

{% tab title="BOOk#2" %}
```python
def solve(G,N):
    adj = defaultdict(list)
    inDeg = [0]*(N+1)

    for x,y in G:
        adj[x].append(y)
        inDeg[y] += 1
        
    topo = []
    Q = deque()
    for i in range(1,N+1):
        if inDeg[i] == 0:
            Q.append(i)
    while Q:
        x = Q.popleft()
        topo.append(x)
        
        for y in adj[x]:
            inDeg[y] -= 1 
            if inDeg[y] == 0:
                Q.append(y)
                
    if len(topo) != N:
        return -1
    # print(topo
    ways = [0]*(N+1)
    ways[topo[0]] = 1
    for i in range(N):
        curr = topo[i]
        for x in adj[curr]:
            ways[x] += ways[curr]
    return ways[1:]


N = 6
G = [[1,2],[1,4],[4,5],[5,2],[2,3],[5,3],[3,6]]
res = solve(G,N)
print(res)
```
{% endtab %}
{% endtabs %}

###

### 2.2 Not-so trivial Questions

* [x] CSES: [Subordinates](https://cses.fi/problemset/task/1674) ✅
* [x] CSES: [Tree Distances II](https://cses.fi/problemset/task/1133) | \*\*`Tree Rerooting` ✅✅✅💪💪💪❤️❤️❤️| \*\*[video](https://www.youtube.com/watch?v=lWCZOjUOjRc\&t=42s)
  * **When is Rerooting DP applicable?**
  * \*\*===> \*\*when **given** `dp(x)`; you can calculated **`dp(y)`** for y:children\[x]
  * \========> mane; parent ki value mei kuch adjust karke uske children ki value nikali jaa sakti ho.
  * \========> e.g. \*\*Tree Distance ||(^) \*\*: get sum of all nodes from node X
  * **FINALLY SAMAJH AAYAAAAA!!!!!!!!!!!!!!!!!!!!!!!!!❤️**
* [x] CSES: [Tree Matching](https://cses.fi/problemset/task/1130) | [kartikArora](https://www.youtube.com/watch?v=RuNAYVTn9qM\&list=PLb3g_Z8nEv1j_BC-fmZWHFe6jmU_zv-8s\&index=2\&ab_channel=KartikArora) ✅
* [x] CF: [Distance in Tree](https://codeforces.com/contest/161/problem/D) | #nodes at dist K from each other
* [x] 968.[Binary Tree Cameras](https://leetcode.com/problems/binary-tree-cameras/) | @kartikArora 📷✅✅✅✅✅✅✅✅
* [x] 337\. [House Robber III](https://leetcode.com/problems/house-robber-iii/) ✅
* [x] 95\. [Unique Binary Search Trees II](https://leetcode.com/problems/unique-binary-search-trees-ii/) ✅| @MindTickle
* [x] 1339\. [Maximum Product of Splitted Binary Tree](https://leetcode.com/problems/maximum-product-of-splitted-binary-tree/)| ❤️✅| looks so complicated, yet so easy
* [ ] [https://leetcode.com/problems/longest-zigzag-path-in-a-binary-tree/](https://leetcode.com/problems/longest-zigzag-path-in-a-binary-tree/)
* [ ] [https://leetcode.com/problems/maximum-sum-bst-in-binary-tree/](https://leetcode.com/problems/maximum-sum-bst-in-binary-tree/)
* [ ] [https://leetcode.com/problems/number-of-ways-to-reorder-array-to-get-same-bst/](https://leetcode.com/problems/number-of-ways-to-reorder-array-to-get-same-bst/)

{% tabs %}
{% tab title="Subordinates" %}
```python
'''
TC: O(N)
'''
from collections import defaultdict
I = lambda : map(int,input().split())

# ===============================================
def dfs(x,p):
    dp[x] = 0
    
    for y in adj[x]:
        if y == p: continue
        dfs(y,x)
        dp[x] += 1+dp[y]

# ==============================================
n = int(input())
l = list(I())
adj = defaultdict(list)
dp = [0]*(n+1)
for i in range(2,n+1):
    adj[l[i-2]].append(i)
    
dfs(1,1)
print(dp[1:])
```
{% endtab %}

{% tab title="TreeDist2💪" %}
```python
# STEP:1 ======================= preprocessing :: rooted@1
def preprocess_dfs(x, p):

    subtree_size[x] = 1

    for y in adj[x]:
        if y != p:
            preprocess_dfs(y, x)
            subtree_size[x] += subtree_size[y]
            subtree_dist[x] += subtree_dist[y] + subtree_size[y]

# STEP:2 ======================= use values w.r.t 1 to get values for other nodes
def dfs(x, p):
    dp[x] = dp[p] - subtree_size[x] - subtree_dist[x] # detatch x from p
    dp[x] += n - subtree_size[x] + subtree_dist[x]    # add all nodes to x
    
    for y in adj[x]:
        if y != p:
            dfs(y,x)
            
n = int(input())
adj = defaultdict(list)
subtree_size = [0] * (n + 1)
subtree_dist = [0] * (n + 1)
dp = [0] * (n + 1)

for _ in range(n - 1):
    x, y = I()
    adj[x].append(y)
    adj[y].append(x)

# root the tree at any(here 1) node & preprocess values w.r.t. it
preprocess_dfs(1, -1)

# now use those precomputed values w.r.t. 1 to get values for other nodes
dp[1] = subtree_dist[1]
for x in adj[1]:
    dfs(x,1)

print(subtree_size)
print(subtree_dist)

print(dp[1:])
```
{% endtab %}

{% tab title="TreeMatching" %}
```cpp
/*
STATES: 
    * u : root node
    * picked = 0/1 : whether any edge(u--v) was picked 
ANS: max(dp(1,0), dp(1,1))
RECUR: 
    * dp(u,0) = SUM{ max(y,0), max(y,1) } for y:children[x]
    * dp(u,1) = SUM{max(y,0),max(y,1)}     # for y: c1...c(i-1)
                + 1 + dp(ci, 1)            # select this edge (u---ci)
                + SUM{max(y,0), max(y,1)}  # for y: c(i+1)....cn 
*/
vector<int>adj[MAX];
ll dp[MAX][2];
 
void dfs (int src){
    int leaf=1;
    dp[src][1]=0;
    dp[src][0]=0;

    for(auto child:adj[src]){
        leaf = 0;
        dfs(child);
    }
    if(leaf==1)return;

    for(auto child:adj[src]){
        dp[src][0]+=max(dp[child][0],dp[child][1]);
    }

    for(auto child:adj[src]){
        dp[src][1]=max(
                dp[src][1],
                1+ dp[child][0]+( dp[src][0]-max(dp[child][0],dp[child][1]))
            );
    }
}
 
 int main(){
     int n;
     cin>>n;
     for(int i=0;i<n-1;i++){
        int ss,ee;
        cin>>ss>>ee;
        adj[ss].push_back(ee);
     }
     dfs(1);
     cout<<max(dp[1][0],dp[1][1])<<endl;
}
```
{% endtab %}

{% tab title="968.📷✅" %}
```python
@lru_cache(None)
def minCameras(node=root, parent_covered=True, parent_camera=False):
    if not node: return 0
    camera_here = 1 + minCameras(node.left, parent_camera=True) + minCameras(node.right, parent_camera=True)

    if parent_camera:
        no_camera_here = minCameras(node.left) + minCameras(node.right)
        return min(camera_here, no_camera_here)

    if parent_covered:
        mincams = camera_here
        if node.right:
            mincams = min(mincams, minCameras(node.right, False) + minCameras(node.left, True))
        if node.left:
            mincams = min(mincams, minCameras(node.left, False) + minCameras(node.right, True))
        return mincams

    return camera_here

return minCameras()
```
{% endtab %}

{% tab title="HouesRobber3" %}
```python
MEMO = {}
def dp(x):
    if not x:
        return 0
    if not x.left and not x.right:
        return x.val
    if x in MEMO:
        return MEMO[x]
    opt1 = dp(x.left) + dp(x.right) # do not rob this node
    
    #rob this node
    opt2 = x.val 
    if x.left:
        opt2 += dp(x.left.left) + dp(x.left.right)
    if x.right:
        opt2 += dp(x.right.left) + dp(x.right.right) 
    MEMO[x] = max(opt1, opt2)
    return MEMO[x]
    

return dp(root)
```
{% endtab %}

{% tab title="95" %}
```python
 def solve(arr):
		#Base conditions
    if len(arr) < 1:
        return [None]
    if len(arr) == 1:
        return [TreeNode(arr[0])]
    
    ret = []
    for i,item in enumerate(arr):
        leftTrees = f(arr[0:i])
        rightTrees = f(arr[i+1:])
        
        for lt in leftTrees:
            for rt in rightTrees:
                r = TreeNode(arr[i])
                r.left = lt
                r.right = rt
                ret.append(r)
    return ret

return solve(list(range(1,n+1)))
```
{% endtab %}

{% tab title="1339.❤️✅" %}
```python
def maxProduct(self, root: Optional[TreeNode]) -> int:
        
    # dfs to get sum of subtree rooted @node
    def dfs(node):
        if not node: return 0
        ans = dfs(node.left) + dfs(node.right) + node.val
        res.append(ans)
        return ans
    
    res = []
    dfs(root)
    sum_all = max(res)
    return max(i*(sum_all-i) for i in res) % (10**9 + 7)
```
{% endtab %}

{% tab title="PlanetQueries!" %}
```cpp
#include <bits/stdc++.h>
using namespace std;

const int MAXN = 2e5+5;
const int MAXD = 30; // ceil(log2(10^9))

// number of planets and queries
int n, q;
// parent matrix where [i][j] corresponds to i's (2^j)th parent
int parent[MAXN][MAXD];

int jump(int a, int d) {
	for(int i=0; i<MAXD; i++) if(d & (1<<i))
		a = parent[a][i];
	return a;
}

int main() {
	cin >> n >> q;
	for(int i=1; i<=n; i++) {
		cin >> parent[i][0];
	}
	// evaluate the parent matrix
	for(int d=1; d<MAXD; d++){
	    for(int i=1; i<=n; i++) {
		    parent[i][d] = parent[parent[i][d-1]][d-1];
        }
	}   
	// process queries
	while(q--) {
		int a, d;
		cin >> a >> d;
		cout << jump(a, d) << '\n';
	}
}
/*
Time Complexity :  O(NlogN)
*/
```
{% endtab %}
{% endtabs %}

### Binary Lifting

* [x] CSES#1: [Company Queries I](https://cses.fi/problemset/task/1687) | **`Binary Lifting` 💪✅✅❤️**
* [x] CSES#2: [Company Queries II](https://cses.fi/problemset/task/1688) | **`LCA + Binary Lifting` 🐽🐽**
* [ ] CSES: [Planets Queries I](https://cses.fi/problemset/task/1750) | Binary Lifting

{% tabs %}
{% tab title="CSES#1: Binary Lifting 101" %}
```python
"""
# Binary Lifting

up(u,x) : parent of node 'u' which is 2^x level up
x = log2(N)

TC: O(NlogN)

RECURSION:

* up(u,x) = up(up(u,x-1),x-1)   # because 2^(x-1) + 2^(x-1) = 2^x

BC:
1. up(u,0) = par[u]
2. up(root,x) = -1

"""

from collections import defaultdict
I = lambda: map(int, input().split())

def dfs(u, p):
    up[(u, 0)] = p  # BC.1

    # setup values for node u
    for i in range(1, 20):
        if (u, i - 1) in up and up[(u, i - 1)] != -1:
            up[(u, i)] = up[(up[u, i - 1], i - 1)]
        else:
            up[(u, i)] = -1  # BC.2
    # recurs on u's children
    for v in adj[u]:
        if v != p:
            dfs(v, u)

def query(x, k):
    if x == -1 or k == 0:
        return x

    for i in range(19, -1, -1):  # jump the highest --> lowest set bit
        if k >= (1 << i):
            return query(up[(x,i)], k - (1 << i))


n, q = I()
l = list(I())
adj = defaultdict(list)
up = {}

for i in range(2, n + 1):
    adj[i].append(l[i - 2])
    adj[l[i - 2]].append(i)

dfs(1, -1)
# print(up)
for _ in range(q):
    x, k = I()
    print(query(x, k))
```
{% endtab %}

{% tab title="CSES#2: LCA in LlogN" %}
```cpp
#include<bits/stdc++.h>
using namespace std;
  
int n, q, a, b, p[200005][20], d[200005];
  
int dp(int x){
    if (d[x]) return d[x];
    if (x == 1) return d[x] = 1;
    return d[x] = dp(p[x][0])+1;
}
int solve(int a, int b){
    int x = dp(a), y = dp(b);
    if (x > y){
        swap(a, b);
        swap(x, y);
    }
    y -= x;
    for (int i = 0; i < 20; i++){
        if (y & (1<<i)) b = p[b][i];
    }
    if (a == b) return a;
    for (int i = 19; i >= 0; i--){
        if (p[a][i] != p[b][i]){
            a = p[a][i];
            b = p[b][i];
        }
    }
    return p[a][0];
}
  
int main() {
    cin >> n >> q;
    for (int i = 2; i <= n; i++){
        cin >> p[i][0];
    }
    for (int i = 1; i < 20; i++){
        for (int j = 1; j <= n; j++){
            p[j][i] = p[p[j][i-1]][i-1];
        }
    }
    while (q--){
        cin >> a >> b;
        cout << solve(a, b) << "\n";
    }
}
```
{% endtab %}
{% endtabs %}

##

## ProblemSet

* [https://leetcode.com/discuss/interview-question/1337373/Tree-question-pattern-oror2021-placement](https://leetcode.com/discuss/interview-question/1337373/Tree-question-pattern-oror2021-placement)
* [https://leetcode.com/problems/path-sum/discuss/548853/recursive-solution-with-takeaway-to-solve-any-binary-tree-problem](https://leetcode.com/problems/path-sum/discuss/548853/recursive-solution-with-takeaway-to-solve-any-binary-tree-problem)

## Resources:

* Youtube playlist by \*\*WilliamFiset \*\* : [here](https://www.youtube.com/watch?v=0qgaIMqOEVs\&list=PLDV1Zeh2NRsDGO4--qE8yH72HFL1Km93P\&index=9\&ab_channel=WilliamFiset)
* **Resources: Tree DP**
  * ✅Kartik Arora's Playlist: [Tree DP](https://www.youtube.com/watch?v=fGznXJ-LTbI\&list=PLb3g_Z8nEv1j_BC-fmZWHFe6jmU_zv-8s\&ab_channel=KartikArora)
  * Aditya Verma's Playlist: [TreeDP](https://www.youtube.com/watch?v=qZ5zayHSH2g\&list=PL_z\_8CaSLPWfxJPz2-YKqL9gXWdgrhvdn\&ab_channel=AdityaVerma)