[<-- Home](/)

# TEK 5030 - Getting started on a Mac

These instructions have been tested on MacOS Monterey on a MacBook Air 2018.

In this guide we will:

- Install Homebrew

   [Homebrew](https://brew.sh/) is "the missing package manager for MacOS", and if you haven't used it before, it's about time!
It will simplify your life as a programmer quite significantly. Head over to https://brew.sh/ to read more.

- Install VS Code editor

   We will here document how to get started with TEK 5030 and VS Code editor. We choose VS Code because we can then maintain lab guides that will hopefully work on both Mac, Linux and Windows.
   
   If you rather use Xcode, then I assume that you have a certain level of experience and won't need a guide ;-)

- Install Conan (for C++)

   [Conan](https://conan.io) is a free and open source C++ package manager that we will use to maintain dependencies for our projects. Conan can be utilized on both Linux, Mac and Windows. Conan is created with Python, so we will install Python as well. In addition, it's convenient to have installed in case you want to solve the labs using Python. There is no downside to reading the  ["getting started"](https://docs.conan.io/en/latest/getting_started.html) section of the conan documentation, so please take a look.
   If you intend to only program the labs using Python, you can skip the installation of conan.
   
   (Conan will deprecate https://github.com/tek5030/setup_scripts, which is a set of helper scripts for system wide installation of C++ dependencies on Ubuntu 18.04).

- Try to compile a simple C++ program using Visual Studo Code

- Try to run the same program in Python

## Install Homebrew

Open a terminal and install Homebrew as documented on their front page:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

If you already have Hombrew installed, it's sensible to update before proceeding:

```bash
brew update
```

## Install VS Code editor

Now that you have Homebrew, [installing VS Code](https://formulae.brew.sh/cask/visual-studio-code) is a walk in the park:

```bash
brew install --cask visual-studio-code
```

For the curious: [_What is Homebrew Cask??_](https://github.com/Homebrew/homebrew-cask)

## Make sure you have a C++ compiler (clang)

Clang may already be installed on your Mac. To verify that it is, open a macOS Terminal window and enter the following command:

```bash
clang --version
```

If Clang isn't installed, enter the following command to install the command line developer tools:

```bash
xcode-select --install
```

Using Clang in Visual Studio Code: https://code.visualstudio.com/docs/cpp/config-clang-mac


## Install Python

We will [install python3.8](https://formulae.brew.sh/formula/python@3.8), since that is the version we have on the lab computers.

```bash
brew install python@3.8
```


## Install VS Code extensions

To make it easier to automate and configure VS Code, it is possible to list, install, and uninstall extensions [from the command line](https://code.visualstudio.com/docs/editor/extension-marketplace#_command-line-extension-management). We will utilize this feature in order to install a handfull of extensions that are usefult for C++ and Python development:

```bash
code --install-extension ms-vscode.cpptools
code --install-extension ms-vscode.cpptools-extension-pack
code --install-extension jeff-hykin.better-cpp-syntax
code --install-extension ms-python.python
```

Extensions can also be installed graphically from within VS Code. Read more here: https://code.visualstudio.com/docs/editor/extension-marketplace

## Install conan

```bash
brew install conan

conan profile new default --detect  # <-- Important step
```

# Our first C++ program

Type the following in a new Terminal window:

```bash
git clone https://github.com/tek5030/lab_00_solution.git
cd lab_00_solution/cpp
conan install . --install-folder build
vscode .
```

It is outside the scope of this guide to explain the usage of conan in-depth, but in short:

- The command `conan install . --install-folder build` will install the `dependencies` of our project.   
  The dependencies are listed in a `conanfile.txt` within our project. It will be parsed by conan.
- The installation path of each dependency (the actual libraries) is somewhere within the directory `~/.conan/data`.
- Inside the `build` folder, conan will generate files that will help your build system locate the dependencies.
- (Just so you know, you can never do anything wrong if you delete the contents of `~/.conan/data`. The worst thing that can happend is that you will experience a time consuming reinstallation of dependencies when building your next project.)

Now we will go through the procedure of building and running the example project:

---

Upon launch of VS Code, expect to see a dialog like this: Press Yes

<img width="474" alt="image" src="https://user-images.githubusercontent.com/11663739/215351568-bf8b7712-dc65-4b06-be47-68df0558592f.png">

In the next diaglog, appearing at the top of the program window, select your compiler. I chose "Unspecified (Let CMake guess (...)"

<img width="627" alt="image" src="https://user-images.githubusercontent.com/11663739/215352392-866e3748-4758-4d49-9faa-6cc293062319.png">

---

Now, at the bottom toolbar of VS Code, we will press a few buttons.

<img width="446" alt="image" src="https://user-images.githubusercontent.com/11663739/215352414-65376262-9cca-4c29-8595-b4e5b044d74e.png">

First press the "CMake: &lsqb;Debug&rsqb;: Ready". In the following dialog, I chose "Release"

<img width="510" alt="image" src="https://user-images.githubusercontent.com/11663739/215352428-d7a06e52-3618-4979-a4b5-427e5369864c.png">

---

Next, press the "_cogwheel_ Build" to build your project.

Then, press the &lsqb;all&rsqb; - button and select `lab_00_intro EXECUTABLE`, so that we can run our program.

<img width="481" alt="image" src="https://user-images.githubusercontent.com/11663739/215352483-af544eac-73d4-4875-b95c-06a6805d5a72.png">

Press the play button to run your program. The first time you launch, expect to see a dialog similar to this: Press OK.

<img width="261" alt="image" src="https://user-images.githubusercontent.com/11663739/215352609-68819300-dc72-4ea8-bf56-40c4eff8f358.png">

(If you screw this up and click Deny, just follow the instructions of the error message if camera is denied access)

> OpenCV: camera access has been denied. Either run 'tccutil reset Camera' command in same terminal to reset application authorization status, either modify 'System Preferences -> Security & Privacy -> Camera' settings for your application.

---

If everything goes as expected, expect to see live video feed from your camera (it might show up _behind_ your vscode window) 🤩

<img width="652" alt="image" src="https://user-images.githubusercontent.com/11663739/215354088-ccef48e4-e3e8-4dde-8bd2-e20965afe17b.png">

Press `q` to close the window.

### Fallback solution

If all the dialog boxes and clicking in VS Code does not work out for you, this command line approach _should_ work if everything is set up correctly:

```bash
cd ~/tek5030/lab_00_solution/cpp

conan install . --install-folder build
cd build
cmake .. -DCMAKE_BUILD_TYPE=Release
cmake --build .
./lab_00_intro
```

# Python

While we're at it, let's try to get the python lab running as well.

Go to your terminal and into the directory `lab_00_solution/py`. Continue with the following commands:

```bash
cd ~/tek5030/lab_00_solution/py

python3.8 -m venv venv
source venv/bin/activate.
# expect to see (venv) at the beginning of your prompt.
pip install --upgrade pip  # <-- Important step!
pip install -r requirements.txt

python main.py
```

You might get this dialog again: Press OK

<img width="261" alt="image" src="https://user-images.githubusercontent.com/11663739/215354444-7a734870-df60-4078-8268-2f68994baa9b.png">

Now, expect success.

## Python in VS Code

In my experience, it's best to set up the virtual environment _before_ launching VS Code, but we'll try both. I assume you already typed all the previous commands, so now let's just

```bash
(venv) code .  # assumed you are in the "py" directory, and venv is already activated
```

When you select `main.py` in the file explorer to the left, you should hopefully see a toolbar like this on the bottom right of VS Code:

<img width="491" alt="image" src="https://user-images.githubusercontent.com/11663739/215354627-1c126001-1f02-412b-840a-2dca3924266a.png">

If your view is like mine, with "3.8.16 ('venv': venv)" in the lower right, all you have to do is to press the play in the upper right:

<img width="109" alt="image" src="https://user-images.githubusercontent.com/11663739/215354682-dc7256d6-a299-466b-8adc-8895f09628d3.png">

Expect success 💪

---

Let's assume you did not create a virtual environment, but went straigt into VS Code:

```bash
cd ~/tek5030/lab_00_solution/py

code .
```

For me, the toolbar looks like this, with a yellow "⚠️ Select Interpreter" on the lower right toolbar.

<img width="503" alt="image" src="https://user-images.githubusercontent.com/11663739/215354888-592501e2-37b4-4e4c-98a8-d6828a2e3a14.png">

Here are the alternatives on _my_ computer, but unfortunately, none of these will suffice, as we have not installed the dependencies in `requirements.txt` _yet_.

<img width="603" alt="image" src="https://user-images.githubusercontent.com/11663739/215354918-de6be653-181d-43b7-8e50-f41be5af57bf.png">

It's a good habit to create _virtual environments_, to keep dependencies of each project _local_ to that project. It is possible to do system wide installation of all dependendencies, but the common advice is not to. Just google "why use python virtual environments" if you need to be convinced, I have no intentions of replicating Internet here :)

Let's use the opportunity to learn how to open a terminal within VS Code:

- Press Command + Shift + P
- Type "Terminal"
- Select "Terminal: Create New Terminal (In Active Workspace)
- (I don't know why every word is capitalized, don't blame me)

<img width="597" alt="image" src="https://user-images.githubusercontent.com/11663739/215355182-a91d9bdc-38fd-407a-9501-04709fd34ca0.png">

In the new terminal that opened, type

```
python3.8 -m venv venv
```

in order to create the new virtual environment.

Whoa, clever VS Code detected the new environment!

<img width="461" alt="image" src="https://user-images.githubusercontent.com/11663739/215355269-8dc12c1f-e71c-4b2d-9a3b-a92a322b89ee.png">


Select "Yes". Still, we must continue with the installation of requirements:

```bash
pip install --upgrade pip
pip install -r requirements.txt
```

### What happens if you don't?

Press the play button to find out:

>     import cv2
> ModuleNotFoundError: No module named 'cv2'

_- Ah, forgot to install the requirements!_ 

`pip install -r requirements.txt` (oups, did upgrade pip!)

> WARNING: You are using pip version 22.0.4; however, version 22.3.1 is available.
> You should consider upgrading via the '(...)/python3.8 -m pip install --upgrade pip' command.

Okay, so on this computer, it seems we're actually fine and get away with just a warning.
On the Jetsons on the lab (Ubuntu 18.04), however, the installation will fail, and we are _required_ to upgrade pip before proceeding.

Anyhow, upgrading pip in the virtual environment won't hurt, so just keep it as a habit as well.

That's it(?)

Good luck with the rest of tek5030 🤓
