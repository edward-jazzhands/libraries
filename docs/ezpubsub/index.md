# EZPubSub

![badge](https://img.shields.io/badge/linted-Ruff-blue?style=for-the-badge&logo=ruff)
![badge](https://img.shields.io/badge/formatted-black-black?style=for-the-badge)
![badge](https://img.shields.io/badge/type_checked-MyPy_(strict)-blue?style=for-the-badge&logo=python)
![badge](https://img.shields.io/badge/type_checked-Pyright_(strict)-blue?style=for-the-badge&logo=python)
![badge](https://img.shields.io/badge/license-MIT-blue?style=for-the-badge)

[Link to Github Repository](https://github.com/edward-jazzhands/ezpubsub)

A tiny, modern alternative to [Blinker](https://github.com/pallets-eco/blinker) – typed, thread-safe, and built for today’s Python.

ezpubsub is an ultra-simple pub/sub library for Python. Its only goal is to make publishing and subscribing to events as easy and as safe as possible. No async complexity, no extra features, no dependencies—just clean, synchronous pub/sub that works anywhere.

## Features

- Thread-Safe by Default – Safe to publish and subscribe across threads.
- Strongly Typed with Generics – Signals are fully generic (`Signal[str]`, `Signal[MyClass]`), letting Pyright/MyPy catch mistakes before runtime. This also unlocks powerful combinations with Typed Objects as signal types.
- Synchronous by Design – 100% sync to keep things predictable. Works fine in async projects.
- Automatic Memory Management – Bound methods are weakly referenced and automatically unsubscribed when their objects are deleted. Normal functions are strongly referenced and must be manually unsubscribed.
- Lightweight & Zero Dependencies – Minimal API, no legacy baggage, designed for 2025-era Python.

## Why ezpubsub / Project philosophy

### Why not just use Blinker?

Blinker is an excellent, battle-tested library. If you’re writing a simple, single-threaded, synchronous app (e.g., Flask extensions), Blinker is still a great choice.

However, ezpubsub was designed as a modern alternative:

1. **Full Static Typing with Generics**  
    Blinker’s signals are effectively untyped (Any everywhere). ezpubsub’s `Signal[T]` lets Pyright/MyPy enforce that subscribers receive the correct data type at development time, as well as unlocks powerful combinations with Typed Objects as signal types. This makes it much easier to catch mistakes before they happen, rather than at runtime.
2. **Thread-Safe by Default**  
    Blinker assumes single-threaded execution. ezpubsub uses proper locking, making it safe in threaded or mixed sync/async environments.
3. **Type Safety Over Dynamic Namespaces**
    Blinker’s string-based namespaces allow arbitrary signal creation (`ns.signal("user_created")`), but at the cost of type safety; there’s nothing stopping you from accidentally publishing the wrong object type. ezpubsub treats each signal as an explicitly typed object (`Signal[User]`), making such mistakes enforced at compile time instead of runtime.

### Why not use an "async-first" pub/sub library?

There are dozens of tiny “AIO pub/sub” libraries on GitHub. I was personally not satisfied with any of them for these reasons:

1. **Async should not be the core mechanism**  
    Pub/sub is just a dispatch mechanism. Whether you call a subscriber directly or schedule it on an event loop is application logic. Some people might say this is a hot take, but I believe in it. It's not terrible to include async support as an option, but it should not be the primary focus of a pub/sub library.
2. **Async-First Usually Means Bad Ergonomics**  
    These libraries often force you into awkward patterns: creating tasks for every subscription, manual event loop juggling, weird API naming. No benefit, more pain.

There is a reason that the most popular pub/sub libraries in the Python ecosystem (blinker, Celery, PyDispatcher, etc) are all synchronous. It’s the simplest, most predictable way to do pub/sub. Async-first versions, in my opinion, are usually just [reinventing the square wheel](https://exceptionnotfound.net/reinventing-the-square-wheel-the-daily-software-anti-pattern/).

I would certainly be open to implementing some very simple async support in future versions (As of writing this it's only 0.1.0!), but it would be an optional feature, and need to follow the same principles of simplicity and ergonomics as the rest of the library.

### Comparison table - ezpubsub vs Blinker

| Feature                   | ezpubsub                 | blinker         | Category        |
| ------------------------- | ------------------------ | --------------- | --------------- |
| Thread-Safe by Default    | ✅ Yes                    | ❌ No            | Core Philosophy |
| Generically Typed Payload | ✅ Yes (Signal[T])        | ❌ No (**kwargs, Any) | Core Philosophy |
| Weak-Reference Support    | ✅ Yes                    | ✅ Yes           | Core Philosophy |
| Sender-Specific Filtering | ❌ No (Not planned)       | ✅ Yes           | Core (Blinker)  |
| Namespacing               | ❌ No (Not planned)       | ✅ Yes           | Core (Blinker)  |
| Async Support             | ❌ Possible future update | ✅ Yes           | Nice-to-have    |
| Decorator API             | ❌ Possible future update | ✅ Yes           | Nice-to-have    |
| Context Managers          | ❌ Possible future update | ✅ Yes           | Nice-to-have    |
| Metasignals (on connect)  | ❌ Possible future update | ✅ Yes           | Nice-to-have    |

## Documentation

### [Click here for documentation](docs.md)

## Questions, Issues, Suggestions?

Use the [issues](https://github.com/edward-jazzhands/ezpubsub/issues) section for bugs or problems, and post ideas or feature requests on the [discussion board](https://github.com/edward-jazzhands/ezpubsub/discussions).

## License

MIT License
