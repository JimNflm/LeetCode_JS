# 1. Two Sum

## Question

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:

```txt
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

## Ans

```js
var twoSum = function (nums, target) {
  for (let key, obj = {}, i = 0, len = nums.length; i < len; i++) {
    key = target - nums[i]
    if (obj.hasOwnProperty(key)) {
      return [obj[key], i]
    }
    obj[nums[i]] = i
  }
}

```