# General

|/|The "anchor"of the filesystem (root)|
|/usr|The Unix System Resource, contains all the system files|
|/usr/bin|Executable files for programs installed on the computer|
|/usr/lib|Shared libraries for use by programs on the computer|
|/etc|System configuration|
|/var|Logs, caches, etc.|
|/home|User-owned data|
|proc|Runtime process data|
|/tmp|Temporary data storage|

Symbolic Files — File that references another file

Command — ln -s “destination file” “pointer file”
Moving this file when given a relative path, an error will be thrown — Use Absolute path.
Hard Links — Perfect link to the original file

Command — ln “destination file” “pointer file”
Changes in the original file made after hard linking will not be reflected in the linked file
Pipes

| — unidirectional
mkfifo — First come first output

<in_file: redirect in_file into the command's input

> out_file: redirect the commands output into out_file
> 2>error_file: redirect the command's errors into error_file
