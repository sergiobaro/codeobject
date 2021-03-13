---
title: Weak self on closures
date: 2021-03-05 12:18:40
tags: swift
---

It took me a while to understand why sometimes you do NOT need to use `[weak self]` in some closures.

When `weak` is usually needed:
- Stored escaping closures: when a closure is stored in another object. (`@escaping`)
- Optional closures: since an optional is actually an enum, it is a stored closure.

    ```swift
    public enum Optional<Wrapped> {
        case none
        case some(Wrapped)
    }
    ```

When `weak` is not needed:
- Non-escaping closures: like higher order functions (`map`, `filter`, `reduce`).

When `weak` is not always needed:
- Temporal retain cycle: in some cases the retain cycle lasts only a few milliseconds ([`DispatchQueue`](https://developer.apple.com/documentation/dispatch/dispatchqueue),  [`UIView.animate`](https://developer.apple.com/documentation/uikit/uiview/1622418-animate))

It is important to understand the lifetime of the closure and the objects captured in it. If you are not sure, just use `weak`.

The only example I found for using `unowned` is when an object retains a closure that captures itself. In that case you are sure that the lifetime of the closure is the same as the objects been captured in the closure, so if the object captured is released the closure is released.
