wksp
====

A simple bash script to help manage development workspaces.

I switch between projects very often at work--sometimes multiple times a day. I made wksp to help me quickly set up
everything I use for working on different projects: tailing logs, new editor instances, different configuration,
starting local servers, etc.

## Install
* Copy `wksp` somewhere included in your PATH. I have mine in `$HOME/bin`.
* If you want argument completion enabled, source `wksp-completion.sh`, e.g., in `.bash_profile`.

## Configuration Directory
By default wksp looks for workspace configurations in `$HOME/.wksp.d`. You can change where it looks by setting the
`WKSP_DIR` environment variable to another location. Any files in the directory that end with `.wksp` will be
considered workspace configurations.

For example, running `$ wksp example_project`
will look for the file `$WKSP_DIR/example_project.wksp`.

## Workspace files
The workspace files, `$WKSP_DIR/*.wksp`, are plain bash script files that wksp sources when starting the workspace.

## Example
```bash
$ ls -1 .wksp.d/
example_project.vim
example_project.wksp

$ cat .wksp.d/example_project.wksp 
#!/bin/bash
if [ ! -d "$HOME/Projects/example_project" ]; then
	echo "Can't find project."
	return 1
fi
cd "$HOME/Projects/example_project"
# Start up local server
service apache2 start
# New terminal
gnome-terminal
# Open gvim and run project config file
gvim -S "$WKSP_DIR/example_project.vim"
# Keep an eye on the log
tail -f "$HOME/Projects/logs/example_project/error.log"

$ cat .wksp.d/example_project.vim
" No tabs
set tabstop=2 softtabstop=2 shiftwidth=2 expandtab
```
