#  最近的请求次数

> 	写一个 RecentCounter 类来计算特定时间范围内最近的请求。
>
> 请你实现 RecentCounter 类：
>
> RecentCounter() 初始化计数器，请求数为 0 。
> int ping(int t) 在时间 t 添加一个新请求，其中 t 表示以毫秒为单位的某个时间，并返回过去 3000 毫秒内发生的所有请求数（包括新请求）。确切地说，返回在 [t-3000, t] 内发生的请求数。
> 保证每次对 ping 的调用都使用比之前更大的 t 值。

~~~javascript
var RecentCounter = function() {
	this.q = [];
};

RecentCounter.prototype.ping = function(t) {
	this.q.push(t);
	while (this.q[0] < t - 3000) {
		this.q.shift();
	}
	return this.q.length;
};
~~~

#  20.有效的括号

> 给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。
>
> 有效字符串需满足：
>
> 左括号必须用相同类型的右括号闭合。
> 左括号必须以正确的顺序闭合。
> 注意空字符串可被认为是有效字符串。

~~~javascript
/**
 * 方法1
 */
var isValid = function(s) {
	if (s.length % 2 === 1) {
		return false;
	}
	const statck = [];
	for (let i = 0; i < s.length; i++) {
		const c = s[i];
		if (c === '(' || c === '{' || c === '[') {
			statck.push(s[i]);
		} else {
			let t = statck[statck.length - 1];
			if ((c === ')' && t === '(') || (c === ']' && t === '[') || (c === '}' && t === '{')) {
				statck.pop();
			} else {
				return false;
			}
		}
	}
	return statck.length === 0;
};
/**
 * 方法2
 */
var isValid = function(s) {
	if (s.length % 2 === 1) {
		return false;
	}
	const statck = [];
	let map = new Map();
	map.set('(', ')');
	map.set('[', ']');
	map.set('{', '}');
	for (let i = 0; i < s.length; i++) {
		const c = s[i];
		if (map.get(c)) {
			statck.push(s[i]);
		} else {
			let t = statck[statck.length - 1];
			if (map.get(t) === c) {
				statck.pop();
			} else {
				return false;
			}
		}
	}
	return statck.length === 0;
};


~~~

#  环形链表

> 给定一个链表，判断链表中是否有环。
>
> 如果链表中有某个节点，可以通过连续跟踪 next 指针再次到达，则链表中存在环。 为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。注意：pos 不作为参数进行传递，仅仅是为了标识链表的实际情况。
>
> 如果链表中存在环，则返回 true 。 否则，返回 false 。

~~~javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */

/**
 * @param {ListNode} head
 * @return {boolean}
 */
var hasCycle = function(head) {
	let p1 = head;
	let p2 = head;
	while (p1 && p2 && p2.next) {
		p1 = p1.next;
		p2 = p2.next.next;
		if (p1 === p2) {
			return true;
		}
	}
	return false;
};
~~~

#  349.两个数组的交集

> 给定两个数组，编写一个函数来计算它们的交集。
>
> **说明：**
>
> - 输出结果中的每个元素一定是唯一的。
> - 我们可以不考虑输出结果的顺序。

~~~javascript
/**
 * 方法一：set
 */
var intersection = function(nums1, nums2) {
	return [ ...new Set(nums1) ].filter((_value) => nums2.includes(_value));
};

/**
 * 方法二：map
 */
var intersection = function(nums1, nums2) {
	let map = new Map();
	nums1.forEach((v) => {
		map.set(v, true);
	});
	let res = [];
	nums2.forEach((v) => {
		if (map.get(v)) {
			res.push(v);
			map.delete(v);
		}
	});
	return res;
};
~~~

# 1.两数之和

> 给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。
>
> 你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。
>
> 示例:
>
> 给定 nums = [2, 7, 11, 15], target = 9
>
> 因为 nums[0] + nums[1] = 2 + 7 = 9
> 所以返回 [0, 1]

~~~~javascript
var twoSum = function(nums, target) {
	let map = new Map();
	for (let i = 0; i < nums.length; i++) {
		let n = nums[i];
		let t = target - n;
		if (map.has(t)) {
			return [ map.get(t), i ];
		} else {
			map.set(n, i);
		}
	}
};
~~~~

# 3.无重复字符串最长子串

> 给定一个字符串，请你找出其中不含有重复字符的 **最长子串** 的长度。
>
> 示例 1:
>
> 输入: "abcabcbb"
> 输出: 3 
> 解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
> 示例 2:
>
> 输入: "bbbbb"
> 输出: 1
> 解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
> 示例 3:
>
> 输入: "pwwkew"
> 输出: 3
> 解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
>      请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。

