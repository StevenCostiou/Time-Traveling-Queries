
## Full example: a query class finding all sends to `helloWorld`

```smalltalk
"Define the SelectMessageSends class with a targetSelector instance variable"
SeekerSelectionFunction subclass: #SelectMessageSends
    instanceVariableNames: 'targetSelector'
    classVariableNames: ''
    package: 'MyPackage'.

"Accessor methods for targetSelector"
SelectMessageSends>>targetSelector
    ^targetSelector

SelectMessageSends>>targetSelector: aSelector
    targetSelector := aSelector

"#value: method using targetSelector"
SelectMessageSends>>#value: pState
    ^pState isMessageSend
        and: [pState messageSelector = targetSelector]
```

```smalltalk
"Instantiate the class and set targetSelector to #helloWorld"
| selectorQuery |
selectorQuery := SelectMessageSends new.
selectorQuery targetSelector: #helloWorld.
```