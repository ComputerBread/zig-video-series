# Illegal Behavior

Many programming languages have the idea of "Undefined Behaviors" that refers
to programs which behavior is not well specified, and their results will depend
on the compiler which is allowed to do anything it wants!
To minimize the number of Undefined Behaviors, and make the language safer, Zig
defines the concept of "Illegal Behaviors" ; operations that are known to be
wrong, and should be avoided at all costs!

Trying to access an element outside of an array, integer overflows, and dividing by
zero are examples of illegal behavior.
There are many more and they "all?" are documented in the documentation:

List of Illegal Behaviors

- Reaching Unreachable Code
- Index out of Bounds
- Cast Negative Number to Unsigned Integer
- Cast Truncates Data
- Integer Overflow
- Exact Left Shift Overflow
- Exact Right Shift Overflow
- Division by Zero
- Remainder Division by Zero
- Exact Division Remainder
- Attempt to Unwrap Null
- Attempt to Unwrap Error
- Invalid Error Code
- Invalid Enum Cast
- Invalid Error Set Cast
- Incorrect Pointer Alignment
- Wrong Union Field Access
- Out of Bounds Float to Integer Cast
- Pointer Cast Invalid Null


At compile-time, detected illegal behavior will produce compilation errors.
If there are not detected at compile-time, then there's two possibilities,

1. the first one is refered to as "safety-checked Illegal behavior". When possible
the Zig compiler will insert "safety checks", such that at runtime if an illegal
behavior is detected, by failing this safety check, then the program will panic and crash!
The default panic handler will print a nice stack trace!

(<https://ziglang.org/documentation/0.16.0/#Wrong-Union-Field-Access>)
For example, if you define a function taking a union as a parameter, but expecting
a specific field to be used, then this will not trigger any compile error

```zig
const Foo = union {
    float: f32,
    int: u32,
};

fn bar(f: *Foo) void {
    f.float = 12.34;
    std.debug.print("value: {}\n", .{f.float});
}
```

but at runtime if you pass it a value using the wrong union field:

```zig
pub fn main() void {
    var f = Foo{ .int = 42 }; // instead of .float
    bar(&f);
}
```

then it will trip on the safety check and crash:

```
thread 504992 panic: access of union field 'float' while field 'int' is active
/home/arthur/work/ComputerBread/scripts/zig/runtime_wrong_union_field_access.zig:14:6: 0x11d2e6e in bar (runtime_wrong_union_field_access.zig)
    f.float = 12.34;
     ^
/home/arthur/work/ComputerBread/scripts/zig/runtime_wrong_union_field_access.zig:10:8: 0x11d2dae in main (runtime_wrong_union_field_access.zig)
    bar(&f);
       ^
/home/arthur/.local/share/zigup/0.16.0/files/lib/std/start.zig:698:59: 0x11d26b1 in callMain (std.zig)
    if (fn_info.params.len == 0) return wrapMain(root.main());
                                                          ^
/home/arthur/.local/share/zigup/0.16.0/files/lib/std/start.zig:190:5: 0x11d20e1 in _start (std.zig)
    asm volatile (switch (native_arch) {
    ^
fish: Job 1, 'zig run runtime_wrong_union_fie…' terminated by signal SIGABRT (Abandon)
```


This is true in debug and releaseSafe mode, but these checks are disabled by
default in ReleaseFast and ReleaseSmall mode! But you can decide to enable or
disable them manually at the block-level, no matter what optimization mode you choose,
using `@setRuntimeSafety`. <https://ziglang.org/documentation/0.16.0/#setRuntimeSafety>


```zig
{
    @setRuntimeSafety(false);

    const a: u8 = 10;
    var b: u8 = 1;
    b -= 1;
    const c = a / b;

    std.debug.print("dividing by 0: {} / {} = {}", .{ a, b, c });
}
```


Most Illegal Behaviors are safety-checked.
But All the other one, are part of the second category:

2. "Unchecked illegal behavior", these are the Undefined Behaviors of Zig,
if one is invoked at runtime, then anything can happen: usually it will crash,
but the compiler or optimizer is free to do what it wants

An example of "unchecked illegal behavior" is to dereference an invalid pointer,
like one pointing outside of an array!


```zig
const a = [_]u8{ 1, 2, 3 };
const ptr = &a[0];
const outside: *const u8 = @ptrFromInt(@intFromPtr(ptr) + 10);
std.debug.print("outside: {}", .{outside.*});
```

And that's it for Illegal Behaviors!
So even tho, Zig comes with mechanisms to detect as many as possible, try to avoid them!


<https://ziglang.org/documentation/0.16.0/#Illegal-Behavior>




- [Reaching Unreachable Code](https://ziglang.org/documentation/0.16.0/#Reaching-Unreachable-Code)
- [Index out of Bounds](https://ziglang.org/documentation/0.16.0/#Index-out-of-Bounds)
- [Cast Negative Number to Unsigned Integer](https://ziglang.org/documentation/0.16.0/#Cast-Negative-Number-to-Unsigned-Integer)
- [Cast Truncates Data](https://ziglang.org/documentation/0.16.0/#Cast-Truncates-Data)
- [Integer Overflow](https://ziglang.org/documentation/0.16.0/#Integer-Overflow)
  - [Default Operations](https://ziglang.org/documentation/0.16.0/#Default-Operations)
  - [Standard Library Math Functions](https://ziglang.org/documentation/0.16.0/#Standard-Library-Math-Functions)
  - [Builtin Overflow Functions](https://ziglang.org/documentation/0.16.0/#Builtin-Overflow-Functions)
  - [Wrapping Operations](https://ziglang.org/documentation/0.16.0/#Wrapping-Operations)
- [Exact Left Shift Overflow](https://ziglang.org/documentation/0.16.0/#Exact-Left-Shift-Overflow)
- [Exact Right Shift Overflow](https://ziglang.org/documentation/0.16.0/#Exact-Right-Shift-Overflow)
- [Division by Zero](https://ziglang.org/documentation/0.16.0/#Division-by-Zero)
- [Remainder Division by Zero](https://ziglang.org/documentation/0.16.0/#Remainder-Division-by-Zero)
- [Exact Division Remainder](https://ziglang.org/documentation/0.16.0/#Exact-Division-Remainder)
- [Attempt to Unwrap Null](https://ziglang.org/documentation/0.16.0/#Attempt-to-Unwrap-Null)
- [Attempt to Unwrap Error](https://ziglang.org/documentation/0.16.0/#Attempt-to-Unwrap-Error)
- [Invalid Error Code](https://ziglang.org/documentation/0.16.0/#Invalid-Error-Code)
- [Invalid Enum Cast](https://ziglang.org/documentation/0.16.0/#Invalid-Enum-Cast)
- [Invalid Error Set Cast](https://ziglang.org/documentation/0.16.0/#Invalid-Error-Set-Cast)
- [Incorrect Pointer Alignment](https://ziglang.org/documentation/0.16.0/#Incorrect-Pointer-Alignment)
- [Wrong Union Field Access](https://ziglang.org/documentation/0.16.0/#Wrong-Union-Field-Access)
- [Out of Bounds Float to Integer Cast](https://ziglang.org/documentation/0.16.0/#Out-of-Bounds-Float-to-Integer-Cast)
- [Pointer Cast Invalid Null](https://ziglang.org/documentation/0.16.0/#Pointer-Cast-Invalid-Null)
