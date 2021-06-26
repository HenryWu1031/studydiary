# LEETCODE刷题笔记之三

作者：why

#### 前情提要

最近做了一些关于链表的题目，所以想写一个刷题笔记，来记录一下我的刷题过程，并强化我对于链表的理解。

### 第一道题目

#### 问题描述

#### LEETCODE 206

反转一个单链表。

#### 输入输出

```
输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
```

#### 思路

我能想到的解决方案有两个大方向

- 首先是我们可以把这些节点的值全部用一个java的容器记录下来然后我们把这个容器中的值全部反转，然后我们再把它输出成一个单链表
- 另外的思路我们就采用链表的断开连接方式进行链表的反转
  - 我们可以使用递归的方法
  - 我们也可以使用迭代的方法来进行反转

#### 方法一 用容器记录并反转容器最后输出

```java
class Solution {
    public ListNode reverseList(ListNode head) {
        if(head==null)
			return null;
        if(head.next==null)
            return head;
		ArrayList<Integer> ans=new ArrayList<Integer>();
		while(head!=null) {
			ans.add(head.val);
			head=head.next;
		}
		ListNode pre=new ListNode(0);
		ListNode p=pre;
		for(int i=ans.size()-1;i>=0;i--) {
			p.next=new ListNode(ans.get(i));
			p=p.next;
		}
		return pre.next;
    }
}
```

这个方法是我本人觉得非常好理解的一种方法，我们也能成功的a掉这道题目，但是这个本质上其实没有用到单链表的性质去进行反转操作，所以笔者不推荐使用这样的方法去进行单链表的反转，而且我们可以很明显的看出这样的反转方法的效率是比较低的。

#### 方法二 递归方法进行链表的反转

```java
public ListNode reverseList(ListNode head) {
        if(head==null||head.next==null){
            return head;
        }
        ListNode newHead=reverseList(head.next);
        head.next.next=head;
        head.next=null;
        return newHead;
    }
```

说明：我们在这个方法中，使用了递归的思想，其实我们的想法很简单，我们要做的就是，我们现在的反转链表，就是把目前的第一个节点放到后面几个节点反转后的链表之后去。至于如何实现，主要就是这么几行代码

```java
head.next.next=head;
head.next=null;
```

如何去理解这个代码，比如我现在的链表是1→2→3→4→5，那么我的递归就是有一个这样的链表，它的开头是newHead，然后是5→4→3→2。这个时候我们怎么把1这个节点放到末尾，因为1的next再next是2的后面的值是null，我们这个时候把2后面的值变成1，所以有这么一行代码head.next.next=head; 之后我们要注意1后面的值不是null而是一堆值，那么我们要把它修改成null，即head.next=null;

#### 方法三 迭代的方法进行链表的反转

代码如下：

```java
public ListNode reverseList(ListNode head) {
        ListNode prev=null;
        ListNode curr=head;
        while(curr!=null){
            ListNode next=curr.next;
            curr.next=prev;
            prev=curr;
            curr=next;
        }
        return prev;
    }
```

说明：如何去理解这么一段代码呢？首先我们看到我们把两个链表的结点prev和curr分别是null和head来初始化。之后我们经过了一个迭代，这个迭代的过程是怎么样的我们慢慢来分析

- 假设我们的链表还是1→2→3→4→5

- 首先我们把next定为2（背后的一整条链为2→3→4→5）
- 然后我们把curr的下一个结点变成prev，得到curr变成1（1→null）
- 我们把prev变成（1→null）
- 然后把curr和next相同，都是（2→3→4→5）
- 之后就是迭代的过程，我写的简略一点
- next=（3→4→5）
- curr=（2→1→null）
- prev=（2→1→null）
- curr=（3→4→5）

所以这样以后就不是很难理解我们的算法的运行过程啦

#### 总结

我在单链表的理解方面还是存在很多不足的，希望这篇文章能够帮助自己和大家，一起变得更强！