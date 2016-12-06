## Comparisions

    * Arithmetic tests
    
        . `-eq`
        . `-ne`
        . `-lt`
        . `-gt`
        . `-le`
        . `-ge`
        
    * String tests
    
        . `-z`
        . `-n`
        . `=`
        . `==`
        . `!=`
        . `<` 
        . `>` 
        
    * File checking
    
        . `-e` exits
        . `-f` normal file
        . `-S` Socket
        . `-d` directory
        . `-L` symbolic link
        . `-h` symbolic link
        . `-g` sgid set # Allow file has the group permission when executed. chmod 2755 <file>
        . `-u` suid set # Allow file has the user permission when executed. chmod 4755 <file>
        . `-r` readable
        . `-x` executable
        . `-w` writable
        . `-s` size bigger than 0 ( not empty file )
        . `<FILE1> -nt <FILE2>` newer than
        . `<FILE1> -ot <FILE2>` older than
        . `<FILE1> -ef <FILE2>` refer to the same device and inode number
        
## Parameters expansion         

    - Simple usage
    
        `$PARAM`
        `${PARAM}`
    - 
    - Indirection 
    
        `${!PARAM}` 
        
    - Case modification
    
        `${PARAM^}`
        `${PARAM,}`
        `${PARAM^^}`
        `${PARAM,,}`
        `${PARAM~}`
        `${PARAM~~}`
        
	- Variable name expansion
        `${!PREFIX@}`
        `${!PREFIX*}`
        
	- Substring removal (also for filename manipulation!)
        `${PARAM#PATTERN}`
        `${PARAM##PATTERN}`
        `${PARAM%PATTERN}`
        `${PARAM%%PATTERN}`
       
	- Search and replace
	- String length
	- Substring expansion
	- Use a default value
	- Assign a default value
	- Use an alternate value
	- Display error if null or unset
	 
##  Color 
    * Escape sequence \e[  \x1B
    * 
## Sticky bit 
    drwxrwxrw[t] file mode, letter 't' at the end.
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
