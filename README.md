# Skio Development Machine Setup

Setup Instructions For Developers (OSX Only Right Now)

Conventions:
-`$ [SOME COMMAND]` indicates a normal user terminal prompt. The dollar sign
  should not be used in the commands

## Global Prerequisites

### Install Homebrew
- Homebrew is a package manager for OSX that makes installing other useful software super easy
- To install, open up your terminal and paste the following:
  `$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
- In general, you can install almost any kind of open source software by typing the following into your console: 
  `$ brew install [name of package]`
- For more information, visit http://brew.sh/

### SublimeText3
#### Install SublimeText 3
1. `$ brew tap homebrew/versions`
2. `$ brew install Caskroom/versions/sublime-text3`

#### Install SublimeText Package Control
1. Open SublimeText3 and follow the instructions here: https://packagecontrol.io/installation

### Install Git
1. `brew install git`
