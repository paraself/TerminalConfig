# TerminalConfig
My Mac Terminal config.
### Features
- Colors for different commands.
- Seperator between each command.

Source:
http://lifehacker.com/5840450/add-a-handy-separator-between-commands-in-your-terminal-on-mac-os-x-and-linux  
http://osxdaily.com/2013/02/05/improve-terminal-appearance-mac-os-x/

### Usage
1. Open your mac terminal app
2. type `nano .bash_profile`
3. copy and paste the following code
4. press <kbd>Control</kbd> + O to save
5. press <kbd>Control</kbd> + X to exit from nano
6. restart your terminal app to see the changes

```bash
# Colorize terminal
export PS1="\[\033[36m\]\u\[\033[m\]@\[\033[32m\]\h:\[\033[33;1m\]\w\[\033[m\]\$ "
export CLICOLOR=1
export LSCOLORS=ExFxBxDxCxegedabagacad
alias ls='ls -GFh'

# Command divider
# ###########################
# Fill with minuses
# (this is recalculated every time the prompt is shown in function prompt_command):
fill="--- "

reset_style='\[\033[00m\]'
if [ -z "$VIM" ];
then status_style=$reset_style'\[\033[0;90m\]' # gray color; use 0;37m for lighter color
else status_style=$reset_style'\[\033[0;90;107m\]'
fi
prompt_style=$reset_style
command_style=$reset_style'\[\033[1;29m\]' # bold black
# Prompt variable:

OLD_PS1="$PS1"
PS1="$status_style"'$fill \t\n'"$prompt_style$OLD_PS1$command_style"

# Reset color for command output
# (this one is invoked every time before a command is executed):
trap 'echo -ne' DEBUG


function prompt_command {

    # create a $fill of all screen width minus the time string and a space:
    let fillsize=${COLUMNS}-9
    fill=""
    while [ "$fillsize" -gt "0" ]
    do
        fill="-${fill}" # fill with underscores to work on
        let fillsize=${fillsize}-1
    done

    # If this is an xterm set the title to user@host:dir
    case "$TERM" in
    xterm*|rxvt*)
        bname=`basename "${PWD/$HOME/~}"`
        echo -ne "\033]0;${bname}: ${USER}@${HOSTNAME}: ${PWD/$HOME/~}\007"
        ;;
    *)
        ;;
    esac

}
PROMPT_COMMAND=prompt_command
```
