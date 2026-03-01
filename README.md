# DAO Pattern — Sample

A minimal demonstration of the DAO (Data Access Object) pattern in Java + Spring Boot.

---

## What It Demonstrates

**DAO** is a pattern that hides data access details behind an interface. Business logic works against the `UserRepository` interface and has no knowledge of where or how data is stored — whether in a HashMap, ArrayList, PostgreSQL, or anything else.

The project illustrates this with a concrete example: the same `UserRepository` interface is implemented two ways — via `HashMap` and via `ArrayList`. Behavior is identical, implementation is different.

---

## Structure

The entire project intentionally fits in a single file — so the pattern is visible in full, without unnecessary noise:

```
DaoArchitecture.java
│
├── User                          # Model — record with id and name
├── UserRepository                # DAO contract — interface with findById / findAll / save / delete
├── InMemoryMapUserRepository     # Implementation via HashMap — O(1) lookup by id
├── InMemoryListUserRepository    # Implementation via ArrayList — sequential scan
└── DaoArchitecture               # Spring Boot entry point + demo()
```

---

## Key Points

**Interface as contract.** `UserRepository` defines what to do — not how. The calling code (`demo()`) is written against the interface and has no idea which implementation is in use.

**Two implementations — one behavior.** `InMemoryMapUserRepository` stores data in a `HashMap` — O(1) lookup by id. `InMemoryListUserRepository` stores data in an `ArrayList` — sequential scan at O(n). From the outside, there is no difference.

**Substitutability.** Swapping the implementation requires changing a single line in `demo()`. Nothing else changes — that is the point of DAO.

---

## Running

```bash
./mvnw spring-boot:run
```

Console output:

```
MAP:  Optional[User[id=1, name=jack]]
LIST: Optional[User[id=1, name=jack]]
```

Both implementations return the same result.
