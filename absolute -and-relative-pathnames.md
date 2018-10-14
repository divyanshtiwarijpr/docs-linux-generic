## *ABSOLUTE PATHS* AND *RELATIVE PATHS*

1. All files on Linux system are stored on filesystems which is organized into a single **inverted tree** of directories known as **file system hierarchy**. This tree is inverted because the root of the tree is said to be at top of the hierarchy and the branches of the tree stretch below the root.
    
    The directory `/` is the root directory at the **top** of the filesystem hierarchy. 

    The `/` character is **also** used as a **directory separator** in file names.

    The whole filesystem hierarchy is **standardized**.

- **Absolute paths**: An absolute path is a fully qualified location of a file beginning from the root directory (`/`) to the exact file. Every file in a filesystem has a unique absolute path name.

    Any path with a forward slash (`/`) as the first character is always an absolute path name.

    Theren are 2 additional absolute paths that exists in every directory in linux:

    1. `~` - Your home directory.
    2. `~USERNAME` - Home directory of user USERNAME.


- **Relative paths**: A relative path identifies a unique file but it specifies only the path necessary to reach the file from the current working directory.

    Any path starting with any character other than forward slash (`/`) is a relative path name.
 
    Theren are 2 additional relative paths that exists in every directory in linux: 

    1. `.` - Current directory.
    2. `..` - Previous directory.



- Paths beginning with a `.` character are hidden files and directories meant to store configuration files.



- The path name of a file has basic rules:

    1. The path name of a file including all `/` characters must not be more than **4095** bytes long.

    2. Each component of the path name separated by `/` characters must not be more than **255** bytes long. 

    3. Files can use any **UTF-8** encoded Unicode character except `/` and `NUL` character. 

    4. No character will take more than **four bytes**.



- **References**

`man 7 hier`

`man 7 file-hierarchy`
   
