title: From React to Elm
class: animation-fade
layout: true

<!-- This slide will serve as the base layout for all your slides -->
.bottom-bar[
  {{title}}
]

---
class: middle, center

# From React to Elm

Sebastian Porto | Stax.io

---

## Stax.io

Mostly React app
Elm slowly growing

---
class: middle, center

# What is great

---

# No runtime errors (almost)

Missing props is a common occurrence for us:

```js

<a onClick={props.showMessage} ... />

props.showMessage is not a function
```

## Elm compiler

```elm
props does not have a field named showMessage
```

---

## Anything can be null / undefined in JS

```js
if (state.selectedUser.age > 18) { .... }
```
Cannot read property 'age' of undefined

---

## Elm have Maybe and Result

```elm
case state.selectedUser of
  Ok user ->
    if user.age > 18 then
      ..
  Nothing ->
```

---

# We use Flow (Type system)

```js

type PropsType = {
  showMessage: (msg: string) => void,
}


function Widget(props: PropsType) { ... }
```
---

## Works, but

--

*it* misses plenty of stuff:

```js
var users: Array<User> = ...

var result = _(users)
    .filter(over18)
    .map(getNames)
    .values()
```

Flow has no idea what `result` is

--

TS is the same

---

## Elm always knows

```elm
let
  names = 
    users
      |> List.filter over18
      |> List.map .name
```

```elm
names : List String
```
---
class: middle, center

# Thanks to this robust type system

---

# Refactoring is much faster

- Change the thing you want

- Follow compiler errors

- Fix

- Usually works

---

# We can iterate faster

---

## In React

- Write code
- Browse
- Get a runtime error
- Change

---

## With Elm

- Write code
- Compile 
- Get feedback
- Change

This is way faster than browsing


---
# Ignoring possible errors in JS is easy
.
```js
var date = new Date(someString)

... do something with date

```
.
What if `someString` is an invalid date?

---

## Elm forces you to handle all possible outcomes
.
```elm

case parseDate someString of
    Ok date ->
        ...
    Err err ->
       ...
```

---

Http responses:

```elm
case response of
    Success users ->
        ...
    Failure err ->
        ...
```

Instead of null:

```elm
case selectedUser of
    Just user ->
       ...
    Nothing ->
       ...
```

---
class: middle, center

# Less decisions to make

---

## How should we manage our *state* in React?

- State
- Props
- Context
- Redux
- Some other thing

---

## Elm has only one way

.

```elm
update : Msg -> Model -> Model
```

---

# How do I write my views?

##  React

- Classes
- Stateless functions
- HOCs

We often start with one thing e.g. Stateless and the refactor to a class

---

## Elm has only functions

```elm
view model =
    div [] []
```
---
class: middle, center

# And functions are more convenient than JSX

---

E.g. tables

- React always needs to return a root element, hard for tables

- Elm, return whatever you want, compose as you want

---

E.g. mapping

### JSX

```js
list.map(item => <Item key={item.id} item={item} />)
```

### Elm

```elm
List.map itemView items
```
---

# What libs should I use?
.

|| React | Elm |
|---|--- | --- |
| Managing state | Redux, MobX, etc | Elm |
| State | POJOs, Immutable.js | Elm |
| Data transformation | Lodash, ramda | Elm |
| Http | Fetch, Axios | Elm http |

---
class: center, middle

# Easier setup

---

## React

- Babel / Flow or Typescript
- React, React DOM
- Redux
- Some immutable library
- Ramda, lodash
- Many babel plug-ins
- Webpack

---

## With Elm

- Elm
- Maybe Webpack
---

# Immutable data

A typical bug in JS:

```js
var today = moment()
var tomorrow = addOneDay(today)

// What is today?
```

---

## Immutable.js

- **Immutable.js** isn't great as you can still mutate items inside a collection
- No strong guarantees

.

## Other libs in JS

- Lots of mutable state e.g. **moment**
---
class: center, middle

# Elm doesn't let you do the wrong thing.
## Data is always immutable.

---
class: center, middle

# Learning

---

# JS has a lot of baggage

Prototypes, cohesions, classes, promises, ES6 sugar, scoping, ...


Many different ways of doing things:

- Functional vs OOP
- Two way data binding vs unidirectional flow
- Callback, promises, generators

---

# Elm

- Less concepts to learn
- Fewer ways of doing things

---
class: center, middle

# The not so great parts

---

## Code splitting, code sharing and SSR

Still not a thing, but some of this coming soon in 0.19

---

## More DIY that React

- Harder to find ready made components

---

## Interacting with JavaScript and the DOM

- Not straightforward like JS
- Use ports

---

## JSON decoders

- Hard at first
- No big deal after a while

---

## CSS

- Still a WIP
- Not as mature are the React ecosystem

---
class: center, middle

# Thank you


