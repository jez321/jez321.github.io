---
layout: post
title: 'Common Go memory leaks'
date: 2022-04-30 08:49:30 +0900
categories: go
---

While thanks to Go's garbage collector much of the burden of memory management is transferred from the developer to the runtime itself, there still remain some situations where memory leaks can occur, some of the most common of which are outlined here.

### Unterminated goroutines

```go
func leak() {
  ch := make(chan int)
  go func() {
    <-ch
    fmt.Println("Goroutine finish")
  }()
}
```

[Go Playground](https://go.dev/play/p/4Q5W7FKsocH){:target="\_blank"}

In this most basic example a goroutine is created and sits waiting for data on channel `ch`.
The function returns before any writes to `ch` that would unblock the goroutine, and so it continues waiting forever, never releasing its resources.

As [Dave Cheney](https://dave.cheney.net/2016/12/22/never-start-a-goroutine-without-knowing-how-it-will-stop){:target="\_blank"} puts it, never start a goroutine without knowing how it will stop. This should also be clear to anyone reading the code at a later date too, through writing readable code, and if necessary, appropriate comments.

### Ever-growing caches

```go
var cache = map[string]string{}

func get(key string) string {
  if v, ok := cache[key]; ok {
    return v
  }
  cache[key] = "value" // get value from db etc.
  return cache[key]
}
```

[Go Playground](https://go.dev/play/p/aoDboUb1pV9){:target="\_blank"}

While not exactly a memory leak, and not specific to Go, not having any mechanism for removing values from caches can be another source of out of control memory growth. Resources not being unlimited, at some point you will need to remove values from your cache, whether it be by time, when a particular event occurs, or something else.

### Not closing resources

```go
resp, err := http.Get("https://example.com")
if err != nil {
  return err
}
// defer resp.Body.Close() - add this
```

[Go Playground](https://go.dev/play/p/QnqaLSaAb3L){:target="\_blank"}
(Note that this code won't run on Playground since external HTTP requests are not supported)

Certain resources such as HTTP response bodies have a `Close()` method that should be called when you are finished with them so that they can be garbage collected correctly. Not calling `Close()` can result in memory leaks. The general idiomatic way to handle this case is to defer the call to `Close()` right after successfully opening the resource.<br />

(Note that response bodies require closing [even if they are not read from](https://stackoverflow.com/a/18601625){:target="\_blank"})

### References

- [Ultimate Go Programming, Second Edition - William Kennedy](https://learning.oreilly.com/videos/ultimate-go-programming/9780135261651/){:target="\_blank"}
- [Never start a goroutine without knowing how it will stop - Dave Cheney](https://dave.cheney.net/2016/12/22/never-start-a-goroutine-without-knowing-how-it-will-stop){:target="\_blank"}

{% include share-buttons.html %}
