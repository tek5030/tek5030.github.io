Welcome to the resource pages for the cource [TEK5030 - Computer Vision](https://www.uio.no/studier/emner/matnat/its/TEK5030/)!

Here you will find instructions on how to set up your computer with the software that is necessary in order program the lab exercises.

## REMEMBER

**You are *NOT* required to setup any software on your own computer.**

We have several machines in the lab at ITS, already configured and prepared with all you need to solve the lab exercises. TEK5030 is neither a progamming course, nor a how-to-install-software-on-your-personal-computer course. *Please* don't spend to much time setting up your computer if you run into troubles. Just come to Kjeller and get the most out of your precious time! 🙂

Still, we experience that many students want to run the labs on their own machine, so we have created these resource pages in order to document

- How we have set up the lab computers
- Suggestions for how you may set up your computer

With that out of the way, we can move on.

## Lab setup - current state

- For all the lab exercises, you can choose between Python and C++ as a programming language.
   - Python is usually easier for the unexperienced programmer, both the software setup and the actual programming.
   - Many students use the opportunity to learn C++, however. Not with the intention of scaring you away from C++, but you should probably expect a steeper learning curve, as the programs may be more difficult to compile and debug.
   - The labs are independent, so you can choose the programming language for each new lab if you want.
- Editors:
   - We have documented the labs with tutorials for [PyCharm](https://www.jetbrains.com/pycharm/) for python, and [CLion](https://www.jetbrains.com/clion/) for C++. These are powerful IDEs that help you spend more time on solving the problem, and less time fiddling around with syntax errors and other issues in your code. Both PyCharm and CLion require a licence, but you can either get a free educational licence or use the lab computers which are connected to a licence server.
- Setup:
    - As of 2023, the computers on the lab are running [Ubuntu](https://ubuntu.com/desktop) 18.04. That is why we _recommend_ you to use the same, so that we don't have to maintain tutorials for many different versions. That is also why we have provided a custom Ubuntu ISO disk image which students can run in a VirtualBox virtual machine. The installation of the required software dependencies has been documented in the [tek5030/setup_scripts](https://github.com/tek5030/setup_scripts) repository, but the scripts and written documentation in that repository are only targeting Ubuntu 18.04.

During "lab 0" this year, we saw that too many students, however, had problems with the virtual machine. As an attempt to amend this, we adapt!

- We introduce [Conan](https://conan.io/) as a dependency manager for the C++ labs. It will help with the installation of required 3rd-party libraries, regardless of operating system 🤞
- We provide, without obligations, a suggestion for setup on MacOS and Windows.
- We aim for a careful transition towards [Visual Studio Code](https://code.visualstudio.com/), a free and lightweight editor that can be installed on most systems and architectures. Besides, we see that VS Code is what you promising youngsters tend to use, and we also want to be cool.

## Further reading

(A final reminder: always remember that you can use the lab computers prepared for you at ITS, Kjeller.)

- [Getting started on MacOS](/tutorial/macos.md)
- [Getting started on Windows](/tutorial/windows.md)

- (No further tutorials published, yet 🤷)
