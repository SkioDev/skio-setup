# Skio Development Machine Setup

Setup Instructions For Developers (OSX Only Right Now)

Conventions:
- `$ [SOME COMMAND]` indicates a normal user terminal prompt. The dollar sign
  should not be used in the commands

## Global Prerequisites

### Install XCode Command Line Tools
- `$ xcode-select --install`
- Click install

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

## Back End Development Prerequisites

### Java

#### Install jenv
- jenv manages all of your java installations and allows you to easily switch
  between JVMs
- `brew install jenv`
- Add the following lines to your ~/.bashrc (you can use `subl ~/.bashrc`)
```bash
# Jenv configuration
if which jenv > /dev/null; then eval "$(jenv init -)"; fi
```

#### Install java
- `$ brew cask install java` (make sure you confirm all the prompts)
- `$ jenv global 1.8`
- Confirm installation: `$ java -version`
- Output should be very similar to:
```
java version "1.8.0_77"
Java(TM) SE Runtime Environment (build 1.8.0_77-b03)
Java HotSpot(TM) 64-Bit Server VM (build 25.77-b03, mixed mode)
```

### Ruby

#### Install Ruby Version Manager (RVM)
- RVM is used to switch between different ruby versions / interpreters
- Helpful for switching between MRI (the reference implementation) and JRuby
- See 
- `$ brew install curl gpg`
- `$ gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3`
- `$ \curl -sSL https://get.rvm.io | bash -s stable --auto-dotfiles`
- `$ source ~/.rvm/scripts/rvm`

#### Install Ruby (MRI) 2.2.3
- `$ rvm install 2.2.3`
- Install bundler and pry gems: `$ gem install bundler pry`

#### Install JRuby 9.0.5.0
- `$ rvm install jruby-9.0.5.0`
- Create an alias for jruby: `$ rvm alias create j9k jruby-9.0.5.0`
- To switch to jruby, you must type `rvm use j9k`
- Install bundler and pry gems: `$ gem install bundler pry`
- Speed up startup time: `$ echo "export JRUBY_OPTS=--dev" >> ~/.bashrc`

### Other Libraries & Prerequisites
- `$ brew install ant maven openssl python wget`

### Install Postgres
- `$ brew install postgresql`
- `$ launchctl unload ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist`
- Paste the following into the terminal:
```bash
cat >> /usr/local/var/postgres/pg_hba.conf << EOF
# Skio Setup - allows all users local access
# "local" is for Unix domain socket connections only
local   all             all                                     trust
# IPv4 local connections:
host    all             all             127.0.0.1/32            trust
# IPv6 local connections:
host    all             all             ::1/128                 trust
EOF
```
- `$ launchctl load ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist`
- Run `$ psql` to confirm that it was installed correctly. It should start an
  interactive database prompt. Type `\q` to quit
- Postgres will now run anytime your computer is running


### Install Redis
- `$ brew install redis`
- `$ launchctl unload ~/Library/LaunchAgents/homebrew.mxcl.redis.plist`
- `$ launchctl load ~/Library/LaunchAgents/homebrew.mxcl.redis.plist`
- Run `$ redis-cli` to confirm that it was installed correctly. It should start
  an interactive prompt. Type `quit` to quit
- Redis will now run anytime your computer is running

### Install ElasticSearch
- `$ brew install elasticsearch`
- `$ launchctl unload ~/Library/LaunchAgents/homebrew.mxcl.elasticsearch.plist`
- `$ launchctl load ~/Library/LaunchAgents/homebrew.mxcl.elasticsearch.plist`
- Run `$ curl localhost:9200` to confirm that Elasticsearch was installed
  correctly. It should return something like this:
```json
{
  "name" : "Kofi Whitemane",
  "cluster_name" : "elasticsearch_brew",
  "version" : {
    "number" : "2.2.0",
    "build_hash" : "8ff36d139e16f8720f2947ef62c8167a888992fe",
    "build_timestamp" : "2016-01-27T13:32:39Z",
    "build_snapshot" : false,
    "lucene_version" : "5.4.1"
  },
  "tagline" : "You Know, for Search"
}
```


