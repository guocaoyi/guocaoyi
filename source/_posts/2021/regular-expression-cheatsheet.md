---
layout: post
title: Regular Expression Cheatsheet
date: 2021-4-20
tags:
  - lang/regexp
---

# Regular Expression Cheatsheet

## Character classes

```regexp
.  			any character except newline
\w\d\s  		word, digit, whitespace
\W\D\S		not word, digit, whitespace
[abc]			any of a, b, or c
[^abc]		not a, b, or c
[a-g]			character between a & g
```

## Anchors

```typescript
^abc$ //start/end of the string
\b\B //word, not-word boundary
```

## Escaped characters

```typescript
\.\*\\  // escaped special characters
\t\n\r  // tab, linefeed, carriage return
```

<!-- more -->

## Groups & Lookaround

```
(abc)			capture group
\1 			backreference to group #1
(?:abc)		non-capturing group
(?=abc)		positive lookahead
(?!abc)		negative lookahead
```

## Quantifiers & Alternation

```
a*a+a?		0 or more, 1 or more, 0 or 1
a{5}a{2,}		exactly five, two or more
a{1,3}		between one & three
a+?a{2,}?		match as few as possible
ab|cd			match ab or cd
```
