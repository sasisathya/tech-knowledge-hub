Here’s the high-level picture:

### What is Java?

* A **programming language** and **platform** designed for “**write once, run anywhere**.”
* You write **.java** source, compile to **bytecode (.class)**, and that runs on a virtual machine (the JVM).
* Statically typed, object-oriented (with modern functional features), huge ecosystem.

### JVM (Java Virtual Machine)

* The **runtime** that executes Java bytecode.
* Provides **just-in-time (JIT) compilation**, **garbage collection**, and security sandboxing.
* Different vendors implement it (HotSpot, OpenJ9), but bytecode is portable across them.

### JRE (Java Runtime Environment)

* Everything needed to **run** Java apps: **JVM + core libraries** (and modules).
* Historically downloadable separately; today it’s mostly thought of as “the runtime part of the JDK.”

### JDK (Java Development Kit)

* Everything in the **JRE**, **plus developer tools** to **build** Java apps:

  * `javac` (compiler), `java` (launcher), `javadoc`, `jar`, `jlink`, debuggers, profilers, etc.
* If you’re **developing**, install a **JDK** (not just a runtime).

### How they fit together (flow)

`Your .java code` → **javac** (from JDK) → `.class` bytecode → **JVM** runs it using **JRE** libraries.

**Quick tip:** After installing a JDK, check:

```
java -version
javac -version
```
### Just-In-Time (JIT) Compilation

* JIT is a runtime optimization technique where code is compiled into machine code only when it’s needed (just in time) — not beforehand.

If both work, you’re set.
