# Installation
fastdup is currently only supported on Ubuntu 20.04 or 18.04 OS.


## Ubuntu 20.04/18.04 LTS Machine Setup
Required machine setup
```bash
sudo apt update
sudo apt -y install software-properties-common
sudo add-apt-repository -y ppa:deadsnakes/ppa
sudo apt update
sudo apt -y install python3.8
sudo apt -y install python3-pip
sudo apt -y install libgl1-mesa-glx
python3.8 -m pip install --upgrade pip
```


# Pip Package setup

## Using pypi

```bash
python3.8 -m pip install fastdup
```

Note: you may need to upgrade your pip, using the command `python3.8 -m pip install -U pip`.

## Using stable release

- download the latest wheel for your system from our [release page](https://github.com/visualdatabase/fastdup/releases). Assuming the wheel file is found in your working folder, run:

```bash
python3.8 -m pip install *.whl
```

Note: you may need to upgrade your pip, using the command `python3.8 -m pip install -U pip`.

# Conda setup (Python 3.7 only)
## Using Anaconda channels:
```bash
conda install -y pandas tqdm opencv numpy
conda install -c dbickson fastdup
```

## Using stable release
- download the latest bz2 for your system from our [release page](https://github.com/visualdatabase/fastdup/releases). Assuming the wheel file is found in your working folder, run:
```bash
conda install -y pandas tqdm opencv numpy
conda install fastdup-<VERSION>-py37_0.tar.bz
```

Note: don't forget to replace the <VERSION> with the latest version for example 0.45


# Debian package install
- download the latest deb for your system from our [release page](https://github.com/visualdatabase/fastdup/releases). Assuming the wheel file is found in your working folder, run:
```bash
sudo dpkg -i fastdup-<VERSION>-ubuntu-20.04.deb
```
Application name is fastdup.

# Docker

##Pull from docker hub the latest ubuntu

```bash
docker pull karpadoni/fastdup-ubuntu-20.04
```


## Build your own docker

```bash
docker build -f Dockerfile -t fastdup-ubuntu .
```




# Currently supported software/hardware

Operating system
- `Ubuntu 20.04 LTS`
- `Ubuntu 18.04 LTS`
- `Mac OSX M1 Chip` (tested on Big Sur)
- `Mac Intel Chip` (tested on Mojave)

Software versions
- `Python 3.8` (via pip) or `Python 3.7` (via pip or conda) or a `debian package` (Python is not required)

Hardware support
- CPU (GPU not needed!)




# Common installation issues and their solution

ERROR: fastdup-0.39-cp38-cp38-manylinux_2_31_x86_64.whl is not a supported wheel on this platform.
- Check that you are on ubuntu 20.04 or 18.04 (via the command `lsb_release -r`). Alternatively on Mac M1 Big Sur or Mac Intel Mojave (use the command `sw_vers`) 
- Check that you are using the right python version (python3.8 and not python) 
- Make sure pip is up to date using `python3.8 -m pip install -U pip`). 
- Make sure you install using `python3.8 -m pip install..` and not just `pip install...`.
- If that does not work, please open an issue with the otuput of `python3.8 -m pip debug --verbose` or join our slack channel.

ERROR on Ubuntu: `libGL.so.1: cannot open shared object file: No such file or directory`
- Need to install depedency: `sudo apt -y nstall libgl1-mesa-glx`

Error on Mac+conda: `OMP: Error #15: Initializing libomp.dylib, but found libomp.dylib already initialized.
OMP: Hint This means that multiple copies of the OpenMP runtime have been linked into the program. That is dangerous, since it can degrade performance or cause incorrect results. The best thing to do is to ensure that only a single OpenMP runtime is linked into the process, e.g. by avoiding static linking of the OpenMP runtime in any library. As an unsafe, unsupported, undocumented workaround you can set the environment variable KMP_DUPLICATE_LIB_OK=TRUE to allow the program to continue to execute, but that may cause crashes or silently produce incorrect results. For more information, please see http://openmp.llvm.org/
zsh: abort      python3`
- Solution from [StackOverflow](https://stackoverflow.com/questions/53014306/error-15-initializing-libiomp5-dylib-but-found-libiomp5-dylib-already-initial)
- You should install all packages without MKL support:
```
conda install nomkl
conda install numpy scipy pandas tensorflow
conda remove mkl mkl-service # may fail, don't worry
```
