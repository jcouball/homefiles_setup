# homefiles_setup

Store files from your home directory in Git for backup and tracking.

This is a good way to tracking changes to your shell startup files.

Based on the article [The best way to store your dotfiles: A bare Git repository](https://developer.atlassian.com/blog/2016/02/best-way-to-store-dotfiles-git-bare-repo/).

## Usage

### Setup

1. Clone this repository.
2. Create an empty GitHub repository to store your homefiles. 
3. Run the `homefiles_setup` script

   ```shell script
   $ homefiles_setup https://github.com/jcouball/homefiles
   ```

This will create a bare repository in `~/.homefiles`, add the usual Bash and Z Shell
startup scripts, and push them to your new repository.

Restart your shell to enable the `homefiles` command.

### Managing Home Files

Use the `homefiles` command to manage your home files. Since `homefiles` is an alias for
`git`, you can use all the same `git` commands you are already familiar with.

Run `homefiles` from your home directory:

* See what files have been changed:  

   ```shell script
   homefiles status
   ```

* See the changes are:

   ```shell script
   homefiles status
   ```

* Add a new file to Git: 

   ```shell script
   homefiles add .gemrc
   homefiles commit -m 'Add my gem configuration'
   homefiles push
   ```

## About Shell Startup Files

### Bash

[Bash startup files](https://www.gnu.org/software/bash/manual/html_node/Bash-Startup-Files.html)
showing the order (A, B, etc.) which files are sourced depending on how the shell was run. 

| File | Interactive<br/>Login | Interactive<br/>non-login | Script |
| :-------------: | :---: | :---: | :---: |
| **STARTUP<br/>FILES** | |       |       |
| /etc/profile    | A     | --    | --    |
| /etc/bashrc     | --    | A     | --    |
| ~/.bashrc       | --    | B     | --    |
| ~/.bash_profile | B1    | --    | --    |
| ~/.bash_login   | B2    | --    | --    |
| ~/.profile      | B3    | --    | --    |
| BASH_ENV        | --    | --    | A     |
|                 |       |       |       |
| **SHUTDOWN<br/>FILES** | |      |       |
| ~/.bash_logout  | C     | --    | --    |

List all possible Bash dotfiles:

```shell
ll /etc/profile /etc/bashrc ~/.bashrc ~/.bash_profile ~/.bash_login ~/.profile ~/.bash_logout
```

On my system:
* `/etc/profile` sources `/etc/bashrc` if not running bash
* `/etc/bashrc` sources `/etc/bashrc_$TERM_PROGRAM` — there isn’t one for iTerm.app
* `~/.bashrc` sources `/etc/bashrc`
* `~/.bash_profile` sources `~/.bashrc`

### Z Shell

[Z Shell startup files](http://zsh.sourceforge.net/Intro/intro_3.html)
showing the order (A, B, etc.) which files are sourced depending on how the shell was run. 

| File | Interactive<br/>Login | Interactive<br/>non-login | Script |
| :-----------: | :---: | :---: | :---: |
| **STARTUP<br/>FILES** | |     |       |
| /etc/zshenv   | A     | A     | A     |
| ~/.zshenv     | B     | B     | B     |
| /etc/zprofile | C     | --    | --    |
| ~/.zprofile   | D     | --    | --    |
| /etc/zshrc    | E     | C     | --    |
| ~/.zshrc      | F     | D     | --    |
| /etc/zlogin   | G     | --    |       |
| ~/.zlogin     | H     | --    |       |
|               |       | --    |       |
| **SHUTDOWN<br/>FILES** | |    |       |
| ~/.zlogout    | I     | --    | --    |
| /etc/zlogout  | J     | --    | --    |

List all possible Z Shell dotfiles:

```shell
ll /etc/zshenv ~/.zshenv /etc/zprofile ~/.zprofile /etc/zshrc ~/.zshrc /etc/zlogin ~/.zlogin ~/.zlogout /etc/zlogout
```

On my system:
* `/etc/zshrc` sources `/etc/zshrc_$TERM_PROGRAM` — there isn’t one for iTerm.app
* `~/.zshrc` sources `$ZSH/oh-my-zsh.sh`
