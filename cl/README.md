# Configuring your terminal
On OSX, open Terminal. Click on "Terminal" at the top right, then "Preferences...". Configure dimensions, font, colours etc..

## Navigating

Print current working directory
`pwd`

List files (including directories)
`ls`

List files including hidden files
`ls -a`

Detailed file listing
`ls -alFh`

Change directories
`cd /absolute/path/I/want/to/go/to`
`cd relative/path/to/file`
`cd ../../another/relative/path`
`cd ~/relative/to/home/dir`

Go up to parent directory
`cd ..`

Go to my home directory (e.g. /Users/matthewh)
`cd`

Change directories pushing onto stack
`pushd /path/I/want/to/go/to`

Go back, popping from stack
`popd`

Beginning of line (bash)
`Ctrl + a`

End of line (bash)
`Ctrl + e `

Delete single word (bash)
`Ctrl + w`

## Making files and directories

Make a directory
`mkdir name_of_my_directory`

Make a file
`touch name_of_my_file`

Or you can just open it with your text editor and then when you save it it will be created:
`vim name_of_my_file`

## Moving and renaming files and directories

Renaming a file
`mv old_name new_name`

This will clobber any file called new_name if it already exists. You can be warned if you like, using the `-i` option:
`mv -i old_name new_name`

"Renaming" is really just a special case of moving:
`mv file_name the/directory/where/I/want/it/to/go/`

Again, use `-i` if you want to be warned before clobbering a file in the new location.

## Deleting files

`rm the_file_I_want_to_delete`

This is permanent. It doesn't merely chuck the file in the trash.

To get an "Are you sure?" message before proceeding, using `-i`:
`rm i the_file_I_want_to_delete`

To delete an empty directory:
`rmdir the_directory_I_want_to_delete`

To permanently delete a directory and everything in it:
`rm -r the_directory`

Depending on permissions, you might receive prompts when you try to delete things. These can get repetitive. To recursively delete a directory (or file) and all it contains, without receiving any prompts, do:
`rm -rf the_directory`

Use with caution – it's permanent.

## Finding files

Search for a file recursively within current directory:
`find . -name exact_name_of_file`
`find . -name '*part_name_of_file*'`

Remember quotes when "globbing"!

Search within some other directory:
`find /some/other/directory -name name_of_file`

## Viewing files

See the top few lines of a file
`head some_file`

See the last few lines of a file
`tail some_file`

See the last few lines and keep updating it as more lines are added (good few live-viewing log files and such)
`tail -f some_file`

See the top 30 lines of a file
`head -30 some_file`

See the last 30 lines of a file
`tail -30 some_file`

Output the entire file contents to console
`cat some_file`

View a large file bit by bit
`less some_file`
Edit a file (wink)
`vim some_file`

## Inspecting processes

List running processes:
`ps aux`

Search for processes containing a given string:
`ps aux | grep the_string`

This will give you a list of processed with "pids" (process IDs). You can kill a process by passing its pid to `kill`:
`kill 12345`

This generally causes the process to be shut down cleanly. Sometimes process refuse to die. You can then resort to an "unclean kill" with `-9`. Try not to do this unless you really have to:
`kill -9 12345`

Monitor running processes (press q to quit)
`top `

## Searching previous commands

Searching previous commands used (bash)
`Ctrl + r `

Start typing for search, Ctrl + Shift + r for reversing

You can also use up and down arrows to view previous commands. Or look in ~/.bash_history, ~/.zsh_history.

Remember tab key for autocompletion (better in zsh (wink) ).

## Some handy substitutions:

Refer to previous command:
`!!`

E.g. to run the last command with `sudo`:
`sudo !!`

To grab the last argument passed to the last command:
`!$`

This too can be substituted into another command, and can be quite handy. zsh usefully autocompletes these aliases on tab.

## Filtering/Redirection

Redirecting with Pipe  and Grep - |
`rake routes | grep account`
// Shows routes with the word account in the output

You can search for regular expressions. `egrep` is often more convenient here as it allows more regex syntax. This will search case-insensitively for "account" or "job":
`rake routes | egrep -i 'account|job'`

## Executable files

Let's say you've written a Ruby script, which lives at ~/scratch.rb. Say that contents are
puts "Hello, world!"

If I'm in the my directory,I could execute this with:
ruby scratch.rb

But I may want to execute this file directly without having to user the `ruby` command. To do this I would have to do a couple of things:
Tell the shell how to interpret the script. Do this by putting the line `#!/usr/bin/env ruby` at the top of the file.
Make the file executable: `chmod +x scratch.rb`.
Execute the file by providing a path to it: `./scratch.rb`. (Just typing the file name won't work.)
Getting help with command line programs
Many command-line programs have a quick `--help` option that outputs a small chunk of info on basic usage.
E.g.
`ack --help`
For in-depth help, command-line programs will usually have a "man page" as well, e.g.:
`man ack`

## Aliases and shell configuration

You might find yourself running the same commands again and again. To save time, you can create a an alias:
`alias blob="echo hello"`
`blob`
hello

This will only last for your current shell session though. To make it permanent, put it in ~/.bashrc (or ~/.zshrc if you're using ~/.zsh). You can also put other commands in ~/.bashrc that you want to be run every time you start up the shell.

To see a list of all your current aliases, type `alias`.

It's advisable not to use existing commands as aliases for something else. For example, you might be tempted to alias `rm` as `rm -i` as a "safety measure".

The danger here occurs when you're on another machine without those aliases, and unconsciously assume that they're still in place. 

Instead, give your aliases a novel name, e.g. `alias del="rm -i"`.

## Handy command line utilities

These may or may not be installed on your machine already. If they aren't, you can probably use brew to install them.

brew to install stuff is a must on OSX.

egrep is like grep but a bit better.

ack is like grep but designed to make it easy to search source code.

tmux is a terminal multiplexer, as is screen . One physical terminal can be split between multiple shells / processes etc.. It also lets you quickly split the terminal window into multiple panes etc..

tmuxinator is a configuration/automation tool for tmux which can be useful for quickly starting up a project with preconfigured windows and panes, along with any processes (e.g. `rails s`) you need to be running for development.

z is really useful for jumping around between your favourite directories without having to remember / type their exact paths.

