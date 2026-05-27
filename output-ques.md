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

---

- this will:

```
funcs := []func(){}

for i := 0; i < 3; i++ {
    funcs = append(funcs, func() {
        fmt.Println(i)
    })
}

for _, f := range funcs {
    f()
}
```

give you 3,3,3

but this:

```
for i := 0; i < 3; i++ {
    defer fmt.Println(i)
}
```

will be 2,1,0

---

- strings are immutable , rest almost everything is mutable

- Go is always pass by value. For slices, maps, and channels the value being copied is a pointer/header — so element modifications affect the original but reassignment doesn't.

```
func changeElement(s []int) {
    s[0] = 99       // modifies underlying array → affects original
}

func appendSlice(s []int) {
    s = append(s, 99)  // modifies copy of slice struct → does NOT affect original
}

s := []int{1, 2, 3}
changeElement(s)
fmt.Println(s)   // [99 2 3] — element changed ✅

appendSlice(s)
fmt.Println(s)   // [99 2 3] — append didn't affect original ❌
```

Pass by Reference: Map, Slice, Channel, Pointer, Function/Closure, Interface
Pass by Value: int, float, bool, string, Struct, Array
