## Command Pattern... and beyond

Marcin Malinowski

- Twitter: [@orientman](https://twitter.com/orientman)
- GitHub: https://github.com/orient-man
- Blog: https://orientman.wordpress.com/

***

## Intencja

Encapsulate a request as an object, thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations

*Skojarzenia*: Dependency Inversion, słabe vs. silne powiązania, AOP (aspekty), zdarzenia

***

## Motywacja

It's necessary to issue requests to objects without knowing anything about the operation [...] or the receiver.

---

### Example: UI toolkit

User interface toolkits include objects like buttons and menus that carry out a request in response to user input. But the toolkit can't implement the request explicitly in the button or menu [...] have no way of knowing the receiver of the request or the operations that will carry it out.

---

### Let's see...

![Overview](./images/cmd_in_ui.jpg)

---

### Paste Command

![Paste Command](./images/pastecmd.jpg)

Receiver: document->Paste()

---

### Open Command

![Open Command](./images/opencmd.jpg)

Receiver: application->Add(doc)

---

### Macro Command

Sekwencje komend:

![Macro Command](./images/macrocmd.jpg)

***

## Zastosowanie

- Commands are an object-oriented replacement for *callbacks*.
- When you want to: specify, queue, and execute requests at different times (asynchronicznie, zdalnie etc.)
- Support undo (Execute/Unexecute, store state needed to reverse)
- Logging (restore crashed system state from commands i.e. transactional journal)
- Structure a system around high-level operations built on primitives operations

***

## Structure

![Structure](./images/structure.jpg)

---

## Collaborations

![Collaborations](./images/collaborations.jpg)

***

## Konsekwencje

1. Command *decouples* the object that invokes the operation from the one that knows how to perform it.
2. Commands are *first-class objects*. They can be manipulated and extended like any other object (see: Decorator Pattern).
3. You can assemble commands into a *composite command* (see: Composite Pattern)

***

### Implementation / Considerations

1. How intelligent should a command be? Simple forwarding to receiver or full blown logic inside?
2. Supporting undo and redo i.e. storing history list of commands that have been executed
3. Using C++ templates (or C# generic) - if no need for undo or different arguments

***

DEMO

http://jsfiddle.net/cvcLLyLx/5/
