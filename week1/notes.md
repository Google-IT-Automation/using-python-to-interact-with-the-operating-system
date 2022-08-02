# Getting Ready for Python
```shell
# Checking python installed on your computer
$ python --version
$ python3 --version
````
- PyPI : Python package index 
    - It is repository of python external modules
- PIP : It is a cross-platform tool called a package manager used to install, update, or remove external Python modules.
- **[Installing python on different OS](https://realpython.com/installing-python/)**
- **[pip and venv](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/)**

### **Use of shebang on top of python file**
It tells the operating system **what command we want to use** to execute the python script.
```python
#!/usr/bin/env python3      # add this line in top of your python script
```
```shell
$ chmod +x sample.py    # to be able to run our file directly
$ ./sample.py
```
## **IDEs**
These are some of the common editors for Python, available for all platforms:
- [Atom](https://atom.io/)
- [vscode](https://code.visualstudio.com/)
- [pycharm](https://www.jetbrains.com/pycharm/)
- **You can read more about these editors, and others, in these overview comparatives:**
    - [Top 5 Python IDEs for Data Science](https://www.datacamp.com/tutorial/data-science-python-ide)
    - [Python IDEs and Code Editors (Guide)](https://realpython.com/python-ides-code-editors-guide/)

## Pitfalls of automation
Any task or process we automate comes with a trade-off.
- **Is the time and the effort it will take to write the script worth the potential automation benefits ?**
    - time_to_automate < (time_to_perform * amount_of_times_done)
    - [Is it worth to automate](https://xkcd.com/1205/)
    - It can be very useful to automate a complex error prone task, if its critical that the tasks be done correctly. Even if it is not executed that often.

- If underlying systems change and automation isn't updated accordingly, workflows can break.
- If an automated system fails and gone unnoticed the consequences can be really bad.
- **How to avoid silent failures ?**
    - Build a method of notifications into your automated systems, this way if automation fails a human is notified and can be investigated.
    - This notification could be an e-mail, a new ticket, or an update to a dashboard
- **Automation succeeds but performs wrong action**
    - Build periodic tests to check in the behavior of automated systems.

- Along with flagging problems, good automation will make debugging easier by logging, the action it takes. The system log can be extremely useful source of information when you are investigating an issue.

## Practical automation examples
```python
#!/usr/bin/env python3

def get_disk_free_space_in_percentage():
    import shutil
    du = shutil.disk_usage("/")
    disk_free = du.free/du.total * 100
    return disk_free

def get_cpu_usage():
    import psutil
    # this function recevies an interval of seconds and return avg % of usage in that interval
    return psutil.cpu_percent(0.5)  # lets try with 0.5 seconds
```

## VM (Virtual Machines)
Virtual Machines are nothing but computer simulated through software.
- This software simulates all the necessary hardware to the operating system that's running inside the machines.
- For some simulated hardware the VM will use a portion of the underlying hardware for the simulation.
- Quicklabs are the virtual machines that run in cloud. Remember when we say that a service is running in the cloud, we mean it's running in a data center or on a remote server.
- `ssh` is the command that lets you to interact with the remote Linux computers.

# Graded Assignment

### **shutil**
The shutil module offers a number of high-level operations on files and collections of files. In particular, it provides functions that support file copying and removal. It comes under Python's standard utility modules. disk_usage() method is used to get disk usage statistics of the given path. This method returns a named tuple with the attributes total, used, and free. The total attribute represents the total amount of space, the used attribute represents the amount of used space, and the free attribute represents the amount of available space, in bytes.

### **psutil (Python system and process utilities)**
psutil (Python system and process utilities) is a cross-platform library for retrieving information on the processes currently running and system utilization (CPU, memory, disks, network, sensors) in Python. It's useful mainly for system monitoring, profiling, limiting process resources, and managing running processes. cpu_percent() returns a float showing the current system-wide CPU use as a percentage. When the interval is 0.0 or None (default), the function compares process times to system CPU times elapsed since the last call, returning immediately (non-blocking). That means that the first time it's called it will return a meaningful 0.0 value. When the interval is > 0.0, the function compares process times to system CPU times elapsed before and after the interval (blocking).

### **requests**
Requests is a Python module that you can use to send all kinds of HTTP requests. It's an easy-to-use library with a lot of features ranging from passing parameters in URLs to sending custom headers and SSL verification. You can add headers, form data, multi-part files, and parameters with simple Python dictionaries.You can then access the response data using the same request
```shell
$ sudo apt install python3-requests
```

### Verifying if localhost is correctly configured
```python
import socket
import requests

# localhost is correctly configured
def check_localhost():
    localhost = socket.gethostbyname('localhost')
    return localhost == "127.0.0.1"

# This checks whether the computer can make successful calls to the internet.
def check_connectivity():
    request = requests.get("http://www.google.com")
    return request.status_code == 200
```
