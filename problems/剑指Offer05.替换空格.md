# 题目：剑指Offer 05.替换空格

[力扣题目链接](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/)

请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

示例 1： 
输入：s = "We are happy."    
输出："We%20are%20happy."     

# 思路

如果想把这道题目做到极致，就不要只用额外的辅助空间了！

首先扩充数组到每个空格替换成"%20"之后的大小。

然后从后向前替换空格，也就是双指针法，过程如下：

i指向新长度的末尾，j指向旧长度的末尾。

![替换空格](https://tva1.sinaimg.cn/large/e6c9d24ely1go6qmevhgpg20du09m4qp.gif)

有同学问了，为什么要从后向前填充，从前向后填充不行么？

从前向后填充就是$O(n^2)$的算法了，因为每次添加元素都要将添加元素之后的所有元素向后移动。

**其实很多数组填充类的问题，都可以先预先给数组扩容带填充后的大小，然后在从后向前进行操作。**

这么做有两个好处：

1. 不用申请新数组。
2. 从后向前填充元素，避免了从前先后填充元素要来的 每次添加元素都要将添加元素之后的所有元素向后移动。

时间复杂度，空间复杂度均超过100%的用户。

<img src='https://code-thinking.cdn.bcebos.com/pics/剑指Offer05.替换空格.png' width=600> </img></div>

C++代码如下：

```js
/**
 * @param {string} s
 * @return {string}
 */
//  思路：用双指针法。先获取空格的数量，然后依据数量来扩容数组，左指针指向原数组的最后一个元素，右指针指向扩容后的最后一个元素。依次替换，碰到空格就替换成%02
var replaceSpace = function(s) {
  // 1. 将字符串转换为数组，然后获取其中空格的数量
  let strArr = Array.from(s)
  let count = 0 // 用来记录空格数量

  for(let i=0; i < strArr.length; i++) {
    if(strArr[i] === " ") {
      count++
    }
  }

  // 2. 将数组扩容，并且设置好左指针和右指针
  let left = strArr.length - 1
  let right = strArr.length - 1 + count * 2 // 将1个空格替换为%02，就是将1个东西替换为3个东西，只需要增加两个位置

  while(left >= 0) {
    if(strArr[left] === ' ') {
      strArr[right--] = '0'
      strArr[right--] = '2'
      strArr[right--] = '%'
      left--
    }else {
      strArr[right--] = strArr[left--]
    }
  }

  return strArr.join('') // 将最终替换完的数组转换为字符串输出
};
```

此时算上本题，我们已经做了七道双指针相关的题目了分别是：

* [27.移除元素](https://programmercarl.com/0027.移除元素.html)
* [15.三数之和](https://programmercarl.com/0015.三数之和.html)
* [18.四数之和](https://programmercarl.com/0018.四数之和.html)
* [206.翻转链表](https://programmercarl.com/0206.翻转链表.html)
* [142.环形链表II](https://programmercarl.com/0142.环形链表II.html)
* [344.反转字符串](https://programmercarl.com/0344.反转字符串.html)

# 拓展

这里也给大家拓展一下字符串和数组有什么差别，

字符串是若干字符组成的有限序列，也可以理解为是一个字符数组，但是很多语言对字符串做了特殊的规定，接下来我来说一说C/C++中的字符串。

在C语言中，把一个字符串存入一个数组时，也把结束符 '\0'存入数组，并以此作为该字符串是否结束的标志。

例如这段代码：

```
char a[5] = "asd";
for (int i = 0; a[i] != '\0'; i++) {
}
```

在C++中，提供一个string类，string类会提供 size接口，可以用来判断string类字符串是否结束，就不用'\0'来判断是否结束。

例如这段代码:

```
string a = "asd";
for (int i = 0; i < a.size(); i++) {
}
```

那么vector< char > 和 string 又有什么区别呢？

其实在基本操作上没有区别，但是 string提供更多的字符串处理的相关接口，例如string 重载了+，而vector却没有。

所以想处理字符串，我们还是会定义一个string类型。
