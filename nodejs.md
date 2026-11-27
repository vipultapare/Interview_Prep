
# V8 Engine in JavaScript

## 1. What is the V8 Engine?

V8 is a JavaScript engine developed by Google.

It is responsible for executing JavaScript code. V8 is written in C++ and is used in Google Chrome and Node.js.

### In simple words

We write JavaScript code, but the computer's processor doesn't directly execute JavaScript in the same way it executes machine instructions.

The V8 Engine processes JavaScript and executes it.

For example:

```javascript
let a = 10;
let b = 20;

console.log(a + b);
```

Output:

```text
30
```

V8 helps execute this JavaScript code.

---

## 2. Why do we need the V8 Engine?

JavaScript is a programming language, but it needs an engine to execute it.

The V8 Engine:

- Parses JavaScript code.
- Converts JavaScript into internal representations such as bytecode.
- Executes JavaScript.
- Optimizes frequently executed code.
- Manages memory for JavaScript objects.

Without a JavaScript engine, JavaScript code would not execute in the environment.

---

## 3. How does the V8 Engine work?

The V8 Engine processes JavaScript through multiple stages.

### Step 1: JavaScript Code

We write JavaScript code.

```javascript
function add(a, b) {
  return a + b;
}

console.log(add(5, 10));
```

### Step 2: Parsing

V8 analyzes the JavaScript code.

It checks the syntax and understands the structure of the program.

For example:

- `function` defines a function.
- `a` and `b` are parameters.
- `return` returns a value.
- `console.log()` is a function call.

If the code contains a syntax error, parsing may fail.

### Step 3: Internal Representation

V8 converts the parsed code into internal representations that it can execute efficiently.

A commonly discussed part of this process is the generation of bytecode.

### Step 4: Execution

V8 executes JavaScript using its interpreter and compiler pipeline.

It may optimize frequently executed code to improve performance.

### Step 5: Output

```text
15
```

---

## 4. V8 Engine Architecture

The basic execution flow:

```text
JavaScript Code
       |
       v
     Parser
       |
       v
 Abstract Syntax Tree (AST)
       |
       v
    Ignition
   Interpreter
       |
       v
     Bytecode
       |
       v
 Execution and Optimization
       |
       v
 Machine Code
```

> Note: Modern V8 uses multiple execution tiers, including Sparkplug and Maglev, along with its optimizing compiler pipeline. The above is a simplified conceptual diagram.

---

## 5. Important Components of V8

### 1. Parser

The Parser analyzes the JavaScript code.

It checks whether the code follows JavaScript syntax rules and builds an internal representation of the code.

Example:

```javascript
let name = "Vipul";
console.log(name);
```

The parser analyzes this code and prepares its structure for further processing.

---

### 2. Ignition

Ignition is V8's interpreter.

It generates bytecode from the parsed code and executes that bytecode.

### In simple words

Ignition helps V8 start executing JavaScript without needing to compile the entire program into highly optimized machine code first.

---

### 3. TurboFan

TurboFan is V8's optimizing compiler.

It optimizes frequently executed code to make it run faster.

For example, if a function is executed repeatedly, V8 may identify opportunities to optimize its execution.

### In simple words

Ignition helps execute code quickly at the beginning, while optimizing compilers can make frequently executed code faster.

---

### 4. Memory Management

V8 manages memory required by JavaScript.

When JavaScript creates objects, arrays, functions and other values, memory is allocated.

V8 also uses Garbage Collection to clean up memory that is no longer needed.

Example:

```javascript
let user = {
  name: "Vipul"
};

user = null;
```

When the object is no longer reachable, it may eventually be cleaned up by the Garbage Collector.

> Garbage Collection does not necessarily happen immediately.

---

## 6. Ignition vs TurboFan

| Ignition | TurboFan |
|---|---|
| Interpreter | Optimizing compiler |
| Generates and executes bytecode | Optimizes code for faster execution |
| Helps with fast startup and execution | Helps improve performance of optimized code |
| Executes JavaScript through bytecode | Generates optimized machine code |

---

## 7. What is the relationship between Node.js and V8?

Node.js uses the V8 Engine to execute JavaScript.

However, V8 alone does not provide all the functionality required to build backend applications.

Node.js provides additional APIs such as:

- File System (`fs`)
- HTTP (`http`)
- Path (`path`)
- Process (`process`)
- Streams
- Networking functionality

### Architecture

```text
         JavaScript Code
               |
               v
          Node.js Runtime
               |
      +--------+--------+
      |                 |
      v                 v
   V8 Engine           libuv
      |                 |
      |                 |
      v                 v
 Executes JS      Async I/O and
                  Event Loop support
```

### Example

```javascript
console.log("Hello Node.js");
```

V8 executes the JavaScript code.

But:

```javascript
const fs = require("fs");

fs.readFile("data.txt", "utf8", (err, data) => {
  console.log(data);
});
```

Node.js provides the File System API, and V8 executes the JavaScript code that uses that API.

---

## 8. V8 vs Node.js

| V8 Engine | Node.js |
|---|---|
| JavaScript Engine | JavaScript Runtime |
| Executes JavaScript | Runs JavaScript outside the browser |
| Parses and executes JavaScript | Provides APIs such as `fs`, `http` and `path` |
| Used by Chrome and Node.js | Uses V8 and other runtime components |
| Does not itself provide Node.js APIs | Provides backend capabilities |

---

## 9. Where is V8 used?

V8 is used in:

- Google Chrome
- Node.js
- Other applications that embed the V8 JavaScript engine

V8 allows JavaScript to be executed in different environments.

---

## 10. Interview Questions

### Q1. What is the V8 Engine?

V8 is Google's open-source JavaScript engine written in C++.

It is responsible for parsing, compiling and executing JavaScript code.

It is used in Google Chrome and Node.js.

---

### Q2. Why does Node.js use V8?

Node.js uses V8 to execute JavaScript outside the browser.

V8 provides the JavaScript execution engine, while Node.js provides additional APIs such as filesystem, HTTP, networking and other backend capabilities.

---

### Q3. What is Ignition?

Ignition is V8's interpreter.

It generates bytecode from JavaScript's parsed representation and executes that bytecode.

---

### Q4. What is TurboFan?

TurboFan is V8's optimizing compiler.

It optimizes frequently executed code to improve performance.

---

### Q5. Is V8 responsible for the Event Loop?

No, the Event Loop is not implemented by V8 alone.

Node.js uses libuv for its event-loop and asynchronous I/O coordination. V8 is responsible for JavaScript execution.

