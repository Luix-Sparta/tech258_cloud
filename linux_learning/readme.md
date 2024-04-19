# Command Documentation

## File Manipulation Commands

### nano

`nano chicken-joke.txt`

- **Description:** Opens the file `chicken-joke.txt` in the nano text editor.
- **Usage:** Used to edit text files directly from the command line. Provides a simple text editing interface.

### cat

`cat chicken-joke.txt`

- **Description:** Displays the contents of the file `chicken-joke.txt` in the terminal.
- **Usage:** Used to view the contents of text files. It can also be used to concatenate and display the contents of multiple files.

### head

`head -n 2 chicken-joke.txt`

- **Description:** Prints the top 2 lines of the file `chicken-joke.txt`.
- **Usage:** Useful for quickly previewing the beginning of a file, especially when dealing with large files.

### tail

`tail -n 2 chicken-joke.txt`

- **Description:** Prints the bottom 2 lines of the file `chicken-joke.txt`.
- **Usage:** Helpful for inspecting the end of a file, especially when monitoring log files or other continuously updated files.

### cat -n / nl

`cat -n chicken-joke.txt` / `nl chicken-joke.txt`

- **Description:** Numbers the lines of the file `chicken-joke.txt` when outputting its contents.
- **Usage:** Useful for referencing specific lines in a file or providing context when discussing file contents.

### grep

`grep "chicken" chicken-joke.txt`

- **Description:** Searches for lines containing the keyword "chicken" in the file `chicken-joke.txt` and displays them.
- **Usage:** Helpful for filtering content based on specific criteria, such as searching for keywords or patterns within files.

## Package Management Commands

### sudo apt update -y

`sudo apt update -y`

- **Description:** Updates the package lists for upgrades and new package installations without user interaction.
- **Usage:** Ensures that the package manager has the latest information about available packages and dependencies.

### sudo apt install tree

`sudo apt install tree`

- **Description:** Installs the `tree` package, which is a utility for displaying directory structures in a tree-like format.
- **Usage:** Useful for visualizing directory structures and understanding the hierarchy of files and folders.

### sudo apt upgrade -y

`sudo apt upgrade -y`

- **Description:** Upgrades all installed packages to their latest versions without user interaction.
- **Usage:** Ensures that the system is running the latest software versions with security patches and bug fixes.

## Directory Navigation Commands

### pwd

`pwd`

- **Description:** Prints the current working directory.
- **Usage:** Helps users identify their current location within the filesystem.

### cd

`cd /`

- **Description:** Changes the current directory to the root directory.
- **Usage:** Allows users to navigate to the root of the filesystem.

### sudo su / sudo su ubuntu

`sudo su` / `sudo su ubuntu`

- **Description:** Switches the current user to the superuser (root) or another user, such as "ubuntu."
- **Usage:** Grants administrative privileges to execute commands that require root access.

### exit

`exit`

- **Description:** Exits the current shell session.
- **Usage:** Terminates the current shell session and returns to the previous user or session.

## File Management Commands

### mv

`mv chicken-joke.txt funny_stuff/` \
`mv funny_stuff/chicken-joke.txt .` \
`mv chicken-joke.txt funny_stuff/funny_jokes/` \
`mv funny_stuff/funny_jokes/chicken-joke.txt funny_stuff/funny_jokes/bad_joke.txt` \
`mv bad_joke.txt ..`

- **Description:** Moves or renames files and directories.
- **Usage:** Used to relocate files or directories within the filesystem or change their names.

### rm -r

`rm -r funny_stuff/`

- **Description:** Deletes a directory and its contents recursively.
- **Usage:** Removes directories and their contents permanently from the filesystem.

## Miscellaneous Commands

### tree

`tree`

- **Description:** Displays directory structures in a tree-like format.
- **Usage:** Provides a visual representation of directory hierarchies, making it easier to navigate and understand file organization.

This document serves as a comprehensive reference for various command-line operations and can be consulted whenever needed to perform specific tasks or understand command functionalities.
