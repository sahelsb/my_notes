#### argparse
Handles command-line parsing

```python
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

```python
lambda arguments: expression
```

- **`lambda`**: Keyword used to define a lambda function.
- **`arguments`**: A comma-separated list of parameters that the function takes (like a regular function).
- **`expression`**: A single expression that is evaluated and returned when the lambda function is called.

Lambda functions are commonly used with **functional programming constructs** like `map()`, `filter()`, and `reduce()`.


```python
# Regular function 
def add(x, y): 
return x + y 

# Lambda function 
add_lambda = lambda x, y: x + y
```

```python
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
 
```python
with open('./data/data.txt', 'r' or 'w') as f:
	data = f.read()
	f.write('dddd')

```

- `.read(size = -1)` : This reads from the file based on the number of `size` bytes. If no argument is passed or `None` or `-1` is passed, then the entire file is read.

- `.readline(size = -1)` : This reads at most `size` number of characters from the line. This continues to the end of the line and then wraps back around. If no argument is passed or `None` or `-1` is passed, then only **one** entire line (or rest of the line) is read.

```python
line = f.readline()    # reads only one line and returns it
while line != '':  # The EOF char is an empty string
	print(line)

```

- `.readlines()` : This reads the remaining lines (line by line) from the file object and returns them as a list of elements (one line as one element) and it puts a \n at the end of each line (element)

- ### strip()
The `strip()` method removes any leading, and trailing whitespaces.

```python
 with open("./data/data1.txt") as f:
	data = [line.strip() for line in f.readlines()]
        
```

- ### split()
The `split()` method splits a string into a list. You can specify the separator, default separator is any whitespace. `string.split(separator, maxsplit)`

```python
line.split()[0]
```

## zip()
`zip()` in Python aggregates elements from multiple iterables into tuples. `zip()` is **lazy** in Python, meaning it returns an iterator instead of a list. list(zipped variable) will return a list of tuples.

```python
sorted_first = [2,3,4,5]
sorted_second = [4,5,6,7]
for first,second in zip(sorted_first,sorted_second):
	print(first + second)
```

## dictionary
- ### count.get(a,0)
```python
count = {a:1, b:2}
count.get(a,0)   # return 0 if there is no 'a' in count, otherwise returns its value (here `1`)
```


### Fancy Indexing in Numpy :

- `list[indices]` fails when `indices` is a list of ints (e.g. `[0, 2, 5]`).
- `numpy_array[indices]` **works** and gives a sub-array — **this is called fancy indexing in NumPy.**



### Building Dynamic SQL Queries in Python

When building search or filter features, you often don't know ahead of time which filters a user will pick. You need to build the SQL query dynamically while keeping it safe from **SQL Injection**.

##### The Core Strategy
1. **Default Argument**: Use `filter: dict = None` to make filters optional.
2. **Build Conditions**: Loop through the dictionary to create a **list of placeholders** (like `column_name = ?`).
3. **Keep Values Separate**: Put the actual values into a matching list to pass safely into the executor later.
4. **Join with AND**: Use `" AND ".join()` to glue the conditions together only if filters were actually provided.

```python
def get_filtered_data(filter_dict: dict = None) -> list:
    # 1. Handle optional input gracefully
    if not filter_dict:
        filter_dict = {}

    query = "SELECT * FROM my_table"
    where_clauses = []
    query_params = []

    # 2. Extract columns and separate values from placeholders
    for column, value in filter_dict.items():
        # WARNING: Only do this if 'column' comes from trusted internal code, 
        # never directly from user input (sanitize column names if needed).
        where_clauses.append(f"{column} = ?") 
        query_params.append(value)

    # 3. Assemble the WHERE string only if conditions exist
    if where_clauses:
        query += " WHERE " + " AND ".join(where_clauses)

    # 4. Execute safely
    conn = get_db_connection()
    cursor = conn.execute(query, query_params) # Params replace the '?' safely
    return cursor.fetchall()
```


#### Security risk :

```python
where_clauses.append(f"{column} = ?")   # column name → string-interpolated  
query_params.append(value)               # value → parameterized (?)          

```

 - The value is parameterized (?) → safe from injection. Good.
- The column name is interpolated straight into the SQL string. You cannot parameterize identifiers (column/table names) in SQL — only values. So **if column ever comes from client/user input, that's a SQL-injection hole** (e.g. **a client sends column = "1=1; DROP TABLE …"**).


## Project structure root run

##### The problem
The `src/` folder held flat top-level modules (`api.py, service.py, db.py, …`) that **imported
each other by bare name** (`from service import ...`). **Those imports only resolve when that
exact directory is on Python's import path (sys.path).**
  - `uv run python src/mcp_service.py` worked — **running a script auto-adds the script's own folder (src/) to sys.path.**
  - `uvicorn api:app` did not work from root — the **api:app import string is resolved against
  the current working directory**, which is why it forced `cd src && uvicorn ....`

##### The Solution
Turned the project into a proper installable package
Use a `src/-layout package`, not flat modules. Code lives in `src/<pkgname>/`, imports are relative or package-qualified (`from .db import / from mypkg.db import`).

1. Move `src/*.py` + `static/ `into `src/integra/` (**a real package** with `__init__.py`).
2. Change all **internal imports to relative** (`from .service import ...`).
3. Added a build backend + package config + console entry points in `pyproject.toml`:

  ```python
  
  ## terminal commands your package provides
  ## the command integra-api runs the function run_api inside the module integra.cli
  [project.scripts]
  integra-api   = "integra.cli:run_api"
  integra-mcp   = "integra.mcp_service:main"
  integra-index = "integra.main:main"


## This tells uv/pip: "my project is a real package — here's the tool that knows how to package it.
  [build-system]
  requires = ["hatchling"]
  build-backend = "hatchling.build"


## where your code lives , This is a hatchling-specific setting that answers one question: "which folder is the actual package to install?"
  [tool.hatch.build.targets.wheel]
  packages = ["src/integra"]
  ```
  
- hatchling is a build backend — a small program that knows how to take your source files
  and turn them into an installable package (a wheel).
	  - Without this block, your project was just "a folder with a `pyproject.toml` listing
	  dependencies." uv installed the dependencies but never installed your code — that's
	  exactly why imports depended on the working directory.
	  - With this block, `uv sync` actually installs integra into the venv, so `import integra`
	  works from anywhere.

- command-line command
	- Format is always `command-name = "module.path:function_name"`. The `:` separates the module from the function to call.
	  When you `uv sync`, it generates a tiny executable named integra-api in `.venv/bin/ `that, when run, imports integra.cli and calls run_api(). That's why `uv run integra-api` works from any directory — it's a real installed command, not a script file you have to point at.

  4. `uv sync` installs integra into the venv (editable), so **it imports from any directory**.


##### Summary
`__init__.py` makes a directory an importable package. It's why `from harness.case import Case` resolves. Without it, harness is just a directory on disk.

  Root files don't need one because they're already top-level modules — the project directory
  itself is on sys.path, so import agent works directly. A file at root is a module; a folder
  needs the marker to become a package.
##### Attention
**Never patch `sys.path` at runtime to make imports work. If you're reaching for `sys.path.insert(...)` in the script, the real problem is that the project isn't packaged.**

```python
sys.path.insert(0, str(Path(__file__).parent / "src")) 
```

**Rule of thumb**: if running your app depends on which folder you're standing in, the project isn't packaged correctly yet.