[<-- Home](/)

# TEK 5030 - Getting started with Conan

For MacOS, this topic is covered in [Getting started on MacOS](macos.md).

For Windows, this topic is covered in [Getting started on Windows](windows.md).

---

[Conan](https://conan.io) is a free and open source C++ package manager that we will use to maintain dependencies for our projects. Conan can be utilized on both Linux, Mac and Windows. Conan is created with Python, so we will install Python as well. In any way, it's convenient to have Python installed in case you want to solve the labs using Python. There is no downside to reading the  ["getting started"](https://docs.conan.io/en/latest/getting_started.html) section of the conan documentation, so please take a look.
   If you intend to only program the labs using Python, you can skip the installation of conan.
   
   (Conan will deprecate https://github.com/tek5030/setup_scripts, which is a set of helper scripts for system wide installation of C++ dependencies on Ubuntu 18.04).

## Install conan

On Ubuntu, we will install conan according to [the official documentation](https://docs.conan.io/en/latest/installation.html#install-with-pip-recommended):

Open a new Terminal

### Make sure you have a C++ compiler (gcc/g++)

```bash
sudo apt update
sudo apt install build-essential
```

### Install Python

We will install **python3.8**, since that is the version we have on the lab computers.   
(Versions > 3.8 should also work if that is available on your system.)

```bash
sudo apt update
sudo apt install python3.8 python3.8-dev python3.8-distutils python3.8-venv python3-pip
```

### Install conan

```bash
pip3 install conan

source ~/.profile

conan profile new default --detect
conan profile update settings.compiler.libcxx=libstdc++11 default  # <-- Important step for gcc
```

## Make profit

You should now be able to proceed with our introductory [Lab 0](https://github.com/tek5030/lab_00) 🤓

---

[<-- Home](/)