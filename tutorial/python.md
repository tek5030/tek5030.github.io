[<-- Home](/)

# Python setup for Ubuntu
Installing the basic Python tools is straight forward in Ubuntu.

We will install `python3`, since the version we get with Ubuntu 22 is ok.   
If you are on a different platform, `python3.8` is the oldest version that works with our labs.

Just type the following into a terminal to install the required pacakges:

```bash
sudo apt update
sudo apt install python3 python3-dev python3-distutils python3-venv python-is-python3
```

## Creating a virtual environment

For each lab, we provide a file `requirements.txt` that lists the python requirements for the lab. We highly suggest that you set up a new [virtual environment](https://docs.python.org/3/library/venv.html) for each lab. 

```bash
python3 -m venv venv
source venv/bin/activate.
# expect to see (venv) at the beginning of your prompt.
pip install -U pip
pip install -r requirements.txt
```

---

[<-- Home](/)