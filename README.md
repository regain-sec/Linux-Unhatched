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
      
      su --login
  
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
  
    The user 'systemadmin' can only read the file
    
    The group staff (group that owns the file) can read and write. 
    
    Everyone else can read, write, and execute. 
    
    It doesn't matter if the user is a member of the owner group; once the permissions have been established, only user's permission are           applied. 

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

  Syntax: chown [OWNER TO BE] [FILE]
  
    e.g. chown root hello.sh
    
      NOTE: to change the ownership of a file or even transfer the ownership, requires **administrative acess**. Therefore, use sudo 
      the command. 
      
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

**Removing Files**

  'rm' command is used to delete files and directories.

    It is important to note that unlilke in windows based OS, deleted files do not go to a trash can and are almost always deleted
    permenantly. 

      Syntax:

        rm [FILE]

          e.g. rm linux.txt

          NOTE: Remember, the above syntax can only remove regular "files" and not directories. 

    To remove directories, use '-r' or '-R'. However, it is important to be very careful while doing it as this command will delete directory along with its subdirectories and files. 

      e.g. rm -r School


  NOTE: It is important to note that permissions have an impact on these commands. e.g., to delete a file within a directory, a user should have w permission on the directory. Typically, regular users have these persmissions for their home directories and their sub directories. 

**Filtering Input**

  'grep' is used to filter content in a file. 

    Syntax: 
    
      grep [OPTIONS] PATTERN [FILE]

        e.g. grep sysadmin passwd

      Options are used to further fine tune the search. 

        e.g. grep -c sysadmin passwd (where -c shows how many lines match)

          Other options include: -i (ignore case-sensitivity), -r -R (search recursively in directories), -n (show line number with matches), -v (invert match - show lines that do not match with the Pattern), -o (show only the matched part), -c (the number of lines matched), -E (use extended regex - more powerful pattern rules). 

            BASIC REGEX CHARACTERS (Default for grep)
    
              .	Matches any one single character	gr.p matches: grap, grip, grup
              [ ]	Matches any one character from the set	gr[aeiou]p matches: grap, grep, etc.
              [^ ]	Matches anything except characters listed	gr[^a]p matches grip but not grap
              *	Matches zero or more of the previous character	go*gle matches: ggle, gogle, goooooogle
              ^	Anchors match to start of line	^error matches only when a line starts with "error"
              $	Anchors match to end of line	done$ matches only when a line ends with "done"

**Shutting Down**
  'shutdown' is a command to safely shut the system down. To run this command, administrative rights are required. Therefore, you may have to use su -, su --, su -l, su --login command to shutdown the system. 

    Syntax:

      shutdown [OPTIONS] TIME [MESSAGE]

      Unlike other commands to bring the system down, shutdown command needs a specific time that could be "NOW", "hh:mm" or "+minutes". 

        e.g.: shutdown NOW
              
              OR

              shutdown +5

              OR

              shutdown 01:22

      The time zone your Linux is set could be different from your timezone, therefore, use "date" command to know the time on the Linux (it is displayed as UTC). 

      You can also add a message to the syntax that will appear on the screen to the users before system shuts down. 

        e.g. shutdown +4 "Get Ready for the Next Move"

          ctrl+C is used to bring the screen back to life in Linux. 

**ifconfig**
  
  Syntax:
    
    ifconfig 
    (if config means interface configuration)

      ifconfig can be used to edit configuration, however, this is usually permanent, and thus, not used for this purpose. 

    iwconfig is similar but for wireless newtwork interfaces.

**ping** is a command sent to another machine. If a reply is received by the sender, it would be able to connect to that machine. The ping command sends packets to the target machine. A packet is an eccapsulated form of data that is sent over network. 

By default, this command will continue sending packets (successful or unsuccessful) unless the process is terminated by ctrl+C. 

  The number of pings sent can be limited by using the option of -c followed by the desired number. 

    e.g. ping -c 6 192.168.2.1

      If the ping command is failed, you will receive a message "Destination is unreachable"

        Ping command can also be failed because some system administrators configure their machine or entire network not to respond to ping as a security  measure. The ping command can also work with a hostname or domain. 

**Viewing Processes**

