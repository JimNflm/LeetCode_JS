# 2. Add Two Numbers

## Question

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example:

```txt
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

## Ans

```js
var addTwoNumbers = function (l1, l2) {
  let res = new ListNode(null)
  let item = res
  let carry = 0
  let prev

  while (l1 || l2) {
    let sum = (l1 ? l1.val : 0) + (l2 ? l2.val : 0) + carry
    item.val = sum % 10
    carry = ~~(sum / 10)

    item.next = new ListNode(null)
    prev = item
    item = item.next

    l1 = l1 ? l1.next : null
    l2 = l2 ? l2.next : null
  }

  if (carry > 0) {
    item.val = carry
  } else {
    prev.next = null
  }

  return res
}
```

### Test

```js
function ListNode (val) {
  this.val = val
  this.next = null
}

function createNode (ary) {
  let res = new ListNode(null)
  let item = res
  ary.map((e) => {
    item.val = e
    item.next = new ListNode(null)
    item = item.next
  })

  return res
}

function test () {
  const l1 = createNode([1])
  const l2 = createNode([9, 9])
  const result = addTwoNumbers(l1, l2)
  console.log(`${result.val}, ${result.next.val}, ${result.next.next.val}`)
}

test()

```
