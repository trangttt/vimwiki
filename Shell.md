#SHELL

## Comparisions
Comparisions in bash

1. Arithmetic tests:
   `-eq` `-ne` `-lt` `-gt` `-le` `-ge`

2. String tests
   - `-z` is String zero
   - `-n` is String null
   - `=` equals
   - `==` equals
   - `!=` not equals
   - `<`  lexicographically less than
   - `>`  lexicographically larger than

3. File checking
   - `-e` exits
   - `-f` normal file
   - `-S` Socket
   - `-d` directory
   - `-L` symbolic link
   - `-h` symbolic link
   - `-g` sgid set # Allow file has the group permission when executed. chmod 2xxx <file>
   - `-u` suid set # Allow file has the user permission when executed. chmod 4xxx <file>
   - `-r` readable
   - `-x` executable
   - `-w` writable
   - `-s` size bigger than 0 ( not empty file )
   - `<FILE1> -nt <FILE2>` newer than
   - `<FILE1> -ot <FILE2>` older than
   - `<FILE1> -ef <FILE2>` refer to the same device and inode number


## Parameters expansion

- Simple usage

   - `$PARAM`
   - `${PARAM}`
 
- Indirection 

   - `${!PARAM}` : value reference by the variable referenced by PARAM

- Case modification
   - `${PARAM^}`: uppercase first character
   - `${PARAM,}`: lowercase first character
   - `${PARAM^^}`: uppercase all character
   - `${PARAM,,}`: lowercase all character
   - `${PARAM~}`: reverse case first character
   - `${PARAM~~}`: revercase all character

- Variable name expansion
   - `${!PREFIX@}`
   - `${!PREFIX*}`

- Substring removal (also for filename manipulation!)
   - `${PARAM#PATTERN}`: remove prefix matching pattern
   - `${PARAM##PATTERN}`: removing all prefix matching pattern.
   - `${PARAM%PATTERN}`
   - `${PARAM%%PATTERN}`

- Search and replace
   - `${PARAM/PATTERN/REPLACE}`
   - `${PARAM//PATTERN/REPLACE}`
   - `${PARAM/PATTERN}`
   - `${PARAM//PATTERN}`
   - `${PARAM/#PATTERN/REPLACE}`
   - `${PARAM/%PATTERN/REPLACE}`

- String length
   - `${#PARAM}`

- Substring expansion
   - `${PARAM:OFFSET}`
   - `${PARAM:OFFSET:LENGTH}`
   - Negative offset
   - Negative length
   - Array
   - 
- Use a default value
   - `${PARAM:-DEFAULT}`
   - `${PARAM-DEFAULT}`
   - Array
- Assign a default value
   - `${PARAM:=DEFAULT}`
   - `${PARAM=DEFAULT}`
- Use an alternate value
   - `${PARAM:+REPLACE}`
   - `${PARAM+REPLACE}`
- Display error if null or unset
   - `${PARAM:?ERROR}`
   - `${PARAM?ERROR}`

## Arithmetic 
$[ ]
$(( ))

## Color 

* Escape sequence \e[  \x1B
 
 
## Sticky bit 

rwxrwxrw[t] file mode, letter 't' at the end.
chmod o+t <file>
chmod 1755 <file>
Ensure only the owner of the files are allowed to delete such files.

## Idioms

`filename=$(basename $path)`
`ext=${filename#*.}` Get all extension .tar.gz
`ext=${filename##*.}` Get one extension .zip 
`dir=${path%/*}` Get directory path
`fn=${filename%.*}` Get filename only
    
    
`file -s /dev/xxx` checking filesystem type of device
`strings /dev/sdc | less`

## xargs

-0
-p : prompt
-n <number> : number of args
-L <number>: fetching number of line into one
-I  {} : argument replacement
-J

## sed
`sed '1!G;h;$!d' <file>` : reverse a file


## awk
## Good to remember commands
1. `nl`: line numbering
    `nl -w1 -s". "`: line numbering with width=1, suffix=". "
2. 
3. 
4. 

