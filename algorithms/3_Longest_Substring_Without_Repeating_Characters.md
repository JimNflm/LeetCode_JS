# 3. Longest Substring Without Repeating Characters

## Question

Given a string, find the length of the longest substring without repeating characters.

Example 1:

```txt
Input: "abcabcbb"
Output: 3
Explanation: The answer is "abc", which the length is 3.
```

Example 2:

```txt
Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

Example 3:

```txt
Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

## Ans

```js
var lengthOfLongestSubstring = function (s) {
  const ary = [...s]
  let result = 0
  let r = []

  for (let i = 0, j = 0; i < ary.length;) {
    if (!r.includes(ary[i])) {
      r.push(ary[i])
      i++
      result = Math.max(result, i - j)
    } else {
      r.splice(r.indexOf(ary[j]), 1)
      j++
    }
  }

  return result
}
```

## Ans-Improve-Faster

```js
var lengthOfLongestSubstring = function (s) {
  const ary = [...s]
  let result = 0
  let r = []

  ary.forEach(e => {
    let i = r.indexOf(e)
    if (i === -1) {
      r.push(e)
    } else {
      if (r.length > result) {
        result = r.length
      }
      r.splice(0, i + 1)
      r.push(e)
    }
  })

  if (r.length > result) {
    result = r.length
  }

  return result
}
```
