# STDOUT
According to the [Python documentation](https://docs.python.org/3/library/sys.html#sys.stdout), Python STDOUT is default block buffered (not in real-time) and not line buffered (in real-time). It only appears to be line buffered, because the OS makes it line buffered, when the stream is connected to an interactive device like a terminal (see [GNU libc manual](https://www.gnu.org/software/libc/manual/html_node/Buffering-Concepts.html)). This means if a stream is not in a terminal, the output is not directly visible.  
This Python script is used in the following examples.
```python
import time

for i in range(10):
    print(i)
    time.sleep(1)
```

## In terminal
Running the script in an interactive terminal will directly output the printed text.
```bash
python3 example.py
```

## Pipe into file
The following example is non interactive and therefore the output is not directly visible.
```bash
python3 example.py > log.txt
```

## Docker
Running a docker image, which executes the Python script, will only print the output directly if the **-it** flags are set.
```docker
... some code
CMD ['python3', 'example.py']
```

Block buffered:
```bash
docker run example_image
```

Line buffered:
```bash
docker run -it example_image
```

The docker example is especially tricky, because you won't see logs in a Kubernetes cluster, if STDOUT is block buffered.

## Change this behaviour
You can use the **-u** flag to Change the complete Python execution to a line buffered STDOUT:
```bash
python3 -u example.py
```
Another option with the same result is to set the **PYTHONUNBUFFERED** environment variable.

You can also flush on demand with:
```python
print('some text', flush=true)
```

or 
```python
import sys

print('some text')
sys.stdout.flush()
```

## Trivia
Python prints will only be flushed in a terminal, if the text ends with a line ending. So the prints in the following example are not directly visible:

```python
import time

for i in range(10):
    print(i, end='')
    time.sleep(1)
```
