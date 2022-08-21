# libjson
>Functions for handling JSON in Bash

## Contents
- [About](#About)
- [Speed](#Speed)
- [Usage](#Usage)

## About
These functions are for parsing and using JSON for Bash purposes. Requires `sed, grep, awk`. [The `json::sh` function is originally from dominictarr's JSON.sh.](https://github.com/dominictarr/JSON.sh) It's been modified slightly to work as a function and been made to use more widely adopted version of the UNIX tools. For example, Debian needs these changes: `gawk` -> `awk`, `egrep` -> `grep -E` for the function to work.

## Speed

| lines of JSON | time        |
|---------------|-------------|
| 30            | 0.015s      |
| 300           | 0.050s      |
| 3000          | 0.600s      |

## Usage
Input must be STDIN, no arguments: `cat file.json | json::sh`, or better: `json::sh < file.json`. The results will be printed to STDOUT.

**json::sh()**
```
Parse JSON
```
This function works exactly the same as [`JSON.sh`](https://github.com/dominictarr/JSON.sh), but it's in function form.

---

**json::var()**
```
Parse JSON into Shell variable declarations
```
This parses the output of `json::sh()` into Shell variable declarations, for example:
```
["result","block_header","depth"]    2693828    <- this is output from: json::sh < file.json
result_block_header_depth=2693828               <- this is output from: json::var < file.json        
```
These variables aren't declared, just printed to STDOUT.

---

**json::src()**
```
Declare the JSON values as GLOBAL Shell variables
```
This works the same as `json::var()`, but it actually sources those values into GLOBAL variables:
```
json::src < file.json
echo $result_block_header_depth

2693828
```