---

### Q6. Is Node.js the same as V8?

No.

V8 is a JavaScript engine.

Node.js is a runtime environment that uses V8 and provides additional APIs and runtime components.

---

## 11. Quick Revision

- V8 is a JavaScript Engine.
- V8 is developed by Google.
- V8 is written in C++.
- V8 is used in Chrome and Node.js.
- V8 parses and executes JavaScript.
- Ignition is V8's interpreter.
- TurboFan is an optimizing compiler.
- V8 manages JavaScript memory and Garbage Collection.
- Node.js uses V8 to execute JavaScript outside the browser.
- Node.js provides APIs that V8 alone does not provide.

---

## 12. Remember This

> V8 executes JavaScript.
>
> Node.js provides the runtime environment and additional APIs that allow JavaScript to run on the server.



# Node.js Event Loop

## 1. What is the Event Loop?

The Event Loop is a mechanism in Node.js that helps handle asynchronous operations without blocking the main JavaScript thread while waiting for those operations to finish.

### In simple words

Imagine you are a receptionist in an office.

A visitor asks you to get a document from another department. It will take 10 minutes.

Instead of waiting for 10 minutes doing nothing, you:

1. Request the document from another department.
2. Handle other visitors.
3. When the document arrives, continue helping the first visitor.

The Event Loop helps Node.js coordinate this kind of asynchronous work.

---

## 2. Why do we need the Event Loop?

JavaScript generally executes on a single main thread in Node.js.

If JavaScript had to wait for every asynchronous operation to finish before doing anything else, the application would become inefficient.

The Event Loop helps Node.js:

- Handle asynchronous operations.
- Avoid blocking JavaScript while waiting for I/O.
- Process callbacks when they are ready.
- Handle multiple concurrent I/O requests efficiently.

---

## 3. How does the Event Loop work?

The simplified process:

```text
JavaScript Code
      |
      v
   Call Stack
      |
      v
Async Operation
      |
      v
Node.js APIs / libuv / OS
      |
      v
Operation Completes
      |
      v
Callback or Continuation is Scheduled
      |
      v
   Event Loop
      |
      v
Callback Executes
```

### Step 1: JavaScript executes

JavaScript code executes on the main JavaScript thread.

### Step 2: An asynchronous operation is encountered

For example:

- `setTimeout()`
- File system operations
- Network requests
- Database requests

### Step 3: Node.js initiates or delegates the operation

Node.js uses runtime mechanisms, libuv and operating-system capabilities to handle many asynchronous operations.

The JavaScript thread does not synchronously wait for the operation to finish.

### Step 4: The operation completes

When the operation completes, its associated callback or continuation can be scheduled.

### Step 5: The Event Loop coordinates execution

The Event Loop coordinates when the scheduled work can execute.

### Step 6: Callback executes

The callback executes on the JavaScript thread when JavaScript execution is available.

---

## 4. Example of the Event Loop

```javascript
console.log("Start");

setTimeout(() => {
  console.log("Timer completed");
}, 2000);

console.log("End");
```

### Output

```text
Start
End
Timer completed
```

### Why does this happen?

1. `console.log("Start")` executes immediately.
2. `setTimeout()` schedules a timer.
3. JavaScript doesn't synchronously wait for the timer.
4. `console.log("End")` executes immediately.
5. After the timer threshold is reached and the callback can execute, `Timer completed` is printed.

The Event Loop helps coordinate the execution of the timer callback.

---

## 5. Blocking vs Non-Blocking

### Blocking Code

```javascript
const fs = require("fs");

console.log("Start");

const data = fs.readFileSync("data.txt", "utf8");

console.log(data);

console.log("End");
```

### Execution

```text
Start
File Data
End
```

`readFileSync()` blocks JavaScript execution until the file-reading operation finishes.

---

### Non-Blocking Code

```javascript
const fs = require("fs");

console.log("Start");

fs.readFile("data.txt", "utf8", (err, data) => {
  console.log(data);
});

console.log("End");
```

### Output

```text
Start
End
File Data
```

### Why?

1. Start is printed.
2. File reading is initiated.
3. JavaScript continues executing.
4. End is printed.
5. Once the file-reading operation completes and the callback can execute, the file data is printed.

This is the basic idea of non-blocking I/O.

---

## 6. Event Loop and Database Requests

Imagine a backend API:

```javascript
app.get("/users", async (req, res) => {
  const users = await database.getUsers();

  res.json(users);
});
```

### What happens?

1. A client sends a request.
2. Node.js receives the request.
3. JavaScript executes the API handler.
4. The database query is initiated.
5. JavaScript doesn't synchronously block while waiting for the database.
6. Node.js can process other ready work.
7. When the database query completes, the continuation after `await` becomes ready.
8. JavaScript resumes the handler.
9. The response is sent to the client.

### Important

`await` does not block the entire Node.js process.

It pauses the execution of the async function while allowing other JavaScript work to run.

---

## 7. Event Loop Phases

Node.js has different Event Loop phases.

The commonly discussed phases are:

1. Timers
2. Pending Callbacks
3. Idle and Prepare
4. Poll
5. Check
6. Close Callbacks

### 1. Timers

Handles callbacks associated with:

- `setTimeout()`
- `setInterval()`

These callbacks become eligible after their timer thresholds are reached.

---

### 2. Pending Callbacks

Handles certain I/O callbacks that are deferred to a later loop iteration.

---

### 3. Idle and Prepare

These phases are primarily used internally by Node.js and libuv.

---

### 4. Poll

The Poll phase:

- Handles many I/O-related callbacks.
- Retrieves new I/O events.
- Can wait for I/O when appropriate.

---

### 5. Check

The Check phase is where `setImmediate()` callbacks are executed.

Example:

```javascript
setImmediate(() => {
  console.log("Immediate");
});
```

---

### 6. Close Callbacks

Handles certain close-related callbacks.

Example:

```javascript
socket.on("close", () => {
  console.log("Socket closed");
});
```

> Note: Event Loop phase behavior and timer ordering can vary based on context and Node.js version.

---

## 8. Event Loop vs Call Stack

| Call Stack | Event Loop |
|---|---|
| Executes JavaScript functions | Coordinates scheduled asynchronous work |
| Tracks currently executing functions | Helps determine when callbacks can execute |
| Works during synchronous execution | Coordinates callback execution through the loop |
| Executes JavaScript | Does not independently execute JavaScript |

---

## 9. Is the Event Loop a Thread?

