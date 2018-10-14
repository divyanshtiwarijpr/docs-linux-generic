## BASIC FILE PERMISSIONS IN LINUX

1. In every filesystem access to files and directories is controlled by **file permissions** and **access control lists**.

    Every filesystem can have its own **permissions model** that dictates how files will be accessed by any user or process. 



- The Linux file permissions model is **simple but flexible** and is **POSIX compliant** so we know that it is same for every **POSIX compliant filesystem**.



- There are **two types of file permissions** in Linux:

    1. Basic file permissions.
    2. Special file permissions.
    


- **Categories of users** or **types of ownership** to which file permissions apply:
   
    1. Owner - Generally the user who created the file. This can be changed later.
    
    2. Group - Generally the primary group of the user who created the file. This can be changed later.
    
    3. Other - All other users on the system that are not the owner or member of the owning group.

       

 
- **Basic file permissions**:

    1. `r` - read 

        Numeric value: **4**
    
        Effect on files: Contents of the files can be read.
 
        Effect on directories: Contents of the directory (filenames) can be listed. If only this permission is granted files cannot be accessed.


    2. `w` - write

        Numeric value: **2**

        Effect on files: Contents of the files can be changed.
 
        Effect on directories: Any file in the directory may be created or deleted.


    3. `x` - execute

        Numeric value: **1**
        
        Effect on files: Files can be executed as commands.
 
        Effect on directories: Contents of the directory (filenames) can be accessed if the file permissions allow it. Other details like permissions, time stamps etc. can be queried. If only this permission is granted then the user cannot list the files contained in the directory but can access a file if the user knows the filename and also has permissions to read it.

    These permissions **affect files and directories differently** for which refer to the file `file-permissions-basic-table.docx` in this repository which covers the effect of these peermissions on files and directories in detail.

    So for **three categories of users** there are above **three file permissions** so in total there are **nine** permission bits for either file or directory for all the three categories of users: `rwxrwxrwx`.

    From the above three categories of user permmissions the most specific permissions apply so **user** permissions override **group** permissions which override **other** permissions.

    
- Format of defining and understanding permissions:

    1. When **three** digits are used to get or set permissions they refer to the three types of permissions to three types of users geerally known as basic permissions.

    2. When **four** digits are provided to get or set file permissions, the **first** digit refers to **special permissions** and the remaining three digits refer to basic permissions as describes above. For more details on special permissions refer to file `file-permissions-special-table`in the same repository.


- Rules that must be followed when calculating effective access in Linux.

    1. Linux permissions apply only to file or directory that they are set on. Permissions on a directory are **not inherited automatically** by subdirectories and files within it. 
    
        This type of inheritance is commonly found in NTFS filesystem in which permissions are inherited to subdirectories and files within parent directory.

    2. The permissions on a directory can however block access to subdirectories and files within it so while calculating permissions for a file or directory first check that the user has **appropriate permissions on parent directory**. 

        
    3. Only the **owner** has the right to **change the permissions** of files or directories.
    
    4. Only **root** user has the power to change the **owner and group** owner permissions of both files and directories.

