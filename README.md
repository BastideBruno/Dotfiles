## NEOVIM

#### Installation depuis les sources:

* **1. Installer les dépendences**  

```
cd ~ && \
sudo apt install -y ninja-build gettext libtool libtool-bin autoconf python3-dev \
automake cmake g++ pkg-config doxygen libicu-dev libboost-all-dev libssl-dev \
ripgrep fd-find silversearcher-ag mlocate zoxide python3-pip libsqlite3-dev bat unzip git
```
* **2. Cloner le depot Neovim**  
```
git clone -b release-0.8 https://github.com/neovim/neovim ~/Apps/Neovim
```

* **3. Compiler les sources  
```
cd ~/Apps/Neovim && \
make CMAKE_BUILD_TYPE=RelWithDebInfo && \
sudo make install
```