No, the Event Loop is not a separate JavaScript execution thread.

| Component | Responsibility |
|---|---|
| JavaScript Thread | Executes JavaScript code |
| Call Stack | Tracks executing functions |
| Event Loop | Coordinates callback execution |
| libuv | Provides Event Loop and asynchronous I/O coordination |
| Thread Pool | Handles certain operations using background threads |

Node.js uses a single main JavaScript thread by default, but the runtime can use other threads and operating-system mechanisms.

---

## 10. What happens when CPU-intensive code runs?

Example:

```javascript
console.log("Start");

for (let i = 0; i < 10000000000; i++) {
  // Heavy calculation
}

console.log("End");
```

This loop blocks the main JavaScript thread.

While it is running:

- Other JavaScript callbacks cannot execute on that thread.
- Event Loop callback execution is delayed.
- Requests may experience delays.

### How can we handle CPU-intensive tasks?

We can use:

- Worker Threads
- Child Processes
- Separate microservices
- Job queues

---

## 11. Event Loop Interview Questions

### Q1. What is the Event Loop?

The Event Loop is a mechanism in Node.js that coordinates asynchronous operations and callback execution, allowing Node.js to handle non-blocking I/O efficiently.

---

### Q2. Why is the Event Loop important?

It allows Node.js to handle many concurrent I/O operations without blocking the main JavaScript thread while waiting for each operation to finish.

---

### Q3. Is Node.js single-threaded?

JavaScript execution in a typical Node.js process runs on a single main thread by default. However, Node.js uses additional runtime mechanisms, background threads and operating-system capabilities for certain tasks.

---

### Q4. Does the Event Loop execute JavaScript?

JavaScript callbacks execute on the JavaScript thread. The Event Loop coordinates when callbacks can execute.

---

### Q5. Does `await` block Node.js?

No. `await` pauses the execution of the current async function while allowing other JavaScript work to execute.

---

### Q6. Can CPU-intensive tasks block Node.js?

Yes. CPU-intensive JavaScript code can block the main JavaScript thread and delay Event Loop callbacks.

---

### Q7. What is the relationship between libuv and the Event Loop?

libuv provides the Event Loop implementation and asynchronous I/O coordination used by Node.js.

---

## 12. Quick Revision

- Event Loop helps Node.js handle asynchronous operations.
- JavaScript executes on the main JavaScript thread.
- The Event Loop coordinates callback execution.
- Node.js can initiate or delegate asynchronous operations.
- JavaScript doesn't synchronously block while waiting for many I/O operations.
- Callbacks execute when they are ready and JavaScript execution is available.
- `await` doesn't block the entire Node.js process.
- CPU-intensive JavaScript can block the main thread.
- Node.js uses libuv for Event Loop and asynchronous I/O coordination.

---

## 13. Remember This

> The Event Loop is a mechanism that allows Node.js to coordinate asynchronous operations and execute their callbacks without blocking the main JavaScript thread while waiting for those operations to finish.


# Single-Threaded Architecture in Node.js

## 1. What is Single-Threaded?

Single-threaded means that a program uses one main thread to execute JavaScript code at a time.

In Node.js, JavaScript code normally executes on a single main thread.

This means Node.js executes one JavaScript operation at a time on its main thread.

However, Node.js is not completely single-threaded. It uses background threads, the operating system and other mechanisms to handle certain asynchronous operations.

---

## 2. What is a Thread?

A thread is a path of execution through which a program executes instructions.

Think of a thread as a worker who performs tasks.

- One thread = one worker executing instructions.
- Multiple threads = multiple workers executing tasks simultaneously.

### Example

Imagine a restaurant with one chef.

The chef can prepare one dish at a time. If the chef is busy preparing a dish, they cannot simultaneously prepare another dish on the same thread.

This is similar to JavaScript execution on Node.js's main thread.

---

## 3. Why is Node.js Called Single-Threaded?

Node.js is called single-threaded because JavaScript code in a typical Node.js application executes on one main JavaScript thread.

For example:

```javascript
console.log("Task 1");

console.log("Task 2");

console.log("Task 3");
```

### Output

```text
Task 1
Task 2
Task 3
```

The main JavaScript thread executes these statements one after another.

It doesn't execute all three statements simultaneously.

---

## 4. Is Node.js Completely Single-Threaded?

No!

Node.js is single-threaded primarily in terms of JavaScript execution on its main thread.

Internally, Node.js uses:

- Main JavaScript Thread
- libuv Thread Pool
- Operating System mechanisms
- Worker Threads (when explicitly used)

Therefore, Node.js itself has multiple threads and asynchronous mechanisms.

---

## 5. Node.js Thread Architecture

```text
                  Node.js Application
                          |
                          |
                 Main JavaScript Thread
                          |
                    JavaScript Code
                          |
                Initiates Async Operation
                          |
             +------------+------------+
             |                         |
             |                         |
        libuv Thread Pool          OS Mechanisms
             |                         |
     File System Operations        Network Operations
     Crypto Operations             Sockets etc.
     Certain DNS Operations
             |                         |
             +------------+------------+
                          |
                   Operation Completes
                          |
                Callback / Continuation
                          |
                 Event Loop Scheduling
                          |
              Main JavaScript Thread
```

---

## 6. What is the Main JavaScript Thread?

The main JavaScript thread is where JavaScript code executes.

For example:

```javascript
console.log("Start");

function calculate() {
    console.log("Calculating...");
}

calculate();

console.log("End");
```

### Output

```text
Start
Calculating...
End
```

All these JavaScript statements execute on the main JavaScript thread.

---

## 7. What is the Thread Pool?

Node.js uses the libuv Thread Pool to handle certain operations in the background.

The Thread Pool contains background worker threads.

These workers can handle operations such as:

- Certain file system operations
- Some cryptographic operations
- Certain DNS operations
- Some other operations supported by libuv

This allows the main JavaScript thread to continue executing JavaScript instead of waiting for these operations to finish.

---

## 8. Example of Asynchronous File Reading

```javascript
const fs = require("fs");

console.log("1. Start");

fs.readFile("data.txt", "utf8", (err, data) => {
    if (err) {
        console.log(err);
        return;
    }

    console.log("3. File reading completed");
});

console.log("2. End");
```

### Output

```text
1. Start
2. End
3. File reading completed
```

### How does this work?

**Step 1:**

```javascript
console.log("1. Start");
```

The main JavaScript thread executes this statement.

**Step 2:**

```javascript
fs.readFile("data.txt", "utf8", callback);
```

