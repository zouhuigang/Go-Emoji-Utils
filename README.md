![Go-Emoji-Utils](http://up.tmdvs.me/52074bebc945/d)

# Go Emoji Utils
A collection of useful functions for working with emoji. For example: look up the definition of a specific emoji, or search for all occurrences of emojis in a string.

## Features
 - [x] Find all occurrences of emoji in a string
 - [x] Search a string for the presence specific emoji
 - [x] Look up the definition of a single emoji
 - [x] Look up the definitions for a list of emojis
 - [ ] Find the location of and occurrences of a specific emoji in a string

## Examples
### Find all occurrences of emoji in a string
You can search a string for all occurrences of emoji. You will be returned an array of results specifying which emojis were found, and how many times each occurred.

```go
input := "This is a string 😄 🐷 with some 👍🏻🙈 emoji! 🐷 🏃🏿‍♂️"
result := emoji.FindAll(input)

// result: SearchResults{ SearchResult{ Match: Emoji{…}, Occurrences: 1 }, …}
```

### Search a string for the presence specific emoji
You can search a string for the presence of a specific emoji. You will be returned a `SearchResult` struct with the definition of the matching emoji and how many times it occurred in the string.

```go
input := "This is a string 😄 🐷 with some 👍🏻🙈 emoji! 🐷 🏃🏿‍♂️"
result := emoji.Find("🐷", input)

// result: SearchResult{ Match: Emoji{ Key:"1F437", Value:"🐷", Descriptor: "pig" }, Occurrences: 2 } }
```

### Checking search results for the occurrence of a specific emoji
The `SearchResults` struct has an `IndexOf` method for conveniently checking whether or not a specific emoji appears within the results set. If the emoji is not found a position of `-1` is returned.

```go
input := "This is a string 😄 🐷"
results := emoji.FindAll(input)

pigEmoji := emoji.Emojis["1F437"]
pigIndex := results.IndexOf(pigEmoji)
// pigIndex: 1
```

### Look up the definition of a single emoji
You can lookup the definition of a single emoji character using the `LookupEmoji` function. If a matching emoji can't be found an error will be returned.

```go
result, err := emoji.LookupEmoji("🐷")

// result: Emoji{ Key:"1F437", Value:"🐷", Descriptor: "pig" }
```

### Look up the definitions for a list of emojis
You can lookup the definition of a for each emoji character in an array of emojis using the `LookupEmojis` function. This function is a convenience function that loops through the input slice and passes each emoji to the `LookupEmoji` function.

Results are returned in the same order that the input strings were provided in. If a matching emoji can't be found an error will be appear in for that position in the result slice.

```go
result := emoji.LookupEmojis([]string{"🐷", "🙈"})

// result: []interface{}{ Emoji{ Key:"1F437", Value:"🐷", Descriptor: "pig" }, …}
```
