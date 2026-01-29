
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
query select: [ :state | state isMessageSend and: [state messageSelector == #helloWorld]].
```

Selection functions can be implemented as classes.  In that case, they implement a method `value:` that takes the program state as input parameter and returns a boolean. The examples from above can be implemented in classes:

```smalltalk
SelectMessagesSends>>#value: state
    ^state isMessageSend

SelectMessagesSendsWithSelector>>#value: state
    ^state isMessageSend
        and: [state messageSelector = #helloWorld]
```

Selected function classes inherits from `SeekerSelectionFunction`. Selection function classes are regular classes, and can define their own methods and state that can be reused in the `#value:` interface:

```smalltalk
SeekerSelectionFunction subclass: #SelectMessageSends
    instanceVariableNames: ''
    classVariableNames: ''
    package: 'MyPackage'.
```

These classes can just be instantiated and used:

```smalltalk
query := SelectMessageSends new.
"...query configuration..."
"...query execution..."
```