Node.js initiates the asynchronous file-reading operation.

The main JavaScript thread does not wait for the file reading to finish.

**Step 3:**

```javascript
console.log("2. End");
```

The main JavaScript thread continues executing the next statement.

**Step 4:**

When the file reading operation completes, Node.js schedules the callback.

**Step 5:**

The Event Loop coordinates when the callback can execute.

The callback executes on the main JavaScript thread.

---

## 9. Why Doesn't Node.js Block?

Node.js doesn't block the main JavaScript thread while waiting for supported asynchronous operations to complete.

For example, when Node.js initiates a file-reading operation:

```javascript
fs.readFile("data.txt", callback);
```

The main thread doesn't sit idle waiting for the file.

Instead:

1. Node.js initiates the file operation.
2. The operation is handled using the appropriate underlying mechanism.
3. JavaScript continues executing other code.
4. When the operation completes, its callback is scheduled.
5. The callback eventually executes on the main JavaScript thread.

This is one of the reasons Node.js is efficient for I/O-heavy applications.

---

## 10. What Happens If JavaScript Performs a CPU-Heavy Task?

Node.js can still be blocked if JavaScript performs a CPU-intensive operation on the main thread.

### Example

```javascript
console.log("Start");

for (let i = 0; i < 10000000000; i++) {
    // Heavy computation
}

console.log("End");
```

The main JavaScript thread is busy executing the loop.

During this time, it cannot execute other JavaScript callbacks.

This can delay:

- HTTP requests
- Timers
- Database callbacks
- Other asynchronous callbacks

Therefore, CPU-intensive tasks can affect Node.js performance.

---

## 11. What Are Worker Threads?

Worker Threads allow JavaScript code to execute in separate threads.

They can be used for CPU-intensive tasks.

Unlike the normal main JavaScript thread, a Worker Thread can execute JavaScript independently on a separate thread.

### Main Thread

```text
Handles normal application JavaScript
```

### Worker Thread

```text
Handles CPU-intensive JavaScript work
```

Worker Threads can help prevent CPU-heavy tasks from blocking the main thread.

---

## 12. Main Thread vs Thread Pool vs Worker Threads

| Component | Purpose |
|---|---|
| Main JavaScript Thread | Executes the main JavaScript code and callbacks |
| libuv Thread Pool | Handles certain operations in the background |
| OS Mechanisms | Handle many asynchronous network and other operations |
| Worker Threads | Execute JavaScript on separate threads |

---

## 13. Why Does Node.js Use a Single JavaScript Thread?

Node.js uses this architecture to make handling I/O-heavy workloads efficient.

Instead of creating a separate JavaScript thread for every request, Node.js can:

1. Receive a request.
2. Initiate an asynchronous operation.
3. Continue handling other work.
4. Process the completed operation when its callback or continuation is scheduled.

This approach is useful for applications that handle many requests involving:

- APIs
- Databases
- File systems
- Network communication

---

## 14. Real-World Example

Imagine a receptionist in an office.

The receptionist has one desk.

A customer asks for a document.

Instead of waiting at the desk until the document is ready:

1. The receptionist sends the request to another department.
2. The receptionist continues helping other customers.
3. The other department prepares the document.
4. When the document is ready, the receptionist receives it.
5. The receptionist gives the document to the original customer.

### Mapping

| Office | Node.js |
|---|---|
| Receptionist | Main JavaScript Thread |
| Other Department | Background operation / OS |
| Request | Asynchronous operation |
| Document Ready | Operation completed |
| Receptionist handles document | Callback executes |

This is the basic idea behind Node.js asynchronous architecture.

---

## 15. Important Interview Question

### Q: Node.js is single-threaded, but it uses a Thread Pool. Why?

**Answer:**

Node.js is called single-threaded because JavaScript code in a typical Node.js application executes on one main JavaScript thread.

However, Node.js is not entirely single-threaded. It uses libuv's Thread Pool for certain operations, such as many file system and cryptographic operations, and relies on operating-system mechanisms for many network operations.

When an asynchronous operation is initiated, Node.js can delegate or initiate the work without blocking the main JavaScript thread. The main thread can continue executing other JavaScript code.

When the operation completes, its callback or continuation is scheduled and eventually executes on the main JavaScript thread.

Therefore, Node.js is single-threaded in terms of its main JavaScript execution, but its runtime uses multiple threads and other asynchronous mechanisms.

---

## 16. Quick Revision

- A thread is a path of execution.
- Node.js normally executes JavaScript on one main thread.
- Node.js is not entirely single-threaded.
- libuv provides a Thread Pool for certain operations.
- Many network operations use OS mechanisms instead of the libuv Thread Pool.
- Async operations help avoid blocking the main thread while waiting.
- Callbacks and JavaScript continuations generally execute on the main JavaScript thread.
- CPU-heavy JavaScript can block the Event Loop.
- Worker Threads allow JavaScript to execute on separate threads.
- Node.js is particularly useful for I/O-heavy applications.

---

## Remember This

**Node.js is single-threaded for JavaScript execution, not single-threaded in its entire runtime architecture.**


# Blocking vs Non-blocking I/O in Node.js

# 1. What is I/O?

I/O stands for **Input/Output**.

I/O means a program communicates with something outside its own JavaScript execution.

Examples of I/O operations:

- Reading a file
- Writing a file
- Fetching data from a database
- Calling an external API
- Sending HTTP requests
- Receiving data from a network

### Example

```javascript
const fs = require("fs");

const data = fs.readFileSync("data.txt", "utf8");

console.log(data);
```

Here, Node.js reads data from a file.

Reading the file is an I/O operation.

---

# 2. What is Blocking?

**Blocking means that the execution of further JavaScript code has to wait until the current operation finishes.**

When a blocking operation is running on the main JavaScript thread, the thread cannot execute other JavaScript code in that flow until the operation completes.

## Real-life example

Imagine you are working at a restaurant counter.

1. Customer A orders coffee.
2. You start preparing the coffee.
3. You wait until the coffee is ready.
4. While waiting, you don't serve Customer B.
5. Once the coffee is ready, you serve Customer B.

You are waiting for one task to finish before moving to the next task.

This is similar to blocking.

---

# 3. Blocking I/O in Node.js

Node.js provides synchronous methods that block the main JavaScript thread.

For example:

```javascript
const fs = require("fs");

console.log("Start");

const data = fs.readFileSync("data.txt", "utf8");

console.log(data);

console.log("End");
```

