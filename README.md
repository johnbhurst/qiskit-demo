# Overview

This repo contains some Qiskit samples, and instructions for a first-time user to get set up with these tools for Qiskit development and Quantum Computing:

* Python
* Visual Studio Code
* Git

# Software to install

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

# SSH key for GitHub

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

# Python virtual environment

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

