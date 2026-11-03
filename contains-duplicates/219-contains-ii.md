## LeetCode number: 219 | Contains Duplicates II
- *Data structure:* hash set holding a window of the last k elements
- *Algorithm:* fixed-size sliding window

## Concept and complexity
 Two equal values with |i - j| <= k means the earlier one is still among the last k elements.<br>Keep exactly those in a set. After processing index i, if the set exceeds k elements, evict nums[i-k].
- **Time:** O(n)
- **Space:** O(min(n, k))

## Solution
```cpp
bool containsNearbyDuplicate(vector<int>& nums, int k) {
    unordered_set<int> window;
    for (int i = 0; i < (int)nums.size(); i++) {
        if (window.count(nums[i])) return true;
        window.insert(nums[i]);
        if ((int)window.size() > k) window.erase(nums[i - k]);
    }
    return false;
}
```
