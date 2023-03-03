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
`* ~/.config/nvim/after/plugin/colorscheme.lua`  
`* ~/.config/nvim/after/plugin/nvim-tree.lua`  
`* ~/.config/nvim/after/ftplugin`  
`* ~/.config/nvim/lua`  
`* ~/.config/nvim/lua/bruno`  
`* ~/.config/nvim/lua/bruno/options.lua`  
`* ~/.config/nvim/lua/bruno/packer.lua`  
`* ~/.config/nvim/lua/bruno/keymaps.lua`  
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
* **3. Installer node.js via nvm (gestionnaire de version)** 
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
```  
`Relancer le terminal.`  
```
nvm install 18
```  
* **4. Installer pynvim** 
```
pip3 install pynvim
```  
* **5. Installer paker.nvim** 
```
git clone --depth 1 https://github.com/wbthomason/packer.nvim\
 ~/.local/share/nvim/site/pack/packer/start/packer.nvim
```  
* **6. Editer le ficher packer.lua** 
```
-- Auto install packer if not installed
local ensure_packer = function()
	local fn = vim.fn
	local install_path = fn.stdpath("data") .. "/site/pack/packer/start/packer.nvim"
	if fn.empty(fn.glob(install_path)) > 0 then
		fn.system({ "git", "clone", "--depth", "1", "https://github.com/wbthomason/packer.nvim", install_path })
		vim.cmd([[packadd packer.nvim]])
		return true
	end
	return false
end

local packer_bootstrap = ensure_packer() -- true if packer was just installed

-- Automatically source and re-sync packer when you save `packer.lua`.
local packer_group = vim.api.nvim_create_augroup("Packer", { clear = true })
vim.api.nvim_create_autocmd("BufWritePost", {
	command = "source <afile> | PackerSync",
	group = packer_group,
	pattern = vim.fn.expand("packer.lua"),
})

local packer_ok, packer = pcall(require, "packer")
if not packer_ok then
	return
end

local packer_util_ok, packer_util = pcall(require, "packer.util")
if not packer_util_ok then
	return
end

-- Plugins
packer.startup({
	function(use)
		-- Packer manager
		use("wbthomason/packer.nvim")
	end,
	config = {
		display = {
			open_fn = function()
				return packer_util.float({ border = "single" })
			end,
		},
	},
})

```   

* **7. Installer un theme**  
`Editer le ficher packer.lua`  
```
-- Colorscheme
use("folke/tokyonight.nvim")
-- use { 'catppuccin/nvim', as = 'catppuccin' }
```  
`Editer le ficher nvim/after/plugin/colorscheme.lua`  
```
local tokyo_status, tokyonight = pcall(require, 'tokyonight')
if not tokyo_status then
	return
end

tokyonight.setup({
	style = 'moon' -- 'storm', 'night', 'moon' and 'day'
})

vim.cmd [[ colorscheme tokyonight ]]

-- CATPPUCIN THEME
-- latte, frappe, macchiato, mocha
-- vim.g.catppuccin_flavour = 'macchiato' 
-- require'catppuccin'.setup()
-- vim.cmd [[ colorscheme catppuccin ]]
```  

* **8. Installer la police Hack Nerd Fonts**  

```
wget -P ~/Downloads https://github.com/ryanoasis/nerd-fonts/releases/download/v2.3.3/Hack.zip && \
cd ~/.local/share && \
mkdir fonts && \
cd fonts && \
mv ~/Downloads/Hack.zip . && \
unzip Hack.zip && \
rm -rf Hack.zip
```  
* **9. Installer nvim-tree & Web-Dev-Icons**  
`Editer le ficher packer.lua`  

```
-- nvim-web-devicons => icons
use("nvim-tree/nvim-web-devicons")

-- nvim-tree => file explorer
use({
	"nvim-tree/nvim-tree.lua",
	requires = { "nvim-tree/nvim-web-devicons" },
	tag = "nightly",
})
```  

`Editer le ficher keymaps.lua`  

```
-- ###########
-- # KEYMAPS #
-- ###########

local key = vim.keymap.set
local full_options = { noremap = true, silent = true }
local noremap = { noremap = true }

-- Set leader key as a space.
vim.g.mapleader = " "

-- #############
-- # NVIM-TREE #
-- #############

key("n", "<C-a>", ":NvimTreeToggle<CR>", full_options)
key("n", "<C-f>", ":NvimTreeFindFile<CR>", full_options)
```  

`Editer le ficher init.lua`  

```
require("bruno/options")
require("bruno/packer")
require("bruno/keymaps.lua")
```
