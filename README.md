# Overview

This repo contains some Qiskit samples, and instructions for a first-time user to get set up with these tools for Qiskit development and Quantum Computing:

* Python
* Visual Studio Code
* Git

# Install Software

## macOS

On macOS, install [MacPorts](https://www.macports.org/) to supporting installing standard UNIX tools.

Install Xxcode. Then install the command-line tools by running

``` bash
xcode-select --install
```

Install MacPorts from a `pkg` file from [MacPorts downloads](https://github.com/macports/macports-base/releases/tag/v2.10.5)

Install Git:

``` bash
sudo port install git
```

Install [Visual Studio Code](https://code.visualstudio.com/download).

Install [Python3](https://www.python.org/downloads/macos/).

Install [MacTex 2024](https://www.tug.org/mactex/mactex-download.html).

In Visual Studio Code, click the Extensions button partway down the left side, and search for an install these extensions:

* Python (Microsoft)
* Jupyter (Microsoft)
* LaTeX Workshop (James Yu)
* Insert Unicode (brunnerh)

# Create SSH key for GitHub

Prior to setting up your SSH key, you need to have a GitHub account and have already set up multifactor authentication and/or passkeys.
For example, you can use the Microsoft Authenticator mobile app for authentication.

See GitHub's [Authentication documentation](https://docs.github.com/en/authentication) for all the information about authentication (MFA, passkey, SSH).

Create an SSH private/public key pair:

``` bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Use a filename to indicate the key is for GitHub, e.g. `john.b.hurst-github`.

Configure SSH to use the key and use Apple's keychain support for the passphrase, by putting these lines in `~/.ssh/config`:

```
Host github.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
```

Add the key and passphrase to the Apple keychain:

``` bash
ssh-add --apple-use-keychain ~/.ssh/john.b.hurst-github
```

See GitHub's [Generating a new SSH key and adding it to the SSH agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) for more details.

# Install Python libnaries

With Python we use _virtual environments_ to manage project-specific libraries.
This keeps the project's dependencies local to the project's virtual environment and prevents version clashes between different projects.

Use the commands to create a virtual environment containing common Qiskit libraries:

``` bash
mkdir ~/Projects/qiskit-demo
cd ~/Projects/qiskit-demo
python3 -m venv venv
source venv/bin/activate
pip install -upgrade pip
pip install jupyter matplotlib nbdime pylatexenc qiskit qiskit-aer qiskit-ibm-runtime
```

When you want to use the virtual environment in a new shell, activate it:

``` bash
cd ~/Projects/qiskit-demo
source venv/bin/activate
```

The libraries are:

* jupyter: for interactive Jupyter notebooks ([jupyter.org](https://jupyter.org/))
* matplotlib: for plotting charts and Qiskit circuit diagrams ([matplotlib.org](https://matplotlib.org/))
* nbdime: to show Git differences of Jupyter notebook data ([GitHub](https://github.com/jupyter/nbdime))
* pylatexenc: to display LaTeX-formatted output from Qiskit ([GitHub](https://github.com/phfaist/pylatexenc))
* qiskit: Open-source SDK for quantum computing ([GitHub](https://github.com/Qiskit/qiskit))
* qiskit-aer: high performance simulators with realistic noise models ([GitHub](https://github.com/Qiskit/qiskit-aer))
* qiskit-ibm-runtime: implementations of Qiskit primitives for IBM Quantum hardware ([GitHub](https://github.com/Qiskit/qiskit-ibm-runtime))

# Visual Studio Tips

See the [Tutorial](https://code.visualstudio.com/docs/getstarted/getting-started) for full information.

Use the `code` command in the terminal to open Visual Studio Code on a project or edit specific files:

``` bash
code ~/Projects/qiskit-demo     # opens a new Visual Studio Code window with the project
code teleportation.ipynb        # opens the file in Visual Studio Code
```

Use Cmd+P to open the file-open prompt within Visual Studio Code, to quickly open any file in the project.
Use Shift+Cmd+P to open the Command Palette, to run commands, such as `Git: Push`. or `Insert Unicode: Insert`.
Use Ctrl+` to open or switch to the integrated terminal.

# Git Tips

Git has three different areas for data:

* The _working copy_ is your regular files in the project folder, which may be tracked in Git and may have local (uncommitted) changes.
* The _index_ contains the changes staged for commit.
* The _repository_ contains the entire history of the project.

The index and repository are stored under the `.git/` subdirectory.
There can also be one or more _remotes_, which are remote repositories that can be synchronized to/from. Typically a GitHub repository is set up as a remote.

The typical Git workflow is:

* Sync upstream changes if any (e.g. from GitHub).
* Make changes to files.
* Review changes.
* Stage changes for commit.
* Commit.
* Push changes to the remote (GitHub).

You can do all the most common tasks in Visual Studio Code, using the Git panel in the primary side bar, or `Git:` commands in the palette.
For complex tasks you need to use `git` commands in the terminal, which have many options.

The `git` commands for the basic workflow are:

``` bash
git init                     # creates a repository
git add ...                  # stages files or changes to index
git commit -m"some message"  # commits staged changes
git push                     # pushes changes to the remote
git pull                     # fetches changes from the remote
```

To configure the remote for a new repository, create the repository in GitHub and follow the instructions.

# Qiskit Tips

Qiskit provides two features for output that can be used with the simulators, or with real quantum systems:

* The Sampler feature creates outputs of counts for combinations of measured qubits. For example, suppose you measure two qubits from your circuit, then the possible combinations are 00, 01, 10 and 11, and the Sampler provides the counts observed for each combination. These are typically then plotted in a histogram.
* The Estimator feature lets you specify an observable, and the Estimator computes the estimation of the observable from the circuit. For example you could estimate $C=\sqrt{2}(Z_1Z_0+X_1X_0)$ for studying the CHSH inequality.

In addition to these, Qiskit also can produce several kinds of analytical output when using the simulators:

* Circuit result as a [`Statevector`](https://docs.quantum.ibm.com/api/qiskit/qiskit.quantum_info.Statevector)
* Circuit result as a [`DensityMatrix`](https://docs.quantum.ibm.com/api/qiskit/qiskit.quantum_info.DensityMatrix)
* Circuit operation as a unitary matrix

The [CHSH demo](chsh.ipynb) shows the Sampler and Estimator in action.
The [teleportation demo](teleportation.ipynb) shows `Statevector` output.