Running a command results in something called a "process". In Linux, processes are executed on the basis of the previliges of the users who executes the command. This limited the processes to certain capabilities based upon the user identity. 

  Generally, users with administrative previliges can control any user processes including stopping them. 

    Syntax
      
      ps [OPTIONS]

        The ps command displays the process running in the current terminal by default. 

          "PID" = process identifier - unique to the process. This information is useful for controlling the process by its ID number.
          "TTY" = The name of the terminal where the process is running. 
          "TIME"= The total amount of processor time used by the process. 
          "CMD" = The command that starts the process. 

            Instead of the processes running in the current terminal, you may want to view "every" process. Use -e option. 

              e.g. ps -e

                "-f" is the option used to see more details about the processes running. In the CMD section, you can also view the option used in the command.

                  e.g. ps -ef

**Package Management**

It is a system by which a software can be installed, updated, queried, or removed from a file system. The two most famous package management systems are apt and yum from Debian and RHEL.

  The lowest level of Debian package management system is the "dpkg" command. The front end of this command used is "apt" or "apt-get". 

    A package management system requires administrative rights, and hence, sudo is used before the command. 

      Before isntalling a package, it is recommended to update the current available packages. 

        e.g. sudo apt-get update

              then

                sudo apt-get upgrade

      'apt-cache search [KEYWORD]' is used to find a package with a particular keyword, multiple keywords can be used simulatenously. For example, use cow as a keyword. 

          Once found, a package can be installed using

            'sudo apt-get install [PACKAGE]'

              this command can install new software and update the installed ones. 

      'sudo apt-get purge [PACKAGE]' delete all package file including configuration files. 

      'sudo apt-get remove [PACKAGE]' delete all package files but configuration files. 

**Updating Passwords**

  'passwd' is a command used to update/change a password. A user can change only their password. However, a root user can change anyone's password. 

    Syntax:

      passwd [OPTIONS] [USER]
      
        e.g. 'passwd syadmin'
    
          To check the status information of your password, use

           Syntax:
           
            'passwd -S syadmin'

              The output shows:

                sysadmin P 11/15/2025 0 99999 7 -1

                  Password Status: P = usable password, L = locked paswword, NP = no password
  
                  Change Date: Last time the password was changed
  
                  Minimum: The minimum number of days before a password can be changed. 
  
                  Maximum: The remaining number of days after which a password will be expired. 
  
                  Warn: The number of days prior to password expiry the user is warned. 
  
                  Inactive: The number of days after password expiry a user account remains active. 

**Types of Redirecting**

  There are three main types of file descriptors:
    
    STDIN = Standard inpout is the information the command receives and processes when it is executed. 

    STDOUT = Standard output is the information displayed when a command is executed. 

    STDERR = Standard error messages generated by commands that are not executed correctly. 

      Standard Input (STDIN)

            sysadmin@localhost:~$ ls ~/Documents
      
      Standard Output (STDOUT)

            sysadmin@localhost:~$ ls                                                        
            
            Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos
      
      Standard Error (STDERR)

          sysadmin@localhost:~$ ls fakefile                                               
          ls: cannot access fakefile: No such file or directory

    Syntax:

        [COMMAND] > [FILE]

          e.g. cat food.txt > newfile1.txt

            The sign of > will overwrite any content in the file. 

              To apend a file, use e.g. cat food.txt >> newfile1.txt

                echo can also be used for redirection. 
                
                  e.g. echo "I am a genius" > newfile1.txt 

                  OR

                  echo "I am a genius" >> newfile1.txt


NOTE: TO REDIRECT INFORMATION TO AN EXISTING FILE, A USER MUST HAVE W PERMISSION ON THAT. 

**Using the Text Editor**

Vi (Visual) is a universal text editor for Linux/UNIX, available on all distributions. Vim (Vi Improved) adds extra features but works the same. Vi has three modes: Command (move cursor, edit text), Insert (add text), and Ex (save, quit, open files). Key actions include d (delete), y (copy), p (paste), with motions like h, j, k, l for navigation. Insert mode commands (i, a, o) control text insertion. Ex mode (:) handles file operations (:w, :q, :e). Vi is lightweight, terminal-friendly, and stable across decades.
