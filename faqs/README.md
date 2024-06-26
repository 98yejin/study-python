## FAQs

- [Memory - Heap vs Stack](#memory---heap-vs-stack)
- [Recursion vs Iteration](#recursion-vs-iteration)
- [Process vs Thread](#process-vs-thread)
- [Context Switching](#context-switching)
- [Deadlock](#deadlock)
- [Synchronous vs Asynchronous](#synchronous-vs-asynchronous)
- [Python's Lifecycle Management](#pythons-lifecycle-management)

### Memory - Heap vs Stack

#### Memory - Stack

- **Automatic Memory Management**: The stack is managed automatically by the compiler or runtime environment. Memory allocated on the stack is automatically deallocated when it goes out of scope.
- **Static Memory Allocation**: Memory allocation on the stack follows a Last-In-First-Out (LIFO) strategy. Each function call creates a new stack frame, which includes parameters, local variables, and return addresses.
- **Limited Size**: The stack has a fixed and limited size, typically smaller than the heap. This size is determined at compile time or by system settings.
- **Faster Access**: Accessing memory on the stack is faster than on the heap because it involves simple pointer arithmetic.
- **Scope-based**: Variables allocated on the stack have a limited scope and are only accessible within the block or function in which they are declared.

#### Memory - Heap

- **Manual Memory Management**: Memory on the heap is managed manually by the programmer. To prevent memory leaks and use resources efficiently, memory allocated on the heap must be explicitly deallocated. When a process terminates, the operating system reclaims all resources used by the process, including heap memory. However, if memory is not properly managed during the execution of the program, it can lead to memory leaks.
- **Dynamic Memory Allocation**: Memory allocation on the heap can be dynamic, allowing for flexible memory usage and allocation of memory blocks of varying sizes.
- **Larger Size**: The heap typically has a larger and theoretically unlimited size compared to the stack. However, it can be limited by available system resources.
- **Slower Access**: Accessing memory on the heap involves dereferencing pointers, which can be slower than accessing memory on the stack.
- **Global Scope**: Memory allocated on the heap can have a global scope and can be accessed from anywhere in the program.
- **Potential for Memory Fragmentation**: Memory fragmentation can occur on the heap over time, leading to inefficient memory usage and potential allocation failures.

#### Choosing Between Stack and Heap

- **Lifetime of Data**: Use the stack for data with a short lifetime, such as function parameters and local variables. For variables in the main function, which exist for the lifetime of the program, consider the size and memory requirements. Use the heap for data with a longer lifetime or dynamic memory requirements.
- **Scope**: Use the stack for variables with a limited scope and predictable lifetime. Use the heap for variables with a broader scope or lifetime extending beyond the current scope.
- **Size Consideration**: Consider the size of data when choosing between the stack and heap. Large data structures may exceed the stack's size limit and should be allocated on the heap.

In summary, the stack and heap serve different purposes in memory management, with the stack providing automatic and scoped memory allocation, while the heap offers manual and dynamic memory allocation. The choice between stack and heap depends on factors such as data lifetime, scope, and memory requirements.

### Recursion vs Iteration

- Using recursive algorithms can lead to poor space efficiency. Each recursive call adds a new layer to the stack, which means that O(n) memory is used when the depth of recursion is n.
- For this reason, it may be better to implement recursive algorithms iteratively. However, code implemented iteratively can sometimes be much more complex, so it may be better to compromise.
- By default, the number of recursive calls in Python is set to 1000. It is possible to change this value, but be cautious as it may lead to a recursion error and cause the stack to overflow. In such cases, using an iterative approach can be an alternative solution.

### Process vs Thread

- **Process**: A process can be thought of as an instance of an executing program. It is an independent entity that is allocated system resources such as CPU time and memory. Each process runs in a separate address space and cannot access the variables or data structures of other processes. If one process needs to access the resources of another process, inter-process communication (IPC) must be used. IPC methods include pipes, files, and sockets.

- **Thread**: Threads exist within a process and share the process's resources, such as the heap space. Multiple threads within the same process share the same heap space. However, a process cannot directly access the memory of another process. Each thread has its own registers and stack, but they can read and write to the shared heap memory.

- Threads are like specific execution paths within a process. When one thread modifies the resources of a process, other sibling threads can immediately see the changes.

### Context Switching

Context Switching is the time it takes to switch between two processes. It refers to the time it takes to transition a waiting process to the running state and to transition a running process to the waiting or terminated state. This occurs during multitasking. The operating system needs to load the state information of the waiting process into memory and save the state information of the currently running process. The efficiency of context switching can impact the overall performance of a multitasking system.

### Deadlock

#### Conditions for Deadlock

- **Mutual Exclusion**: Only one process can use a shared resource at a time.
- **Hold and Wait**: A process holding a resource can request additional resources without releasing the ones it already holds.
- **No Preemption**: Resources cannot be forcibly taken away from a process.
- **Circular Wait**: There is a circular chain of two or more processes, where each process is waiting for a resource held by another process in the chain.

Since it is difficult to release Mutual Exclusion for most shared resources, the focus is on preventing Circular Wait.

### Synchronous vs Asynchronous

- **Function Calls and Overhead**

  - **Synchronous Functions**: Synchronous functions have a direct and simple call stack. Each function is executed until completion when called, without any context switching to other tasks. This is highly efficient and eliminates unnecessary delays in the execution of tasks.
  - **Asynchronous Functions**: Asynchronous functions, such as asyncio, schedule and execute tasks using an event loop. This process involves additional steps such as function calls, task preparation, registering tasks with the event loop, and waiting for completion. Each of these steps incurs overhead, which can have an impact on the overall execution time, especially in CPU-bound tasks.

- **Nature of the Task**

  - **CPU-Bound Tasks**: Problems like FizzBuzz involve calculating numbers and evaluating conditions, which are CPU-bound tasks. In such tasks, continuous and fast processing is important. Synchronous processing methods that can handle tasks quickly may be more suitable for CPU-bound tasks.
  - **I/O-Bound Tasks**: Asynchronous functions are effective in handling I/O tasks (e.g., file reading/writing, network requests). I/O tasks have long waiting times, so the event loop can perform other tasks while waiting for the completion of I/O tasks, making efficient use of resources.

- **Suitability of Asynchronous Programming**: Asynchronous programming is designed to optimize inherently inefficient I/O tasks. Therefore, applying asynchronous programming to simple computational tasks that are not I/O-bound can be overkill and may even degrade performance.

In the end, the choice of technology should always be based on the nature of the problem. For CPU-bound tasks like FizzBuzz, traditional synchronous processing methods may be more efficient in terms of performance. Asynchronous programming primarily demonstrates its advantages in I/O-bound tasks, so it is important to understand the nature of the task and choose the appropriate tool.

### Python's Lifecycle Management

#### Program Execution

- **Source Code Interpretation**: When a Python program starts, the Python interpreter first reads the source code. This code can be in the form of a text file (.py) or already compiled bytecode (.pyc).
- **Compilation**: The source code is then compiled into bytecode by the built-in Python compiler. This bytecode is an intermediate form of code that the Python Virtual Machine (PVM) can understand.
- **Execution**: The compiled bytecode is executed by the Python Virtual Machine. The PVM is a stack-based interpreter that processes each operation sequentially.

#### Memory Management and Garbage Collection

- **Automatic Memory Management**: Python provides automatic memory management. Developers can focus on object creation, and the memory allocation for created objects is handled automatically by the Python interpreter.
- **Reference Counting**: Python tracks the number of references to an object and releases the object from memory when the reference count reaches 0. This is the most basic memory management technique.
- **Garbage Collection**: To address cyclic reference problems that cannot be solved by reference counting alone, Python includes a garbage collector. It periodically scans the memory to find and release objects that are no longer reachable.
- **Generational Collection**: Python uses a generational garbage collection algorithm. It divides objects into multiple generations based on how long they have been created. Garbage from younger generations is collected more frequently, while older generations are collected less frequently. This method optimizes memory management efficiency.

#### Termination Handling

- **Cleanup**: When a program is terminated, the Python interpreter performs cleanup tasks such as closing open file handles, terminating network connections, and releasing all system resources allocated to the process.
- **Returning Exit Code**: The Python interpreter returns an exit code to the operating system to indicate whether the program terminated successfully or due to an error.