~~~javascript
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function(s) {
	let l = 0;
	let res = 0;
	let map = new Map();
	for (let r = 0; r < s.length; r++) {
		if (map.has(s[r]) && map.get(s[r]) >= l) {
			l = map.get(s[r]) + 1;
		}
		res = Math.max(res, r - l + 1);
		map.set(s[r], r);
	}
	return res;
};
~~~

# 76. 最小覆盖子串

> 给你一个字符串 S、一个字符串 T 。请你设计一种算法，可以在 O(n) 的时间复杂度内，从字符串 S 里面找出：包含 T 所有字符的最小子串。
>
>  
>
> 示例：
>
> 输入：S = "ADOBECODEBANC", T = "ABC"
> 输出："BANC"
>
>
> 提示：
>
> 如果 S 中不存这样的子串，则返回空字符串 ""。
> 如果 S 中存在这样的子串，我们保证它是唯一的答案。

~~~javascript
/**
 * @param {string} s
 * @param {string} t
 * @return {string}
 */
var minWindow = function(s, t) {
	let l = 0;
	let r = 0;
	let need = new Map();
	for (let c of t) {
		need.set(c, need.has(c) ? need.get(c) + 1 : 1);
	}
	let needType = need.size;
	let res = '';
	while (r < s.length) {
		let c = s[r];
		if (need.has(c)) {
			need.set(c, need.get(c) - 1);
			if (need.get(c) === 0) {
				needType -= 1;
			}
		}
		while (needType === 0) {
			let newRes = s.substring(l, r + 1);
			if (!res || newRes.length < res.length) {
				res = newRes;
			}
			let c2 = s[l];
			if (need.has(c2)) {
				need.set(c2, need.get(c2) + 1);
				if (need.get(c2) === 1) {
					needType += 1;
				}
			}
			l += 1;
		}
		r += 1;
	}
	return res;
};
~~~

#  104.二叉树最大深度

> 给定一个二叉树，找出其最大深度。
>
> 二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。
>
> 说明: 叶子节点是指没有子节点的节点。
>
> 示例：
> 给定二叉树 [3,9,20,null,null,15,7]，
>
>     3
>    / \
>   9  20
>     /  \
>    15   7
> 返回它的最大深度 3 。

~~~javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var maxDepth = function(root) {
	let res = 0;
	const dfs = function(n, l) {
		if (!n) {
			return;
		}
		if (!n.left && !n.right) {
			res = Math.max(res, l);
		}
		dfs(n.left, l + 1);
		dfs(n.right, l + 1);
	};
	dfs(root, 1);
	return res;
};

~~~

#  111.二叉树的最小深度

> 给定一个二叉树，找出其最小深度。
>
> 最小深度是从根节点到最近叶子节点的最短路径上的节点数量。
>
> 说明：叶子节点是指没有子节点的节点。
>
>  
>
> 示例 1：
>
>
> 输入：root = [3,9,20,null,null,15,7]
> 输出：2
> 示例 2：
>
> 输入：root = [2,null,3,null,4,null,5,null,6]
> 输出：5
>
>
> 提示：
>
> 树中节点数的范围在 [0, 105] 内
> -1000 <= Node.val <= 1000

~~~javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var minDepth = function(root) {
	if (!root) {
		return 0;
	}
	let q = [ [ root, 1 ] ];
	while (q.length) {
		const [ n, l ] = q.shift();
		if (!n.left && !n.right) {
			return l;
		}
		if (n.left) {
			q.push([ n.left, l + 1 ]);
		}
		if (n.right) {
			q.push([ n.right, l + 1 ]);
		}
	}
};
~~~

# 二叉树的层序遍历

> 给你一个二叉树，请你返回其按 层序遍历 得到的节点值。 （即逐层地，从左到右访问所有节点）。
>
>  
>
> 示例：
> 二叉树：[3,9,20,null,null,15,7],
>
>     3
>    / \
>   9  20
>     /  \
>    15   7
> 返回其层次遍历结果：
>
> [
>   [3],
>   [9,20],
>   [15,7]
> ]

~~~javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * 方法1
 * @param {TreeNode} root
 * @return {number[][]}
 */
var levelOrder = function(root) {
	if (!root) {
		return [];
	}
	const q = [ [ root, 0 ] ];
	const res = [];
	while (q.length) {
		const [ n, leave ] = q.shift();
		if (!res[leave]) {
			res.push([ n.val ]);
		} else {
			res[leave].push(n.val);
		}
		if (n.left) {
			q.push([ n.left, leave + 1 ]);
		}
		if (n.right) {
			q.push([ n.right, leave + 1 ]);
		}
	}
	return res;
};
/**
 * 方法2
 * @param {TreeNode} root
 * @return {number[][]}
 */