Assume `data.txt` contains:

```text
Hello Node.js
```

## Output

```text
Start
Hello Node.js
End
```

## How does it work?

### Step 1

```javascript
console.log("Start");
```

The main JavaScript thread executes this statement.

Output:

```text
Start
```

### Step 2

```javascript
const data = fs.readFileSync("data.txt", "utf8");
```

Node.js starts reading the file synchronously.

The main JavaScript thread waits until the operation finishes.

### Step 3

Once the file reading is complete, the data is returned.

### Step 4

```javascript
console.log(data);
```

The file contents are printed.

### Step 5

```javascript
console.log("End");
```

The final statement executes.

## Execution flow

```text
Start
  |
  v
readFileSync()
  |
  v
Main JavaScript thread waits
  |
  v
File reading completes
  |
  v
Print file data
  |
  v
End
```

## Important

While the synchronous file-reading operation is waiting, the main JavaScript thread cannot execute other JavaScript code.

This is called **Blocking I/O**.

---

# 4. What is Non-blocking I/O?

**Non-blocking I/O means that Node.js initiates an operation and allows the main JavaScript thread to continue executing other JavaScript code without waiting for that operation to finish.**

When the operation completes, its callback or Promise continuation is scheduled for execution.

## Real-life example

Imagine you are a waiter in a restaurant.

1. Customer A orders food.
2. You send the order to the kitchen.
3. You don't stand in the kitchen waiting.
4. You go to Customer B and take their order.
5. You serve Customer C.
6. When Customer A's food is ready, you serve Customer A.

You don't wait for one task to finish before moving to another.

This is the basic idea of non-blocking I/O.

---

# 5. Non-blocking I/O in Node.js

Node.js provides asynchronous I/O methods.

For example:

```javascript
const fs = require("fs");

console.log("Start");

fs.readFile("data.txt", "utf8", (err, data) => {
    if (err) {
        console.log(err);
        return;
    }

    console.log(data);
});

console.log("End");
```

Assume `data.txt` contains:

```text
Hello Node.js
```

## Output

```text
Start
End
Hello Node.js
```

Notice that `End` is printed before the file contents.

Why?

Because Node.js does not wait for the file-reading operation to finish before executing the next statement.

---

# 6. How does Non-blocking I/O work?

Let's understand the execution step-by-step.

## Step 1: Start

```javascript
console.log("Start");
```

The main JavaScript thread executes the statement.

Output:

```text
Start
```

## Step 2: Initiate file reading

```javascript
fs.readFile("data.txt", "utf8", callback);
```

Node.js initiates the asynchronous file-reading operation.

The main JavaScript thread does not wait for the file reading to finish.

## Step 3: Continue executing JavaScript

```javascript
console.log("End");
```

The main JavaScript thread continues executing the next statement.

Output:

```text
End
```

## Step 4: File reading completes

The underlying file-reading operation completes.

Node.js schedules the callback when it can be executed.

## Step 5: Callback executes

```javascript
console.log(data);
```

The file contents are printed.

## Execution flow

```text
Start
  |
  v
fs.readFile()
  |
  +---------------------------+
  |                           |
  v                           v
Main thread continues     File reading happens
  |                           |
  v                           |
Print End                      |
  |                           |
  |                           v
  |                     File reading completes
  |                           |
  +---------------------------+
              |
              v
        Callback executes
              |
              v
        Print file data
```

---

# 7. Blocking vs Non-blocking

| Blocking I/O | Non-blocking I/O |
|---|---|
| The main thread waits for the operation to finish. | The main thread doesn't wait for the operation to finish. |
| Further JavaScript code in that flow cannot execute until the operation returns. | Further JavaScript code can execute while the operation is in progress. |
| Can prevent the main thread from handling other work during the wait. | Allows the main thread to handle other work while I/O is pending. |
| Often uses synchronous APIs. | Often uses asynchronous APIs. |
| `fs.readFileSync()` | `fs.readFile()` |
| Poor fit for blocking waits in busy servers. | Generally preferred for I/O-heavy server applications. |

---

# 8. Blocking Example

```javascript
const fs = require("fs");

console.log("Request 1: Started");

const data = fs.readFileSync("data.txt", "utf8");

console.log("Request 1: File completed");

console.log("Request 2: Started");
```

## Output

```text
Request 1: Started
Request 1: File completed
Request 2: Started
```

## Execution

```text
Request 1 starts
       |
       v
File reading starts
       |
       v
Main thread waits
       |
       v
File reading finishes
       |
       v
Request 1 continues
       |
       v
Request 2 starts
```

Request 2 cannot execute on this thread until the blocking operation returns.

---

# 9. Non-blocking Example

```javascript
const fs = require("fs");

console.log("Request 1: Started");

fs.readFile("data.txt", "utf8", (err, data) => {
    if (err) {
        console.log(err);
        return;
    }

    console.log("Request 1: File completed");
});

console.log("Request 2: Started");
```

## Output

```text
Request 1: Started
Request 2: Started
Request 1: File completed
```

## Execution

```text
Request 1 starts
       |
       v
File reading initiated
       |
       +--------------------------+
       |                          |
       v                          v
Main thread continues       File reading happens
       |                          |
       v                          |
Request 2 starts                   |
       |                          v
       |                    File reading completes
       |                          |
       +--------------------------+
                   |
                   v
             Callback executes
```

Request 2 doesn't have to wait for Request 1's file reading to finish.

---

# 10. Why is Non-blocking I/O important?

Imagine a Node.js backend server receives three requests.

- Request A: Fetch data from a database.
- Request B: Call an external API.
- Request C: Return a simple response.

## Blocking scenario

Suppose Request A performs a blocking operation that takes 5 seconds.

```text
Main JavaScript Thread

Request A
|
|---- Waiting for database (5 seconds)
|
Request B  ---- Waiting
|
Request C  ---- Waiting
```

While the main thread is blocked, it cannot execute other JavaScript callbacks.

This can reduce the server's ability to handle work.

## Non-blocking scenario

Request A initiates a database operation asynchronously.

While the database is working:

- Request B can be processed.
- Request C can be processed.
- Other JavaScript work can execute.

```text
Main JavaScript Thread

Request A
|
|---- Database operation initiated
|
Request B
|
Request C
|
Other work
|
Request A callback when result is available
```

This allows Node.js to handle multiple I/O operations concurrently.

---

# 11. Does Non-blocking mean Parallel Execution?

No!

Non-blocking and parallelism are different concepts.

## Non-blocking

