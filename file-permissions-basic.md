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

    1. `r` - **read** 

        Numeric value: **4**
    
        **Effect on files**: Contents of the files can be read.
 
        **Effect on directories**: Contents of the directory (filenames) can just be listed.

        This permission enables the querying of just filenames without inode locations from filesystem metadata and thus if only this permission is granted files cannot be accessed as access requires the querying of inode locations from filesystem metadata allowed by granting execute permission.


    2. `w` - **write**

        Numeric value: **2**

        **Effect on files**: Contents of the files can be changed.
 
        **Effect on directories**: Files in the directory may be created or deleted.

        If only this permission is granted without execute permission on directories then it is useless as for modification of directory contents access to inodes is necessary that is only available by granting execute permission.


    3. `x` - **execute**

        Numeric value: **1**
        
        **Effect on files**: Files can be executed as commands.
 
        **Effect on directories**: Contents of the directory (filenames) can be accessed if the file permissions allow it. Other details like permissions, time stamps etc. can be queried. 

        If only this permission is granted then the user cannot list the files contained in the directory but can access a file if the user knows the filename and also has permissions to read it.

        This permission enables the querying of inode locations from filesystem metadata and that is how it enables access.

    These permissions **affect files and directories differently** for which refer to the file `file-permissions-basic-table.docx` in this repository which covers the effect of these peermissions on files and directories in detail.

    So for **three categories of users** there are above **three file permissions** so in total there are **nine** permission bits for either file or directory for all the three categories of users: `rwxrwxrwx`.

    From the above three categories of user permmissions the most specific permissions apply so **user** permissions override **group** permissions which override **other** permissions.

    
- Format of defining and understanding permissions:

    1. When **three** digits are used to get or set permissions they refer to the three types of permissions to three types of users generally known as basic permissions.

    2. When **four** digits are provided to get or set file permissions, the **first** digit refers to **special permissions** and the remaining three digits refer to basic permissions as describes above. For more details on special permissions refer to file `file-permissions-special-table`in the same repository.

    3. In most of the commands like `chmod`, `umask` et. if the four values are not defined in octal mode and only one or two or three digits are provided to the command then the missing values are **assumed to be preceding zeros**.


- Things that should be kept in mind when calculating effective access in Linux.

    1. Linux permissions apply only to file or directory that they are set on. Permissions on a directory are **not inherited automatically** by subdirectories and files within it. 
    
        This type of inheritance is commonly found in NTFS filesystem in which permissions are inherited to subdirectories and files within parent directory.

    2. The permissions on a directory can however block access to subdirectories and files within it so while calculating permissions for a file or directory first check that the user has **appropriate permissions on parent directory**. 

        
    3. Only the **root** user or **owner** has the right to change the **permissions** of files or directories.
    
    4. Only **root** user has the power to change the **owner and group** permissions of both files and directories.
    
    5. Start by calculating access on the uppermost directory and follow the whole path to the target file covering every subdirectory checking that the file or subdirectory permissions must also be correct for proper access.

    6. Remember that permissions set on directories behave differently that permissions set on files.

    7. Always keep in mind that the files themselves are actually the content of the directories and the data present in files forms content of those particular files.

    8. Always remember as the parent directory permissions are not automatically inherited by subdirectories, to modify a directory recursively a user must have write permission on all the subdirectories in the parent directory. 
        
        In this situation any modification of files such as deletion or bulk renaming is not effecive over files conatined in subdirectories without write permission allowing the user that wants to operate in such a way and such an operation will result in partial completion due to wrong permissions on subdirectories. 

        It must be kept in mind that this error is due to wrong permissions on subdirectories not files as files only control their data not modification of the files themselves which is controlled by write and execute permissions on parent directory.