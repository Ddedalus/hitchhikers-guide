# Installing DSSG pre-requisites on Windows 10

This guide will help you install all pre-requisites to be ready for the summer.

## Step 1. Install Python 3.7 and the compiler

[Visual Studio](https://visualstudio.microsoft.com/downloads/) neatly packages Python 3.7 and the Microsoft Compiler to build native extensions.

1. Head over to https://visualstudio.microsoft.com/downloads/ and download Visual Studio Community
2. In the Visual Studio Installer, select the **Python development** and **Data Science and analytical applications**
3. Under Installation details, make sure that under **Python development**, **Python 3 64-bit** and **Python native development tools** are selected and click Install.

You now have Python 3.7 installed!

## Step 2. Install Scoop

[Scoop](https://scoop.sh/) is a command line installer for Windows that will make your life a lot easier.

To install, open a Powershell and run:

```powershell
iwr -useb get.scoop.sh | iex
```

<details>
<summary>If you get an error...</summary>

Note: if you get an error you might need to change the execution policy (i.e. enable Powershell) with

```powershell
Set-ExecutionPolicy RemoteSigned -scope CurrentUser
```

</details>

## Step 3. Install tools

### Minimum pre-requisites

1. SSH - Since April 2018 Windows 10 ships with ssh, but if yours doesn't, here's a powershell command to install it:

        Add-WindowsCapability -Online -Name OpenSSH.Client*

2. Git

        scoop install git-with-openssh
        [environment]::setenvironmentvariable('GIT_SSH', (resolve-path (scoop which ssh)), 'USER')


### Code editors and IDEs

We recommend the following code editors or IDEs:

* Visual Studio Code - `scoop install vscode`
* Sublime Text - `scoop install sublime-text`
* Atom - `scoop install atom`
* PyCharm - `scoop install pycharm`

Note: for some of those, you may need to install additional scoop manifestos:
```powershell
scoop bucket add extras
scoop bucket update
scoop install 7zip
```

### Terminal

The default `cmd` and Powershell terminals in Windows are quite old. Fortunately, Microsoft recently released a really nice Terminal that you can simply install from [this link](https://www.microsoft.com/store/productId/9N0DX20HK701).

## Step 4. Set Python 3.7 as the default Python

1. Open *System Properties* by pressing *Windows+R* and typing `sysdm.cpl`
2. Go to *Advanced* -> *Environment Variables* and in *System variables* double click to `Path`
3. In the *Edit environment variable* window, click *New* and paste

        C:\Program Files (x86)\Microsoft Visual Studio\Shared\Python37_64

4. Repeat step 3 but paste

        C:\Program Files (x86)\Microsoft Visual Studio\Shared\Python37_64\Scripts

    Press OK to confirm. You may want to logout and login again if the next step doesn't work.

5. To see if it worked open a Terminal and type

        python --version

6. Update `pip` and create your user packages folder by running

        python -m pip install --user -U pip

7. Now back in the *Environment Variables* window, in *User variables for `-username-`* double click to `Path` and add:

        C:\Users\-username-\AppData\Roaming\Python\Python37\Scripts

Awesome!

## Step 5. Install Python tools

For managing your python environments and packages, we recommend to use [Pipenv][pipenv].

To install it:

    pip install pipenv

Then navigate to a project folder and install some data science packages by using

    pipenv install jupyter ipython numpy scipy pandas scikit-learn seaborn [...]

Now you can run

    pipenv shell

to switch to that environment, and run

    jupyter notebook

to start coding!

<details>
<summary>Why Pipenv?</summary>

Pipenv is a tool that aims to bring the best of all packaging worlds (bundler, composer, npm, cargo, yarn, etc.) to the Python world.

It automatically creates and manages a virtualenv for your projects, as well as adds/removes packages from your Pipfile as you install/uninstall packages. It also generates the ever-important `Pipfile.lock`, which is used to produce deterministic builds.

The problems that Pipenv seeks to solve are multi-faceted:

* You no longer need to use `pip` and `virtualenv` separately. They work together.
* Managing a `requirements.txt` file can be problematic, so Pipenv uses `Pipfile` and `Pipfile.lock` to separate abstract dependency declarations from the last tested combination.
* Hashes are used everywhere, always. Security. Automatically expose security vulnerabilities.
* Strongly encourage the use of the latest versions of dependencies to minimize security risks arising from outdated components.
* Give you insight into your dependency graph (e.g. `$ pipenv graph`).
* Streamline development workflow by loading `.env` files.

</details>

### What about conda?

If you prefer `conda` you're free to use it! However, `conda` sometimes has outdated packages or doesn't have some packages at all, unlike `pip` which is the official Python package manager, which means you'll have to deal with both package managers at the same time, leading to various issues.

The main distribution, Anaconda, occupies a large amount of space with a lot of packages you may not need. We recommend you to download [miniconda](https://docs.conda.io/en/latest/miniconda.html) instead.


[pipenv]: https://pipenv.pypa.io/en/latest/
