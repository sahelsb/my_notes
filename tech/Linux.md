## Linux notes

#### Force a command to run in shell 
    sh -c "command"

#### Force a command to run in bash 
    bash -c "command"

#### See all the pocess that are running 
    ps -ef 
    # will show only process that has a bag in its name
    ps -ef | bag    

#### Get process id of a process 
    pgrep -f "process name"

#### Get name of the process from PID
    Ps -p PID -o comm=

#### kill a process with pid
    kill pid

#### kill a process with name
    pkill -f -15 'pattern'   ---> -15 (kill gracefully) , -9 (kill immediately)

#### Search the manual of ps
    man ps

#### Copy only missing files from one path to other (it will just copy missing files in another folder)
    rsync -urltv ssh jetsonaxorin:/projects/verum/data semantic_cloud_long
    
#### from host to wsl: in wsl
```
rsync -urltv -e ssh verum:/home/ancud/projects/verum/ros_ws/perf_result img/temp
```
    
##### from wsl to host :  **in wsl**
```
rsync -urltv -e "ssh" octane_sity_small jetsonaxorin:projects/verum/data
```

	 
#### from host to windows:  **in cmd**
```
scp user@cip4d3:/home/cip/2021/user/Documents  uni/documents
```

#### copy all files from one path to another 
```
     scp path1 path2
     scp Documents/filename.txt ancud@jetsonaxorin: Documents/sb
```
    

#### copy files from windows to wsl
```
     first navigate to the desired path in WSL
    # then copy "a.txt" to a folder called tmp in wsl 
    cd ~/workspace/data
    cp /mnt/c/Users/'Sahel Bloukat'/Workspace/Documents/a.txt temp
```


## Check GPU usage and memory (VRAM) for my user

```bash
nvidia-smi | grep -w -f <(pgrep -u $(whoami))
```

```bash
Results :
- GPU 3: 9,268 MiB
    
- GPU 6: 7,010 MiB
    
- GPU 7: 9,520 MiB


You are now using roughly **25 GB** (VRAM) across 3 GPUs.
```

### How to check running PIDS

```bash
 ps -f -p 53142 46611 
```

##### Result: 
```bash
UID        PID  PPID  C STIME TTY      STAT   TIME CMD
bloukats 23862 23842 99 Jan10 ?        Sl   6131:10 python ../sncct/src/lightning_25d/resume_main_mlflow_37761.py
bloukats 46056 46035 99 18:41 ?        Rl    15:23 python ../sncct/src/lightning_25d/finetune/main_mlflow_8348.py
bloukats 46611 44738 99 10:12 pts/82   Rl+  520:57 python src/diff_elucidate_25d/inference.py
bloukats 53142 53120 99 18:45 ?        Sl    10:22 python ../sncct/src/lightning_25d/finetune/main_mlflow_55992.py
```
### SSH Keys
#### create ssh keys
```
     ssh-keygen  
     sh-keygen -t ed25519 -f <filename>
	ssh-keygen -t ed25519 -f <~/.ssh/id_ed25519_nhr_fau>
```

#### Copy ssh keys to a host (specific user)

```
ssh-copy-id -i verum.pub ancud@172.165.27
```
use the `-i` flag to locate your public key on your local machine

#### activate python in terminal 
    python -c "import os; pd.read_csv"

#### Difference of os.system(command) and Subprocess .Popen(command as a list, stdout=DEVNULL)
    os.system() runs the command synchronously, meaning your Python script will wait until the command finishes executing, but
    subprocess.Popen() runs the command asychronously that allows your Python script to continue executing while the subprocess runs in the background.

##### How to install miniconda (comapct version of Anaconda)  :

