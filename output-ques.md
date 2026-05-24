remember these

- Slicing in Go does not create a new array; slices usually share the same underlying array.

- A slice is internally:
  - pointer to underlying array
  - length
  - capacity

- In slicing:
  - start index is included
  - end index is excluded

- For:

```go
b := a[x:y]
```

  - length = `y - x`
  - capacity = `cap(a) - x`

- Length means:
  - how many elements are currently accessible in the slice.

- Capacity means:
  - how many elements are available from the slice start position until the end of the underlying array.

- Modifying elements through a sliced slice modifies the original array because both share the same underlying memory.

- `append()` does not always create a new array.

- If enough capacity exists:
  - `append()` reuses the same underlying array.

- If capacity is exceeded:
  - Go allocates a new bigger underlying array.
  - After reallocation, modifications may no longer affect the original slice.

- A sliced slice is best thought of as:
  - a window/view into an existing array.

- `append()` may unexpectedly modify the original slice if the underlying array is still shared.

- Capacity is important because it determines whether `append()` reuses memory or reallocates.

- Slices are reference-like structures, not deep copies.
