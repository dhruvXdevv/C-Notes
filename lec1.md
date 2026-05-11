# CSC4700 – Spring 2025 | Lecture 1: Welcome and Introduction
**Instructor:** Hartmut Kaiser | **Date:** January 14, 2025
**Course Website:** https://teaching.hkaiser.org/spring2025/csc4700/

---

## 1. Course Overview

- The central idea: **Programs = Algorithms + Data Structures**
- Two main pillars:
  - **Selecting the right data structure**
    - Selecting containers: considered trivial
    - Selecting data types based on type properties: more nuanced
  - **Selecting and developing algorithms**
    - Algorithmic thinking is core
    - Parallelization is treated almost as an afterthought (it comes naturally once good algorithmic thinking is in place)

---

## 2. Admin & Organizational Info

- **Course coverage:** Depth-first introduction → C++ Standard Library → C++ Data Structures & Algorithms → Parallel Algorithms → Scientific Applications → Architectures → Parallel Programming Models
- **Contact:**
  - Website: https://teaching.hkaiser.org
  - Email: hkaiser@cct.lsu.edu
  - Discord: https://discord.gg/Q32sGfKqMS

### Required Reading
- Diehl's *Parallel C++*
- Stepanov's *From Mathematics to Generic Programming*
- Koenig's *Accelerated C++*
- Stroustrup's *Programming – Principles and Practice Using C++*

### Tools
- **GitHub Classroom** for assignment submission
- **VSCode** as the primary development tool

---

## 3. Important Dates

- **Lectures:** Tuesday & Thursday, 10:30–11:50, Room 1212 PFT
- **Grading Breakdown:**
  - Homework: 50%
  - Project: 25%
  - Midterm Exam: 10%
  - Final Exam: 15%
- **Midterm Exam:** March 6
- **Final Exam:** May 8, 5:30 PM – 7:30 PM

---

## 4. Ground Rules

- All course information lives at **teaching.hkaiser.org** — following it positively impacts grade
- **Attendance** is expected and positively impacts grade
- **Assignments:**
  - Up to five individual assignments focused on writing code
  - Use standard C++ algorithms and data structures
  - Use various parallel programming models
  - **Assignment 0** already posted — due: **January 27, 11:59 PM**
- All assignments and the project are hosted on GitHub / managed via GitHub Classroom
- Students must create a GitHub account

---

## 5. Academic Honesty

- LSU Code of Student Conduct (Section 5.1.16) defines plagiarism as: unacknowledged use of someone else's words, structure, ideas, or data
- **Plagiarism is not tolerated** — dealt with per LSU Code of Student Conduct
- Reference: https://www.lsu.edu/saa/students/codeofconduct.php

---

## 6. Policy on ChatGPT / AI Tools

- **The goal is to train your brain, not ChatGPT** — the instructor strongly discourages use
- There are too many developers who copy-paste without understanding
- **If you do use it:**
  - Never use anything without carefully reviewing it
  - Assume what you got is wrong — prove it is correct yourself
  - The skill of reading and understanding code becomes more important than ever
  - Cite and annotate any copied code
- **Bottom line:** Submitting the same code as your neighbor — regardless of source (Google, ChatGPT, classmate) — is plagiarism

---

## 7. How to Learn (Learning Philosophy)

**At the beginning of semester, ask yourself:**
- What scientific problem do I want to solve?
- What do I want to learn from this course to prepare for it?
- Can I write a sequential program to solve it? What is its performance?

**At the end of the semester, ask yourself:**
- Did I master the skillset to solve my scientific problem?
- Can I write a high-performance program to solve it?
- What is the performance? What is the speedup?
- Compare your sequential program with your high-performance program

---

## 8. Tour of the Course

### Hardware Topics
- Basic CPU machine model
  - Hierarchical memory: registers → cache → virtual memory
  - Instruction level parallelism
  - Multicore processors
- Scientific computing and linearization of physics models
- Shared memory parallelism
- GPU computing
- Distributed memory parallelism

