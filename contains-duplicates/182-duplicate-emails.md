## LeetCode number: 182 | Duplicate emails
- *Data structure:* table rows grouped by key (internally a hash or sort-based group)
-  *Algorithm:* GROUP BY + HAVING COUNT(*) > 1

## Concept and complexity
**In SQL:** count occurrences per value and keep those seen more than once. The database groups by hashing or sorting.<br>So it is roughly **O(n) to O(n log n)**, with **O(distinct emails) space**.

## Solution

```sql
SELECT email
FROM Person
GROUP BY email
HAVING COUNT(*) > 1;
```

WHERE filters rows before grouping, and HAVING filters groups after aggregation, so the count condition must go in HAVING.

