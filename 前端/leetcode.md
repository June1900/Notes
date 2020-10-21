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

#  有效的括号

> 给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。
>
> 有效字符串需满足：
>
> 左括号必须用相同类型的右括号闭合。
> 左括号必须以正确的顺序闭合。
> 注意空字符串可被认为是有效字符串。

~~~javascript
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