The main thread does not wait for an I/O operation to finish.

It can continue executing other JavaScript code.

## Parallelism

Multiple tasks are actually executing at the same time on different execution resources.

### Example

```javascript
console.log("A");

setTimeout(() => {
    console.log("B");
}, 1000);

console.log("C");
```

## Output

```text
A
C
B
```

`A` and `C` execute on the main JavaScript thread.

The timer is initiated and JavaScript continues.

When the timer completes, the callback is scheduled and eventually executes on the main JavaScript thread.

Node.js can manage concurrent operations without necessarily executing JavaScript simultaneously.

---

# 12. Concurrency vs Parallelism vs Non-blocking

| Concept | Meaning |
|---|---|
| Blocking | The execution waits for an operation to complete. |
| Non-blocking | The execution can continue without waiting for an operation. |
| Concurrency | Multiple tasks can make progress during overlapping periods of time. |
| Parallelism | Multiple tasks can actually execute at the same time. |

---

# 13. What happens with `await`?

Consider the following code:

```javascript
async function getData() {
    console.log("1. Start");

    const data = await fetchData();

    console.log("3. Data received");
}

console.log("Outside");

getData();

console.log("End");
```

Assuming `fetchData()` returns a Promise that resolves later.

The `await` pauses the execution of the particular async function until its Promise settles.

It does not block the entire main JavaScript thread.

The main thread can execute other JavaScript work while the async function is suspended.

## Important

`await` does not mean blocking the entire Node.js thread.

It suspends the current async function and allows the event loop to process other work.

---

# 14. Blocking vs Non-blocking APIs in Node.js

| Blocking API | Non-blocking API |
|---|---|
| `fs.readFileSync()` | `fs.readFile()` |
| `fs.writeFileSync()` | `fs.writeFile()` |
| `fs.appendFileSync()` | `fs.appendFile()` |
| `fs.unlinkSync()` | `fs.unlink()` |
| `fs.mkdirSync()` | `fs.mkdir()` |

The synchronous methods generally block the main JavaScript thread while the operation executes.

The asynchronous versions allow the main thread to continue while the I/O operation is in progress.

---

# 15. Blocking I/O in a Backend Application

Consider an Express application.

```javascript
const express = require("express");

const app = express();

app.get("/users", async (req, res) => {
    const users = await database.query("SELECT * FROM users");

    res.json(users);
});

app.listen(3000);
```

When the database query is awaiting its result:

1. The request handler's async function is suspended.
2. The main JavaScript thread is not blocked by that asynchronous wait.
3. Node.js can process other work.
4. When the Promise settles, the handler resumes when scheduled.
5. The response is sent.

This is why asynchronous database operations are important in Node.js applications.

---

# 16. Interview Questions

## Q1. What is Non-blocking I/O in Node.js?

Non-blocking I/O in Node.js means that when an I/O operation such as reading a file, querying a database, or making a network request is initiated, the main JavaScript thread does not wait for the operation to complete. Instead, Node.js initiates or delegates the operation using the appropriate underlying mechanism and continues executing other JavaScript code. When the operation completes, its callback or Promise continuation is scheduled for execution. This allows Node.js to handle multiple I/O operations concurrently and improves application throughput.

## Q2. What is the difference between Blocking and Non-blocking I/O?

Blocking I/O means the execution of further JavaScript code has to wait until the current I/O operation completes. Non-blocking I/O means the main JavaScript thread can continue executing other code while the I/O operation is in progress. Node.js generally prefers non-blocking I/O for server applications because it helps handle multiple requests efficiently without blocking the main JavaScript thread during I/O waits.

## Q3. Why does Node.js use Non-blocking I/O?

Node.js uses non-blocking I/O to avoid blocking the main JavaScript thread while waiting for operations such as database queries, file reading and network requests. This allows the main thread to handle other work and improves throughput for I/O-heavy applications.

## Q4. Does Non-blocking mean JavaScript executes in parallel?

No. Non-blocking means the main JavaScript thread doesn't have to wait for an operation to finish. JavaScript code can still execute on a single main thread. Parallel execution requires multiple execution resources working simultaneously.

## Q5. Does `await` block Node.js?

No. `await` suspends the execution of the particular async function until the awaited Promise settles. It does not block the entire JavaScript thread, allowing Node.js to process other work.

---

# 17. Quick Revision

- I/O means Input/Output.
- Examples: Files, databases, APIs and network communication.
- Blocking means waiting for an operation to complete before continuing.
- Non-blocking means initiating an operation and continuing without waiting for it to complete.
- `fs.readFileSync()` is blocking.
- `fs.readFile()` is non-blocking.
- Blocking I/O can prevent the main JavaScript thread from handling other work.
- Non-blocking I/O allows the main thread to work on other tasks while I/O is pending.
- Node.js uses non-blocking I/O to improve throughput and handle concurrent requests.
- Non-blocking does not mean parallel execution.
- `await` suspends the particular async function, not the entire JavaScript thread.

---

# Remember This

**Blocking I/O makes the main JavaScript thread wait.**

**Non-blocking I/O allows the main JavaScript thread to continue working while the I/O operation is in progress.**

This is one of the major reasons Node.js is effective for I/O-heavy applications.
```

If you'd like, we can continue in the same format with **Concurrency vs Parallelism in Node.js**, which is the natural next topic after non-blocking I/O.



# Node.js Streams

## 1. What are Streams in Node.js?

Streams are a way of processing data piece by piece (in chunks) instead of loading the entire data into memory at once.

Streams are useful when working with:

- Large files
- Videos
- Images
- HTTP requests
- HTTP responses
- Network communication
- File uploads and downloads

### Real-life example

Imagine a large water tank connected to a pipe.

Instead of emptying the entire tank before using the water, water flows through the pipe continuously.

You receive water as it flows.

Streams work in a similar way.

Instead of loading all the data into memory at once, Node.js can read and process data in smaller chunks.

---

## 2. Why do we need Streams?

Imagine you have a 1 GB file.

### Without Streams

You might load the entire file into memory before processing it.

```javascript
const fs = require("fs");

const data = fs.readFileSync("large-file.txt");

console.log(data);
```

Here, the file is loaded into memory before the function returns.

### Potential problems

- High memory consumption.
- Processing starts after the entire file has been read.
- Multiple large files can put pressure on RAM.
- May cause out-of-memory problems.

### With Streams

```javascript
const fs = require("fs");

const readableStream = fs.createReadStream("large-file.txt");

