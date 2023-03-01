# Python setup for Ubuntu
Installing the basic Python tools is straight forward in Ubuntu.

We will install `python3.8`, since that is the version we have on the lab computers.
Newer versions should also work, but not older!

Just type the following into a terminal to install the required pacakges:

```bash
sudo apt update
sudo apt install python3.8 python3.8-dev python3.8-distutils python3.8-venv
```

## Creating a virtual environment

For each lab, we provide a file `requirements.txt` that lists the python requirements for the lab. We highly suggest that you set up a new [virtual environment](https://docs.python.org/3/library/venv.html) for each lab. 

```bash
python3.8 -m venv venv
source venv/bin/activate.
# expect to see (venv) at the beginning of your prompt.
pip install --upgrade pip  # <-- Important step for Ubuntu 18.04!
pip install --requirement requirements.txt
```
