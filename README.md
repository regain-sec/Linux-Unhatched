# Linux-Unhatched
Documenting my journey to understand Linux.

A concise record of key commands and concepts from NDG Linux Essential course. 
Useful for quick review and practice. 

**Module 1**
Linux = Kernel + Tools + Shell

Distros = Ubuntu, CentOS/RHEL, Fedora/Debian etc. 

'uname -a' --> system info

'lsb_release -a' --> distribution info

--------

**Module 2**
'/' = root directory

  paths
  
    Absolute -> starts from /
  
    Relative -> starts from location

"Commands"

  'pwd' = current directory
  
  '..' = one directory above the current directory
  
  '.' = current directory
  
  '~' = home directory
  
  'ls -l' = list with details

  **Administrative Access**
  
  'su' = let the user act temporarily as a different user by creating a new shell. If a shell is not specified, it act as a root user. 
  
    "Commands"
      su -
    
      su -l
      
      su --
      
      su -- login
  
  sl is a command that can only be executed with administrative access.
    
    'sudo' = This command helps a user to execute a command as another user without creating a new shell. Just type sudo followed by the command (as an argument). 
  
  If there is a need to switch to another account, use '-u' as an option. 
  
     sl command is usually already installed in Linux. If it is not installed, install by using the following commands:
     
       sudo apt install sl (used on Debian/Ubuntu based systems [uses the APT package manager])
       
       sudo yum install sl (used on Red Hat/CentOS/Fedora-based systems [used YUM package manager])

**Permissions**

'ls -l' = To check files of a directory with permissions 

The first set is about the owner's permission

The second set is about the group

The third set is about others

A user may have less permission then group and everyone else. 

  e.g. -r--rw-rwx systemadmin staff
  
    The user **systemadmin** can only read the file
    
    The group **staff** (group that owns the file) can read and write. 
    
    Everyone else can read, write, and execute. 
    
    It doesn't matter if the user is a member of the owner group; once the permissions have been established, only user's permission are applied. 

**Changing the File Permissions**

'chmod' is used to change a file's permission. chmod = change of _mode of access_

  Tpyes:
  
    symbolic
    
    octal
  
  Command:
  
    chmod [<SET><ACTION><PERMISSIONS>] File
    
    "Set"
    
      u = user owner
      
      g = group owner
      
      o = others
      
      a = all
    
    "Action"
    
      + = add
      
      = = specify the exact permission
      
      - = remove
    
    "Permissions"
    
      
      r = read
      
      w = write
      
      x = execute
      
          e.g.: -rw-r--r-- 1 sysadmin sysadmin 647 Dec 20  2017 hello.sh   
          
          **chmod u+x hello.sh**
          
          check by executing:
          
            ./hello.sh (./ means to execute the file from the current directory)

**Changing File Ownership**

'chown' is used to change the ownership of a file. 

  the first argument is [OWNER TO BE]
  
  the second argument is [FILE]
  
    e.g. chown root hello.sh
    
      NOTE: to change the ownership of a file or even transfer the ownership, requires **administrative acess**. Therefore, use sudo before the command. 
      
        **sudo chown root hello.sh**

**Viewing Files**

'cat' (short form for concatenate) is used to view the content of a small file. This command is used to view content of a file in which scrolling is not required. 

  "The Syntax"
   
    cat [FILE]
    
      to view larger files, a different command is used that will be discussed later. 

'head' and 'tail' commands are used to view the begining and the end (10 lines each) of a file. 

  "The Syntax"
  
     head [FILE]
    
     tail [FILE]
     
       -n argumnet is used to mention  the exact number of lines you want to view. 
       
         "The Syntax"
         
            head -n [NUMBER OF LINES] [FILE]
            
              e.g: head -n 5 alpha.txt

**Copying Files**

'cp' is a command used to copy a file. 

  Syntax

    cp [OPTIONS] [DESTINATION FILE]

      e.g. cp /etc/passwd

  **'mv'** works on a similar pattern

  'dd' is a command used to copy files or entire partitions at the bit level.

  This command has several useful features, including:

      It can be used to clone or delete (wipe) entire disks or partitions.
      
      It can be used to copy raw data to removable devices, such as USB drives and CDROMs.
      
      It can backup and restore the MBR (Master Boot Record).
      
      It can be used to create a file of a specific size that is filled with binary zeros, which can then be used as a swap file (virtual memory).

          dd if=/dev/zero of=/tmp/swapex bs=1M count=50

            if= from where the file needs to be read

            of= to where the file needs to be written

            bs= block size the block size to be used; K, M, G

            count= the number of blocks to be read from the input file

            Note: No need to use the block size or count while copying over entire devices, eg, to clone from one hard drive to another. 

  It is **recommended** to use absoulte path while using dd as it handles the raw data and can delte an entire partition or even hard disk. 

  **Moving Files**

    'mv' command is used to move a file from one directory to another. 

      Syntax

        mv [FILE NAME] [DESTINATION]

          e.g. mv people.csv Work

        'mv' can also be used to rename a file witout changing its location.

        mv [ORIGINAL FILE NAME] [NEW FILE NAME]

        e.g. mv animals.txt zoo.txt
        
  Both write and execute permissions are required to run mv commmand on both ends. 

  
