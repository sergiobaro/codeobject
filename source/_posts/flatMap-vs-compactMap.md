---
title: flatMap vs compactMap
tags: swift
date: 2018-10-30 20:04:15
---

When `flatMap` was deprecated I was confused and I wanted to know more about it.
Only one use of `flatMap` has been deprecated. And it makes sense.

This is the proposal: [SE-0187](https://github.com/apple/swift-evolution/blob/master/proposals/0187-introduce-filtermap.md)

## compactMap

### Remove optionals from a `Sequence`
`[Int?] -> [Int]`

Apple Doc: [Sequence.compactMap(_:)](https://developer.apple.com/documentation/swift/sequence/2950916-compactmap)

```swift
// [[Int]] -> [Int]
[1, 2, nil, 3, 4].compactMap({ $0 }) // -> [1,2,3,4]
```

## flatMap

### To flat a `Sequence`

Apple Doc: [Sequence.flatMap(_:)](https://developer.apple.com/documentation/swift/sequence/2905332-flatmap)

```swift
// [[Int]] -> [Int]
[[1,2], [3,4]].flatMap({ $0 }) // -> [1,2,3,4]
```

### To remove optionals from a `Sequence`

This is the use replaced by `compactMap` on Swift 4.1

Apple Doc: [Sequence.flatMap(_:)](https://developer.apple.com/documentation/swift/sequence/2907182-flatmap)

```swift
// [Int?] -> [Int]
[1, 2, nil, 3, 4].flatMap({ $0 }) // -> [1,2,3,4]
```

### To flat an `Optional`

I have discovered this use by accident.

Apple Doc: [Optional.map(_:)](https://developer.apple.com/documentation/swift/optional/1539476-map)
Apple Doc: [Optional.flatMap(_:)](https://developer.apple.com/documentation/swift/optional/1540500-flatmap)

This two methods are doing something very similar. Both will return nil if the optional is nil without executing the closure. 

The closure is actually run when the value of the optional is not nil, that's why the closure takes a non optional value as the argument. 

The use case for each function, as the documentation says:
- `map`: Use the map method with a closure that returns a non-optional value.
- `flatMap`: Use the flatMap method with a closure that returns an optional value.

```swift
let number: Int? = 3
let closure: (Int) -> Int? = { Int($0) }

String(describing: number.map(closure)) // -> Optional(Optional(3))
String(describing: number.flatMap(closure)) // -> Optional(3)
```

So `flatMap` flats a double optional to a single optional (?? -> ?).