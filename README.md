## NEOVIM

### Installation depuis les sources:

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

* **3. Compiler les sources**  
```
cd ~/Apps/Neovim && \
make CMAKE_BUILD_TYPE=RelWithDebInfo && \
sudo make install
```

### Configuration:  

* **1. Créer l'arborescence** 

`* ~/.config`  
`* ~/.config/nvim`  
`* ~/.config/nvim/init.lua`  
`* ~/.config/nvim/after`  
`* ~/.config/nvim/after/plugin`  
`* ~/.config/nvim/after/ftplugin`  
`* ~/.config/nvim/lua`  
`* ~/.config/nvim/lua/bruno`  
`* ~/.config/nvim/lua/bruno/options.lua`  
`* ~/.config/nvim/plugin`  
`  




* **2. Editer le ficher options.lua** 
```
local vim = vim

local options = {
	-- DISPLAY
	title = true,
	number = true,
	relativenumber = false,
	wrap = false,
	scrolloff = 10,
	sidescrolloff = 10,
	mouse = "a",
	cursorline = true,
	colorcolumn = "80",
	numberwidth = 4,
	textwidth = 80,
	shiftwidth = 2,
	tabstop = 2,
	softtabstop = 2,
	fileencoding = "utf-8",
	signcolumn = "yes",
	cmdheight = 2,
	showmode = false,
	splitbelow = true,
	splitright = true,
	smartindent = true,
	clipboard = "unnamedplus",
	laststatus = 2, -- set to 3 for an unique lualine bar.
	termguicolors = true, -- to enable highlight groups
	updatetime = 1000,
	-- SAVING
	backup = false,
	writebackup = false,
	swapfile = false,
	undodir = vim.fn.expand("~") .. "/.config/nvim/lua/bruno/undodir",
	undofile = true,
	undolevels = 500,
	-- SEARCH
	ignorecase = true,
	smartcase = true,
	hlsearch = false,
	-- COMPLETION
	--wildignore = "*.o,*.r,*.so,*.sl",
	completeopt = { "menu", "menuone", "noselect" }, -- need it for nvim-cmp
	-- REMOVE BEEP
	visualbell = true,
	errorbells = false,
}

for key, value in pairs(options) do
	vim.opt[key] = value
end
```
