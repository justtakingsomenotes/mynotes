# Linux Bible

Note to beginner self: `vim` not good for mental health, use `nano` instead.  
Use `vimtutor` when you start writing lots of stuff because once you get `vim`,  
it is actually useful.  
Additional note to self: Linux Bible is about fedora but most stuff works in  
Ubuntu as well. Identifying the  differences between the distributions helps  
to understand Linux.
  
Find your mouse with `xeyes`

## Ch1 and Ch2

No news but Ubuntu does `sudo` by default while fedora does apparently not.  
Root stuff with `su` in fedora until the Bible explains how to enable  
`sudo`. In case commands are not installed `sudo apt-get install [command]` or    
`sudo snap install [command]` for Ubuntu and `dnf install [command]` for  
fedora.

## Ch 3 Using the Shell

Long command that doesn't fit in one line? Use a backslash and hit enter.  
This will not execute what you already typed in the terminal but let you  
continue in a new line with a secondary prompt called PS2.  
`find /home/an/extraordinarily/long/path/ -type f -iname '*.jpg*' \`  
`>&& continue command here`  
    
`CTRL+ALT+F1-F6` switch between consoles, does not work in Ubuntu by default  
  
who am i / whoami: display username  
  
`grep username /etc/passwd` information about the user, last part shows  
the terminal in use (mostly bash)  
  
`date` shows date  
  
`pwd` shows present working directory  
  
`hostname` shows name of host  
  
`ls` list files in pwd  
  
`ls -lat` l=long, more information, a=all, including hidden files  
which have a dot in front of their name, t=time, list by time  
  
Example of a hidden file: `.bash_history`, visible only when using the  
`-a` argument  
  
`ls --all` does the same as ls -a, double dash is the long way, see man pages  
  
With single letter options (e.g.`-l`) the argument (`ls -l Downloads`  
where Downloads is the argument) typically follows after one space  
  
With full-word options (e.g. `--hide`) the argument often follows an equal  
sign, e.g. `ls --hide=Desktop` (will list all content except the  
Desktop folder)  
  
`tar -cvf backup.tar /home/martin` create (c) file (f) and while you do this  
show verbose (v) messages. backup.tar is an argument for the option f,  
/home/martin is an argument for tar as a whole  
  
`uname` show system information  
  
`date +'%d/%m/%y'` weird syntax of date command, check man pages `man date`  
  
`id` show environment of user, including user's group, all stuff after  
"context" has something to do with SELinux security features...what is SELinux?  
  
`who -uH` shows user, console used and system time, -u information about  
idle time, -H use headings  
  
Commands are located in directories, the Shell knows where the commands are  
because of a user's "path": e.g. `/bin/date` for the `date` command  
  
If commands reside in directories with very long pathnames then you can  
save the time to type the full path by adding those directories to  
the Shell's PATH environment variable  
  
The PATH consists of a list of directories that are sequentially checked  
for the command you enter  
  
`echo $PATH` see your current PATH, the displayed directories are  
separeted by a colon  
  
Own commands or Shell scripts are ideally put in the user's  
bin directory, e.g. `~/bin` which is the same like `/home/martin/bin` if  
martin is the logged-in user  
  
`/home/yourusername/bin` is sometimes automatically added to the  
user's PATH. Sometimes you have to create it and/or add it to PATH manually  
  
When own commands or Shell scripts are added you will need to do this with  
EXECUTE PERMISSION  
  
Executables only run if they are in the user's PATH unless you type their  
absolute or relative location (relative: `./executable.sh`)  
  
Commands are run depending on their location (`echo $PATH`) from  
left to right. The same command twice? The command that is not found first  
(left to right) needs the full pathname or PATH needs to be changed  
  
Some commands are not in PATH but are built into the Shell, some  
commands can be overridden by aliases that do whatever you want them to do  
  
There are also ways to define functions that consist of a stored series of  
commands.  
  
Order in which Shell checks commands you type: aliases, shell reserved word,  
function, built-in command (cd, echo, exit, fg, history, pwd, set, type),  
filesystem command (this is PATH), see also below: `type`  
  
`alias` show what aliases are set, often used to make long commands with  
many options and arguments shorter  
  
`exit` exit from a shell  
  
`fg` bring command running in the background to the foreground  
  
`history` show commands (also the mistyped ones) that were previously used  
  
`set` set Shell options  
  
`type` show location of a command, e.g. `type date` results in:  
`date is hashed (/usr/bin/date)`, use `which` if `type` does not work  

`type which`, `type case`, `type return` and `type -a ls` make the difference  
between command types clearer  
  
Command not found? Spelling, case sensitive! Is it in your PATH variable?  
Permission denied to run command? It is in your PATH but not executable  
  
Don't know where command is located? Use `locate`, e.g. `locate chage`  
Note: not all directories are accessible to you unless you are the root user,  
`locate` may not find all information  
  
`locate` looks all over you filesystem and finds everything accessible that  
contains the string you provided as an argument (e.g. `locate chage`)  
  
Things beginning with a `$` sign in Bash are all variables  
  
`finger` is a user information lookup command (had to be installed,  
was detected automatically by Bash)  
  
`history` shows the last commands  

`!n` where n is a number shown after running `history` runs the command  
following said number  
  
`!!` runs the previous command  
  
`clear` clears the screen in terminal  
  
`!?string?` runs the most recent command containing "string", can be an  
incomplete part of the string  
  
`CTRL+R` reverse incremental search  
  
`CTRL+S` forward incremental search  
  
`ALT+P` reverse search  
  
`ALT+N` forward search  
  
CAREFUL!!! COMMANDS ARE RUN AUTOMATICALLY AFTER CLOSING THE TEXT EDITOR!!!  
`fc` followed by number from `history` opens default terminal editor which is  
in the worst case `vi` (just as bad as `vim`) or you are lucky and `nano` is  
opened. The text editor show the command used. Example: run `history`, pick  
any number you see, say 1, run `fc 1` and the text editor opens and there is  
already the command you saw behind "1" in the text editor.  
  
Exit `vi` or `vim` by typing `:q!` or type `:wq!` to save file and exit.  
AFTER CLOSING THE TEXT EDITOR THE COMMANDS YOU SAW ARE EXECUTED!!!  
  
THESE COMMANDS ARE RUN AFTER CLOSING TEXT EDITOR!!!  
`fc [number from history command] [other number from history command]` puts  
the RANGE of commands from history entries in the text editor. The same as  
above applies: THESE COMMANDS ARE RUN AFTER CLOSING THE TEXT EDITOR!!!  
  
What you see after running `history` is stored in `.bash_history` which should  
be located in the user's home folder. Type `cd ~` to go to the home folder  
and then `nano .bash_history` to see its content which should be the same as  
what you see after running `history`.  
  
Setting $HISTFILE to "null" or $HISTSIZE to 0 is often used for root.  
  
If a Shell is closed using the kill command then the commands used are not  
stored in history because the Shell needs to be closed properly.  
  
Example: `kill -9 1234` kills the process ID "1234" which could be a Shell  
  
TIME SAVER: any letter followed by TAB TAB shows all autocomplete options  
  
`history 8` shows the last 8 commands  

### Connecting and Expanding Commands - useful

Important metacharacters: | & ; ) ( < >  
  
`|` connects output from one command to the input of another command. Example:  
Do `cd /bin` to go to a folder with lots of stuff in it. Do `ls` to realise  
that you cannot see all the output. Then do `ls | more`. You just piped the  
output of `ls` to the input of `more`. Press any key to continue in more's  
list. Press `q` to leave the output of `more`. `q` also lets you exit from  
the man pages of any command, try `man [any command such as ls]` and exit  
what you see by typing `q`.  
  
`cat [any file] [another file]` concatenate files and print them on the  
standard output. Also works with only one file the content of which will be  
printed out on the screen.  

` ; ` sequential commands, use spaces before and after: `[space];[space]`  
  
`&` use the ampersand (&) to run commands in the background, example:  
`troff -me verylargedocument | lpr &` Closing the Shell kills the process  
running in the backgroud.  
  
`$(command)` or the word "command" with backticks in front and after the word  
(not single quotes) make the output of the command interpreted by the shell  
instead of by the command itself in order to use the output as an argument  
for another command. Example: `nano $(find /home | grep xyzzy)`  
  
`$(expression)` passing an arithmetic expression to a command, example:  
`echo "I'm $(2018 - 1985) years old."` or  
`echo "There are $(ls | wc -w) files in this directory."`  
  
`wc` count command, option `-w` counts words  
  
Environmental variables such as PATH or BASH can be expanded if they are  
preceded by a $ sign: `$BASH` the variable is then printed instead of the  
variable name itself  
 
### Using Shell Variables

`$SHELL` identifies the Shell you are using  
  
`$PS1` defines your Shell prompt. Remember the comment on PS2 above?  
Try `echo $PS2`. It is there PS2 variable which defines that the prompt is a `>`  
  
`$MAIL` identifies the location of your mailbox  
  
`set` see all variables of the current Shell. Better use: `set | more`  
  
A subset of all those variables are ENVIRONMENTAL VARIABLES. They are  
exported to any new Shells opened from the current Shell. Type `env` or  
`declare` to see environment variables. Better use: `env | more`  
  
A list of common environment variables is on pp. 86-87 of the Linux Bible  
  
Interesting: `echo $RANDOM` shows a random number between 0 and 99999  
  
### Creating and using aliases

alias commands = shortcuts to any command  
  
Example: `alias p='pwd ; ls -CF'` will run the `pwd` command and then `ls -CF`  
when you type the letter p and press enter  
  
`rm -i` be prompted for each file removal individually, always use `-i` when  
you do not yet feel confident in the Linux terminal  
  
type `alias` as a command to check all aliases that are presently set  
  
`unalias` can remove an alias. However, opening a new shell will fetch aliases  
from a configuration file, so unaliased aliases may be restored by that  
configuration file  

Example that could be added in .bashrc: `alias mypass="cat /etc/passwd"`  
  
### Configuring your shell

Check Linux Bible on p. 88 for bash configuration files:  
`/etc/profile`  
  
`/etc/bashrc`  
  
`~/.bash_profile` is a good place to add environment variables because, once  
set, they are inherited by future shells. Note to self: Flask environmental  
variables here?  
  
`~/.bashrc` a good place to add aliases or user specific prompts, see p. 90 of  
the Linux Bible. This is read in each time you open a new shell.  
  
`~/.bash_logout`  
  
`source` What does the `source` command do? Read and execute commands from  
arguments provided after 'source' in the current shell environment, example:  
`source $HOME/.bashrc`  
Why does `source` look familiar to me? Because I created and activated a  
virtual environment in all the Python tutorials I did and never understood  
what I'm actually doing: `. venv/bin/activate` aka `source venv/bin/activate`  
  
`$HOME` is a replacement for `~` which are both shortcuts to your home folder  
  
### Setting your prompt

This is a prompt:  
`[martin@localhost ~]$`  
   
PS1 to PS4 are the relevant environment variables, examples on p. 90 of the  
Linux Bible  
`echo $PS1` is insightful because you can derive what PS1 must look like in  
order to create the prompt that you want to have. Ever wondered how all those  
highly skilled tech tutorial youtubers can have prompts that are better than  
yours? They changed the PS1 variable.  
Do not ever forget to comment (octothorpe aka hashtag) out what you  
find .bashrc (as backup) and also comment what you change.  
Corey Schafer's PS1 looks probably similar to this (apart from the debian stuff):  
` PS1='\nIt is \e[1;36m\A\e[m. ${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\] in directory:\n\[\033[01;34m\]\w\[\033[00m\] \n$ ' `  
nixCraft is the source you want consult when it comes to stuff like this.  
  
PS2 is often set to `>`  
You get this prompt `>` if you type something in the command line and end it  
with `\`  

### Adding environment variables

Just put them at the end and don't forget to export and comment (octothorpe  
aka hashtag). Check pp. 91-92 of the Linux Bible. This looks useful for  
the Flask variables.  
  
Examples:  
Assuming I saved my own commands in /getstuff/bin then the following line  
would make them accessible: `PATH=$PATH:/getstuff/bin ; export PATH`  
If I now do a `echo $PATH` I would see that `/getstuff/bin` was appended  
to the end of echo's output.  
  
The following is bad practise because it would run commands in any current  
directory: `PATH=$.:$PATH ; export PATH`  
Don't do the line above but be aware that someone could add a malicious  
command in your directory since the dot `.` which is equal to `source`  
would be prepended to your `$PATH` AND an `export` takes place at the same  
time which makes the changes effective not only for the commands being called  
but also in the calling program (bash itself). More on this [here](https://unix.stackexchange.com/a/26067).  
`echo $PATH` would reveal that the dot is at the beginning of the output.  
Remember: commands are checked against `$PATH` from left to right.  
  
Auto time-out after 30 minutes, use seconds: `TMOUT=1800`  
  
You can basically assign anything to an environment variable that is not  
yet used: `COOLSHORTCUT=some_folder ; export COOLSHORTCUT`  

### Getting information about commands

`echo $PATH` shows you all the paths that contain commands  
`help | less` shows built-in commands  
use `-- help` with the command  
use man pages with `man [command]`  
use info pages with `info [command]` in case of `fg` there was much more info  
via `info` than via `man`  
#### Man pages deserve their own heading

Check "VI and VIM" section. The search options there also apply to man pages  
and enable you to search man pages effectively: `/`, `?`, `n` and `N`.
  
There are 8 MAN PAGE SECTIONS:  
  
1. user commands
2. system calls (interesting for programmers)
3. C library functions (see 2)
4. devices and special files
5. file formats and conventions
6. games
7. misc
8. sys admin tools  
  
Just `man` always gives you section 1.  
Access specific sections like this `man 5 passwd`  
  
Access name+summary sections of all man pages typing this:  
`man -k passwd` (VERY COOL)  
In a man page, press `/` then you can search the man page for a specific term.  
  
## Ch 4 Moving around the filesystem

Check directory tree and info on pp. 98-99 for common directories.  
`bin` common linux user commands  
`boot` contains the bootable kernel and the boot loader  
`dev` devices, e.g. tty* (terminal), fd (floppy disk), hd* or sd* (hard disk),  
ram*,  cd*  
`home` directories for each user, except root who has his “home” directory  
in /root  
`etc` administrative configuration files  
`media` standard location for automount devices such as USB drives  
`lib` shared libraries needed by /bin and /sbin to boot the system  
`mnt` nowadays used to mount local or remote filesystems temporarily and is  
the predecessor of `/media`.  
`misc` sometimes used to automount filesystems on request  
`proc` contains information about system resources  
`opt` directory structure available to store add-on application software  
`sbin` daemon processes and administrative commands  
`root` home folder of root user. It’s not within `/home` for security reasons  
`tmp` tmp files used by applications  
`usr` user documentation, games, graphical files (X11), libraries (lib), other  
commands, files not needed during the boot process  
`var` used by various applications, meant to contain stuff that changes often  
such as files on an FTP or web server  

### Using basic file system commands

Google and man pages are your friends: `mkdir`, `touch`, `ls`, `rm`,  
`cp`, `mv`, and (CAREFUL!) `rm` and `rm -r` for folders with subdirectories,  
better always use `rm -ir`.  
  
See table on p. 100 of Linux Bible, important: `chmod` for changing permissions  
  
From $HOME directory: `cd /../../../usr` takes you below `~` on three levels  
and then from there to `/usr`  
  
checking permissions: `ls -ld [something]` gives you  
`drwxrwxr-x. 2 [user] [group] 4096 Dec  8 17:49 [folder]`  
`d` at the beginning shows that this is about a directory  
The fact that a user is in a group with the same name like himself is called  
“user private group scheme”  
  
`chmod 700 [file or directory]` gives me full access (read write execute) to  
the file/directory and everyone else no access at all  
  
### Using metacharacters and operators see pp. 102-105 in Linux Bible
  
File-matching metacharacters, like regular expressions:  
  
`*` matches any number of characters  
`?` matches any one character  
`[...]` Matches any one of the characters between the brackets, which can  
include a hyphen-separated range of letters  
`touch` change file timestamps or create new file if argument does not exist  
`ls [abw]*` any file beginning with a, b, w is matched  
`ls [abw]*[ne]` see above plus ending with either n or e is also matched  
This also works with ranges: `ls [a-g]*`  

### File-redirection metacharacters  

`|` piping standard output of one command to standard input of another, e.g.  
`history | less`  
`<` directs the contents (not the output) of a file to a command  

`>` directs the standard output of a command to a file (Warning:  
overriding whatever is already in the file)  
  
`2>` directs standard error (i.e. error messages) to a file  
  
`&>` directs both standard output and standard error to the file  
  
`>>` directs the output of a command to a file, adding the output to the  
end of the existing file (appending to a new line)  
  
`<<` aka "here text" or "here command". Enables you to type text that can be  
used as STDIN for a command. The text to be used as standard input  
has to be between a free-to-choose word. Example:  
  
`mail root aname bname cusername <<TheStdInForTheMailCommand` - root sends  
the STDIN to the three users  

### Using brace expansion characters

Be careful with this!  
`touch memo{1,2,3}` will create three files: memo1, memo2, memo3  
`rm -f memo{1,2,3}` will remove the three files just created; the -f option  
ignores non-existent files and doesn’t prompt  
`touch {John,Bill,Sally}-{Breakfast,Lunch}` will create all combinations with  
a dash – in between  
`touch {a..f}{1..5}` does what you would expect based on what's above  
`rm -i *` asks you before removing every file, y for yes n for no  
`rm -R` deletes subfolders, be CAREFUL with this  

### Listing files and directories

`ln` creates a hard link by default, option `-s` creates a soft link  
Example on p. 106: `ln [options] [where to point to] [name of the pointer]`  
Example result of the above:  
`lrwxrwxrwx. 1 Fedorauser Fedorauser    5 Dec 23 22:11 pointer_to_apple -> apple`  
`-rwxr-xr-x. 1 Fedorauser Fedorauser    0 Dec 23 22:06 scriptx.sh`  
`drwxrwxr-x. 2 Fedorauser Fedorauser 4096 Dec 23 22:06 Stuff`  
`-rw-rw-r--. 1 Fedorauser Fedorauser    0 Dec  8 21:34 watermelon`  
What you see after the 2nd "Fedorauser" (group name) is the number of  
characters in bytes. Permission part: the `d` indicates a directory, lower  
case L `l` indicates a symbolic link, a hyphen `-` a regular file, the `x` at  
the end indicates that it is executable.  
  
When running `ls -l` there is total `[some number]` in the first line which  
is the space consumed by the displayed files in kilobytes.  
If there is an `s` somewhere in the permission column it means that it can be  
run by any user. However, ownership does not change. This is called a UID/GID  
(user/group ID) program.  
  
If there is a `t` at the end of the permission column it means that there is  
a "sticky bit" which allows other users or groups to create files but prevents  
the removal of others’ files. A capital `T` (sticky bit) and `S` (GID) means  
that the permission was set without execute permission.  
  
A plus sign `+` means that an extended attribute such as SELinux or Access  
Control Lists (ACLs) have been set.  
  
Show your own home directory using the tilde `~`: `echo ~`  
Show other users’ home using `echo ~[otheruser]`  
This also works with root: `echo ~root`  
This also works when navigating: `cd ~someuser/test`  
`cd` takes you to `$OLDPWD`  
A single dot `.` is the `$PWD`  
Two dots `..` are the directory above `$PWD`  
`ls -t` displays the items in the order in which they were last modified  
`ls -F` adds markers to the files to be displayed (easier to read)  
`ls –hide=PATTERN` hides entries according to the pattern, e.g. `ls -hide=g*`  
will hide any file beginning with the letter "g" (this trick is case sensitive)  
`ls -ld some_dir_or_file one_more_file` is useless without the `-l` option.  
But `-ld` shows information only for the specified directory/file  
`ls -R` additionally shows subdirectories (careful, especially on root level!)  
`ls -S` list files by size  

### Understanding file permissions and ownership

There are 9 permission bytes, use `ls -l` to see them and ignore the first  
character (e.g. d=directory, see designators above): `drwxr-xr-x`  
List of designators:  
`d` = directory  
`-` = file  
`l` = symbolic link  
`b` = block device: are addressable in device-specified chunks called blocks  
and generally support seeking, the random access of data. They are often  
abbreviated as `blkdev`. Block devices are accessed via a special file called  
a block device node and generally mounted as a filesystem. Example: Hard-disk.  
`c` = character device: are generally not addressable, providing access to  
data only as a stream, generally characters i.e. bytes. They are often  
abbreviated as `cdev`. They are accessed through a special node in  
filesystem called as character device node. Example: Keyboard  
`s` = socket, a special file used for bi-directional inter-process communication  
`p` = named pipe, unidirectional communication  
  
Example: `drwxr-xr-x`  
the first character is the designator (see above), followed by three sets of  
permissions where the 1st three characters are the owner's permissions, the  
2nd three are the group's permissions and the 3rd three are the permissions  
of all others not belonging to neither owner or group. Also: `r` = read bit,  
`w` = write, `x` = execute and `-` = nothing is assigned  
  
The permissions allow what you would expect, but there is an exception:  
Access to metadata of the files requires `x` permission because of inodes need  
to be read.  
  
Setting permissions with  
`chmod [three numbers, each representing one of the three sets of permissions mentioned above OR letters]`  
where:  
`r` = `4`  
`w` = `2`  
`x` = `1`  
`-` = `0`  
  
Add those numbers to compose permissions, examples below.  

### Changing permissions with chmod (numbers; always change all three bits)

Example permissions of a directory: `drwxr-xr-x`, remember that `d` is a  
designator, `rwx` would be the owner's permission, `r-x` would be the  
group's permission and the second `r-x` would be the permission of all others.  
  
If you own a file you can change the permissions. Add the numbers (see above)  
to define the permission for each type of user/group.  
  
Example for full permission for all types of user/group (7 = 4 + 2 + 1 for all):  
`chmod 777 [some file or directory]`  
You can use `chmod` recursively to set the permissions for deeper levels of  
the folder structure (similar to ls -R): `chmod -R 755 $HOME/myapps`  
The above would apply `755` permissions to the directory itself AND all  
subdirectories.  
  
### Changing permissions with chmod (letters; more precise, see below)

See above for the letters: `r`, `w`, `x` and the hyphen `-`  
  
`+` and `-` to add/remove permission respectively  
change permissions for the user = `u`, group = `g`, others = `o`, or all = `a`  
syntax is `chmod [ugoa][+-][rwx-]`  
Example1: `chmod a-w filename`  
Example2: `chmod -R ug+rx folder`  
Why is this more precise? `chmod -R o-w $HOME/myapps` changes one bit only  
as opposed to `chmod 755` or `chmod 644`  

### Setting default file permissions (users and root) with umask

A file created as a regular user gets by default:  
`-rw-rw-r--`  
Files created by root may have other values. These default values are  
determined by the `umask` command. Type `umask` to find out what the present  
umask value is, example: `0002`. This is an octal value. Octal values stolen  
from the Prophet (nixCraft):  
  
0 = read, write and execute  
1 = read and write  
2 = read and execute  
3 = read only  
4 = write and execute  
5 = write only  
6 = execute only  
7 = no permissions  
  
To change permanently, add a `umask` command to `.bashrc` (near the end of  
the file). `umask -S` makes that stuff human readable, see man pages.  

### Changing file ownership

Use `chown` - only root can do this.  
  
`chown joe /home/joe/memo.txt` – memo.txt, created by root in joe’s `$HOME`  
now belongs to joe  
`chown joe:joe /home/joe/memo.txt` memo.txt’s ownership AND group just  
changed to joe and the joe-group  
`chown` also works with the recursive option (=the directory itself and all  
of its contents are included): `chown -R joe:joe /media/myusb`  

### Moving, copying and removing files

Known stuff, except:  
Better do an alias for `mv` to `alias mv='mv -i'` to ensure no files are  
accidentally deleted which is the default of `mv` if not aliased  
`mv -b` creates a backup of any file that would be overridden  
  
`cp file1 file2`  
`cp [file] [directory]` (the name of file is kept at the new location)  
`cp -r /some_directory* /some_target_directory` recursive  
`cp -ra` does the same as above, `-a` is for maintaining permissions and  
date/time stamps  
see also `cp --preserve` in the man pages  
aliasing `rm` to `alias rm="rm -i"` is also recommended  
`rmdir` delete EMPTY directories, CAREFUL: delete directories with `rm -r` and  
consider to only use `rm -ri [directory]`  
run any command unaliased by using a backslash in front, e.g. `\mv`  

## Ch 5 Working with Text Files

See p. 119. Mental stability suffers when using `vi` or `vim`. `nano` is often  
available as well and saves you lots of headaches. Purists seem to prefer  
vi(m) though.  

### VI and VIM

vi has a command mode and an input mode:  
vi always starts in command mode before you can edit a file in the input mode.  
The `ESC` key (sometimes 2x `ESC`) brings you back to command mode when you  
are in input mode.  
Command mode commands (more: see book):  
`a` - add text to the file, to the right of the cursor  
`A` - add text to the end of the current line  
`i` - insert to the left of the cursor  
`I` - insert at the beginning of the current line  
`o` - opens a line below the current line and puts you in i mode  
`O` - opens a line above the current line and puts you in i mode  
`H` - move cursor to the upper-left corner of the screen  
`M` - see above but middle line  
`L` - see above but lower-left  
`x` - delete text under the cursor  
`X` - delete text directly before the cursor  
`d + arrow keys` - delete some text  
`c + arrow keys` - changes some text  
`y + arrow keys` - yanks=copies text  
`P` - copies strings to the left of the cursor, more than one line is copied  
above the current line  
`p` - see above but to the right and below  
  
Repeating commands: repeat the action (e.g. you just copied some text) by  
typing a period, see p. 122.  
  
Exiting vi:  
`ZZ` or `:wq` - save and exit  
`:w` - save only  
`:q` - exit without saving (doesn't work if changes were made)  
`:q!` - exit without saving and closing vi  
`u` - undo changes  
`CTRL+R` - undo the undo  
  
DO NOT EVER USE CAPS LOCK in vi  
  
OK, seems to be a strength of vi: `:![some shell command]` - use any shell  
command from within vi and then return to vi after execution  
`CTRL+G` - show info about the file and where you are  
`/[some word]` - search for the word, forward direction, also works in man pages  
`?[some word]` - see above but backwards, also works in man pages  
`/The.*foot` - search for a line that has "The" and after that at some point  
"foot"  
`?[pP]rint` - search backward for either print or Print  
  
After searching, type `n` (same direction) or `N` (opposite direction) to  
search again.  Also works in man pages.  
The vi editor is based on the ex editor which has some useful commands, see  
p. 124.  

### Finding files with grep, locate, find and other tools

Note: user permissions may limit the files that can be found, searches are  
case sensitive, use [OPTION] to ignore case sensitive, e.g. `locate -i`  
  
`locate` - find commands by name, searching through a database which is  
usually automatically updated on startup by the updatedb command --> faster  
but maybe not up to date, not every file is stored in said database, see  
`/etc/updatedb.conf` <-- check out with conf which files are not included in  
the database.  
  
best they say --> `find` - find files based on lots of different attributes  
such as size, user or permission (see p. 128: `-iname` and `-name`); live  
search through the filesystem -->slower  
  
`grep` - search within text files to find lines in files that contain search  
text. Cool example when you want to start Flask the 2nd time in your life:  
`history|grep FLASK`  
  
Too many error messages? Use, for example, `find test /root 2> /dev/null` to  
send STDERR to the next option, in this case Linux Nirvana `/dev/null`. See  
also: [Null device wikipedia page](https://en.wikipedia.org/wiki/Null_device)  
  
File matching characters `*` and `?` are supported  
  
Searching by size:  
  
`find /usr/share/ -size +10M -size -5Gf`
  
Searching by user:  
  
`find /home -user someuser -or -user someotheruser -ls`  
`-not`, `-or` and `-group` also work as described above  
  
Searching by permission: --> a good way to identify security issues  
  
`find /home/someuser -perm -755 -type d -ls`  
What do you find with -002? see p. 130  
  
Searching by date and time:  
  
Find files that were changed within the last 10 minutes: `find /etc/ -mmin -10`  
  
Find the evil hacker with `find /bin /usr/bin /sbin /usr/sbin -ctime -3` which  
shows whether ownership or permissions changed within the last 3 days  
  
`find /var/ftp /var/www -atime +300` have not been accessed for +300 days  
Check man pages: `-atime -ctime -mtime -amin -cmin -mmin`  
  
Combine all of the above:  
  
`find /var/all \( -user joe -or -user -chris -not group joe -and size +1M\) -ls`  
  
Search and execute:  
  
`find [options] -exec command {} \;` <-- prompt does not ask questions  
`find [options] -ok command {} \;` <-- prompt does ask questions, the curly  
braces indicate where on the command line to read in each file that is found,  
each file can be included multiple times, `\;` means ending a line.  
  
EXAMPLES:  
`find /etc -iname iptables -exec echo "I found {}" \;`  
`find /var/allusers/ -user joe -ok mv {} /tmp/joe/ \;`  
  
grep:  
  
search single files or directory structures recursively  
case sensitive is default, use `-i` option to search case-insensitive  
you can also search standard output  
  
`-v` find all stuff that does NOT include what you passed with grep as an  
argument, example: `grep -vi tcp /etc/services`  
`grep -i tcp /etc/services`
`--color`this highlights the found text  
  
super useful: pipe stuff to grep: `ip addr show | grep inet` (see also: Flask  
example above)  
  
## Ch 6 Managing running processes

Process = running instance of a command, note to self: check whether this is  
the same concept as classes and their instances in Python  
  
Process ID = unique number, may be reused, associated with a particular user  
account and group account  
  
each process stores its raw information in a subdirectory of `/proc`  
  
use `cat` or `less` or `more` within `/proc` for more information

### Listing processes with ps

`ps` = list processes associated with the terminal  
  
`top` = more screen oriented and can change the status of processes  
  
`ps u` = provides more information (STAT column: R=running process,  
S=sleeping process, + = foreground operation, etc; VSZ column = virtual set size,  
RSS = resident set size which is memory in kb allocated to the process and  
used respectively, RSS cannot be swapped as it is physical memory; TIME  
column = CPU time used in seconds)  
  
`ps aux | less` = show all process of all users, not only associated with  
the terminal, also background processes  
  
`ps ux` = same as above except only processes for user running the commands  
  
`ps -eo pid,user,rss --sort=-rss | less` = `-e` running processes, `-o` show  
items specified after the command options and sort by RSS column  
Listing processes with top (VERY COOL)  
  
`top` sorts by default by CPU time currently used  
(renice means reprioritise)  
  
only root can kill processes using `top` unless `top` is used to kill a  
process owned by user running `top`  
  
information of `top` is updated every 5 seconds by default  
p. 141 for `top` options  
  
press `1` to toggle through the different CPUs, press `u` and enter  
username to display user-specific processes  
  
Killing and renicing (NI column show nice value) processes while `top` is  
running:  
take a note of the process ID and press `r` to renice, type in PID and give  
new priority from -20 to 19 (aka nice value) where negative numbers mean  
higher priority  
...or press `k` to kill a process. Then type `15` to kill cleanly or `9` to  
kill outright  

### Listing processes with System Monitor (Gnome)

By default, only running processes associated with the user are displayed.  
Menu button with "3 bars" lets you select other users' processes.  

### Managing background and foreground processes

VERY COOL - in terminal: `firefox &` means to run firefox without attaching  
it to the terminal it was run from which means to run it in the BACKGROUND.  
  
Conclusion of using the ampersand `&`: `&` results in a line in terminal  
looking like `[3] 12345` where `[job number] [PID of what's in front of &]`.  
Then the program is started outside the terminal without blocking it.  
Not using `&` would (normally) block the terminal until the program is closed.  
  
`at` let's you schedule processes (see man pages, tons of options)  
`at` is useful in principle but seems to require lots of set up work, see  
[this comment](https://stackoverflow.com/a/10468304) in Stackoverflow for more  
information. Note to self: check `man cron`. Everyone is talking about `cron`.  
  
`jobs` = show commands running in the background, +/- signs mean that the  
process has been placed to the foreground/background most recently respectively  
  
all jobs requiring terminal input cannot run in the background and are  
therefore stopped until put back to the foreground again  
  
`jobs -l` also shows the PID which can be used to further investigate the  
job with `ps`  
  
`fg %1` gets job number 1 back to the foreground; if job1 was `vim`, then it  
was "frozen" before and comes back as it was, see comment on jobs requiring  
terminal input above  
  
`fg %some_string` also works, but needs to be unambiguous  
  
`fg %?some_string` see above but the job only needs to contain the string,  
not match exactly  
  
`bg %1` for running jobs in the background  

### Killing and renicing processes

`kill` and `killall` commands, see p. 147 and man pages  
  
Actually, those commands send SIGNALS to the PID (e.g. end, pause,  
reread config files, etc...):  
  
`man 7 signal` shows all information on signals including a complete looking  
table about the signals, their number and description.  
  
Signal - number - description, see also: `man 7 signal`  
  
SIGHUP - 1 - hang-up detected, either on controlling terminal or death of  
controlling process (re-read configuration, usefull for PIDs running on a  
server when config has changed)  
  
SIGINT - 2 - interrupt from keyboard  
  
SIGQUIT - 3 - quit from keyboard  
  
SIGABRT - 6 - abort signal from abort(3)  
  
SIGKILL - 9 - kill signal (no clean kill, cannot be blocked by process)  
  
SIGTERM - 15 - termination signal (clean kill, default)  
  
SIGCONT - 19,18,25 - continue if stopped  
  
SIGSTOP - 17,19,23 - stop process (cannot be blocked by process)  
Three numbers? First one is for Alpha and Sparc CPU architectures, middle  
for x86 and PowerPC, last for MIPS.  
  
Examples:  
  
`kill 10432` (this is the default which does the same as next line)  
`kill -15 10432` = `kill SIGTERM 10432`  

`killall` uses names instead of PIDs  
`killall bash` kills all bash (CAREFUL, you may not want to kill all  
processes with the same name)  

### Setting processor priority with nice and renice (these do not apply to child processes)

nice values: -20 to 19 (already mentioned above), default is 0, the more  
negative the more priority  
  
regular users can't set a negative value and can only give lower priority,  
never higher priority  
  
`renice` for running processes, `nice` for starting processes with a given priority  
  
Examples:  
  
`nice +5 updatedb &`  
`renice -n -5 20284` -n is the same as --priority, see man pages  

### Limiting processes with cgroups aka control groups

Cgroups can be used to identify a process as a task, belonging to a  
specific control group.  
Tasks can be set up in a hierarchy. Limitations are inherited down the  
hierarchy. Limitations to be set include (see p. 150):  
  
- Storage (blkio)  
- Processor scheduling (cpu)  
- Process accounting (cpuacct, reports in CPU usage)  
- CPU assignment (cpuset)  
- Device access (devices)  
- Suspend/resume (freezer)  
- Memory usage (memory)  
- Network bandwidth (net_cls)  
- Network traffic (net_prio)  
- Name spaces (ns, a cgroup can only "see" things within the name space)  
  
`cgcreate` command: create cgroup  
  
relevant files/directories:  
`/etc/cgconfig.conf`, `/etc//etc/cgrules.conf`, `/sys/fs/cgroup`; see p. 151  
for useful guides, including:  
1. RHEL Resource Management and Linux Containers  
2. Kernel documentation on cgroups  
  
`xeyes &` is fun

## Ch 7 Writing simple shell scripts

Complex shell scripts are slower than compiled programs, consider scripting  
with Python. Options may be specified and everything after the options is  
referred to as command-line argument.  
  
To run a script (example script below):  
  
- Use filename as an argument, e.g. `bash [filename]`, stolen from  
`man bash`, "Arguments" section: `bash`assumes that [filename] above is the  
1st argument, being set to `$0` and that [filename] contains Shell commands.  
Successful comman execution or executing no command at all results in  
`exit status 0`. Bash tries to open [filename] in the $PWD. If the file is not  
there, Bash follows along the $PATH.
  
OR  
  
- Have the name of the interpreter in the first line of the script preceded  
with the shebang characters aka `#!` (e.g. `#!/bin/bash`) with the script  
being executable, using `chmod +x [filename]`  
  
- Stolen from German "shebang" wikipedia page: `#!/usr/bin/env python` would  
use the machine's local environment, i.e. $PATH to find out where Python can  
be found on the local machine. This is useful when the script is supposed to  
run on different machines with a different folder structure.  
  
Example script #1, taking user input:  
  
`#!/bin/bash`  
`read -p "Type three things: " var1 var2 var3`  
`echo "Here is what you typed: $var1 $var2 and finally $var3"`  
  
Example script #2, taking arguments and doing stuff as commented:  
  
```
#!/bin/bash  
# This is a comment: Script to echo out stuff  
echo "First argument is $1, second is $2."  
echo "The command itself is $0."  
echo "The number of parameters is $#."  
echo "All arguments given were $@."  
DATESET=$`date`  
sleep 5  
DATEREAD=$(date)  
echo $DATEREAD #5 seconds more because of sleep and the brackets  
echo $DATESET #this date and time is set when $DATESET is defined because of the backticks  
echo -e "The exit status of the last command executed was $?  
where zero means that said command was executed succesfully and  
anything other than zero means something went wrong, see bash man page.  
Newlines can be made using echo with the -e parameter and n with  
a backslash in front."  
```  
  
`echo` - place an echo with quotes at the beginning of lines within a body  
of a loop to see what's going on, no permanent changes are made that way  
  
use dummy echo statements everywhere to check whether the correct logic  
branch is being taken  
  
VERY COOL: `bash -x some_script` or "set -x" near the beginning of the  
script to display each command that is executed  
  
Comment! A lot!  

### Understanding shell variables

Variable naming convention, touching the equal sign: `NAME=value`  
  
Variables can contain the output of a command or the output of a series of  
commands, e.g. use pipe `|` <-- VERY COOL!  
  
`MYDATE=$(date)` assigns the output of the date command to the variable AT  
THE TIME WHEN THE VARIABLE IS READ  
  
In contrast:  
```
MYDATE=$`date`
```  
assigns the output of the date command to the variable AT THE TIME WHEN  
THE VARIABLE IS SET, note the backticks vs the brackets  

### Escaping special shell characters

```
$ ! ` *
```  
and probably others are special characters  
  
escape a single character with a backslash  
  
escape a string of characters with two single quotes  
  
two double quotes escape all but the special characters, except asterisks  
  
Example:
  
```
echo '$HOME *** `date`'
```  
versus   

```
echo "$HOME *** `date`"
```  
  
More examples:  

Storing the number of files in a folder to a variable:
`NUM_FILES=$(/bin/ls | wc -l)`  
  
Storing PC info to a variable:  
```
MACHINE=$`uname -n ; uname -a`
```  
  
see metacharacters for most efficient use of scripts  
  
### Preserving a variable value that may change in the future

Just assign the present value of a variable to another variable,  
e.g. `BALANCE="$CurBalance"`
  
Note how the `$` sign is used  
  
### Special shell positional parameters

`$0, $1, §2, $n` where `$0` (see remarks above) is special and these can be  
used as placeholders similar to Python's f-strings  
  
VERY COOL: `man bash` for all kinds of magic, including loops, if-statements  
and other stuff  

### Reading in parameters

see example above  
`read -p "[see above]"  
echo "[see above"  

### Parameter expansion in bash

`$VAR` is shorthand for `${VAR}`  
  
Curly braces are used when the value of the parameter needs to be placed  
next to other text without a space.  
  
Examples:  
`${VAR:-value}` --> if variable is unset or empty, expand this to value  
`${VAR:##pattern}` --> chop the longest match for pattern from the front of  
var's value  
  
VERY COOL: see p. 157-158 for REGEX like stuff  

### Performing arithmetic shell scripts

Variables are normally treated as strings (i.e. text).  
  
Use `declare` to specify another file type.  
  
Use in-built `let` to let bash know that we are dealing with numbers, see  
also: `help let`  
  
External options: `expr` (evaluate expressions) and `bc`, see man pages  
  
`let foo=$RANDOM; echo $foo`  
  
`let` doesn't like spaces between operands  
`expr`, however, does  
  
`bc` is not that picky and accepts both most of the time  
  
Set the variable `I` to zero and then echo out `$((++I)) $((I++)) $((--I)) $((I--))$((-I))`  
and see how the number is incremented or decreased  

### Using programming constructs in shell scripts

Evaluate conditional expressions with `test` VERY COOL: `help test`   
See p. 159-169 for more VERY COOL, operators on p. 161  
  
The condition can be the output of a command.  
  
`-eq` works better for numbers while `=` works better with strings  
  
Better put strings in double quotes.  
  
`!=` unequal, like Python  
  
`if [ condition ]; then`  
`elif`  
`else`  
`fi`  
  
Double pipe: `[ condition ] || action`  
  
Double ampersand: `[ condition ] && action` <-- you can combine them `||` and  
`&&` for a one-line if-then-else  
  
`dirname="/tmp/testdir"`  
  
`[ -d "$dirname" ] || mkdir "$dirname"` <-- If directory isn't there then create it.  
  
`case` condition ends in `esac`  
  
each `case` is "ended" with a double semi-colon `;;`  
  
single pipe `|` means "or" within the body  
  
weird syntax for catchall backup condition: ` *)`  
  
Example from p. 163:  
  
```  
case `date +%a` in # when the date output has...  
    "Mon") # ..."Mon" in it...  
        BACKUP=/home/myproject/data0 # ...then backup this...  
        TAPE=/dev/rft0 # ...using this (tape?) device.  
        ;; # First case is ended with two semi-colons  
    "Tue" | "Thu") # second case uses the OR operator |  
        BACKUP=/home/myproject/data1 # Different date...  
        TAPE=/dev/rft1 # ...different (tape?) device.  
        ;;  
    *) # catchall placeholder since backups are only made Mon and Tue  
        BACKUP="none" # The string "none"...  
        TAPE=/dev/null # ...is sent to Linux Nirvana  
        ;;  
esac # ends the case command, "esac" is reversed "case"   
```  
  
for...do loop example:  
  
```
for N in 0 1 2 3  
do  
echo The number is $N  
done  
```
  
Another example:  
```
for FILE in `/bin/ls` #that's the location of the ls command which creates a list of the $PWD  
do  
echo $FILE  
done  
```
  
You can use C syntax as well...which I should learn first before attempting this.  
  
while...do loop example:  
  
```
N=0  # below, note the space after and before the brackets  
while [ $ N -lt 10 ] ; do # -lt = less than, check table on p. 161  
    echo -n $N # no trailing newline using -n  
    let N=$N+1 # note the use of in-built let command, see also "help let" in bash  
done  
```  
  
until...do loop example, same output as above:  
  
```
N=0  
until [ $ N -eq 10 ] ; do # -eq = equal operator, see p. 161  
    echo -n $N  
    let N=$N+1  
done  
```  

### Trying some useful text manipulation programs

`grep`, `cut`, `tr`, `awk` and `sed`  
  
grep = General RegEx Parser  
sed = Stream EDitor  
  
`env | grep ^HO` which env variables start with HO?  
  
`grep /home /etc/passwd | cut -d':' -f6 -` 6th field, delimiter is a colon `:`  
and the hyphen `-` tells `cut` to read from STDIN (from the pipe)  
  
tr =  "translate" or rather search&replace, see man pages  
  
`tr` example:  
    
```
FOO="MiXeD"  
echo $FOO | tr [A-Z] [a-z]  
```  
  
`tr [:blank:] [_]` #replace blanks with underscores  
  
For `sed`, check online documentation. It can remove lines which contain a  
certain pattern), also: weird syntax alert.  
  
`sed` example: `cat somefile.txt | sed 's/Mac/Linux/g' > fixed_file.txt`  

### Using simple shell scripts - phone list example

```
#!/bin/bash  
# (@)/ph  
# A very simple telephone list  
# Type "ph new name number" to add to the list, or  
# just type "ph name" to get a phone number  
  
PHONELIST=~/.phonelist.txt  
  
# If no command line parameters ($#), there  
# is a problem, so ask what they're talking about.  
if [ $# -lt 1 ] ; then  
        echo "Whose phone number did you want? "  
         exit 1  
fi  
  
# Did you want to add a new phone number?  
if [ $1 = "new" ] ; then  
        shift  
	echo $* >> $PHONELIST  
        echo $* >> added to database  
        exit 0  
fi  
  
# Nope. But does the file have anything in it yet?  
# This might be our first time using it, after all.  
if [ ! -s $PHONELIST] ; then  
        echo "No names in the phone list yet! "  
        exit 1  
else  
    	grep -i -q "$*" $PHONELIST      # Quietly search the file  
        if [ $? -ne 0 ] ; then          # Did we find anything?  
         echo "Sorry, that name was not found in the phone list"  
         exit 1  
        else  
         grep -i "$*" $PHONELIST  
        fi  
fi  
exit 0  
```  
  
see also: info bash  
  
Backup script example:  
```
#!/bin/bash  
# (@)/my_backup  
# A simple backup script  
#  
  
# Change the TAPE device to match your system.  
# Check /var/log/messages to determine your tape device.  
# You may also need to add scsi-type support to your kernel.  
# Not sure if I really need to do this nowadays?  
TAPE=/dev/rft0  
  
# Rewind the tape device $TAPE  
mt $TAPE rew  
' Get a list of home directories  
HOMES=`grep /home /etc/passwd | cut -f6 -d':'` # see previous examples for stuff after the pipe  
# Back up the data in those directories  
tar cvf $TAPE $HOMES  
# Rewind and eject the tape.  
mt $TAPE rewoffl  
```

#### My own first script - Ubuntu Linux update script

Script:  
```
#!/bin/bash
# This script does update Ubuntu and finish up with autoremove

sudo apt-get --assume-yes update # could also be -y or --yes, see man pages  
sudo apt-get -y upgrade  
sudo apt-get -y dist-upgrade  
sudo apt-get -y autoremove  
echo "/nI did sudo apt-get update, upgrade, dist-upgrade and autoremove for you"  
```  
  
Save that in a file, copy that file to `~/.local/bin` since this is already in  
the $PATH. Then give change permissions in order to execute. Lazy solution:  
`sudo chmod --reference=[old_script_with_correct_permissions]  [new_script_that_needs_permissions_changed`  



## Ch 8 Becoming a Linux System Administrator

Most fedora and RHEL graphical config tools start with `system-config-`, for example:  
`system-config-network`  
  
The following seems to be fedora / RHEL only:  
- `system-config-bind` configure a Domain Name System
- `system-config-httpd` computer as Apache server
- `system-config-nfs` share folder using NFS
- `system-config-rootpassword` does what is says
- `system-config-samba` Windows (SMB) file sharing
- `system-config-services` configure which services are running at different runlevels
- `authconfig-gtk` how are users authenticated on the system?
- `system-config-date` obvious
- `system-config-firewall` obvious
- `system-config-language` obvious
- `system-config-printer` obvious
- `policycoreutils-gui` Set SELinux enforcing modes and default policy
- `system-config-users` obvious
- `gconf-editor` edit GNOME configuration database, also for Ubuntu
- `gnome-utils` display info about hard disks and removable storage
- `gnome-disks` partitions and filesystems
- `system-config-kickstart` install multiple Linux systems without user  
interaction, also for Ubuntu, VERY COOL
  
#### Brower-based tools

- [OpenStack](https://www.openstack.org/)
- Red Hat Enterprise Virtualization

### Using the root user account

root user's home folder: `/root`  
The /etc/passwd file contains information about root's home directory and other  
information associated with root  

`cat /etc/passwd` shows the following for root:  
`root:x:0:0:root:/root:/bin/bash` where  
user:?:user set to 0: group set to 0:?:home directory of user:shell for user  
Note to self: investigate question marks above.  
You can change `/etc/passwd` but `usermod` command is a better choice for  
doing this, see Ch 11 and man pages  
  
Ubuntu does not have a root password set, forcing you to use `sudo` every time.  
  
`su` itself does not read in the root user's environment. To achieve this, use  
`su -`, this way, for instance, `cd ~` leads to the root user's home, not the  
user's home who needs root privileges. Note to self: test your assumption when  
on a fedora system  
  
`su - otheruser` become otheruser  
  
`exit` = `CTRL+D` = return to non-root shell  

### Gaining administrative access with sudo

check `man sudoers`  
  
Simply add a user to `/etc/sudoers` and define what privilege the user should  
get. Ubuntu: "This file MUST be edited with the `visudo` command as root".  
  
Therefore, use `visudo`, see also man pages of `vipw` and `vigr`  
  
Note: `visudo` will open the default text editor as defined in the $EDITOR  
variable. For some reason, this variable is not defined in Ubuntu but the  
default editor is `nano`. Note to self: check on fedora system with  
`printenv | grep EDITOR` and `printenv | grep VISUAL`  

## Exploring adminstrative commands, configuration files, and log files


