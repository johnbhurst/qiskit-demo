# Qiskit Demo

This repo contains some Qiskit samples, and instructions for a first-time user to get set up with these tools for Qiskit development and Quantum Computing:

* Python
* Visual Studio Code
* Git

## Software to install

### macOS

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

## SSH key for GitHub

Create an SSH private/public key pair:

``` bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Use a filename to indicate the key is for GitHub, e.g. `john.b.hurst-github`.