var levelOrder = function(root) {
	if (!root) {
		return [];
	}
	const q = [ root ];
	const res = [];
	while (q.length) {
		let len = q.length;
		res.push([]);
		while (len--) {
			const n = q.shift();
			res[res.length - 1].push(n.val);
			if (n.left) {
				q.push(n.left);
			}
			if (n.right) {
				q.push(n.right);
			}
		}
	}
	return res;
};

~~~

# 94.二叉树中序遍历

> 给定一个二叉树，返回它的中序 遍历。
>
> 示例:
>
> 输入: [1,null,2,3]
>    1
>     \
>      2
>     /
>    3
>
> 输出: [1,3,2]
> 进阶: 递归算法很简单，你可以通过迭代算法完成吗

~~~javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * 方法1:递归算法
 * @param {TreeNode} root
 * @return {number[]}
 */
var inorderTraversal = function(root) {
	let res = [];
	const rec = (n) => {
		if (!n) return;
		rec(n.left);
		res.push(n.val);
		rec(n.right);
	};
	rec(root);
	return res;
};
/**
 * 方法2:非递归
 * @param {TreeNode} root
 * @return {number[]}
 */
var inorderTraversal = function(root) {
	const res = [];
	const stack = [];
	let p = root;
	while (stack.length || p) {
		while (p) {
			stack.push(p);
			p = p.left;
		}
		const n = stack.pop();
		res.push(n.val);
		p = n.right;
	}

	return res;
};

~~~

# 112.路径总和

> 给定一个二叉树和一个目标和，判断该树中是否存在根节点到叶子节点的路径，这条路径上所有节点值相加等于目标和。
>
> 说明: 叶子节点是指没有子节点的节点。
>
> 示例: 
> 给定如下二叉树，以及目标和 sum = 22，
>
>               5
>              / \
>             4   8
>            /   / \
>           11  13  4
>          /  \      \
>         7    2      1
> 返回 true, 因为存在目标和为 22 的根节点到叶子节点的路径 5->4->11->2。

~~~javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @param {number} sum
 * @return {boolean}
 */
var hasPathSum = function(root, s) {
	let res = false;
	if (!root) {
		return res;
	}
	const dfs = (n, sum) => {
		if (!n.left && !n.right && s === sum) {
			res = true;
		}
		if (n.left) {
			dfs(n.left, sum + n.left.val);
		}
		if (n.right) {
			dfs(n.right, sum + n.right.val);
		}
	};
	dfs(root, root.val);
	return res;
};
~~~

# 65.有效数字

> 验证给定的字符串是否可以解释为十进制数字。
>
> 例如:
>
> "0" => true
> " 0.1 " => true
> "abc" => false
> "1 a" => false
> "2e10" => true
> " -90e3   " => true
> " 1e" => false
> "e3" => false
> " 6e-1" => true
> " 99e2.5 " => false
> "53.5e93" => true
> " --6 " => false
> "-+3" => false
> "95a54e53" => false
>
> 说明: 我们有意将问题陈述地比较模糊。在实现代码之前，你应当事先思考所有可能的情况。这里给出一份可能存在于有效十进制数字中的字符列表：
>
> 数字 0-9
> 指数 - "e"
> 正/负号 - "+"/"-"
> 小数点 - "."
> 当然，在输入中，这些字符的上下文也很重要。

~~~javascript
/**
 * @param {string} s
 * @return {boolean}
 */
var isNumber = function(s) {
	const graph = {
		0: { balck: 0, sign: 1, '.': 2, digit: 6 },
		1: { digit: 6, '.': 2 },
		2: { digit: 3 },
		3: { digit: 3, e: 4 },
		4: { digit: 5, sign: 7 },
		5: { digit: 5 },
		6: { digit: 6, '.': 3, e: 4 },
		7: { digit: 5 }
	};

	let state = 0;
	for (let c of s.trim()) {
		if (c >= '0' && c <= '9') {
			c = 'digit';
		} else if (c === ' ') {
			c = 'black';
		} else if (c === '+' || c === '-') {
			c = 'sign';
		}
		state = graph[state][c];
		if (state === undefined) {
			return false;
		}
	}

	if (state === 3 || state === 5 || state === 6) {
		return true;
	}

	return false;
};
~~~

# 417.太平洋大西洋水流问题

