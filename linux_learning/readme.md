# Command Documentation

## File Manipulation Commands

### nano

`nano joke.txt`

- **Description:** Opens the file `joke.txt` in the nano text editor.
- **Usage:** Used to edit text files directly from the command line. Provides a simple text editing interface.

### nano provision.sh

`nano provision.sh`

- **Description:** Opens the file `provision.sh` in the nano text editor.
- **Usage:** Used to edit shell scripts directly from the command line.

### chmod

`chmod 777 provision.sh` \
`chmod +x provision.sh`

- **Description:** Changes the permissions of a file or directory.
- **Usage:** Allows users to modify the access permissions of files or directories. `777` grants read, write, and execute permissions to all users, while `+x` adds execute permission.

## Script Execution Commands

### ./provision.sh

`./provision.sh`

- **Description:** Executes the shell script `provision.sh`.
- **Usage:** Runs a shell script located in the current directory.

### bash provision.sh

`bash provision.sh`

- **Description:** Executes the shell script `provision.sh` using the bash interpreter.
- **Usage:** Alternative method to run a shell script using the bash interpreter.

## Service Management Commands

### systemctl

`systemctl status nginx` \
`sudo systemctl stop nginx` \
`sudo systemctl start nginx` \
`sudo systemctl restart nginx` \
`sudo systemctl enable nginx`

- **Description:** Manages system services using the systemctl utility.
- **Usage:** Allows users to view the status, start, stop, restart, and enable/disable services. In this example, nginx is used as a service.

## Environment Commands

### printenv

`printenv` \
`printenv USER`

- **Description:** Displays environment variables and their values.
- **Usage:** Useful for viewing environmental settings and configuration.

### export

`export MYNAME=l`

- **Description:** Sets an environment variable.
- **Usage:** Assigns a value to the environment variable `MYNAME`.

### echo

`MYNAME=l` \
`echo $MYNAME`

- **Description:** Prints the value of a variable.
- **Usage:** Displays the value assigned to the variable `MYNAME`.

## Filesystem Navigation Commands

### cd

`cd /`

- **Description:** Changes the current directory to the root directory.
- **Usage:** Allows users to navigate to the root of the filesystem.

## Miscellaneous Commands

### nano .bashrc

`nano .bashrc`

- **Description:** Opens the .bashrc file in the nano text editor.
- **Usage:** Used to edit the .bashrc configuration file, which contains settings for the bash shell.

### source

`source .bashrc`

- **Description:** Loads the contents of a script file into the current shell session.
- **Usage:** Executes the commands in the specified file within the current shell context.

This document serves as a comprehensive reference for various command-line operations and can be consulted whenever needed to perform specific tasks or understand command functionalities.
