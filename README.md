# LEETCODE-Backtracking-1593
The goal is to split this string into the maximum number of unique substrings.

### Initial Setup:
- `s = "ababccc"`
- `idx = 0` (starting index for substring)
- `st = {}` (empty HashSet to store unique substrings)
- `currcount = 0` (current count of unique substrings)
- `maxcount = [0]` (array to store the maximum count of unique substrings)

### Dry Run Step-by-Step:

#### Call 1: `solve(s, 0, {}, 0, [0])`
- Explore substrings starting from index 0:
  - **For j = 0**: `str = "a"`
    - `st = {"a"}`, `currcount = 1`
    - Recurse: `solve(s, 1, {"a"}, 1, [0])`

#### Call 2: `solve(s, 1, {"a"}, 1, [0])`
- Explore substrings starting from index 1:
  - **For j = 1**: `str = "b"`
    - `st = {"a", "b"}`, `currcount = 2`
    - Recurse: `solve(s, 2, {"a", "b"}, 2, [0])`

#### Call 3: `solve(s, 2, {"a", "b"}, 2, [0])`
- Explore substrings starting from index 2:
  - **For j = 2**: `str = "a"`
    - `"a"` is already in `st`, skip.
  - **For j = 3**: `str = "ab"`
    - `st = {"a", "b", "ab"}`, `currcount = 3`
    - Recurse: `solve(s, 4, {"a", "b", "ab"}, 3, [0])`

#### Call 4: `solve(s, 4, {"a", "b", "ab"}, 3, [0])`
- Explore substrings starting from index 4:
  - **For j = 4**: `str = "c"`
    - `st = {"a", "b", "ab", "c"}`, `currcount = 4`
    - Recurse: `solve(s, 5, {"a", "b", "ab", "c"}, 4, [0])`

#### Call 5: `solve(s, 5, {"a", "b", "ab", "c"}, 4, [0])`
- Explore substrings starting from index 5:
  - **For j = 5**: `str = "c"`
    - `"c"` is already in `st`, skip.
  - **For j = 6**: `str = "cc"`
    - `st = {"a", "b", "ab", "c", "cc"}`, `currcount = 5`
    - Recurse: `solve(s, 7, {"a", "b", "ab", "c", "cc"}, 5, [0])`

#### Call 6: `solve(s, 7, {"a", "b", "ab", "c", "cc"}, 5, [0])`
- We've reached the end of the string (`idx == s.length()`).
- Update `maxcount[0] = max(0, 5) = 5`
- Backtrack and remove `"cc"` from `st`.

#### Backtrack to Call 5:
- `st = {"a", "b", "ab", "c"}`, `currcount = 4`
- Backtrack and remove `"c"` from `st`.

#### Continue Backtracking...
- The algorithm continues to explore other possible substrings and backtrack when necessary, updating `maxcount[0]` if a higher count is found.

### Final Result:
After the recursion explores all possible splits, the maximum number of unique substrings is stored in `maxcount[0]`, which would be 5 for the string `"ababccc"`.

The possible unique split with 5 substrings could be: `["a", "b", "ab", "c", "cc"]`.

### Time Complexity:
Since the algorithm checks all possible partitions of the string, the time complexity is exponential in terms of the length of the string `n`. Thus, the worst-case complexity is \(O(2^n)\).