> 给定一个 m x n 的非负整数矩阵来表示一片大陆上各个单元格的高度。“太平洋”处于大陆的左边界和上边界，而“大西洋”处于大陆的右边界和下边界。
>
> 规定水流只能按照上、下、左、右四个方向流动，且只能从高到低或者在同等高度上流动。
>
> 请找出那些水流既可以流动到“太平洋”，又能流动到“大西洋”的陆地单元的坐标。
>
>  
>
> 提示：
>
> 输出坐标的顺序不重要
> m 和 n 都小于150
>
>
> 示例：
>
>  
>
> 给定下面的 5x5 矩阵:
>
>   太平洋 ~   ~   ~   ~   ~ 
>        ~  1   2   2   3  (5) *
>        ~  3   2   3  (4) (4) *
>        ~  2   4  (5)  3   1  *
>        ~ (6) (7)  1   4   5  *
>        ~ (5)  1   1   2   4  *
>           *   *   *   *   * 大西洋
>
> 返回:
>
> [[0, 4], [1, 3], [1, 4], [2, 2], [3, 0], [3, 1], [4, 0]] (上图中带括号的单元).

~~~javascript
/**
 * @param {number[][]} matrix
 * @return {number[][]}
 */
var pacificAtlantic = function(matrix) {
	if (!matrix || !matrix[0]) {
		return [];
	}
	const m = matrix.length;
	const n = matrix[0].length;
	const flow1 = Array.from({ length: m }, () => {
		return new Array(n).fill(false);
	});
	const flow2 = Array.from({ length: m }, () => {
		return new Array(n).fill(false);
	});

	const dfs = (r, c, flow) => {
		flow[r][c] = true;
		[ [ r - 1, c ], [ r + 1, c ], [ r, c - 1 ], [ r, c + 1 ] ].forEach(([ nr, nc ]) => {
			if (nr >= 0 && nr < m && nc >= 0 && nc < n && !flow[nr][nc] && matrix[nr][nc] >= matrix[r][c]) {
				dfs(nr, nc, flow);
			}
		});
	};

	for (let r = 0; r < m; r += 1) {
		dfs(r, 0, flow1);
		dfs(r, n - 1, flow2);
	}

	for (let c = 0; c < n; c += 1) {
		dfs(0, c, flow1);
		dfs(m - 1, c, flow2);
	}

	const res = [];
	for (let r = 0; r < m; r += 1) {
		for (let c = 0; c < n; c += 1) {
			if (flow1[r][c] && flow2[r][c]) {
				res.push([ r, c ]);
			}
		}
	}
	return res;
};

~~~

# 133.克隆图

> 给你无向 连通 图中一个节点的引用，请你返回该图的 深拷贝（克隆）。
>
> 图中的每个节点都包含它的值 val（int） 和其邻居的列表（list[Node]）。
>
> class Node {
>     public int val;
>     public List<Node> neighbors;
> }
>
>
> 测试用例格式：
>
> 简单起见，每个节点的值都和它的索引相同。例如，第一个节点值为 1（val = 1），第二个节点值为 2（val = 2），以此类推。该图在测试用例中使用邻接列表表示。
>
> 邻接列表 是用于表示有限图的无序列表的集合。每个列表都描述了图中节点的邻居集。
>
> 给定节点将始终是图中的第一个节点（值为 1）。你必须将 给定节点的拷贝 作为对克隆图的引用返回。

~~~javascript
/**
 * // Definition for a Node.
 * function Node(val, neighbors) {
 *    this.val = val === undefined ? 0 : val;
 *    this.neighbors = neighbors === undefined ? [] : neighbors;
 * };
 */

/**
 * @param {Node} node
 * @return {Node}
 */
var cloneGraph = function(node) {
	if (!node) {
		return;
	}
	const visited = new Map();
	const dfs = (n) => {
		const nCopy = new Node(n.val);
		visited.set(n, nCopy);
		(n.neighbors || []).forEach((_v) => {
			if (!visited.has(_v)) {
				dfs(_v);
			}
			nCopy.neighbors.push(visited.get(_v));
		});
	};
	dfs(node);

	return visited.get(node);
};

~~~

# 215.数组中的第K个元素

> 在未排序的数组中找到第 k 个最大的元素。请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。
>
> 示例 1:
>
> 输入: [3,2,1,5,6,4] 和 k = 2
> 输出: 5
> 示例 2:
>
> 输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
> 输出: 4
> 说明:
>
> 你可以假设 k 总是有效的，且 1 ≤ k ≤ 数组的长度。

