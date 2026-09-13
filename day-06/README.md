# Basics of Shell Scripting

Shell scripting is the process of writing a series of commands in a file and executing them together using a **shell**.

Shell scripts are widely used in **Linux administration, DevOps, automation, deployment, monitoring, and system management**.


## 1. What is a Shell?

A **shell** is a command-line interface that allows users to interact with the operating system.

It accepts commands from the user and passes them to the operating system for execution.

```text
User
  |
  ↓
Shell
  |
  ↓
Operating System
  |
  ↓
Hardware
```

### Common Shells

* Bash
* Zsh
* Fish
* Korn Shell (Ksh)
* C Shell (csh)

**Bash (Bourne Again Shell)** is one of the most commonly used shells in Linux environments.


## 2. What is Shell Scripting?

A **shell script** is a text file containing a sequence of shell commands.

Instead of executing commands one by one, we can put them into a script and execute them together.

Example:

```bash
#!/bin/bash

echo "Hello, World!"
echo "Welcome to Shell Scripting"
```

Save the file as:

```text
hello.sh
```

## 3. How to Run a Shell Script

### Method 1 — Using Bash

```bash
bash hello.sh
```

### Method 2 — Give Execute Permission

```bash
chmod +x hello.sh
```

Then run:

```bash
./hello.sh
```

## 4. Shebang

The first line of a shell script is commonly called the **shebang**.

```bash
#!/bin/bash
```

It tells the system which interpreter should be used to execute the script.

For Bash:

```bash
#!/bin/bash
```

# 5. Comments

Comments are used to explain the code and are not executed.

A single-line comment starts with `#`.

```bash
# This is a comment

echo "Hello"
```

Comments make scripts easier to understand and maintain.

# 6. Variables

Variables are used to store values.

```bash
name="Surya"
age=23

echo $name
echo $age
```

Output:

```text
Surya
23
```

### Important

There should be **no spaces** around `=`.

Correct:

```bash
name="Surya"
```

Incorrect:

```bash
name = "Surya"
```

# 7. User Input

The `read` command is used to accept input from the user.

```bash
#!/bin/bash

echo "Enter your name:"
read name

echo "Hello $name"
```

Example:

```text
Enter your name:
Surya

Hello Surya
```

# 8. Command-Line Arguments

Shell scripts can accept arguments when they are executed.

Example:

```bash
#!/bin/bash

echo "Hello $1"
```

Run:

```bash
./hello.sh Surya
```

Output:

```text
Hello Surya
```

### Common Arguments

| Variable | Meaning             |
| -------- | ------------------- |
| `$0`     | Script name         |
| `$1`     | First argument      |
| `$2`     | Second argument     |
| `$#`     | Number of arguments |
| `$@`     | All arguments       |


# 9. Conditional Statements

Conditions allow a script to make decisions.

### Example

```bash
#!/bin/bash

age=20

if [ $age -ge 18 ]
then
    echo "You are an adult"
else
    echo "You are a minor"
fi
```

Output:

```text
You are an adult
```

### Common Comparison Operators

| Operator | Meaning               |
| -------- | --------------------- |
| `-eq`    | Equal                 |
| `-ne`    | Not equal             |
| `-gt`    | Greater than          |
| `-lt`    | Less than             |
| `-ge`    | Greater than or equal |
| `-le`    | Less than or equal    |


# 10. File Conditions

Shell scripting can check whether files and directories exist.

```bash
if [ -f "test.txt" ]
then
    echo "File exists"
else
    echo "File does not exist"
fi
```

Common tests:

| Test | Meaning                  |
| ---- | ------------------------ |
| `-f` | Regular file exists      |
| `-d` | Directory exists         |
| `-e` | File or directory exists |
| `-r` | Readable                 |
| `-w` | Writable                 |
| `-x` | Executable               |


# 11. Loops

Loops are used to execute commands repeatedly.

## For Loop

```bash
#!/bin/bash

for name in Alice Bob Charlie
do
    echo "Hello $name"
done
```

Output:

```text
Hello Alice
Hello Bob
Hello Charlie
```

