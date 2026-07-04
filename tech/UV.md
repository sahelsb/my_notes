
### Install UV

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```


```
uv init
```

This will create a `pyptoject.toml` file and set the directory you are in as the project directory
It also initialize the directory as a git directory

then you can install packages with

```bash
uv add langchain
```

this will install and add the package in the dependencies section in `pyproject.toml`


`uv.lock` has all the exact versions of all the packages installed so can be completely reproduced



```
uv pip install langchain
```

this will just install the package but not  creating the `uv.lock` or `pyproject.toml` and also add the package to dependencies section in `pyproject.toml`


to run the project

```bash
uv run main.py
```


To remove a package installed

```bash
uv remove package_name
```


If we pass this project to someone and they want to get the environment ready without running the application they do : 

```bash
uv sync
```


**Note** 
All the info we need to run our code is in `pyproject.toml` and `uv.lock` so if we remove the virtual environment and then run `uv run main.py` and it will install all the packages again automatically


---



``` bash
cd src && uv run uvicorn api:app --host 0.0.0.0 --port 10000


ORRR

uv run uvicorn api:app --app-dir src --host 0.0.0.0 --port 10000
```