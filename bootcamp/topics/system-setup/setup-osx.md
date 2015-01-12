# OSX Setup

### System Package Manager: Homebrew

Install Homebrew (http://brew.sh/)
Copy and past into terminal:

    ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

    # Sample commands
    brew list
    brew search
    brew update
    brew doctor

Then add the following line to your .bashrc or .zshrc (or run bootstrap.sh):

    export PATH="$(brew --prefix coreutils)/libexec/gnubin:/usr/local/bin:$PATH"

Changing ownership of usr/local. This will benefit you when using node’s package manager, and will mean you won’t have to use sudo when installing into /usr/local:

    sudo chown -R $USER /usr/local

Install:

    # Make sure we’re using the latest Homebrew.
    brew update

    # Upgrade any already-installed formulae.
    brew upgrade

    # Install GNU core utilities (those that come with OS X are outdated).
    # Don’t forget to add `$(brew --prefix coreutils)/libexec/gnubin` to `$PATH`.
    brew install coreutils
    sudo ln -s /usr/local/bin/gsha256sum /usr/local/bin/sha256sum

    ## Install some other usefull utilities
    brew install tree
    brew install autojump (some additional setup required)
    brew install git
    brew install node
    ...

    ## Always good to perform cleanup at the end
    brew cleanup

More utilities:
See https://github.com/mathiasbynens/dotfiles
See https://github.com/KingScooty/dotfiles

### Language Setup

System Preferences - Language & Region - Preferred language
Set to English (if not already)

### The basics

The easy way

    ## Install OSX Applications (http://caskroom.io/)
    brew install caskroom/cask/brew-cask
    brew cask install google-chrome
    (brew cask install sublime-text-3)
    brew cask install grandperspective
    brew cask install iterm2
    brew cask install sourcetree
    brew cask install spectacle
    brew cask install appcleaner
    brew cask install p4merge

Google Chrome
    (https://www.google.com/intl/en/chrome/browser/)  use English version

SourceTree (GIT Client)
    (http://www.sourcetreeapp.com/)
    You need to create an Atlassian account.

Sublime Text 3 (Editor)
    http://www.sublimetext.com/3
    Install
        - Package Control
        - EditorConfig
        - MarkdownEditing

Window Size Manager
    [Spectacle](http://spectacleapp.com/)

Uninstaller
    [App Cleaner](http://www.freemacsoft.net/appcleaner/)

Better terminal
    [iTerm](http://iterm2.com/)

### Some short-cuts & tips

For dummies:

![OSX Keys](http://faculty.cs.gwu.edu/~timwood/wiki/lib/exe/fetch.php/learn:key-symbols.gif)

Short-cuts

* **Cmd + Space**: Spotlight search
* **Cmd + Shft + 3**: Take screenshots
* **Cmd + Shft + 4**: Take screenshots of area
* **Cmd + Shft + 4** & space: Take screenshots window
* **Cmd + Opt + D**: Hide your dock
* **Cmd + Opt + Esc**: Force Quit dialog
* **Cmd + Opt + Shft + Esc**: Force Quit current application
* **Cmd + Opt + Ctrl + Eject**: Force shutdown (direct!)
* **Cmd + plus(+) or min(-)**: Zoom in & out

* **fn + BS**: Delete (to remove from the front of the cursor)
* **fn + Up or Down**: Page up / down

Tips

* Us keyboard 'US-international' for all those french characters. Show 'Character viewer' and/or 'Keyboard Viewer' for other symbols.
* When you have a file open (sublime, photoshop, word), you can drap the icon to move the file.
* When you have a file open (sublime, photoshop, word), you can cmd + click the filename in the title to view its location.
* When **Cmd + Tab** switch between application, press **Q** to quit app, **H** to hide it.
* The spotlight search has a calculator build in.

More: http://www.danrodney.com/mac/index.html

### More utilities & tools

Some free, other commercial:

* http://pilotmoon.com/popclip/  (easy copy/past)
* http://marked2app.com/ (markdown)
* http://cord.sourceforge.net/ (remote desktop)
* http://grandperspectiv.sourceforge.net/ (disk space)
* https://cyberduck.io/ (FTP, SFTP, WebDav, ...)
* http://www.videolan.org (the video player)
* Office 2011 for mac (via office365)
* Outlook 2014 for mac (via office365)

Node Utils:

    npm install -g serve
    npm install -g md-fileserver

### dotfiles

Copy /dotfiles (hidden files included) to your home

    ./bootstrap.sh

### OSX Goodies

#### General UI/UX

    # Save to disk (not to iCloud) by default
    defaults write NSGlobalDomain NSDocumentSaveNewDocumentsToCloud -bool false

    # Remove duplicates in the “Open With” menu (also see `lscleanup` alias)
    #/System/Library/Frameworks/CoreServices.framework/Frameworks/LaunchServices.framework/Support/lsregister -kill -r -domain local -domain system -domain user

    # Disable local Time Machine backups
    hash tmutil &> /dev/null && sudo tmutil disablelocal

#### SSD-specific tweaks

    # Disable local Time Machine snapshots
    sudo tmutil disablelocal

    # Disable hibernation (speeds up entering sleep mode)
    sudo pmset -a hibernatemode 0

    # Remove the sleep image file to save disk space
    sudo rm /Private/var/vm/sleepimage
    # Create a zero-byte file instead…
    sudo touch /Private/var/vm/sleepimage
    # …and make sure it can’t be rewritten
    sudo chflags uchg /Private/var/vm/sleepimage

    # Disable the sudden motion sensor as it’s not useful for SSDs
    sudo pmset -a sms 0

#### Finder

    # Finder: allow quitting via ⌘ + Q; doing so will also hide desktop icons
    defaults write com.apple.finder QuitMenuItem -bool true

    # Finder: show hidden files by default
    #defaults write com.apple.finder AppleShowAllFiles -bool true

    # Finder: show all filename extensions
    defaults write NSGlobalDomain AppleShowAllExtensions -bool true

    # Finder: show status bar
    defaults write com.apple.finder ShowStatusBar -bool true

    # Finder: show path bar
    defaults write com.apple.finder ShowPathbar -bool true

    # Finder: allow text selection in Quick Look
    defaults write com.apple.finder QLEnableTextSelection -bool true

    # Display full POSIX path as Finder window title
    defaults write com.apple.finder _FXShowPosixPathInTitle -bool true

    # When performing a search, search the current folder by default
    defaults write com.apple.finder FXDefaultSearchScope -string "SCcf"

    # Avoid creating .DS_Store files on network volumes
    defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool true

    # Show the ~/Library folder
    chflags nohidden ~/Library


More info: https://github.com/mathiasbynens/dotfiles/blob/master/.osx

### Additional utils

#### New Terminal at Folder

    System Preferences - Keyboard - Shortcuts
    Check "New Terminal at Folder"

#### New iTerm at Folder

    http://peterdowns.com/posts/open-iterm-finder-service.html



