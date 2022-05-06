---
layout: post
title: 'When to use values vs pointers in Go'
date: 2022-05-06 08:49:30 +0900
categories: go
---

Coming from languages that don't expose pointers to the developer, pointers in Go were
one of the more difficult things I had to get my head around at first.
While the question of when and when not to use pointers can occasionally depend on the particular situation, in most cases we can use the following guidelines to help us make the correct choice.

## Built-in types - use values

Built-in types (string, int, bool etc.), should be passed around (used as function parameters, method receivers, return values, or struct fields) as values.
This can be seen in the standard library, and conceptually treating these values as immutable helps to keep your code consistent and easier to reason about.

```go
// Bad
func increment(val *int) {
	val++
}

// Good
func increment(val int) int {
	return int + 1
}
```

The one exception to this rule is when you want to be able to represent a null value when marshalling/unmarshalling, since a built-in type can't be nil (while a pointer to a built-in type can).

**Note:** It doesn't seem there's any perfect solution to this (except for not having nullable fields to begin with) but if making a field a pointer just to support null values bothers you you may want to consider using a library such as [guregu/null](https://github.com/guregu/null){:target="\_blank"}.

## Reference types - use values

Reference types are slices, maps, functions, channels, and interface values, and should also be passed around by value. Values of these types already contain pointers and so further creating a pointer causes confusion and makes code more complex while providing no real benefit.

```go
// Bad
func increment(vals *[]int) {
	for i, _ := range *vals {
		(*vals)[i]++
	}
}

// Good
func increment(vals []int) []int {
	incVals := make([]int, len(vals))
	for i := range vals {
		incVals[i] = vals[i] + 1
	}
	return incVals
}
```

The exception to this rule is when decoding or unmarshalling a slice or map.
The original value is mutated in this case and so a pointer is required.

## User/struct types - prefer values

User defined structs should generally use values when possible, and pointers when not.
You should also think about what makes the most sense conceptually for the type in question.
If mutating the value fundamentally changes what the value "is", use values.
For example an error code may be defined by a number. If you change this number, you now have a different error code representing a completely different error.

```go
func message(code ErrorCode) string {
	switch code {
		case ENotFound:
			return "Not found"
		...
	}
}
```

On the other hand, if you have a `User` type and you increment their `age` field, you still have the same user, just one year older, and so pointers may be more appropriate.

```go
func happyBirthday(u *User) {
	u.Age++
}
```

If you're not sure, pointers are the safer choice as not all values can be copied. You can always refactor later if values turn out to be more suitable (unless your package is public).

## Be consistent

Above all, be consistent. All methods on a struct should either use pointers or values but not a mix of both (apart from the exceptions mentioned above). This holds true for types from external packages as well - if the New() constructor function for a type returns a pointer, you should be passing it as a pointer as well. If all the methods of an imported type use value receivers, you should be using it as a value.

Note that care must also be taken with consistency in constructs such as for loops. If you've decided a particular struct should be represented by pointers, it should be treated as a pointer everywhere and operations should modify the actual value being pointed to, not a copy of that value.

```go
// Bad
func happyBirthday(users []User) {
	for _, v := range users {
		// this is a bug
		// we've made a copy of the value being pointed to (don't do that)
		// and modified the copy - changes won't be seen by the caller
		v.age++
	}
}

// Good
func happyBirthday(users []Users) {
	for i, _ := range users {
		// users[i] is the actual user, changes will be seen by the caller
		users[i].age++
	}
}
```

Mixing up your semantics by treating pointers as values and vice versa can be source of confusion and hard to find bugs.

## Final word

While consistency is king, using values where possible and reasonable will in general make your code easier to reason about as mutations are made more obvious and it becomes harder for functions and methods to have unexpected side effects on passed parameters. There may be a case for more liberal use of pointers in some situations with large structs and strict performance requirements, but this should only factor in when benchmarks have proven that the benefits outweigh any sacrifice in understandibility/readability.

### References

- [Ultimate Go Programming, Second Edition - William Kennedy](https://learning.oreilly.com/videos/ultimate-go-programming/9780135261651/){:target="\_blank"}

{% include share-buttons.html %}