readableStream.on("data", (chunk) => {
    console.log("Received chunk");
});
```

Node.js reads the file in chunks.

Instead of loading the entire file into memory, your application can process each chunk as it arrives.

### Benefits of Streams

- Memory efficient when processing large data.
- Processing can begin before the entire data has arrived.
- Useful for handling large files.
- Useful for file uploads and downloads.
- Useful for HTTP and network communication.
- Helps avoid unnecessarily buffering entire data sets in memory.

---

## 3. What is a Chunk?

A chunk is a small piece of data that is delivered or processed as part of a stream.

Imagine a file contains:

```text
Hello Node.js, I am learning Streams.
```

The stream might deliver the data in chunks such as:

```text
Chunk 1: Hello Node
Chunk 2: .js, I am
Chunk 3: learning
Chunk 4: Streams.
```

These are illustrative chunk boundaries. Actual chunk sizes and boundaries depend on the underlying stream and system.

### Example

```javascript
const fs = require("fs");

const readableStream = fs.createReadStream("data.txt");

readableStream.on("data", (chunk) => {
    console.log(chunk);
});
```

Each time the stream emits a `data` event, the callback receives a chunk.

A chunk is not necessarily a complete line, sentence, JSON object or record.

It is simply a piece of data.

---

# 4. The Four Types of Streams

Node.js has four fundamental stream types.

| Stream | Purpose |
|---|---|
| Readable | Read data |
| Writable | Write data |
| Duplex | Read and write data |
| Transform | Read, process, and output data |

---

# 5. Readable Stream

A Readable Stream is used to read data piece by piece from a source.

### Examples

- Reading files.
- Receiving HTTP request data.
- Reading data from network connections.

### Example: Reading a file

```javascript
const fs = require("fs");

const readableStream = fs.createReadStream("data.txt");

readableStream.on("data", (chunk) => {
    console.log("Received chunk:");
    console.log(chunk.toString());
});

readableStream.on("end", () => {
    console.log("Finished reading file");
});

readableStream.on("error", (err) => {
    console.log("Error:", err.message);
});
```

### What happens?

| Code | Meaning |
|---|---|
| `fs.createReadStream()` | Creates a readable stream. |
| `data` event | Fires when a chunk is available for consumption. |
| `chunk` | The piece of data received. |
| `chunk.toString()` | Converts the Buffer into readable text. |
| `end` event | Indicates that no more data is available to read. |
| `error` event | Handles stream errors. |

### Example output

```text
Received chunk:
Hello Node.js
Finished reading file
```

The output depends on the file size and the chunk boundaries.

A small file may arrive in one chunk, while a large file may arrive in multiple chunks.

---

# 6. Writable Stream

A Writable Stream is used to write data to a destination piece by piece.

### Examples

- Writing files.
- Sending data to network connections.
- Writing data to HTTP responses.

### Example: Writing to a file

```javascript
const fs = require("fs");

const writableStream = fs.createWriteStream("output.txt");

writableStream.write("Hello ");
writableStream.write("Node.js ");
writableStream.write("Streams!");

writableStream.end();

writableStream.on("finish", () => {
    console.log("Writing completed");
});
```

### How does it work?

#### Step 1

```javascript
const writableStream = fs.createWriteStream("output.txt");
```

Creates a writable stream to write data into the file.

#### Step 2

```javascript
writableStream.write("Hello ");
```

Writes a piece of data.

#### Step 3

```javascript
writableStream.write("Node.js ");
```

Writes another piece of data.

#### Step 4

```javascript
writableStream.write("Streams!");
```

Writes another piece of data.

#### Step 5

```javascript
writableStream.end();
```

Signals that no more data will be written.

#### Step 6

The `finish` event fires when all data has been processed by the writable stream.

### Output in output.txt

```text
Hello Node.js Streams!
```

### Important

- `write()` sends data into the writable stream.
- `end()` signals that writing is complete.
- `finish` indicates that the writable stream has finished processing the data.

---

# 7. Duplex Stream

A Duplex Stream can both read data and write data.

Imagine a telephone conversation.

- You can hear the other person.
- You can speak to the other person.

Both directions of communication are possible.

A Duplex Stream works similarly.

### Example

A TCP socket is a Duplex Stream.

```text
             TCP Socket

     Incoming data       Outgoing data
          |                   |
          v                   v
        READ                WRITE
          |                   |
          +-------- Socket ----+
```

A socket can:

- Receive data from another system.
- Send data to another system.

Both operations can happen independently.

### Where are Duplex Streams used?

- TCP sockets.
- Network communication.
- Communication channels.

### Simple definition

A Duplex Stream can read and write data, but the readable and writable sides do not necessarily have to be related.

---

# 8. Transform Stream

A Transform Stream receives data, processes or modifies it, and then produces transformed output.

Imagine a water filtration machine.

- Water enters.
- The machine processes the water.
- Clean water comes out.

A Transform Stream works similarly.

### Example: Convert text to uppercase

```javascript
const { Transform } = require("stream");

const upperCaseTransform = new Transform({
    transform(chunk, encoding, callback) {
        const result = chunk.toString().toUpperCase();

        callback(null, result);
    }
});

upperCaseTransform.on("data", (chunk) => {
    console.log(chunk.toString());
});

upperCaseTransform.write("hello ");
upperCaseTransform.write("node.js ");
upperCaseTransform.write("streams");

upperCaseTransform.end();
```

### Output

```text
HELLO 
NODE.JS 
STREAMS
```

### How does it work?

| Step | Operation |
|---|---|
| 1 | Data is written into the Transform Stream. |
| 2 | `transform()` processes the incoming chunk. |
| 3 | The chunk is converted to uppercase. |
| 4 | The transformed data is sent to the readable side. |
| 5 | The `data` listener receives the transformed chunk. |

### Where are Transform Streams used?

- Compression.
- Decompression.
- Encryption.
- Decryption.
- Data formatting.
- Data processing.

---

# 9. Readable vs Writable vs Duplex vs Transform

| Type | What it does | Example |
|---|---|---|
| Readable | Reads data | `fs.createReadStream()` |
| Writable | Writes data | `fs.createWriteStream()` |
| Duplex | Reads and writes | TCP socket |
| Transform | Reads, processes and outputs | Gzip compression |

---

# 10. What is pipe() in Node.js?

`pipe()` connects a Readable Stream to a Writable Stream.

It allows data to flow from the readable source to the writable destination.

### Example

Imagine you want to copy data from:

- `input.txt`
- To `output.txt`

Instead of manually handling every chunk, you can connect the streams.

```javascript
const fs = require("fs");

