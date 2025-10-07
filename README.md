# GDB Debugging Help Sheet
.md helper file with GDB debbuging commands and how they work.


## 🧭 Starting & Setup
**Command** | **Description**
--- | ---
`gdb ./program` | Start debugging an executable.
`gdb --args ./program arg1 arg2` | Start with command-line arguments.
`run` (or `r`) | Start running the program inside GDB.
`quit` (or `q`) | Exit GDB.
`help` | Show general help or `help <command>` for details.
`file <program>` | Load a new program into the same GDB session.

---

## 🎯 Breakpoints
**Command** | **Description**
--- | ---
`break main` | Set a breakpoint at function `main`.
`break file.c:42` | Break at line 42 of file.c.
`break my_func` | Break at the start of `my_func()`.
`tbreak my_func` | Temporary breakpoint (auto-removed after hit).
`info breakpoints` | List all breakpoints.
`delete <n>` | Delete breakpoint n.
`disable <n>` / `enable <n>` | Temporarily disable/enable a breakpoint.

---

## ▶️ Running & Control Flow
**Command** | **Description**
--- | ---
`continue` (or `c`) | Resume execution until next breakpoint.
`next` (or `n`) | Execute next line (skip into functions).
`step` (or `s`) | Step *into* function calls.
`finish` | Run until current function returns.
`until` | Run until the current loop ends or next line in same frame.
`return` | Force-return from current function.
`Ctrl-C` | Interrupt the running program.

---

## 🔍 Inspecting Program State
**Command** | **Description**
--- | ---
`print <expr>` (or `p`) | Print value of an expression, variable, or pointer.
`p *ptr` | Dereference and show what a pointer points to.
`display <expr>` | Auto-print this expression each step.
`undisplay <n>` | Stop auto-printing display n.
`info locals` | Show local variables in current function.
`info args` | Show function arguments.
`bt` (or `backtrace`) | Show the call stack (functions leading to here).
`frame <n>` | Jump to a specific stack frame from `bt`.
`info frame` | Show info about the current stack frame.

---

## 🧠 Memory Inspection
**Command** | **Description**
--- | ---
`x/<count><format><size> <address>` | Examine memory (e.g. `x/10xb ptr` shows 10 bytes).
Formats | `x` (hex), `d` (decimal), `s` (string), `i` (instruction)
Sizes | `b` (byte), `h` (halfword), `w` (word 4B), `g` (8B)
Examples | `x/4xw &arr` → show 4 words in hex from arr.
`info registers` | Show CPU registers (useful in assembly view).

---

## 🧩 Source Navigation
**Command** | **Description**
--- | ---
`list` (or `l`) | Show 10 lines around current execution point.
`list file.c:20` | Show source near line 20 in file.c.
`list my_func` | Show function source.
`info source` | Show which file is currently loaded.

---

## 🪜 Stack & Frames
**Command** | **Description**
--- | ---
`bt` | Show backtrace of all function calls.
`up` / `down` | Move up/down the call stack.
`frame <n>` | Select a specific frame number.

---

## ⚙️ Program State Modification
**Command** | **Description**
--- | ---
`set var <var>=<value>` | Change a variable’s value while paused.
`call <func>(args)` | Call a function manually.
`jump <line>` | Force the program to continue from another line.

---

## 🧱 Watchpoints (Track Variables)
**Command** | **Description**
--- | ---
`watch <var>` | Break when a variable changes.
`rwatch <var>` | Break when variable is read.
`info watchpoints` | List all active watchpoints.

---

## 🧩 Arguments, Env, and I/O
**Command** | **Description**
--- | ---
`run arg1 arg2` | Run program with arguments.
`set args arg1 arg2` | Set default run arguments.
`show args` | Show current default arguments.
`set env NAME=VALUE` | Set an environment variable.
`unset env NAME` | Remove environment variable.
`tty /dev/pts/...` | Redirect stdin/stdout to a terminal.

---

## 🧰 Useful Modes & TUI
**Command** | **Description**
--- | ---
`start` | Run program and stop at main().
`starti` | Run and stop at first instruction.
`tui enable` | Enable split-screen text UI.
`tui disable` | Disable TUI.
`layout src / asm / split` | Choose layout (source, assembly, split).
`refresh` | Redraw the TUI display.

---

## ⛓️ Breakpoint Management (Extras)
**Command** | **Description**
--- | ---
`break file.c:function` | Break at function in file.
`break if <cond>` | Conditional breakpoint.
`condition <n> <cond>` | Add condition to breakpoint n.
`commands <n>` ... `end` | Run commands when bp n hits.

---

## 🧵 Threads & Processes
**Command** | **Description**
--- | ---
`info threads` | List threads.
`thread <id>` | Switch to thread.
`break ... thread <id>` | Thread-specific breakpoint.
`set follow-fork-mode child|parent` | Choose process to follow after fork.
`set detach-on-fork on|off` | Keep or detach from the other process.

---

## 🚨 Signals
**Command** | **Description**
--- | ---
`info signals` | List signals and handling.
`handle SIGSEGV print stop` | Customize signal behavior.
`signal 0` | Continue without delivering signal.

---

## 🧩 Core Files & Post-mortem
**Command** | **Description**
--- | ---
`gdb ./prog core` | Open a core dump.
`where` | Show backtrace at crash.
`info registers` | Check registers at crash time.

---

## 💻 Disassembly & Mixed Mode
**Command** | **Description**
--- | ---
`disassemble` | Disassemble around PC.
`disassemble /m` | Mixed source/assembly view.
`x/i $pc` | Show next instruction.
`set disassemble-next-line on` | Auto-show next instruction.

---

## 🧾 Scripting & QoL Tweaks
**Command** | **Description**
--- | ---
`set pagination off` | Disable “--More--” pauses.
`set print pretty on` | Pretty-print structs.
`set print elements 0` | Show full arrays.
`set confirm off` | Disable confirmation prompts.
`set history save on` | Save GDB command history.
`source .gdbinit` | Run custom script.
`define hook-stop ... end` | Run commands every time program stops.

---

## ⚡ Quick Example
```bash
gdb ./buggy-factorial
(gdb) break main
(gdb) run 5
(gdb) next
(gdb) print n
(gdb) backtrace
(gdb) quit
```

---

✅ **Tip:** Rebuild with `-g` flag to include debugging symbols:  
```bash
gcc -g -std=c99 program.c -o program
```

