# Examples

## Function-like class instances

Some classes behave like functions;
or, sometimes we create classes to extend a function.

Decorators can be used to create instances out of function definitions.

(Script available in [repo](https://github.com/MichaelKim0407/python-decorators/tree/master/3-examples/5-class).)

```python
class Task(object):
    def __init__(self, func):
        self.__func = func
        self.__next = []

    def next(self, task):
        if not isinstance(task, Task):
            task = Task(task)
        self.__next.append(task)
        return task

    def __call__(self, *args, **kwargs):
        result = self.__func(*args, **kwargs)
        for task in self.__next:
            task(*args, **kwargs)
        return result

@Task
def task_1(x):
    print(type(x))

@task_1.next
def task_2(x):
    print(x)

@task_1.next
def task_3(x):
    print(2 ** x)

@task_2.next
def task_4(x):
    print(x ** 2)

if __name__ == '__main__':
    task_1(10)
```

[Prev](../4-generator/README.md) /
[Up](../README.md) /
[Next](../../4-builtins/README.md)