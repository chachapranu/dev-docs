
# Control Structures

Control structures are used to control the flow of execution in a shell script.

**If-else:**

```bash
if [ -f "/etc/passwd" ]; then
    echo "File exists"
else
    echo "File does not exist"
fi
```

**For loop:**

```bash
for i in {1..5}; do
    echo $i
done
```

[Back to Shell Scripting](./index.md)
