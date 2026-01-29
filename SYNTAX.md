
We focus on a specific part of the TTQ syntax that is the _selection function_. 

Inside a selection function, `state` is an object implementing the `ProgramState` API, _i.e._, a `state` object can receive and answer any of the API methods described in [API.md](API.md).


**The selection function** is a method that implements a condition to decide if a program state is of interest for a given query.
When evaluated, a function returns `true` if the program state should be selected and `false` otherwise.
In the following script, we configure our query to select program states corresponding to *message sends*:

```smalltalk
"A selection function that finds all states corresponding to message-sends."
query select: [ :state | state isMessageSend ].
```
Smalltalk boolean operators (`and:`, `or:`, `not`) and comparison operators (`=`, `==`, `~=`,  `<=`,  `>=`,  `<`,  `>`) may be used inside a query to combine [API.md](API.md) methods return values:

```smalltalk
"A selection function that finds all states corresponding to message-sends with a selector #helloWorld."
query select: [ :state | state isMessageSend and: [state selector == #helloWorld]].
```