~~~javascript
class MinHeap {
	constructor() {
		this.heap = [];
	}
    getParentIndex(i) {
		return (i - 1) >> 1;
	}
	getLeftIndex(i) {
		return i * 2 + 1;
	}
	getRightIndex(i) {
		return i * 2 + 2;
	}
	swap(i1, i2) {
		const temp = this.heap[i1];
		this.heap[i1] = this.heap[i2];
		this.heap[i2] = temp;
	}
	shiftUp(index) {
		if (index == 0) {
			return;
		}
		const parentIndex = this.getParentIndex(index);
		if (this.heap[parentIndex] > this.heap[index]) {
			this.swap(parentIndex, index);
			this.shiftUp(parentIndex);
		}
	}
	shiftDown(index) {
		const leftIndex = this.getLeftIndex(index);
		const rightIndex = this.getRightIndex(index);
		if (this.heap[leftIndex] < this.heap[index]) {
			this.swap(leftIndex, index);
			this.shiftDown(leftIndex);
		}
		if (this.heap[rightIndex] < this.heap[index]) {
			this.swap(rightIndex, index);
			this.shiftDown(rightIndex);
		}
	}
	/**
     * 插入数据
     * @param {插入数据值} value 
     */
	insert(value) {
		this.heap.push(value);
		this.shiftUp(this.heap.length - 1);
	}
	/**
     * 删除堆顶
     * @param {} value 
     */
	pop(value) {
		this.heap[0] = this.heap.pop();
		this.shiftDown(0);
	}
	/**
     * 获取堆顶元素
     */
	peek() {
		return this.heap[0];
	}
	/**
    * 获取堆大小
    */
	size() {
		return this.heap.length;
	}
}

/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var findKthLargest = function(nums, k) {
    const h = new MinHeap();
    nums.forEach(_v => {
        h.insert(_v);
        if(h.size() > k){
            h.pop();
        }
    })
    return h.peek();
};
~~~

# 347.前 K 个高频元素

> 给定一个非空的整数数组，返回其中出现频率前 k 高的元素。
>
>  
>
> 示例 1:
>
> 输入: nums = [1,1,1,2,2,3], k = 2
> 输出: [1,2]
> 示例 2:
>
> 输入: nums = [1], k = 1
> 输出: [1]
>
>
> 提示：
>
> 你可以假设给定的 k 总是合理的，且 1 ≤ k ≤ 数组中不相同的元素的个数。
> 你的算法的时间复杂度必须优于 O(n log n) , n 是数组的大小。
> 题目数据保证答案唯一，换句话说，数组中前 k 个高频元素的集合是唯一的。
> 你可以按任意顺序返回答案。

~~~javascript
class MinHeap {
	constructor() {
		this.heap = [];
	}
	getParentIndex(i) {
		return (i - 1) >> 1;
	}
	getLeftIndex(i) {
		return i * 2 + 1;
	}
	getRightIndex(i) {
		return i * 2 + 2;
	}
	swap(i1, i2) {
		const temp = this.heap[i1];
		this.heap[i1] = this.heap[i2];
		this.heap[i2] = temp;
	}
	shiftUp(index) {
		if (index == 0) {
			return;
		}
		const parentIndex = this.getParentIndex(index);
		if (this.heap[parentIndex] && this.heap[parentIndex].value > this.heap[index].value) {
			this.swap(parentIndex, index);
			this.shiftUp(parentIndex);
		}
	}
	shiftDown(index) {
		const leftIndex = this.getLeftIndex(index);
		const rightIndex = this.getRightIndex(index);
		if (this.heap[leftIndex] && this.heap[leftIndex].value < this.heap[index].value) {
			this.swap(leftIndex, index);
			this.shiftDown(leftIndex);
		}
		if (this.heap[rightIndex] && this.heap[rightIndex].value < this.heap[index].value) {
			this.swap(rightIndex, index);
			this.shiftDown(rightIndex);
		}
	}
	/**
     * 插入数据
     * @param {插入数据值} value 
     */
	insert(value) {
		this.heap.push(value);
		this.shiftUp(this.heap.length - 1);
	}
	/**
     * 删除堆顶
     * @param {} value 
     */
	pop(value) {
		this.heap[0] = this.heap.pop();
		this.shiftDown(0);
	}
	/**
     * 获取堆顶元素
     */
	peek() {
		return this.heap[0];
	}
	/**
    * 获取堆大小
    */
	size() {
		return this.heap.length;
	}
}
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number[]}
 */
var topKFrequent = function(nums, k) {
	const map = new Map();
	nums.forEach((_v) => {
		map.set(_v, map.has(_v) ? map.get(_v) + 1 : 1);
	});
	const h = new MinHeap();
	map.forEach((value, key) => {
		h.insert({ value, key });
		if (h.size() > k) {
			h.pop();
		}
	});
	return h.heap.map((a) => a.key);
};
~~~