const readableStream = fs.createReadStream("input.txt");

const writableStream = fs.createWriteStream("output.txt");

readableStream.pipe(writableStream);
```

### Architecture

```text
input.txt
    |
    v
Readable Stream
    |
    v
   pipe()
    |
    v
Writable Stream
    |
    v
output.txt
```

### What does pipe() do?

1. Reads data from the source.
2. Sends chunks to the destination.
3. Manages flow between streams.
4. Helps manage buffering and backpressure.
5. Ends the destination by default when the readable source ends, unless configured otherwise.

---

# 11. What is Backpressure?

Backpressure occurs when data is being produced faster than the destination can consume or process it.

### Real-life example

Imagine:

- A pipe sends water very quickly.
- A small bucket receives water slowly.
- Water arrives faster than the bucket can handle.

The bucket is overwhelmed.

This is similar to backpressure in Streams.

### In Node.js

Imagine:

- Readable Stream produces 100 chunks per second.
- Writable Stream processes only 10 chunks per second.

Without flow control, data could accumulate in memory.

### Architecture

```text
Readable Stream
      |
      | Produces data quickly
      v
    Buffer
      |
      | Data may accumulate
      v
Writable Stream
      |
      | Consumes data slowly
      v
  Destination
```

### How do Streams handle it?

Node.js Streams provide buffering and flow-control mechanisms.

When a Writable Stream reaches its buffering threshold, it can signal that the producer should temporarily slow down or stop sending more data.

When the destination is ready again, data flow can resume.

`pipe()` helps manage this flow automatically.

### Why is Backpressure important?

- Prevents excessive memory consumption.
- Helps manage fast producers and slow consumers.
- Improves reliability when transferring large amounts of data.

### Simple definition

Backpressure helps prevent a fast data producer from overwhelming a slower data consumer.

---

# 12. What is Buffer in Node.js?

A Buffer is a temporary memory area used to hold binary data.

Node.js often represents stream chunks using Buffer objects.

### Example

```javascript
const fs = require("fs");

const readableStream = fs.createReadStream("data.txt");

readableStream.on("data", (chunk) => {
    console.log(chunk);
    console.log(chunk.toString());
});
```

### Buffer output example

```text
<Buffer 48 65 6c 6c 6f>
```

This represents the bytes of the text:

```text
Hello
```

### Why do we use Buffers?

Computers work with bytes when dealing with many types of data, such as:

- Files.
- Images.
- Videos.
- Network data.
- Binary data.

Buffers help Node.js work with these bytes.

---

# 13. Streams vs Reading the Entire File

| Reading entire file | Streams |
|---|---|
| Loads the file into memory before processing it. | Processes data incrementally. |
| Can consume more memory for large files. | Can reduce memory consumption. |
| Processing may begin after the file is fully read. | Processing can begin as chunks arrive. |
| Convenient for small files. | Particularly useful for large files and data transfer. |

---

# 14. Real-World Stream Use Cases

## A. Reading large files

```javascript
const fs = require("fs");

const readStream = fs.createReadStream("large-file.csv");

readStream.on("data", (chunk) => {
    console.log("Processing chunk...");
});
```

Useful for:

- CSV files.
- Log files.
- Large data files.

## B. File uploads

Streams can help process or forward uploaded data without unnecessarily buffering the entire file.

## C. File downloads

HTTP responses can stream data to clients as it becomes available.

## D. Video streaming

Video data can be delivered incrementally instead of requiring the entire video file to be downloaded before playback begins.

## E. Compression

Transform Streams can compress data.

## F. Logging

Large log files can be processed incrementally.

---

# 15. Interview Questions

## Q1. What are Streams in Node.js?

Streams in Node.js are a mechanism for processing data incrementally, in chunks, instead of loading the entire data into memory at once. They are useful for working with large files, network communication, HTTP requests and responses, and data transformations. Streams help improve memory efficiency and allow processing to begin before all the data has arrived.

## Q2. What are the four types of Streams?

Node.js has four fundamental stream types:

- Readable: Used to read data.
- Writable: Used to write data.
- Duplex: Used to read and write data.
- Transform: Used to read, process or transform data, and output it.

## Q3. What is a Chunk?

A chunk is a piece of data delivered or processed as part of a stream. Instead of processing the entire data at once, streams can process smaller pieces as they arrive.

## Q4. What is pipe()?

`pipe()` connects a Readable Stream to a Writable Stream. It transfers data from the readable source to the writable destination and helps manage data flow and backpressure.

## Q5. What is Backpressure?

Backpressure is a flow-control mechanism that helps prevent a data producer from overwhelming a slower data consumer. Node.js Streams can pause or regulate data flow when the destination cannot keep up.

## Q6. Why do we use Streams?

Streams are useful for processing large data efficiently, reducing memory pressure, and allowing data processing to begin while data is still being received or read.

## Q7. What is the difference between Duplex and Transform Streams?

A Duplex Stream supports reading and writing, and the two sides can operate independently.

A Transform Stream is also readable and writable, but its purpose is to process or transform incoming data and produce output.

## Q8. Does a Stream load the entire file into memory?

Not necessarily. Streams allow data to be processed incrementally. They use buffers internally, but generally do not require the entire file to be loaded into memory at once.

---

# 16. Quick Revision

- A Stream processes data piece by piece.
- A chunk is a small piece of data.
- Streams can help reduce memory consumption when processing large data.
- Readable Streams read data.
- Writable Streams write data.
- Duplex Streams read and write.
- Transform Streams process or transform data.
- `pipe()` connects streams.
- Backpressure helps manage data flow when the consumer is slower than the producer.
- Buffers hold chunks of data temporarily.
- Streams are useful for files, HTTP, networking, uploads, downloads, compression and other data-processing tasks.

---

# Remember This

**Streams allow Node.js to process data piece by piece instead of loading the entire data into memory at once.**

- Readable = Read
- Writable = Write
- Duplex = Read + Write
- Transform = Read + Process + Output
- pipe() = Connect streams
- Backpressure = Prevent a fast producer from overwhelming a slow consumer
- Buffer = Temporary storage for chunks of binary data
```

This README follows the fundamental stream concepts in the [official Node.js Streams documentation](https://nodejs.org/api/stream.html). <Cite refs={["turn423425search0"]}/>

Next, I'd recommend **Buffers in Node.js**—it will complete your understanding of how Node.js handles binary data, chunks, and streams.


