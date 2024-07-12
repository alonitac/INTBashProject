# Bash Project  [![][autotest_badge]][autotest_workflow]

## Project Goals

In this project, you will implement a bash script which applies default Bash profile configurations for new added Linux users.

Similarly to the [LinuxProject][LinuxProject], this project is aimed for beginners who want to get familiar with Git and GitHub workflows, debug Linux errors and turn Linux commands towards a mature Bash script.


## Preliminaries

1. Fork this repo by clicking **Fork** in the top-right corner of the page. 
2. Clone your forked repository by:
   ```bash
   git clone https://github.com/<your-username>/<your-project-repo-name>
   ```
   Change `<your-username>` and `<your-project-repo-name>` according to your GitHub username and the name you gave to your fork. E.g. `git clone https://github.com/johndoe/BashProject`.
3. Open the repo as a code project in your favorite IDE (Pycharm, VSCode, etc..).

Later on, you are encouraged to change the `README.md` file content to provide relevant information about your project.

Let's get started...

## Guidelines

In many Linux systems, the `/etc/skel` directory provides a way to assure new users are added to your Linux system with default Bash profile configurations.

When adding a new user with the `adduser` command, it will create the user's home directory (usually under `/home/<username>`), and copy files from `/etc/skel` to the new user's home directory.
Typically, the `/etc/skel` directory contains a file called `.bash_profile`. This file, when copied to the user's home directory, can customize the Bash environment of the user.

The `/etc/skel` directory itself is owned by the `root` user and has restrictive permissions (mode `755`), which means that only the `root` user can modify its contents.

1. In `/etc/skel` edit the `.bash_profile` file (or create it if it doesn’t exist) using your favorite text editor (`nano`, `vi`, etc...) as detailed below. It's highly recommended to backup the original file before you start.
    - Greet the user. E.g. if the username is **john**, the message `Hello john` will be printed to stdout.
    -  Define an environment variable called `COURSE_ID` with a value equals to `DevOpsTheHardWay`.
    - If the file `.token` exists in the home directory of the user, check its permissions. If the octal representation of the permissions set is different from `600` (read and write by the user only), print the following warning message to the user:

      ```text
      Warning: .token file has too open permissions
      ```
    - Change the `umask` of the user such that the default permissions of new created files will be `r` and `w` for the user and the group only.
    - Add `/home/<username>/usercommands` (while `<username>` is the linux username) to the end of the `PATH` env var.
    - Print the current `date` on screen in ISO 8601 format. The precision should be seconds, and the timezone should be UTC. The correct format should look like: `2022-03-18T08:54:21+00:00`.
    - Define a [command alias](https://tldp.org/LDP/abs/html/aliases.html), as follows - whenever the user is executing `ltxt`, all files with `.txt` extension are printed (tip: wildcards).
    - If it doesn't exist, create the `~/tmp` directory on the user's home dir. If it exists, clean it (delete all the directory's content without removing the dir itself).
    - If it exists, kill the process that is bound to port `8080` (ports will be discussed later on in the course). [This resource](https://stackoverflow.com/questions/11583562/how-to-kill-a-process-running-on-particular-port-in-linux) may help.
    - Feel free to add any additional configurations of yours.
1. Create a new Linux user using `adduser` command. If everything is done well, the new user's Bash environment should have the custom script profile you created.
1. Login to the new user terminal session: `su -l <username>`. Replace `<username>` to the created user. Example for the user's terminal behavior might be:

```console
username@localhost:~$ su -l john
Password:
Hello john

Warning: .token file has too open permissions

The current date is: 2022-03-18T08:54:21+00:00

john@localhost:~$ ltxt
a.txt
john@localhost:~$ echo $COURSE_ID
DevOpsTheHardWay
john@localhost:~$ ls -l tmp
total 0
john@localhost:~$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/home/john/usercommands
```

1. When done, copy the content of your `/etc/skel/.bash_profile` file into `bash_project/.bash_profile` in this repo.


## Submission

Time to submit your solution for testing.

1. Commit your changes. The **only** file that has to be committed is `.bash_profile`.
2. Push your commits to GitHub. 
3. In [GitHub Actions][github_actions], watch the automated test execution workflow (enable Actions if needed). 
   If there are any failures, click on the failed job and **read the test logs carefully**. Fix your solution, commit and push again.

Upon successful test execution, you'll see a green checkmark (✅) and the following message would be printed in the test logs:

```text
Well Done! you've passed all tests
```

# Good Luck


[LinuxProject]: https://github.com/alonitac/INTLinuxProject
[autotest_badge]: ../../actions/workflows/project_auto_testing.yaml/badge.svg?event=push
[autotest_workflow]: ../../actions/workflows/project_auto_testing.yaml/
[github_actions]: ../../actions
