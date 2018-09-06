# 4. Median of Two Sorted Arrays

## Question

There are two sorted arrays nums1 and nums2 of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

You may assume nums1 and nums2 cannot be both empty.

Example 1:

```txt
nums1 = [1, 3]
nums2 = [2]

The median is 2.0
```

Example 2:

```txt
nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5
```

## Ans

```js
var findMedianSortedArrays = function (nums1, nums2) {
  const m = nums1.concat(nums2).sort((a, b) => a - b)
  const mIndex = ~~((m.length - 1) / 2)
  const result = m.length % 2 === 1 ? m[mIndex] : (m[mIndex] + m[mIndex + 1]) / 2

  return result
}
```

## Ans-Improve-Fast

```js
var findMedianSortedArrays = function (nums1, nums2) {
  if (nums1.length > nums2.length) {
    let temp = nums1
    nums1 = nums2
    nums2 = temp
  }

  let m = nums1.length // m should be less than or equal to n
  let n = nums2.length
  let minIdx = 0
  let maxIdx = m
  let maxLeft
  let minRight

  while (minIdx <= maxIdx) {
    let i = Math.floor((minIdx + maxIdx) / 2)
    let j = Math.floor((m + n + 1) / 2) - i

    if (i > 0 && nums1[i - 1] > nums2[j]) {
      maxIdx = i - 1
    } else if (i < m && nums1[i] < nums2[j - 1]) {
      minIdx = i + 1
    } else {
      if (i === 0) {
        maxLeft = nums2[j - 1]
      } else if (j === 0) {
        maxLeft = nums1[i - 1]
      } else {
        maxLeft = Math.max(nums1[i - 1], nums2[j - 1])
      }

      if ((m + n) % 2) {
        return maxLeft
      }

      if (i === m) {
        minRight = nums2[j]
      } else if (j === n) {
        minRight = nums1[i]
      } else {
        minRight = Math.min(nums1[i], nums2[j])
      }

      return (maxLeft + minRight) / 2
    }
  }
}
```
