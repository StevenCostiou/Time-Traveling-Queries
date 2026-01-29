The `ProgramState` is a programming interface from an abstract object named "program state" or "state", that exposes execution data. The available API depends on the concrete "state" of the execution. The general execution data API is always available. The message send and assignment API are only available when a message send or an assignment are actually executed.


## Methods of the `ProgramState` API to obtain general execution data of the debugged program

| Method | Description |
|--------|-------------|
| `arguments:` Array | Returns an array containing the objects in the arguments of the current activated method. |
| context: Context | Returns the suspended `Context` object, i.e., the context of the activated method at the top of the stack of the debugged process. |
| isAssignment: Boolean | Returns true if the current bytecode instruction is an assignment, false otherwise. |
| isMessageSend: Boolean | Returns true if the bytecode instruction is a message send, false otherwise. |
| method: CompiledMethod | Returns the CompiledMethod of the suspended context. |
| node: RBProgramNode | Returns the AST node corresponding to the current bytecode instruction of the suspended context. |
| receiver: Object | Returns the receiver object of the current activated method context in the top of the stack. |
| receiverClass: Class | Returns the class of the receiver object. |
| receiverClassName: Symbol | Returns the name of the class of the receiver object. |
| receiverPackage: RPackage | Returns the object representing the package of the receiver class. |
| selector: Symbol | Returns the selector of the activated method of the suspended context. |
| willCreateBlock: Boolean | Returns true if the current bytecode instruction will create a `BlockClosure`. |
| willReturn: Boolean | Returns true if the current bytecode is a return instruction. |


## Methods of the `ProgramState` API to obtain instruction-specific program execution data related to message-sends

| Method | Description |
|--------|-------------|
| isInstantiationMessage: Boolean | Returns true if the method about to execute is an instantiation primitive. |
| methodAboutToExecute: CompiledMethod | Returns the CompiledMethod that will be executed by the message-send. |
| messageReceiver: Object | Returns the object that will receive the message. |
| messageSelector: Symbol | Returns the selector of the message being sent. |
| messageArguments: Array | Returns an array with the arguments of the message. |
| classAboutToBeInstantiated: Class | Returns the class of the object that will be instantiated by the instantiation message. |


## Methods of the `ProgramState` API to obtain instruction-specific program execution data related to assignments

| Method | Description |
|--------|-------------|
| assignmentVariable: Variable | Returns the `Variable` object on the left side of the assignment. |
| assignmentVariableName: Symbol | Returns the name of the assignment variable. |
| assignmentCurrentValue: Object | Returns the current value of the assignment variable, i.e., before the assignment occurs. |
| assignmentNextValue: Object | Returns the value about to be assigned to the variable. |
