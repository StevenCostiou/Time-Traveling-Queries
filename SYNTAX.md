`state` is an object implementing the `ProgramState` API, _i.e._, a `state` object can receive and answer any of the API methods described in [API.md](API.md).

We focus on a specific part of the TTQ syntax that is the _selection function_. 

**The selection function** is a method that implements a condition to decide if a program state is of interest for a given query.
The function is evaluated for each item of the data source (in the same way as the OCL selection clause).
When evaluated, this condition returns `true` if the program state should be selected and `false` otherwise.
In the following script, we configure our query to select program states corresponding to *message sends*:

```smalltalk
"A selection function that finds all states corresponding to message-sends."
query select: [ :state | state isMessageSend ].