### Software Topics
- Elements of C++
- Elements of software organization
- Elements of software practice
- Elements of performance measurement and optimization

The course balances **Hardware** and **Software** — like two sides of the same coin.

---

## 9. What This Course Is About

- How **algorithms, data, software, and hardware interact** to affect performance — and how to orchestrate them for high performance
- **Upon completion, students will be able to:**
  - Write software that fully utilizes hardware performance features
  - Describe principal architecture mechanisms for high performance and the algorithmic/software techniques to take advantage of them
  - Recognize opportunities for performance improvement in existing code
  - Describe a strategy for tuning HPC code
- Skills that are relevant **today and years from now**

---

## 10. Why HPC (High-Performance Computing) Matters

- Computing is considered the **3rd (and 4th?) pillar** of science and engineering
- Enables investigations where physical experiments would be too fast, too slow, too hot, too cold, too costly, or too dangerous
- Examples: Weather forecasting, climate modeling, nuclear fusion, crash testing
- HPC → more and better scientific discovery → better world, survival of the planet

### Uses of HPC (Sample List)
Cosmology, Earthquake simulation, Weather, Climate modeling, Automobile crash testing, Aircraft design, Jet engine design, Stockpile stewardship, Nuclear fusion, Protein folding, Modeling the brain, Modeling the bloodstream, Epidemiology, CGI Rendering, Signals intelligence, Blockchains, Gene sequencing, and more.

---

## 11. The HPC Canon (as of 2025)

| Technology | Paradigm | Tool ("Hammer") |
|---|---|---|
| CPU (single core) | Sequential | C compiler |
| SIMD/Vector (single core) | Data parallel | Intrinsics (asm) |
| Multicore | Threads | pthreads (C) library |
| NUMA shared memory | Threads | pthreads (C) library |
| GPU | GPU | CUDA |
| Clusters | Message passing | MPI (C) library |

→ This entire course uses **C++** as the single unifying tool across all these paradigms.

---

## 12. CPU Architecture Progression

### Simplest CPU Model
- CPU fetches and executes instructions one at a time
- Many cycles per instruction

### Pipelining
- Instructions fetched in a stream (i0, i3, i4, i5, i6 simultaneously in different pipeline stages)
- Long trip from memory is a bottleneck

### Hierarchical Memory
- Special fast memory (L1, L2 cache) keeps data and instructions close to the processor
- Registers → L1 cache (I & D) → L2 → Main memory (DRAM)

### Multicore CPUs
- Multiple cores on one chip (replicate 2×, 4×)
- Cores share slower memory (L3)
- Caches need to be kept **coherent**
- DRAM is very slow (super-slow compared to caches)

### Symmetric Multi-Processor (SMP)
- Multiple CPU chips ("sockets")
- Memory may be **uniformly shared** among sockets → **UMA (Uniform Memory Access)**
- Caches still need to be kept coherent

### Asymmetric Multi-Processor (NUMA)
- Multiple CPU chips, but memory is **non-uniformly shared** among sockets
- **CC-NUMA (Cache-Coherent NUMA)** — most common in modern servers
- Memory access time depends on which socket the memory is attached to

### GPU
- Graphics Processing Unit — massively parallel co-processor
- Programmed with CUDA (NVIDIA)

### Clusters / Supercomputers
- Sockets → Blades → Chassis → Racks → Data Centers → Cloud
- This is how supercomputers are built
- Inter-node communication via MPI (Message Passing Interface)

---

## 13. Computational Science

All scientific computing follows this pipeline:

**System of Partial Differential Equations (PDEs)**
→ *discretize*
→ **System of Nonlinear Equations** [F(x) = 0]
→ *linearize*
→ **System of Linear Equations** [Ax = b]

Three PDE types: Elliptic, Parabolic, Hyperbolic — all reduce to solving linear systems.

---

## 14. Why C++?

