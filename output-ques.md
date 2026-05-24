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

- Modifying elements through a sliced slice modifies the original array because both share the same underlying memory.

- If capacity is exceeded:
  - Go allocates a new bigger underlying array.
  - After reallocation, modifications may no longer affect the original slice.

- `append()` may unexpectedly modify the original slice if the underlying array is still shared.

- Capacity is important because it determines whether `append()` reuses memory or reallocates.

- Map returns zero value for missing keys.

```
m := map[string]int{
    "a": 1,
    "b": 2,
}

val := m["c"]
fmt.Println(val)
```

this will be 0