## While Loop

```bash
#!/bin/bash

count=1

while [ $count -le 5 ]
do
    echo "Count: $count"
    count=$((count + 1))
done
```

# 12. Functions

Functions allow you to group commands and reuse them.

```bash
#!/bin/bash

greet() {
    echo "Hello, Welcome to DevOps!"
}

greet
```

A function can also accept arguments:

```bash
greet() {
    echo "Hello $1"
}

greet Surya
```

Output:

```text
Hello Surya
```

# 13. Arithmetic Operations

Shell scripts can perform basic mathematical operations.

```bash
a=10
b=5

sum=$((a + b))

echo "Sum: $sum"
```

Output:

```text
Sum: 15
```

Other operations:

```bash
sum=$((a + b))
difference=$((a - b))
multiplication=$((a * b))
division=$((a / b))
```


# 14. Useful Shell Commands

Shell scripting commonly uses Linux commands such as:

```bash
pwd
ls
cd
mkdir
touch
cp
mv
rm
cat
grep
find
echo
date
whoami
df
du
ps
top
systemctl
```

Example:

```bash
#!/bin/bash

echo "Current user:"
whoami

echo "Current directory:"
pwd

echo "Files:"
ls
```

# 15. Pipes

A pipe `|` sends the output of one command as input to another command.

Example:

```bash
ls | grep ".txt"
```

This lists files and filters the output to show `.txt` files.

```text
Command 1
   |
   | Output
   ↓
Command 2
```

# 16. Redirection

Redirection is used to send command output to a file.

### `>` — Overwrite

```bash
echo "Hello" > output.txt
```

### `>>` — Append

```bash
echo "Welcome" >> output.txt
```

### `<` — Input

```bash
command < input.txt
```

# 17. Exit Status

Linux commands return an **exit status** after execution.

Usually:

```text
0 → Success
Non-zero → Error/Failure
```

Check the previous command's exit status:

```bash
echo $?
```

Example:

```bash
ls
echo $?
```

If `ls` succeeds:

```text
0
```

# 18. Basic Error Handling

You can check whether a command was successful.

```bash
mkdir test

if [ $? -eq 0 ]
then
    echo "Directory created successfully"
else
    echo "Failed to create directory"
fi
```

A commonly used Bash option is:

```bash
set -e
```

It causes the script to stop when a command returns a non-zero status.

# 19. Simple Shell Script Example

```bash
#!/bin/bash

# Display system information

echo "===== System Information ====="

echo "Hostname:"
hostname

echo "Current User:"
whoami

echo "Current Directory:"
pwd

echo "Disk Usage:"
df -h

echo "Memory Usage:"
free -h

echo "=============================="
```

This type of script can be useful for basic **system administration and monitoring**.

# 20. Shell Scripting in DevOps

Shell scripting is commonly used for:

* System administration
* Server configuration
* Application deployment
* Log management
* Backup automation
* Monitoring
* File management
* AWS CLI automation
* CI/CD pipelines
* Infrastructure automation

Example DevOps workflow:

```text
Shell Script
     |
     ↓
AWS CLI
     |
     ↓
AWS Resources
```

A Bash script can, for example, use AWS CLI commands to list EC2 instances, S3 buckets, or other AWS resources.


# 21. Basic Shell Script Workflow

```text
Write Script
     ↓
Save as .sh
     ↓
Give Execute Permission
     ↓
Run Script
     ↓
Check Output
     ↓
Debug if Required
```

Example:

```bash
nano script.sh
```

```bash
chmod +x script.sh
```

```bash
./script.sh
```


# Key Takeaways

* **Shell** provides an interface to interact with the operating system.
* **Bash** is one of the most commonly used Linux shells.
* A **shell script** contains multiple commands that can be executed together.
* Variables store values.
* `if` statements are used for decision-making.
* Loops execute commands repeatedly.
* Functions help reuse code.
* Pipes and redirection help process command output.
* Exit status helps determine whether a command succeeded.
* Shell scripting is an important skill for **Linux, Cloud, and DevOps automation**.


