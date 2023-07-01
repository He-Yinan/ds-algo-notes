# LC88. Merge Sorted Array

- Difficulty: Easy
- Type: Array, Two Pointers, Sorting

## Question

You are given two integer arrays `nums1` and `nums2`, sorted in non-decreasing order, and two integers m and n, representing the number of elements in `nums1` and `nums2` respectively.

Merge `nums1` and `nums2` into a single array sorted in non-decreasing order.

The final sorted array should not be returned by the function, but instead be stored inside the array `nums1`. To accommodate this, `nums1` has a length of m + n, where the first m elements denote the elements that should be merged, and the last n elements are set to 0 and should be ignored. `nums2` has a length of n.

**Example 1:**

Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3

Output: [1,2,2,3,5,6]

Explanation: The arrays we are merging are [1,2,3] and [2,5,6].
The result of the merge is [1,2,2,3,5,6] with the underlined elements coming from nums1.

**Example 2:**

Input: nums1 = [1], m = 1, nums2 = [], n = 0

Output: [1]

Explanation: The arrays we are merging are [1] and []. The result of the merge is [1].

**Example 3:**

Input: nums1 = [0], m = 0, nums2 = [1], n = 1

Output: [1]

Explanation: The arrays we are merging are [] and [1]. The result of the merge is [1]. Note that because m = 0, there are no elements in nums1. The 0 is only there to ensure the merge result can fit in nums1.

**Constraints:**

- nums1.length == m + n
- nums2.length == n
- 0 <= m, n <= 200
- 1 <= m + n <= 200
- -109 <= nums1[i], nums2[j] <= 109

Follow up: Can you come up with an algorithm that runs in `O(m + n)` time?

## Solution

- Time complexity: `O(m + n)`
- Space complexity: `O(1)`

### Train of Thought

We know that `nums1` has padded placeholder zeros on the right. So we can start with the largest numbers from two arrays and work our way down to find the larger number to fill in the positions in `nums1`. This way, we do not need to use additional storage.

We need 3 pointers. `nums1_ptr` to store the location in `nums1`, `nums2_ptr` to store the location in `nums2`, and `cur_ptr` to store the position we want to fill in `nums1`.

### Python

```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """

        nums1_ptr = len(nums1) - 1 - len(nums2)
        nums2_ptr = len(nums2) - 1
        cur_ptr = len(nums1) - 1

        while nums1_ptr >= 0 and nums2_ptr >= 0:
            if nums2[nums2_ptr] > nums1[nums1_ptr]:
                nums1[cur_ptr] = nums2[nums2_ptr]
                nums2_ptr -= 1
            else:
                nums1[cur_ptr] = nums1[nums1_ptr]
                nums1_ptr -= 1
            
            cur_ptr -= 1

        while nums2_ptr >= 0:
            nums1[cur_ptr] = nums2[nums2_ptr]
            nums2_ptr -= 1
            cur_ptr -= 1
```

### C++

```c++
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int nums1_ptr = size(nums1) - 1 - size(nums2);
        int nums2_ptr = size(nums2) - 1;
        int cur_ptr = size(nums1) - 1;

        while (nums1_ptr >= 0 && nums2_ptr >= 0) {
            if (nums2[nums2_ptr] >= nums1[nums1_ptr]) {
                nums1[cur_ptr] = nums2[nums2_ptr];
                nums2_ptr -= 1;
            }

            else {
                nums1[cur_ptr] = nums1[nums1_ptr];
                nums1_ptr -= 1;
            }

            cur_ptr -= 1;
        }

        while (nums2_ptr >= 0) {
            nums1[cur_ptr] = nums2[nums2_ptr];
            nums2_ptr -= 1;
            cur_ptr -= 1;
        }
    }
};
```
