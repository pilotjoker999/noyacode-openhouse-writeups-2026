# CTF Writeup

We first analyze the source code provided:

```python
if __name__ == '__main__':
    print(eval(input("Enter math: ")))
````

## What the code does

This code prompts the user for input (a “math expression”), evaluates that input, and prints the result.

## Vulnerability

The vulnerability is the unsafe use of `eval()`.

`eval()` takes a string and executes it as Python code. That means it doesn’t just evaluate math expressions - it will run *any* valid Python expression provided by the user. As a result, an attacker can supply malicious Python code and have it executed by the program.

## Exploit

In this challenge, we input:

```python
open('flag.txt').read()
```

This expression instructs the program to open `flag.txt` and read its contents (commonly where the flag is stored in CTF challenges). Since the program prints the result of `eval(...)`, the contents of `flag.txt`—the flag—get printed.
