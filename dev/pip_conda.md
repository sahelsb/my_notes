
### Installation directory of packages

When installing Python packages, `pip` typically installs them in either system-wide directories or user-specific directories, like `/home/hpc/iwi1/iwi1115h/.local/bin`. If a package includes executable scripts (e.g., `tqdm`), they get installed in `~/.local/bin`. In this case the executable is not recognized by default after installing it in your shell. The issue arises because this directory isn't automatically added to the system's `PATH`, so you need to manually add it to be able to run these commands from anywhere.

Packages like `torch` or `omegaconf` don't have this issue, as they don't provide command-line tools and are installed directly into the active conda environment. However, when you use the `--user` flag or install with `pip` outside of the environment, packages can be installed in `~/.local/bin` instead of the environment’s `bin/` directory, leading to the PATH issue.

To avoid this, ensure you activate the conda environment first, install packages without the `--user` flag, and prefer using conda where possible. If executables end up in `~/.local/bin`, you can add that directory to your `PATH` to make them accessible. `export PATH=$PATH:/home/hpc/iwi1/iwi1115h/.local/bin`

By default packages installed through `pip` or `distutils` with the `--user` flag are installed under the `$HOME` directory. As quota on `$HOME` is scarce and we regularly backup and snapshot `$HOME` it makes sense, to install packages on a filesystem without backup, like `$WORK`.
The installation path for `pip` and `distutils` can be changed by setting the environment variable `PYTHONUSERBASE`.
To install packages that do not need to be backed up into `$WORK` run:
`export PYTHONUSERBASE=$WORK/software/private`
Future packages will be installed into `$WORK/software/private`.


### Using a conda/virtual environment in a Jupyter Notebook

when the environment is activated in the terminal but when opening a jupyter notebook, the environment is not recongnized or used then do the following:

you need to explicitly **install a Jupyter kernel** that **points** to your new **Python virtual environment**. You can't simply activate Jupyter-lab or Notebook from the virtual environment.

So Register your environment in Jupyter as another kernel by running the follwoing command : 

**Registration, must only be performed once**

``` 
pip install ipykernel
python3 -m ipykernel install --user --name=<env-name>
```

This **registers the current environment** as a **Jupyter kernel** under the name specified with the `--name` flag.


### Using jupyter notebook server in browser

so first start your jupyter notebook **on the remote server** in your terminal :

```
jupyter notebook --port=2345
```

Then **On your local machin**e create a port forwarding to the **remote machine**. This will allow accessing the remote Jupyter Notebook running on that port , on your local machine on the same port

```
ssh -L <local port>:localhost:<remote port> <remote server>
ssh -L 2785:localhost:2781 iwi1115h@tinygpu
```