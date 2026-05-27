#### argparse
Handles command-line parsing

```
import argparse
def parse_args(): 
	parser = argparse.ArgumentParser(description='Train a neural network to      
	classify CIFAR10') 
	parser.add_argument('--model', type=str, default='r18', help='model to train 
	(default: r18)')
	return parser.parse_args()
```



#### lambada function

A **lambda function** in Python is a concise way to create an **anonymous function**, meaning a function that is defined without a name

```
lambda arguments: expression
```

- **`lambda`**: Keyword used to define a lambda function.
- **`arguments`**: A comma-separated list of parameters that the function takes (like a regular function).
- **`expression`**: A single expression that is evaluated and returned when the lambda function is called.

Lambda functions are commonly used with **functional programming constructs** like `map()`, `filter()`, and `reduce()`.


```
# Regular function 
def add(x, y): 
return x + y 

# Lambda function 
add_lambda = lambda x, y: x + y
```

```
numbers = [1, 2, 3, 4]
# Square each number using a lambda function 
squared = map(lambda x: x ** 2, numbers)
```

- The lambda function `lambda x: x ** 2` squares each element in the `numbers` list.

## File handling
- ### Read/Write files

 `open()` opens files for reading or writing and returns a file handle (`f` in this case) that provides methods that can be used to read or write data to the file.
It’s important to remember that it’s your responsibility to close the file. In most cases, upon termination of an application or script, a file will be closed eventually. However, there is no guarantee when exactly that will happen. This can lead to unwanted behavior including resource leaks.
 The best way to close a file is to use the `with` statement. The `with` statement automatically takes care of closing the file once it leaves the `with` block, even in cases of error.
 
```
with open('./data/data.txt', 'r' or 'w') as f:
	data = f.read()
	f.write('dddd')

```

- `.read(size = -1)` : This reads from the file based on the number of `size` bytes. If no argument is passed or `None` or `-1` is passed, then the entire file is read.

- `.readline(size = -1)` : This reads at most `size` number of characters from the line. This continues to the end of the line and then wraps back around. If no argument is passed or `None` or `-1` is passed, then only **one** entire line (or rest of the line) is read.

```
line = f.readline()    # reads only one line and returns it
while line != '':  # The EOF char is an empty string
	print(line)

```

- `.readlines()` : This reads the remaining lines (line by line) from the file object and returns them as a list of elements (one line as one element) and it puts a \n at the end of each line (element)

- ### strip()
The `strip()` method removes any leading, and trailing whitespaces.

```
 with open("./data/data1.txt") as f:
	data = [line.strip() for line in f.readlines()]
        
```

- ### split()
The `split()` method splits a string into a list. You can specify the separator, default separator is any whitespace. `string.split(separator, maxsplit)`

```
line.split()[0]
```

## zip()
`zip()` in Python aggregates elements from multiple iterables into tuples. `zip()` is **lazy** in Python, meaning it returns an iterator instead of a list. list(zipped variable) will return a list of tuples.

```
sorted_first = [2,3,4,5]
sorted_second = [4,5,6,7]
for first,second in zip(sorted_first,sorted_second):
	print(first + second)
```

## dictionary
- ### count.get(a,0)
```
count = {a:1, b:2}
count.get(a,0)   # return 0 if there is no 'a' in count, otherwise returns its value (here `1`)
```


### Fancy Indexing in Numpy :

- `list[indices]` fails when `indices` is a list of ints (e.g. `[0, 2, 5]`).
- `numpy_array[indices]` **works** and gives a sub-array — **this is called fancy indexing in NumPy.**