- You can't learn to program without a language
- C++ allows expression of ideas from the **largest number of application areas**
- **Most widely used language in engineering domains**
  - Reference: http://www.research.att.com/~bs/applications.html
- Large parts of modern society's software rely on C/C++:
  - Windows, Linux, Office Suite, Adobe products
  - Self-driving cars, industrial equipment
  - The Internet
- C++ is **precisely and comprehensively defined by an ISO standard** (C++17, now also C++23)
- Available on almost all kinds of computers
- Concepts transfer to other languages (C, Java, C#, Fortran)
- **C++ jobs are among the best-paid jobs available**

---

## 15. Why Parallel C++?

- Modern computers have **more than one core** — often many more
- Many programs require doing **many things at once (MTAO)**
- Scientific computing requires a lot of number crunching — parallelization is essential to reduce execution times
- **C++ offers:**
  - Parallel algorithms (divide a loop into simultaneously processed subtasks)
  - Task and Data parallelism
    - Task parallelism: distributing tasks across cores
    - Data parallelism: dividing data arrays into chunks processed in parallel
  - Asynchronous execution

### Motivation for Parallelism
- Operating systems: processes, interrupts, background maintenance
- Networked servers: multiple simultaneous connections
- Parallel programs: better performance
- UI programs: responsiveness during computation
- Network/disk-bound programs: hide latency, sequence access steps

---

## 16. A First C++ Program

```cpp
// Our first C++ program
#include <algorithm>
#include <print>
#include <vector>

int main()  // main() is where a C++ program starts
{
    std::vector<double> data = { 1.0, 2.0, 3.0, 4.0, 5.0, 6.0 };
    auto sum = std::reduce(data.begin(), data.end());
    std::print(std::stdout, "Sum of all values: {}\n", sum);
    return 0;
}
```

### Key Concepts Introduced
- **Expressions:** compute something, yield a result, may have side effects; involve operands, operators, and types
- **Scope:** part of the program where a name has meaning
  - Global scope
  - Namespace scope
  - Block scope
- **Algorithms:** e.g., `std::reduce`
- **Program structure:** free-form except string literals, `#include`, and comments
- **Types:** data structures and their operations (built-in and user-defined)
- **Functions:** code structure; helps isolate/abstract sub-functionalities
- **Namespaces:** group related names (e.g., `std::`)

### Special Character Literals
| Sequence | Meaning |
|---|---|
| `\n` | Newline |
| `\t` | Horizontal tab |
| `\b` | Backspace |
| `\"` | Double quote (doesn't terminate string) |
| `\'` | Single quote (doesn't terminate char literal) |
| `\\` | Backslash (no special meaning to next char) |

---

## 17. A First Parallel C++ Program

```cpp
#include <algorithm>
#include <execution>
#include <print>
#include <vector>

int main()
{
    std::vector<double> data = { 1.0, 2.0, 3.0, 4.0, 5.0, 6.0 };
    auto sum = std::reduce(std::execution::par, data.begin(), data.end());
    std::println("Sum of all values: {}", sum);
    return 0;
}
```

- `std::execution::par`: execution policy that tells the library it's OK to execute out of order
- This is a **hint** to the library — implementation decides how to execute; no direct control over execution

---

## 18. A First Parallel HPX Program

```cpp
#include <hpx/algorithm.hpp>
#include <hpx/execution.hpp>
#include <print>
#include <vector>

int main()
{
    std::vector<double> data = { 1.0, 2.0, 3.0, 4.0, 5.0, 6.0 };
    hpx::execution::experimental::num_cores nc(2);
    auto sum = hpx::reduce(hpx::execution::par.with(nc), data.begin(), data.end());
    std::println("Sum of all values: {}", sum);
    return 0;
}
```

- `hpx::execution::par`: tells library to execute out of order
- `hpx::execution::experimental::num_cores`: encapsulates control over number of cores
- `.with(nc)`: associates the core count with the execution policy
- This **guarantees** the algorithm runs on exactly 2 cores — unlike `std::execution::par` which is only a hint

---

## 19. Algorithmic Thinking: Number of Unique Elements

**Problem:** Given `int a[] = { 1, 3, 1, 4, 1, 5 };`, how many unique integers?

### Naive Solution (Correct but Slow)
```cpp
#include <set>
std::set<int> set_of_ints(a, a + 6);
std::println("{}", set_of_ints.size());
```
- Uses a Red-Black Tree — O(n log n) with a **large constant coefficient**
- Re-sorts the entire data structure for each insertion unnecessarily

### Why Not Just Use Equality?
- Finding unique elements might seem to only need equality (not ordering)
- But we actually need **search/find**:
  - Equality → linear search O(n)
  - Sorting → binary search O(log n) — much faster

### Correct Solution
```cpp
#include <algorithm>
std::sort(a, a + std::size(a));
std::println("{}", std::unique(a, a + std::size(a)) - a);
```
- `std::unique` eliminates equal adjacent elements and returns an iterator to the first duplicate
- Must sort first; then `std::unique` runs in O(n) after O(n log n) sort

---

## 20. Use the Correct STL Data Structures

- **Rule: Whenever possible, use `std::vector`.**
- If you can't, find a way to make it work with `std::vector`
- Avoid advanced data structures except arrays:
  - Advanced structures are typically **slower** than simple ones due to modern hardware behavior
  - What worked in textbooks 10+ years ago is often no longer optimal
  - Computers have changed drastically — cache behavior dominates performance
- Occasionally the course will ask for other data structures — mostly to illustrate a specific point

---

## 21. Compilation and Linking

The build process:

1. You write **C++ source code** (human-readable)
2. **C++ compiler** translates it to **object code** (machine code the CPU understands)
3. **Linker** links your object code with system/library code (I/O, OS, windowing)
4. Result: an **executable program** (`.exe` on Windows, `a.out` on Unix)

```
C++ Source Code → [Compiler] → Object Code → [Linker + Library Object Code] → Executable
```

---

## 22. CMake

- CMake is a family of tools for **building, testing, and packaging** software
- This course uses it for building and testing
- CMake generates build system files (Makefiles, workspaces)
- User writes a single set of descriptive scripts defining **targets** and their **inter-dependencies**
- Well-integrated with many IDEs (including VSCode)

### Simplest CMakeLists.txt Example
```cmake
cmake_minimum_required(VERSION 3.0)
project(Demo1)
add_executable(Demo1 demo1.cpp)
```

### Build Steps
```bash
cd demo1
ls        # → CMakeLists.txt   demo1.cpp
cmake .   # → Detects compilers, generates Makefiles
make      # → Compiles and links
./Demo1   # → Hello, world!
```

---

## 23. Homework and Projects Setup

- **VSCode** is the primary development environment
  - Assignment 0 will guide through installation
  - Alternative: GitHub Codespaces (fully online)
- **GitHub Classroom** manages submissions
  - Get a GitHub account at github.com (required for Assignment 0)
  - Learn Git source control system throughout the course
  - A special lecture will cover the development environment (git, cmake, etc.)

---

## 24. Hello, World! — Its Importance

"Hello, World!" is a critically important program because it verifies:
- The **compiler** is working
- The **program development environment** is set up
- The **program execution environment** is functional

After getting it to work, deliberately introduce errors to see how tools respond:
- Forget the header
- Forget to terminate the string
- Misspell `return` (e.g., `retrun`)
- Forget a semicolon
- Forget `{` or `}`

---

## 25. Summary / Key Takeaways

- **Single-thread performance is improving very slowly** — to run programs significantly faster, programs must utilize multiple processing elements or specialized hardware
- Writing parallel programs is **challenging** — requires problem partitioning, communication, synchronization
- **Knowledge of machine characteristics is critical**, especially understanding **data movement**
- Modern computers have **tremendously more processing power** than most programs use — the key is using it efficiently

---

*End of Lecture 1 Summary*
