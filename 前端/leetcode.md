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

