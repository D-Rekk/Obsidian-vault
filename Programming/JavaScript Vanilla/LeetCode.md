# LeetCode

Created: November 15, 2022 11:59 AM
Status: Open
Updated: January 23, 2023 7:28 PM

---

### 2225. Find players with Zero or One Losses

- Description
    
    You are given an integer array `matches` where `matches[i] = [winneri, loseri]` indicates that the player `winneri` defeated player `loseri` in a match.
    
    Return *a list* `answer` *of size* `2` *where:*
    
    - `answer[0]` is a list of all players that have **not** lost any matches.
    - `answer[1]` is a list of all players that have lost exactly **one** match.
    
    The values in the two lists should be returned in **increasing** order.
    

```jsx
var findWinners = function(matches) {
    const wins = new Map();
    const losses = new Map();
    
    for(const match of matches) {
        const [winner, loser] = match;
        
        wins.set(winner, (wins.get(winner) || 0) + 1);
        losses.set(loser, (losses.get(loser) || 0) + 1);
    }
    
    const answer = [[],[]];
    
    for(const [winner, value] of wins) {
        if(!losses.get(winner)) {
            answer[0].push(winner);
        }
    }
    
    for(const [loser, value] of losses) {
        if(value === 1) {
            answer[1].push(loser);
        }
    }
    
    answer[0].sort((a, b) => a-b); // increasing
    answer[1].sort((a, b) => a-b); // increasing 
    
    return answer;
    
};
```

### 222. Count Complete Tree Nodes

- Description
    
    Given the `root` of a **complete** binary tree, return the number of the nodes in the tree.
    
    According to **[Wikipedia](http://en.wikipedia.org/wiki/Binary_tree#Types_of_binary_trees)**, every level, except possibly the last, is completely filled in a complete binary tree, and all nodes in the last level are as far left as possible. It can have between `1` and `2h` nodes inclusive at the last level `h`.
    
    Design an algorithm that runs in less than `O(n)` time complexity.
    

```jsx
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
 
var countNodes = function(root) {
    if (!root) return 0
    return ( 1 + countNodes(root.left) + countNodes(root.right))
}
```

---

### 947. Most Stones Removes with Same Row or Column

- Description
    
    On a 2D plane, we place `n` stones at some integer coordinate points. Each coordinate point may have at most one stone.
    
    A stone can be removed if it shares either **the same row or the same column** as another stone that has not been removed.
    
    Given an array `stones` of length `n` where `stones[i] = [xi, yi]` represents the location of the `ith` stone, return *the largest possible number of stones that can be removed*.
    

*What is the minimum number of stones we can have remaining?*
We can find the number of remaining stones by finding the number of disjointed set. We initialize 

```jsx
var removeStones = function(stones) {
    const rows = new Map();
    const cols = new Map();

		/*For every [r,c], we Set where that row/col appears
			row{0: c0, c1, c2; 
					1: c0, c2;
			set(r, getSet() OR new Set()) then .add(c)
			}
			col{...} 
		  Setting row -> 
				if row at r doesn't exist, create next Set()
				else get that row(r)
			Then add(c). Think of it as array.push
			Setting col -> Same as above
		*/
    for (const [r, c] of stones) {
        rows.set(r, (rows.get(r) || new Set()).add(c));
        cols.set(c, (cols.get(c) || new Set()).add(r));
    }
    const visited = new Set();

    const dfs = (i, j) => {        
        const key = `${i}-${j}`;
        if (visited.has(key)) return;
        visited.add(key);
        const adjRow = rows.get(i);
        for (const col of adjRow) {
            dfs(i, col);
        }
        const adjCol = cols.get(j);
        for (const row of adjCol) {
            dfs(row, j);
        }
    }
    
    let remainingStones = 0;
    for (const [r, c] of stones) {
        const key = `${r}-${c}`;
        if (visited.has(key)) continue;        
        dfs(r,c);
        remainingStones++;        
    }
    return stones.length - remainingStones;
};
```

---

<aside>
💡

</aside>

 Something

---