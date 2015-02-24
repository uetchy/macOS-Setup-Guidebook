# osx-setup

The guidebook to configure OS X for development.

## Before setup

* Install Xcode and Command Line Tools.

# Install essentials

## Website

```console
# edit /etc/apache2/httpd.conf
sudo sed -i -e "s|/Library/WebServer/Documents|/Users/${USER}/Dropbox/Sites|g" /etc/apache2/httpd.conf
sudo apachectl configtest
sudo launchctl load -w /System/Library/LaunchDaemons/org.apache.httpd.plist
sudo chmod 755 $HOME/Dropbox
ln -s $HOME/Dropbox/Sites/ ./Sites
```

## Sublime Text

```console
SUBLIME_LOCAL_DIR="$HOME/Library/Application Support/Sublime Text 3"
SUBLIME_SYNC_DIR="$HOME/Dropbox/Apps/Sublime Text"

rm -rf "$SUBLIME_LOCAL_DIR/Installed Packages"
rm -rf "$SUBLIME_LOCAL_DIR/Packages"
ln -s "$SUBLIME_SYNC_DIR/Installed Packages" "$SUBLIME_LOCAL_DIR/Installed Packages"
ln -s "$SUBLIME_SYNC_DIR/Packages" "$SUBLIME_LOCAL_DIR/Packages"
```

## Finder

###QLEnableSelection

```console
defaults write com.apple.finder QLEnableTextSelection -bool TRUE; killall Finder
```

### Shell

```console
brew install zsh
sudo sh -c "cat <<EOD > /etc/paths 2>&1
/usr/local/bin
/usr/bin
/bin
/usr/local/sbin
/usr/sbin
/sbin
EOD"
sudo sh -c "echo '/usr/local/bin/zsh' >> /etc/shells"
chsh -s /usr/local/bin/zsh
```

### Homebrew

```console
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap homebrew/dupes
brew tap caskroom/cask
brew tap uetchy/nlp
brew tap uetchy/backyard
brew install curl --with-ssh
brew install readline brew-cask git openssl wget ssh-copy-id peco subl hub
```

### vim

```console
brew install macvim --override-system-vim
```

### Ruby

```console
brew install ruby-build rbenv rbenv-binstubs rbenv-gem-rehash rbenv-readline rbenv-default-gems
eval "$(rbenv init -)"
echo \
"bundler
pry
lunchy
cocoapods
html2slim
sass
shenzhen" > $HOME/.rbenv/default-gems

REQUIRED_RUBY_VERSION=2.2.0
CONFIGURE_OPTS="--disable-install-rdoc --with-readline-dir=$(brew --prefix readline) --with-openssl-dir=$(brew --prefix openssl) --without-tcl --without-tk --enable-shared" rbenv install $REQUIRED_RUBY_VERSION
rbenv global $REQUIRED_RUBY_VERSION

echo -n "gem: --no-ri --no-rdoc" > $HOME/.gemrc
echo -n "--skip-bundle --skip-test-unit" > $HOME/.railsrc
gem update --system
gem update
```

### Vagrant

```console
# gem install vagrant
vagrant plugin install sahara
```

### Python

```console
brew install python
pip install virtualenv virtualenvwrapper readline
pip install numpy scipy PIL nltk python-dateutil pytz pyparsing six matplotlib
```

### OpenCV

```console
brew install opencv --with-jasper --with-qt --with-tbb
```

### Node.js

```console
brew install node --without-npm
curl https://www.npmjs.org/install.sh | sh
npm install -g bower browserify coffee-script component ember-cli express-generator gulp karma-cli lice mocha supervisor svgo vtop
```

### ImageMagick

```console
brew cask install xquartz
brew install imagemagick
brew link imagemagick
```

### rmagick

```console
MAGICK_PREFIX_PATH=`magick-config --prefix`/lib
PKG_CONFIG_PATH=$MAGICK_PREFIX_PATH/pkgconfig gem install rmagick
```

### MeCab

```console
brew install mecab mecab-ipadic
```

### TeX ###
```console
brew cask install basictex
```
