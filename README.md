# Joaquim’s dotfiles

This is a fork of [Mathias Bynens](https://mathiasbynens.be/) [dotfiles repository](https://github.com/mathiasbynens/dotfiles). Before anything else I recommend looking into his repository for inspiration. To a large extent, this is a subset of the configuration in the original repository. The main relevant difference is that I use zsh and not bash.

## Installation

**Warning:** If you want to give these dotfiles a try, you should first fork this repository, review the code, and remove things you don’t want or need. Don’t blindly use my settings unless you know what that entails. Use at your own risk!

You can clone the repository wherever you want (I like to keep it in `~/dotfiles`). The bootstrapper script will pull in the latest version and copy the files to your home folder.

### Setting up a new Mac

Before anything else, generate an SSH key and set up SSH accesss to GitHub:

```bash
curl -O https://raw.githubusercontent.com/quimrstorres/dotfiles/master/ssh.sh && chmod +x ssh.sh && ./ssh.sh
```

This script will ask the user for some data and assumes 2FA is set up for GitHub.

Clone the repository and move inside:

```bash
git clone --recursive -j8 git@github.com:quimrstorres/dotfiles.git
cd dotfiles
```

Install [Homebrew](https://brew.sh/) formulae and casks:

```bash
./brew.sh
```

Some of the functionality of these dotfiles depends on formulae installed by `brew.sh`. If you don’t plan to run `brew.sh`, you should look carefully through the script and manually install any particularly important ones. A good example is Bash/Git completion: the dotfiles use a special version from Homebrew.

### Install some things that are not available through Homebrew

```
# Install the Rust language server (requires rustup)
rustup component add rls rust-analysis rust-src
```

Next, set some sensible macOS defaults:

```bash
./macos.sh`
```

Finally, bootstrap dotfiles:

```bash
source bootstrap.zsh
```

### Configure/update existing Mac

```bash
git clone --recursive -j8 git@github.com:quimrstorres/dotfiles.git && cd dotfiles && source bootstrap.zsh
```

To update, `cd` into your local `dotfiles` repository and then:

```bash
source bootstrap.zsh
```

Alternatively, to update while avoiding the confirmation prompt:

```bash
set -- -f; source bootstrap.zsh
```

### Additional steps

#### Specify the `$PATH`

If `~/.path.zsh` exists, it will be sourced along with the other files.

Here’s an example `~/.path.zsh` file that adds `/usr/local/bin` to the `$PATH`:

```bash
export PATH="/usr/local/bin:$PATH"
```

#### Add custom commands without creating a new fork

If `~/.extra.zsh` exists, it will be sourced along with the other files. You can use this to add a few custom commands without the need to fork this entire repository, or to add commands you don’t want to commit to a public repository.

My `~/.extra.zsh` looks something like this:

```bash
# Git credentials
# Not in the repository, to prevent people from accidentally committing under my name
GIT_AUTHOR_NAME="Mathias Bynens"
GIT_COMMITTER_NAME="$GIT_AUTHOR_NAME"
git config --global user.name "$GIT_AUTHOR_NAME"
GIT_AUTHOR_EMAIL="mathias@mailinator.com"
GIT_COMMITTER_EMAIL="$GIT_AUTHOR_EMAIL"
git config --global user.email "$GIT_AUTHOR_EMAIL"
```

You could also use `~/.extra.zsh` to override settings, functions and aliases from my dotfiles repository. It’s probably better to [fork this repository](https://github.com/quimrstorres/dotfiles/fork) instead, though.

## Original author

| [![twitter/mathias](http://gravatar.com/avatar/24e08a9ea84deb17ae121074d0f17125?s=70)](http://twitter.com/mathias "Follow @mathias on Twitter") |
|---|
| [Mathias Bynens](https://mathiasbynens.be/) |

## The original author thanks to…

* @ptb and [his _macOS Setup_ repository](https://github.com/ptb/mac-setup)
* [Ben Alman](http://benalman.com/) and his [dotfiles repository](https://github.com/cowboy/dotfiles)
* [Cătălin Mariș](https://github.com/alrra) and his [dotfiles repository](https://github.com/alrra/dotfiles)
* [Gianni Chiappetta](https://butt.zone/) for sharing his [amazing collection of dotfiles](https://github.com/gf3/dotfiles)
* [Jan Moesen](http://jan.moesen.nu/) and his [ancient `.bash_profile`](https://gist.github.com/1156154) + [shiny _tilde_ repository](https://github.com/janmoesen/tilde)
* [Lauri ‘Lri’ Ranta](http://lri.me/) for sharing [loads of hidden preferences](http://osxnotes.net/defaults.html)
* [Matijs Brinkhuis](https://matijs.brinkhu.is/) and his [dotfiles repository](https://github.com/matijs/dotfiles)
* [Nicolas Gallagher](http://nicolasgallagher.com/) and his [dotfiles repository](https://github.com/necolas/dotfiles)
* [Sindre Sorhus](https://sindresorhus.com/)
* [Tom Ryder](https://sanctum.geek.nz/) and his [dotfiles repository](https://sanctum.geek.nz/cgit/dotfiles.git/about)
* [Kevin Suttle](http://kevinsuttle.com/) and his [dotfiles repository](https://github.com/kevinSuttle/dotfiles) and [macOS-Defaults project](https://github.com/kevinSuttle/macOS-Defaults), which aims to provide better documentation for [`~/.macos`](https://mths.be/macos)
* [Haralan Dobrev](https://hkdobrev.com/)
* Anyone who [contributed a patch](https://github.com/mathiasbynens/dotfiles/contributors) or [made a helpful suggestion](https://github.com/mathiasbynens/dotfiles/issues)
