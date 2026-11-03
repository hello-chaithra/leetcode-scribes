##  LeetCode number: 220  | Contains Duplicates III
- *Data structure:* ordered set (std::set<long long>), with buckets (hash map) as the O(n) alternative
- *Algorithm:* sliding window plus nearest-value search

## Concept and complexity
For each x, we need a number y in the window with |x - y| <= valueDiff, that is, y in [x - valueDiff, x + valueDiff].<br>Find the smallest y >= x - valueDiff with lower_bound. If it exists and y <= x + valueDiff, you're done. Then insert x and evict nums[i - indexDiff].
- **Time:** O(n log k)
- **Space:** O(k)<br>A plain set (not a multiset) is enough. If x were already in the window, the check would have returned true (diff 0 ≤ valueDiff).

 ## Solution (ordered set)
```cpp
bool containsNearbyAlmostDuplicate(vector<int>& nums, int indexDiff, int valueDiff) {
    set<long long> window;
    for (int i = 0; i < (int)nums.size(); i++) {
        long long x = nums[i];
        auto it = window.lower_bound(x - valueDiff);
        if (it != window.end() && *it <= x + valueDiff) return true;
        window.insert(x);
        if ((int)window.size() > indexDiff) window.erase((long long)nums[i - indexDiff]);
    }
    return false;
}
```
*Bonus: O(n) bucket version*<br>Note: Each bucket holds at most one element, because two in the same bucket would already have returned true. The negative-number floor division is the classic bug here.

```cpp
bool containsNearbyAlmostDuplicate(vector<int>& nums, int indexDiff, int valueDiff) {
    long long w = (long long)valueDiff + 1;
    auto id = [&](long long x) { return x >= 0 ? x / w : (x + 1) / w - 1; }; // floor division
    unordered_map<long long, long long> bucket;
    for (int i = 0; i < (int)nums.size(); i++) {
        long long x = nums[i], b = id(x);
        if (bucket.count(b)) return true;
        if (bucket.count(b - 1) && x - bucket[b - 1] <= valueDiff) return true;
        if (bucket.count(b + 1) && bucket[b + 1] - x <= valueDiff) return true;
        bucket[b] = x;
        if (i >= indexDiff) bucket.erase(id(nums[i - indexDiff]));
    }
    return false;
}
```
