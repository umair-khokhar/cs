## String Concepts
### Sequence
A sequence is an ordered list of elements, where the elements follow one another in a specific order.

**Example**:
- Sequence: `1, 2, 3, 4`
- Valid subsequence: `1, 2, 3, 4`
- Invalid subsequence: Any sequence where elements are missing.

### Subsequence
- A subsequence is derived from another sequence by deleting some or no elements without changing the order of the remaining elements.
- The remaining elements must preserve their relative order, but they do not have to be contiguous.
- A sequence is also considered its subsequence.

**Example**:
- Given the sequence `1, 2, 3, 4`:
  - Subsequences: `1, 3`, `2, 4`, `1, 2`, `3, 4`, `1, 2, 3`, etc.
  - Non-subsequences: `3, 2` (because the relative order is not maintained).