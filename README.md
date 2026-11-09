# LeetCode 35: Search Insert Position

## Problem Description

Given a sorted array of distinct integers `nums` and a target value `target`, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with **\(O(\log n)\)** runtime complexity.

### Examples

**Example 1:**
* **Input:** `nums = [1, 3, 5, 6]`, `target = 5`
* **Output:** `2`

**Example 2:**
* **Input:** `nums = [1, 3, 5, 6]`, `target = 2`
* **Output:** `1`

**Example 3:**
* **Input:** `nums = [1, 3, 5, 6]`, `target = 7`
* **Output:** `4`

---

## Solution Algorithm

The solution implements a classic **Binary Search** strategy to achieve the required logarithmic time complexity:

1. **Initialization:** Set two pointers, `left` at the beginning (`0`) and `right` at the end (`len(nums) - 1`) of the array.
2. **Search Loop:** While `left <= right`:
   * Compute the middle index: `mid = (left + right) // 2`.
   * If `nums[mid] == target`, the element is found, and we return `mid` immediately.
   * If `nums[mid] < target`, the target must lie in the right half, so we narrow our window by setting `left = mid + 1`.
   * If `nums[mid] > target`, the target must lie in the left half, so we narrow our window by setting `right = mid - 1`.
3. **Insertion Index:** If the loop terminates without finding the target, the pointers will cross. The `left` pointer will naturally settle at the exact index where the target should be inserted to maintain sorted order.

---

## Python Code Implementation

```python
from typing import List

class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums) - 1
        
        while left <= right:
            mid = (left + right) // 2
            
            if nums[mid] == target:
                return mid
            elif nums[mid] < target:
                left = mid + 1
            else:
                right = mid - 1
                
        # If not found, left will be the correct insertion index
        return left

# Local testing block
if __name__ == "__main__":
    solution = Solution()
    
    # Test case 1: Target exists in the array
    print(solution.searchInsert([1, 3, 5, 6], 5))  # Expected Output: 2
    
    # Test case 2: Target does not exist (inserted in the middle)
    print(solution.searchInsert([1, 3, 5, 6], 2))  # Expected Output: 1
    
    # Test case 3: Target does not exist (inserted at the end)
    print(solution.searchInsert([1, 3, 5, 6], 7))  # Expected Output: 4
```

---

## Complexity Analysis

* **Time Complexity:** $\mathcal{O}(\log n)$ — The search space is divided in half during each iteration of the while loop.
* **Space Complexity:** $\mathcal{O}(1)$ — The algorithm operates in-place, relying only on a few pointer variables (`left`, `right`, `mid`).
