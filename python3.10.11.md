# BUILDING A SPECIFIC VERSION OF PYTHON ALONGSIDE AN EXISTING ONE

## Specifications
- Ubuntu 24.04
- Built in WSL
- Python 3.10.11

I needed this because I was running some applications that needed to be built in Ubuntu 22, but Essentia hadn't recieved updates for Python 3.12. It also generally seems useful to build Python from source, as well as side by side with other versions without using pyenv.

I like to build from source in my Tools folder in the home directory: If I make changes, they're easy to find, if not I can remove after.
```bash
cd Tools
```

```bash
# Install dependencies.
sudo apt update
sudo apt install -y \
    build-essential \
    libssl-dev \
    zlib1g-dev \
    libbz2-dev \
    libreadline-dev \
    libsqlite3-dev \
    wget \
    curl \
    llvm \
    libncurses5-dev \
    libncursesw5-dev \
    xz-utils \
    tk-dev \
    liblzma-dev \
    libgdbm-dev \
    libnss3-dev \
    libffi-dev \
    libsqlite3-dev \
    libssl-dev \
    git

# Clone gpython from github.
sudo git clone --no-checkout https://github.com/python/cpython.git
cd cpython
# Checkout python3.10.11
sudo git checkout 0c47759

# Build python.
sudo ./configure --enable-optimizations --prefix=/usr/local
sudo make -j$(nproc)  # Use all available CPU cores to speed up the build
sudo make altinstall  # Use altinstall to avoid overwriting the system Python
/usr/local/bin/python3.11 --version
```
