# Completion Scripts

Generate customized completion scripts for your shell of choice.

## Generating and Installing Completion Scripts

Command-line tools that you build with `ArgumentParser` include a built-in option for generating completion scripts, with support for Bash, Z shell, and Fish. To generate completions, run your command with the `--generate-completion-script` flag to generate completions for the autodetected shell, or with a value to generate completions for a specific shell.

```
$ example --generate-completion-script bash
#compdef example
local context state state_descr line
_example_commandname="example"
typeset -A opt_args

_example() {
    integer ret=1
    local -a args
    ...
}

_example
```

The correct method of installing a completion script depends on your shell and your configuration.

### Installing Zsh Completions

If you have [`oh-my-zsh`](https://ohmyz.sh) installed, you already have a directory of automatically loading completion scripts — `.oh-my-zsh/completions`. Copy your new completion script to that directory.

```
$ example --generate-completion-script zsh > ~/.oh-my-zsh/completions/_example
```

> Your completion script must have the following filename format: `_example`.

Without `oh-my-zsh`, you'll need to add a path for completion scripts to your function path, and turn on completion script autoloading. First, add these lines to `~/.zshrc`:

```
fpath=(~/.zsh/completion $fpath)
autoload -U compinit
compinit
```

Next, create a directory at `~/.zsh/completion` and copy the completion script to the new directory.

### Installing Bash Completions

If you have [`bash-completion`](https://github.com/scop/bash-completion) installed, you can just copy your new completion script to the `/usr/local/etc/bash_completion.d` directory.

Without `bash-completion`, you'll need to source the completion script directly. Copy it to a directory such as `~/.bash_completions/`, and then add the following line to `~/.bash_profile` or `~/.bashrc`:

```
source ~/.bash_completions/example.bash
```

### Installing Fish Completions

Copy the completion script to any path listed in the environment variable `$fish_completion_path`.  For example, a typical location is `~/.config/fish/completions/your_script.fish`.

## Customizing Completions
