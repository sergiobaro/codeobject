---
title: Optional Pattern Matching
tags: swift
date: 2019-03-03 22:39:15
---

Pattern matching in swift can be quite verbose, specially when dealing with optionals.
The optional pattern `_?` is just another way to write `.some(_)`.

```swift
let value: Int? = 4

switch value {
case _?:
// case .some(_): 
    print("not nil")
case .none:
    print("nil")
}
```

It can be used with `let`:

```swift
let value: Int? = 4

switch value {
case let first?: 
//case .some(let first):
  print(first)
case _: 
  print("whatever")
}
```

It can be used with tuples:

```swift
let name: (first: String?, last: String?) = ("first", nil)

switch name {
case (let first?, .none):
//case (.some(let first), nil):
  print(first)
case (.none, let last?):
  print(last)
case (_?, _?):
  print("Full name")
case (_, _):
  print("No name")
}
```
