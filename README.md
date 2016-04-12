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

### Install Git
- `$ brew install git`
- Setup your personal identity on git:
  + `$ git config --global user.name "YOUR NAME"`
  + `$ git config --global user.email YOUR_EMAIL`
- Configure some useful git worflow settings:
  + Simple push: `$ git config --global push.default simple`
  + Use colors: `$ git config --global color.ui true`
  + Save your credentials: `$ git config --global credential.helper osxkeychain`
  + Pull does a rebase rather than merge: `$ git config --global pull.rebase true`
  + Branches do a rebase rather than merge: `$ git config --global branch.autosetuprebase always`


### Clone skio-setup Repository
- Navigate to or create a folder to hold your developer files
- `$ git clone https://github.com/SkioDev/skio-setup.git`
- The folder containing the repository will be referenced in the remainder
  of this document as $SKIO_SETUP

### SublimeText3

#### Install SublimeText 3
- `$ brew tap homebrew/versions`
- `$ brew install Caskroom/versions/sublime-text3`
- Homebrew should automatically link the the SublimeText command line script
- To verify: `$ subl` should open a new window

#### Install SublimeText Package Control
- Open SublimeText3 and follow the instructions here: https://packagecontrol.io/installation

#### Install Recommended Packages and Settings
- Close SublimeText
- `$ cd ~/Library/Application\ Support/Sublime\ Text\ 3/Packages/`
- `$ rm -r User`
- `$ ln -s $SKIO_SETUP/sublime-text3/User`
- Reopen SublimeText. There may be some glitchiness and weirdness initially, but
  give it a few minutes, and it should return to normal

#### Use SublimeText3 as default git editor
- `$ git config --global core.editor "subl -w"`

### Set up shell preferences

#### Setup .bashrc
- `$ cp $SKIO_SETUP/terminal/.bashrc ~`
- `$ cp $SKIO_SETUP/terminal/.bash_profile ~`

#### Setup Terminal Preferences
- Open Terminal
- In the Menu Bar, click Terminal -> Preferences
- Select the profiles tab
- Click the settings button at the bottom of the left profile selector pane
- Browse to the $SKIO_SETUP/terminal folder
- Select `Solarized Dark.terminal` and click open
- Select `Solarized Dark` from the left profile selector pane and click default
  at the bottom

## Back End Prerequisites

### Java

#### Install jenv
- jenv manages all of your java installations and allows you to easily switch
  between JVMs
- `brew install jenv`
- Add the following lines to your ~/.bashrc
```bash
# Jenv configuration
if which jenv > /dev/null; then eval "$(jenv init -)"; fi
```