follow this link [Installing on Linux — conda 4.14.0 documentation](https://docs.conda.io/projects/conda/en/4.14.x/user-guide/install/linux.html)

##### Auto activate of conda env after startuo in shell would be deactivated :  
	conda config --set     
	auto_activate_base false

##### Create virtual env : 
	conda create --n name_of_environment      python=3.10


##### Search :

	fzf | xargs code
activate fuzzy search , it will open     the file founded in vscode 

	pip list | grep "searchname"


#### checking the disk usage 

```
# show disk usage
du -sh foldername
du -sh .*

# list largest files in a directory
find . -type f -exec du -h {} + | sort -rh | head -20
```



## **Installing software packages from source or debian :**

Installing software from source or using Debian packages refers to two different methods of installing software on a Linux system:

- ### **Installing from Source:**
  - When you install software from source, you download the source code of the software package from the project's repository (typically hosted on platforms like GitHub or GitLab).
  - You then compile the source code on your system using build tools like  **make**  and  **gcc** This process converts the human-readable source code into executable binaries that your computer can run.
  - Installing from source gives you more control over the software configuration and allows you to customize the installation according to your specific needs.
  - However, it can be more complex and time-consuming, as you need to resolve dependencies, configure the build environment and compile the code yourself.

- ### **Using Debian Packages:**
  - Debian packages are pre-compiled binary packages that contain the software along with its dependencies in a format suitable for installation on Debian-based Linux distributions (e.g., Debian, Ubuntu).
  - These packages are managed by package managers like **apt** or **apt-get** , which handle the installation, removal, and updating of software packages and their dependencies.
  - Installing software via Debian packages is generally simpler and more convenient, as the package manager takes care of resolving dependencies and ensuring compatibility with your system.
  - However, you may have less flexibility and control over the software configuration compared to installing from source, as you're limited to the versions and configurations provided by the package repositories.




## Install WSL

```
wsl --list --all   # list all wsl distributions installed in CMD or Powershell

wsl --unregister <DistroName>   ## Uninsatll a distribution like Ubuntu

wsl --install   ## will install latest version of Ubuntu (24.04)

wsl --install -d Ubuntu-22.04

wsl --set-default Ubuntu-22.04    # set a distro as default 

lsb_release -a  ## check the version of Ubuntu in wsl terminal

```

## Ubuntu

#### install zsh plugin

```
sudo apt install zsh

chsh -s /usr/bin/zsh    # make it default shell

echo $SHELL   # now it is default after logging out and in

```
#### install oh-my-zsh plugin

```
sudo apt install wget git

wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh
```
	
##### Change the config

Copy the template _.zshrc.zsh-template_ configuration file to the home directory _.zshrc_ and apply the configuration by running the source command

```
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc  
source ~/.zshrc
```


##### install zsh autosuggestions

```

sudo apt install git

git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

```


#### .zshrc config changes
```
plugins=(git zsh-autosuggestions)

export GIT_PAGER=

source $ZSH/oh-my-zsh.sh

alias python="python3"
alias ls="ls -A --color=auto"

# extended pattern matching
setopt extendedglob

export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
export PATH=$PATH:/snap/bin
```


## Reinstall WSL on Windows 10 (clean way):

### **Uninstall wsl and related stuff**

In powershell (as admin)

    #list all installed distros :
     wsl -l -v

    #destroy distros :
     wsl --unregister Ubuntu
     wsl --unregister Debian # and so on

#### In Settings \> Apps \> Apps & Features** :

search for Ubuntu (then Debian, etc), and if something is found, click on uninstall

search for Linux, and if something is found, click on uninstall on all results

#### In Start Menu \> Turn Windows Features on or off** :

Untick Virtual Machine Platform checkbox

Untick Windows Subsystem for Linux checkbox

Reboot


### **Re-install and configure wsl to use systemD**

The process of installing wsl have become super straightforward.

Installing wsl - In powershell (as admin)

     #install wsl
     wsl --install

Then reboot and wait for the Ubundu installation to complete and ask for username (it might takes some time).

#### Optional: Changing distribution - In powershell (as admin)

     #list available distributions
     wsl --list --online

     #install favorite distro
     wsl --install -d Debian

     #set Debian as default
     wsl --set-default Debian

NB: wsl --set-default-version 2 is not needed anymore.

#### Enabling systemD support - Inside wsl:

Launch your distribution

Edit /etc/wsl.conf (or create the file if it doesn't exist):

     [boot]
     systemd=true




#### Create a shell alias:

This way with creating an alias you can just access the folder in your windows with an alias in wsl terminal

 ```bash
 echo "alias obsidian='cd /mnt/c/Users/slbloukat/workspace/obsidian'" >> ~/.zshrc
 ```