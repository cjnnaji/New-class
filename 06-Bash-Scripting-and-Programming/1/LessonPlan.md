## 6.1 Lesson Plan: Advanced Bash

### Class Overview

In today's class, students will combine commands, create custom commands, and begin writing bash scripts. 

For the next two classes, students will use these skills to collect evidence, audit and reconfigure a Linux machine, and take steps to harden the system. 

### Class Objectives

By the end of class, students will be able to:

- Construct compound commands using `&&`, `|`, and file redirects;

- Create and save alias commands to their `~/.bashrc` file;

- Edit `$PATH` variables to include a custom `~/scripts` directory; and

- Create simple bash scripts comprised of a list of commands.

### Instructor Notes

Students may have varying levels of competency regarding bash scripting. 

- For students with less technical experience, today's class will serve as an introduction bash. They will be equipped with the knowledge to work through scripts without getting lost.  

- For more technically advanced students, today's class activities should provide enough bonuses in order to keep those students engaged and challenged. 

- For the partner activities, pairing some non-technical students with more technical students may make the work flow better.

### Lab Environment

For today's lesson, use your web lab virtual machine. Log in using the following credentials: 

- Instructor access:

   - Username: `instructor`

   - Password: `instructor`

- Student access:

   - Username: `sysadmin`

   - Password: `cybersecurity`


### Module Day 1 Contents

- [x] [01. Instructor Do: Compound Commands](LessonPlan.md#01-instructor-do-compound-commands-015)
- [x] [02. Student Do: Compound Commands](LessonPlan.md#02-student-do-compound-commands-015)
- [x] [03. Instructor Review: Compound Commands](LessonPlan.md#03-instructor-review-compound-commands-005)
- [x] [04. Instructor Do: Creating Aliases](LessonPlan.md#04-instructor-do-creating-aliases-010)
- [x] [05. Student Do: Creating Aliases](LessonPlan.md#05-student-do-creating-aliases-015)
- [x] [06. Instructor Do: Creating Aliases Review](LessonPlan.md#06-instructor-do-creating-aliases-review-010)
- [x] [07. Break](LessonPlan.md#07-break-015)
- [x] [08. Instructor Do: Creating Bash Scripts](LessonPlan.md#08-instructor-do-creating-bash-scripts-020)
- [x] [09. Student Do: Creating a Bash Script](LessonPlan.md#09-student-do-creating-a-bash-script-020)
- [x] [10. Instructor Do: First Bash Script Review](LessonPlan.md#10-instructor-do-first-bash-script-review-010)
- [x] [11. Instructor Do: Custom Commands](LessonPlan.md#11-instructor-do-custom-commands-015)
- [x] [12. Student Do: Custom Commands](LessonPlan.md#12-student-do-custom-commands-020)
- [x] [13. Instructor Do: Custom Commands Review](LessonPlan.md#13-instructor-do-custom-commands-review-010)


### Lesson Slideshow  

The slides for today can be viewed on Google Drive here: [6.1 Slides](https://docs.google.com/presentation/d/1rXTU9pSmvUmCx6tPCThFm_muPIFyfajiOjMO_wj2dKk/edit?usp=sharing).

- To add slides to the student-facing repository, download the slides as a PDF by navigating to File > "Download as" and choose "PDF document." Then, add the PDF file to your class repository along with other necessary files.

- **Note:** Editing access is not available for this document. If you or your students wish to modify the slides, please create a copy by navigating to File > "Make a copy...".

### Time Tracker

The time tracker for todays lesson can be viewed on Google Drive here: [6.1 Time Tracker](https://docs.google.com/spreadsheets/d/1oJmVHrawxXCB1qOlj0OrlfxjDs30EKHEoOgsV1nAh10/edit#gid=1047115118).

### Student Guide

Distribute the student-facing version of the lesson plan: [6.1 Student Guide](StudentGuide.md)

---

### 01. Instructor Do: Compound Commands (0:15)

Welcome the students to class and provide a quick overview of the topics we will be covering today:

- Creating compound commands by chaining several commands together.

- Creating custom commands using aliases.

- Creating short bash scripts.

- Creating custom commands from bash scripts.

Let's get started with creating compound commands.

#### Creating Compound Commands

Using compound commands on the command line is a fundamental IT skill, especially for **system administrators**.

-  Navigating Linux directories, quickly searching large log files, and writing small scripts to automate tasks will save you time and energy.

- Because Linux is used widely throughout the security field, these same skills will prove invaluable in many security roles.

A **compound command** is the combination of multiple commands, joined together and executed in succession. We can also think of it as chaining together different programs in order to accomplish a given task.

For example: `file $(find / -iname *.txt 2>/dev/null) > ~/Desktop/text_files ; tail ~/Desktop/text_files`  

- This command does the following:  

   - Searches the entire computer for files ending in `.txt`.

   - Verifies that the files found are text files, ignores any errors it comes across, and creates a list of all found files before saving that list to the desktop.

   - Finally, it will open the file and print the last ten lines that were added. 

By the end of the day, students should be able to describe the function of each character in these types of commands, improve the syntax of the command, and create new commands to accomplish new tasks.

#### Breaking Down the Command

Review the three components of a command that students are already familiar with:

1. The **program** is a binary program that you are running.

2. The program's **options** will change the behavior of the program being run in the first part of the command.

3. The **arguments** provided usually point the command towards something, such as a directory or file that you want the program to act on.

Commands typically follow this format:

`program -options arguments`

Explain that in this case, the `arguments` part of the command is acting as input for the command.

   - However, when you start chaining commands together, the output of one command becomes the input of the next, and so the `argument` is only needed for the first command in the chain.

Compound commands typically follow this format:   

`program -options arguments | program -options | program -options | program -options`

Students have already been chaining commands together using various techniques like `>`, `>>`, and `|`.

#### Chaining Commands Refresher

In this section, we will review some chaining methods that students are familiar with. We will also introduce a few new options used for creating compound commands. 

Log into the lab environment with the username `sysadmin` and password `cybersecurity`.

Using the slides, review the following chaining methods:

#### Chaining with `>` and `>>`

Cover the following:

`ls > list.txt`

-  This command takes the output of the `ls` command and sends it into a new file named `list.txt`. _If_ the file `list.txt` already exists, it is overwritten with the output of the `ls` command.

`> list.txt`

- Without a command in front of `>`, there is no output to send to the `list.txt` file.

- However, the file is still written just with no output, so a blank file is written. _If_ the file `list.txt` exists, it is overwritten with nothing.

`ls >> list.txt`

- `>>` will append the output of the `ls` command to the `list.txt` file.

- If the `list.txt` file does not exist, it is created.

- Therefore, using `>>` instead of `>` is always safer, unless you want the file to be overwritten.

#### Piping with `|`

Ask the students if they remember what the `|` does.

- The pipe (` | `) takes the output of one command and sends it to the input of another command.

Remind students that compound commands with pipes typically follow this format:

- `program -options arguments | program -options | program -options | program -options`

For example: `ls -l | grep '.txt'`

- Break down the syntax:

   - `ls -l` creates a list of files.

   - `|` pipes the list from `ls` into the command that follows.

   - `grep` searches the files from `ls` for the string that follows.

   - `.txt` matches any file that contains .txt in the filename.

Review some other common programs users pipe to:

- `| head` prints only the first 10 lines of output.

- `| tail` prints only the last 10 lines of output.

- `| sort` sorts the output alphabetically.

- `| sed`  searches and replaces parts of the output.

- `| awk`  displays only specified parts of the output.

Using the slides, present this advanced example of chaining commands together using `|`.

- `cat /etc/passwd | grep sysadmin | awk -F ':' '{print $6}'`.

- Ask the class if anyone can walk through what this command does. Then break down the syntax:

   - `cat /etc/passwd` dumps the contents of `/etc/passwd` to output.

   - `|` pipes that output into the command that follows.

   - `grep sysadmin` displays lines that contain `sysadmin`.

   - `|` pipes that output into the command that follows.

   - `awk -F ':' '{print $6}'` prints only the sixth field of the line.

   - `awk` usually looks for a space to use as a `field separator`, but in this case, we want it to separate the line by a colon, because `/etc/passwd` uses colons to separate its fields.

- If we run `cat /etc/passwd | grep sysadmin | awk -F ':' '{print $6}'`, it would output the following:

   ```bash
      /home/sysadmin
   ```

Explain that now we will introduce `;`.

#### Combining with `;`

Explain that we can also use a `;` to run a series of commands back to back.

When using `;`, each command is running on its own. It is not sending its output to the next command. Therefore, each command can have its own arguments.

- For example, rather than typing this:

   ```bash
   $ mkdir dir
   $ cd dir
   $ touch file
   $ ls -l
   -rw-r--r-- 1 user user 0 Sep  4 15:33 file
   ```

   We can use one command:

   - Run `cd ..`.

   - Run `rm -r dir`.

   - Type `mkdir dir; cd dir; touch file; ls -l`.

   Explain that each command will happen in succession.

   - First, the `mkdir` command, then `cd`, `touch`, and finally `ls`.

Explain that compound commands using `;` typically follow this format:

`program -options arguments ; program -options arguments ; program -options arguments ; program -options arguments `

- Run `mkdir dir; cd dir; touch file; ls -l`.

   Your output should look similar to:

   ```bash
   $ mkdir dir; cd dir; touch file; ls -l
   -rw-r--r-- 1 user user 0 Sep  4 15:33 file
   ```
 **Pause for a knowledge check**

- :question: Pose the following question to the class: 

  - "Can anyone think of how a string of commands separated by `;` would be affected?" 

    > Answer: Explain that `;` will run each command back to back, no matter the outcome of the commands. Therefore, using `;` to chain commands together may not always give you the correct outcome.

Remove the files you just created.

- Run `cd ..`.

- Run `rm -r dir`.

   **NOTE:** Remember from earlier modules that `rm -r` removes the directory and the files contained in it

Note the misspelling in the following command. 

- Type `mkdir dir; cd dor; touch file; ls -l`.

   - Point out that this command will fail because you are trying to move into the directory `dor` which has not been created. However, the commands `touch` and `ls` will still run.

- Run `mkdir dir; cd dor; touch file; ls -l`.

   Your output should be similar to:

   ```bash
   -bash: cd: dor: No such file or directory
   drwxr-xr-x 2 user user  4096 Sep  4 15:52 dir
   -rw-r--r-- 1 user user     0 Sep  4 15:52 file
   ```

Point out the error reported for `cd`.

- We still have a `file` and the `ls` command to run, but we did not get our desired output because we were not in directory `dor`.

#### Combining with `&&`

 **Pause for a knowledge check**

- :question: Pose the following question to the class: 

  - "So if a string of commands seperated by `;`  will run each command back-to-back, no matter the outcome of the commands, how do you think the `&&` would affect a chain of commands?" 

    > Answer: Explain that `&&` will run the next command only if the first command was successful.

- Type `mkdir dir && cd dir && touch file && ls -l`.

   - If the command was written this way, `cd` would only run if `mkdir` was successful, `touch` would only run if `cd` was successful, and `ls` would only run if `touch` was successful.

Explain that compound commands using `&&` typically follow this format:

- `program -options arguments && program -options arguments && program -options arguments && program -options arguments`

In this following command, the only commands that run are `mkdir dir` and `cd dor`. `cd dor` fails, so `touch` and `ls` are ignored.

- Run `mkdir dir && cd dor && touch file && ls -l`.

   Your output should be similar to:
   
   ```bash
   -bash: cd: dor: No such file or directory
   ```

- Run `ls` to show that `dir` was created.

#### Section Summary

Remind the students that we reviewed the following:

- `>`: to create or write to existing files with text or output of a command. It creates a file if the file does not exist.

- `>>`: to append text or output of a command to a file. It creates a file if the file does not exist.

- `|`: pipes the output of one command into another command.

In this demo we covered:

- `;`: to chain commands together in succession.

- `&&`: to chain commands together. The second of two commands runs only if the previous command was successful.

Ask if students have any questions about using any of these before moving on to the activity.

[<- Back to Module Contents](LessonPlan.md#module-day-1-contents)

---

### 02. Student Do: Compound Commands (0:15)

Explain the following to students:

- In the previous Linux classes, you learned a lot of different commands that you typically execute one at a time. Now we can start combining commands together to save us time when working on the command line.

- In this activity, you are working on auditing a new system and would like to simplify your job with automation. You will begin by combining several commands together to make fewer overall commands.

- This exercise will give you an opportunity to explore creating some useful commands that combine several steps they took during the system audit from Linux Day 1.

Send students the following link:

- [Activity File: Compound Commands](Activities/02_Compound_Commands/Unsolved/Readme.md)

[<- Back to Module Contents](LessonPlan.md#module-day-1-contents)

---

### 03. Instructor Review: Compound Commands (0:05)

:bar_chart: Run a comprehension check poll before reviewing the activity. 

Remind students that the point of this exercise is to get acquainted with compound commands.

Explain that completing this task requires:

- Creating a directory and automatically copying log files to it with one command.

- Finding a list of executable files and saving it to a text file inside your directory with one command.

- Saving an edited list of the 10 most active processes to your directory with one command.

- Creating a list of home folders and users with a user identifier (UID) of less than 1000 and saving that to your directory, all with one command.

Use the following solution file to review the activity:

- [Solution Guide: Compound Commands](Activities/02_Compound_Commands/Solved/Readme.md)

Answer any questions students may have before continuing to the next section.

[<- Back to Module Contents](LessonPlan.md#module-day-1-contents)

---

### 04. Instructor Do: Creating Aliases (0:10)

Point out that compound commands are useful but do require a lot of typing. If you use a compound command often, it might be nice to save it somewhere so you can easily reference it.

Explain that an **alias** is a shorthand or custom command that you can define, which will launch any command or compound command, including arguments and redirection.

Next, we will create custom commands using aliases and save them into a configuration file so that they are available every time you login.

- System administrators commonly use custom commands in everyday work to save time.

- Today, we are going to use them to make our audit commands even easier to remember and use.

**NOTE:** Many Linux distributions have aliases installed by default.

- `ls` by default shows the files and directories in the current directory in white.  

- In our system, there is already an alias for `ls` that outputs `ls --color-auto`, which shows files in white, directories in blue, and executables in green.

#### Aliases Demo

In this demonstration, we will create aliases. 

Log into the lab environment with the username `sysadmin` and password `cybersecurity`. Open up the Terminal.

1. Explain that the syntax for creating an alias is as follows:

   - Type `alias lh='ls -lah'`.

      - Break down the syntax:

         - `alias` indicates that we are creating an alias.

         - `lh` is our custom command that we will use to store the command we want to run.

         - `ls -lah` is the command that will run when we use our alias `lh`.

   - Run `alias lh='ls -lah'`.

   - Run `lh`.

      Output should resemble:

      ```bash
      $ alias lh='ls -lah'
      $ lh
      total 52K
      drwxr-xr-x  6 user user 4.0K Sep  4 16:00 .
      drwxr-xr-x 28 user user 4.0K Aug 27 14:46 ..
      drwxr-xr-x  3 user user 4.0K Aug 28 12:51 1
      drwxr-xr-x  3 user user 4.0K Aug 28 12:52 2
      drwxr-xr-x  2 user user 4.0K Aug 27 14:46 3
      drwxr-xr-x  2 user user 4.0K Sep  4 16:00 dir

      ```

   - Now, anytime we use `lh`, it will run `ls -lah`. 

2. Naming an alias after a command that already exists will change the way that command behaves. It may even possibly stop the command from working. 

   - For example, if we wanted the `ls` command to _always_ default to `ls -l`, we could create an alias to override the `ls` command.

   - Run `alias ls='ls -l'`.

   - Type `ls` to show that the behavior has changed.

      - We can see a list of all the aliases we currently have access to by simply typing `alias`.

   - Type `alias`.

      Your output should be similar to:

      ```bash
      $ alias
      alias egrep='egrep --color=auto'
      alias fgrep='fgrep --color=auto'
      alias grep='grep --color=auto'
      alias ls='ls -l'
      alias ll='ls -alF'
      alias la='ls -A'
      alias l='ls -CF'
      alias lh='ls -lah'
      ```

   Explain that all the aliases listed are configured by default. We will discuss how to change them in a moment.

3. If we wanted to remove an alias, we can use the `unalias` command.

   - Type `unalias ls`.

   - Type `alias`.

   Your output should show that the `ls` alias has been removed.

   ```bash
   $ unalias ls
   $ alias
   alias egrep='egrep --color=auto'
   alias fgrep='fgrep --color=auto'
   alias grep='grep --color=auto'
   alias ll='ls -alF'
   alias la='ls -A'
   alias l='ls -CF'
   ```

   - Run `ls` to show that the expected output has returned.

4. Aliases created in this way only work for the session in which you have created them. So, once the terminal is closed and re-opened, the alias will be gone.

   - Close and reopen the terminal.

   - Run `lh`.

   You should get:
   ```bash
   -bash: lh: command not found
   ```

#### Keeping Aliases Across Sessions and Logins

Explain that if we want these commands to be available every time we login, we need to store them in a configuration file that loads every time we open a terminal.

- Point out that the terminal has several configuration files, but the best file to use is the `~/.bashrc` file.

- Run `cd` to move to your `/home/instructor/` directory.

- Run `ls -la` to show all your files.

   - Point out the `.bashrc` file.

      ```bash
      drwx------ 26 user user  4096 Sep  4 20:57 .
      drwxr-xr-x  3 root root  4096 Aug 27 14:03 ..
      -rw-------  1 user user  6779 Sep  4 21:48 .bash_history
      -rw-r--r--  1 user user   220 May 15  2017 .bash_logout
      -rw-r--r--  1 user user  3690 Aug 28 18:44 .bashrc
      -rw-r--r--  1 user user   675 May 15  2017 .profile
      ```

Explain that if we want the alias to remain across logins, all we need to do is open the `~/.bashrc` file and add them there.

**Important:** Point out that before we edit this file, we should make a copy of it, in case we make a mistake.

- Run `cp .bashrc .bashrc.bak`.

   - The `.bashrc` file will already have many configurations inside it, the scope of which lies outside this course.
   - All of the existing configurations can be ignored and they can add their aliases to the bottom of the file or the section commented for aliases.

-  Run `nano .bashrc`.

   - Scroll down and point out the section that already has some aliases defined. These are some of the aliases we saw earlier:

   ```
   # some more ls aliases
   alias ll='ls -alF'
   alias la='ls -A'
   alias l='ls -CF'
   ```

Explain that you can add aliases here or modify the ones that already exist. Alternatively, you can create your own alias section at the bottom of the file.

- Move to the bottom of the page and enter your alias along with a `# Custom Alias Section` comment:

   ```bash
   # Custom Alias Section
   alias la='ls -lah'
   ```

Save and close the file.

Point out that in order for the new setting to be loaded, we either have to reload the `~/.bashrc` file, or we need to open a new terminal.

Explain that if we want to simply reload the file, we can use the `source` command.

- Run `source .bashrc` to demonstrate reloading `.bashrc.`.

- Run `la` to show that your alias is working.

Close and reopen the terminal.

- Run `la` to show that your alias is still working.

#### Adding an Alias to `.bashrc`

Finally, in keeping with today's theme of becoming more efficient in the command line, show students how to add an `alias` to their `.bashrc` with one command.

Explain that reloading the `.bashrc` can have its own alias, so we will create one for it now.

- Type `echo "alias rr='source ~/.bashrc'" >> ~/.bashrc && source ~/.bashrc`.

   Break down the syntax:

   - `echo` sends what comes next directly to output.

   - `alias` is our alias declaration.

   - `rr` is our custom command that we use to reload the `.bashrc` file quickly.

   - `'source ~/.bashrc'` is our command that reloads `.bashrc` and will be tied to `rr`.

   - `>>` appends this to a file that we specify.

   - `~/.bashrc` is the file we want to add our alias to.

   - `&&` if the first command is completed successfully, then run the command that comes next.

   - `source ~/.bashrc` reloads the `~/.bashrc` file to enable our new `rr` alias.

Point out that if we wanted to, we could just use `echo "alias rr='source ~/.bashrc'" >> ~/.bashrc` to add the alias, and then reload the `.bashrc` file using `source ~/.bashrc`, but here we are using `&&` to complete it with one command.

From now on, you can just type `rr` to reload the `~/.bashrc`.

Provide one more example of adding an alias this way:

- Suppose we want the `rm` command to always give you a warning before removing a file. According to man pages, the `-i` flag does this. So, we want the `rm` command to always default to `rm -i`.

- Run `echo "alias rm='rm -i'" >> ~/.bashrc && rr`.

  -  Break down the syntax:

      - `echo` sends what comes next directly to output.

      - `alias` is our alias declaration.

      - `rm` is the alias we are using for our new, modified `rm` command.

      - `'rm -i'` is our modified `rm` command that we want to use every time we type `rm`.

      - `>>` appends this to a file that we specify.

      - `~/.bashrc` is the file we want to add our alias to.

      - `&&` if the first command is completed successfully, then run the command that comes next.

      - `rr` is the alias we created a moment ago for `source ~/.bashrc`.

- Run `tail -4 ~/.bashrc` to show the bottom of the file:

   ```bash
   $ tail -4 ~/.bashrc
   fi
   fi
   alias rr='source ~/.bashrc'
   alias rm='rm -i'
   ```

Pause and ask the class if there are any questions about adding aliases to the `.bashrc` file.

[<- Back to Module Contents](LessonPlan.md#module-day-1-contents)

---

### 05. Student Do: Creating Aliases (0:15)

Explain the following to students:

- In the previous activity, you created longer commands by combining commands together to save time. Now, we will take things a step further and create some aliases for these commands along with some other commands that will save you more time when working at the command line.

- In this activity, we will create several aliases and save them to our `~/.bashrc` file so that they will always be available.

Send the following files to students:

- [Activity File: Creating Aliases](Activities/05_Creating_Aliases/Unsolved/Readme.md)

[<- Back to Module Contents](LessonPlan.md#module-day-1-contents)

---

### 06. Instructor Do: Creating Aliases Review (0:10)

Remind students that the point of this exercise is to practice creating custom commands using aliases and the `~/.bashrc` file.

Explain that completing this exercise requires creating the following aliases:

- A custom `ls` command.

- Custom commands to change directories into `Documents`, `Downloads`, and the `/etc` directory.

- A custom command to easily edit the `~/.bashrc` file.

- Custom commands for each of the compound commands they created in the previous activity.

- Reloading the `.bashrc` file so that the commands take effect.

Use the solution file to conduct a walkthrough:

- [Solution Guide: Creating Aliases](Activities/05_Creating_Aliases/Solved/Readme.md)


Ask if there are any questions before going to break.

[<- Back to Module Contents](LessonPlan.md#module-day-1-contents)

---

### 07. Break (0:15)

[<- Back to Module Contents](LessonPlan.md#module-day-1-contents)

---

### 08. Instructor Do: Creating Bash Scripts (0:20)

Let students know that we will now create short bash scripts that use variables and command expansion.

Remind students that a **bash script** is a file containing a sequence of commands that is executed when the script is run.

- Bash scripting is very common among system administrators in order to automate common tasks.

- Creating a bash script and then scheduling it to run at a regular time using `cron` is considered to be a basic ability of any system administrator.

Inform class that in the following demo, we will cover **variables** and **command expansion** before putting it all together into a script.

#### Introduction to Variables

Explain that in computer programing, a variable is a location that stores some kind of data.

- We can think of it as a box that holds something so that you can refer to it later.

- If you no longer need what is in the box, you can overwrite its contents with new contents.

Explain that variables can be overwritten and reused for different purposes. In other words, the data inside them may vary, hence the name _variable_.

- For our purposes, we will use a variable to hold either a number or a string of characters.

- Another common use of variables in a `bash` script might be to hold the value of a file path.

 **Pause for a knowledge check**

- :question: Pose the following question to the class: 

  - "Can anyone define what a basic bash script is?" 

    > Answer: A bash script is quite simply a file that contains a command or sequence of commands that are executed when the script is run.

#### Variable Demo

Log into the lab environment with the username `sysadmin` and password `cybersecurity` and open a terminal.

Let's make a variable for the `/etc/passwd` file path:

- Run `my_variable='/etc/passwd'`.

- Run `echo $my_variable`.

- Your output should look like:

   ```bash
   $ my_variable='/etc/passwd'
   $ echo $my_variable
   /etc/passwd
   ```
   - `my_variable` is the name of the variable you want to create.

   - `=` assigns your variable a value.

   - `'/etc/passwd'` is the value that your variable holds.

- Point out a few more syntax-related notes:

   - There must not be any spaces on either side of the `=` or you will get an error.

   - Quotations must be used for any strings that are stored in a variable, particularly if there are spaces between characters.

When calling on a variable, it must be preceded with a `$`.

- Run `num=5`.

- Run `echo $num`.

- Your output should be:

   ```bash
   $ num=5
   $ echo $num
   5
   ```

Pause for a moment and ask if there are any questions here.

#### Built-In Variables

Point out that bash has a number of built-in variables called **environment variables**. They are also known as **shell variables**.

 **Pause for a knowledge check**

- :question: Pose the following question to the class: 

  - "What's the difference between a bash environment variable and bash local variable?" 

    > Answer: Environment variables are valid system-wide. Local variables are only valid within the current (bash) shell.

They are always defined with all upper case letters. For example, `$PWD` is an environment variable that returns the `pwd` command.

- Run `echo $PWD`.

- Your output should be:

   ```bash
   $ echo $PWD
   /home/sysadmin
   ```

Explain that these can be creatively used to generate useful output:

- Run `echo "My present working directory is $PWD."`.

- Output:

   ```bash
   $ echo "My present working directory is $PWD."
   My present working directory is /home/sysadmin.
   ```

Run the following commands to demonstrate built-in variables:

- `echo "My name is $USER"`: Provides the user name of the current user.

- `echo "My home directory is $HOME"`: Provides the home folder of the current user.

- `echo "The name of my computer is $HOSTNAME"`: Provides the name of the computer.

- `echo "My type of computer is a $MACHTYPE"`: Provides the type of computer.

- `echo "My user ID is $UID"`: Provides the `UID` of the current user.

**Note:** Avoid the `$PATH` variable for now. We will cover it in the next section.

Ask if any students have any questions about using or defining variables.

#### Common expansion

Now we will move onto command expansion. Remind the class of the command we used at the start of the lesson:

- `file $(find / -iname *.txt 2>/dev/null) > ~/Desktop/text\ files ; tail ~/Desktop/text\ files`

Explain that **expansion** in bash refers to any time something on the command line expands or morphs into something else.

- In our command example, the `find` command between the `$()` runs before any other part of the command.

- This `find` command _expands_ into a list of items that it found. The rest of the commands are acting on that list, not acting on the `find` command itself.

Explain that bash syntax uses the `$()` for command expansion.

- You can put any number of commands chained together inside these brackets.

- Bash reads that chunk as whatever is returned from running the commands inside it.

- Then, the rest of the commands on the line run.

Explain that this is quite helpful when writing a script if we want one command to run before another command. To do this, we just surround that command with `$()`.

Point out that the `$` is similar to using it with a variable, but in this case we are receiving the output of the command.

For example, type `echo "The files in this directory are: $(ls)"` and break down the syntax:

- `echo` sends what comes next to output.

- `"The files in this directory are: "` is sent directly to output and creates a headline.

- `$()` Run _this command before_ any other command on this line. In this case, it says "Run the command inside these brackets _before_ running the `echo` command."

- `ls` is the command that runs first.

Run `echo "The files in this directory are: $(ls)"`.

Your output should be similar to:

   ```bash
   echo "The files in this directory are: $(ls)"
   The files in this directory are:file1
   file2
   file3
   file4
   ...
   ```

Point out the lack of line break before `file1`. We can fix this if we use a line break with `echo`.

- To use a line break, we need to use the `-e` flag with `echo` and then place the line break `\n` where we want it.

- Type `echo -e "The files in this directory are: \n$(ls)"`.

Your output should be similar to:

```bash
$ echo -e "The files in this directory are: \n$(ls)"
The files in this directory are:
file1
file2
file3
file4
...
```

Ask if there are any questions about using `$()` to surround a command and cause it to run first or any questions about using line breaks with `echo`.

#### Variables in Scripts Demonstration

Now we will demonstrate how to use these concepts in a script.

Explain that bash script files often end in `.sh` to indicate they are a `shell script`. However, a script file will still run with any extension.

- As an aside, mention that Linux generally ignores file extensions. Instead, it looks at the contents of the file in order to determine how to use it. Therefore, you can create text files without any extension at all, but it is best practice to use the `.sh` file if you think other users may interact with your script.

Point out that in order to create a bash script, it is important to use a text editor that does not add any extra formatting to the file when you save it. Some common options that text editors use in the command line are `nano`, `vim`, and `emacs`.

- In this class, we will stick with `nano` but students are encouraged to explore the other text editors if they are interested in choosing another editor.

Begin by creating an empty file:

- Type `nano my_script`.

- Type `echo "Hello World."`.

Save and close the script.

Explain that if we tell bash what shell to use to execute this file, it can be interpreted as a script.

- Run `bash my_script`.

Your output should look like:

```bash
$ bash my_script
Hello World.
```

Explain that while this format works, it is customary to use the `.sh` file extension in order to easily identify a script.

- Run `mv my_script my_script.sh`.

Explain that in the interest of efficiency, we can create a script file that will always run with `bash`, so we don't have to type `bash my_script.sh` every time we want to use it.

- To do this, at the top of the file, we add a line that starts with `#!` followed by the path of the shell we want the system to use.

- This line tells the system what shell we want to interpret this file.

- `#!` is often referred to as '**Hash Bang**' or '**Shebang**'.

Before we use the hash bang, we need to know the path of the bash.

- Run `which bash` to get the path to bash.

   Your output should be:

   ```bash
   $ which bash
   /bin/bash
   ```

**Note:** Running `bash my_script.sh` is the same as `/bin/bash my_script.sh`. Bash automatically knows what you mean by `bash`. If students ask how bash knows this path, explain that we will cover that in the next part of the class (the `$PATH` variable).

Now we can add the line at the top of the file.

- Run `nano my_script.sh`.

- Above the `echo` line, add `#!/bin/bash`:

   ```bash
   #!/bin/bash
   echo "Hello World."
   ```

Break down the syntax:

- `#!` to indicate that what comes next is the shell we want to use to interpret this file.

- `/bin/bash` is the shell we want to use.

- `echo "Hello World."` is the first line in our script.

Save and close the file.

Explain that before we can run the script, we have to change its permissions to be an executable file.

- Run `ls -l my_script.sh`.

   Output should look like:

   ```
   -rw-r--r-- 1 user user 20 Sep  5 16:20 my_script.sh
   ```

Point out that the file is not executable, so it can't be run on its own.

- Run `chmod +x my_script.sh`.

- Run `ls -l my_script.sh`.

   Your output should look similar to:

   ```
   -rwxr-xr-x 1 user user 20 Sep  5 16:20 my_script.sh
   ```

Now, we can run the file on its own. The system will know to look inside the file for the `#!` line and interpret the file using the `/bin/bash` program.

Explain that in order to run the file at this time, we only need to tell the system that the file is located in our current directory.

- Type `./my_script.sh`.

Explain that `./` is used to tell the system, "Execute the file that follows from _this_ directory."

- Run `./my_script.sh`.

   Your output should be:

   ```bash
   $ ./my_script.sh
   Hello World.
   ```

Pause and ask the class if there are any questions about creating an executable bash script file.

Point out that in the event that a machine doesn't have the `bash` program located at `/bin/bash`, or if it is using a different version of `bash` in another location, this script may fail.

If we want our script to move around to different machines, we can use the line: `#!/usr/bin/env bash`.

-  `/usr/bin/env` will find the version of a program that the system is configured to use. When we use it with `bash`, we are saying, use the `bash` configured on this system to interpret this file.

- `/usr/bin/env bash` is important for students to understand, but for our purposes, using `/bin/bash` is just fine.

Ask if there are any questions about this.

#### Quick Script Demonstration

Now we will create a short script in order to demonstrate how scripting works.

- We will intentionally keep this script to a series of commands in a list.

Open the script:

- Run `nano my_script.sh`.

- Enter this script:

   ```bash
   #!/bin/bash
   name='Jake'
   echo "Hello $name."
   echo -e "\nThis is my script.\n"
   echo -e "The files in $PWD are: \n$(ls)"
   echo -e "\nCopying the passwd file to your current directory.\n"
   cp /etc/passwd $PWD
   echo -e "The files in $PWD are now: \n$(ls)"
   echo " "
   echo "Have a great day!"
   ```

Add or remove commands here as you see fit and then save and exit nano.

Next, run `./my_script.sh`.

- Your output should be similar to:

   ```bash
   Hello Jake.

   This is my script.

   The files in /home/sysadmin are:
   file1
   file2
   file3
   ...

   Copying the passwd file to your current directory.

   The files in /home/sysadmin are now:
   file1
   file2
   file3
   passwd
   ...

   Have a great day!
   ```

 **Pause for a knowledge check**

- :question: Pose the following question to the class: 

  - "If we plan to run our bash scripts on another machine, what would our `shebang` line look like?" 

    > Answer: If we want our script to move around to different machines, we can use the line `#!/usr/bin/env bash` at the top of our script.

Before moving onto the next activity, ask if students have any questions.

Explain that in the next activity, students will get a chance to try out these techniques by using their own bash script.

[<- Back to Module Contents](LessonPlan.md#module-day-1-contents)

---

### 09. Student Do: Creating a Bash Script (0:20)

Explain the following to students:

- In the previous activity, you created several aliases and saved them to your `~/.bashrc` file. You may have noticed that creating long strings of commands can get a bit cumbersome when working on the command line.

- Now, we will put our commands into a script file. Reading, writing, and running bash scripts are a staple of any good sysadmin.

- In this activity, you will create a script that completes several system audit steps automatically.

:globe_with_meridians: This activity will use breakout rooms. Assign students into groups of 2 and move them into breakout rooms. 

Send students the following activity file:

- [Activity file: My First Bash Script](Activities/09_Creating_Bash_Scripts/Unsolved/Readme.md)

[<- Back to Module Contents](LessonPlan.md#module-day-1-contents)

---

### 10. Instructor Do: First Bash Script Review (0:10)

:bar_chart: Run a comprehension check poll before reviewing the activity. 

In this activity, students wrote their first basic script and run it using `./` notation.

Let students know that at this time, the script is intentionally a series of commands that they would normally run individually.

To complete this activity, they needed to:

- Add all the commands in the instructions to your script. (Some of these commands have not been covered and may require some Google Fu.)

- Change the permissions on your script to make it executable.

- Run your script to verify it produces the correct output.

Use the following solution guide to conduct a walkthrough:

- [Solution Guide: My First Bash Script](Activities/09_Creating_Bash_Scripts/Solved/Readme.md)

[<- Back to Module Contents](LessonPlan.md#module-day-1-contents)

---

### 11. Instructor Do: Custom Commands (0:15)

Inform class that next, we will create a custom command that runs our script.

- This requires a bit of knowledge of what happens behind the scenes when you run a command and a built-in variable called the `PATH` variable.

Explain that in this demonstration you will describe what the `PATH` variable is and how to customize it in order to create scripts that become your own custom commands.

#### PATH Demonstration

Log into the lab environment with the username `sysadmin` and password `cybersecurity`.

- Open up a terminal and return to your home folder.

Explain that we know that every command we type is actually a program that runs. Those programs are stored in various directories like `/bin` and `/usr/bin`.

Ask the students the following questions:

- "When you type a command, how does bash know where that program is located?"  

- "If you were to make a copy of one of those programs and modify it, how would bash know whether to use your new copy or the old one?

Reveal that bash makes this decision by looking at the `$PATH` variable.

- Run `echo $PATH` and show the output:

   ```bash
   $ echo $PATH
   /usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games:/snap/bin:/home/user/.local/bin
   ```

Explain that the sole purpose of this environment variable is to hold a list of directories.

- When you type a command, bash searches through this list for the program in order from left to right.

- When bash finds the program, it uses it and stops searching.

To find our current path, we type `ls`. First, bash searches for the `ls` program in the `/usr/local/bin` directory. If it isn't there, it searches the `/usr/bin` directory and so on down the list.

- If the program is not found in any of the directories in the `$PATH` variable, bash will return 'Command Not Found.'

- Because bash searches these directories in order, if we have 2 versions of a program, bash will run the first one it finds.

- Since `$PATH` is just a variable, we can easily change it. We can add new directories for bash to search, or even remove directories we don't want bash to search.

- If we had a `scripts` directory full of custom scripts we wanted to use as commands, we only need to add that `scripts` directory to our `$PATH` and those scripts can then be run directly.

Demonstrate creating a `scripts` directory and adding it to your `$PATH`:

- Run `mkdir my_scripts`.

- Run `mv sys_info.sh my_scripts/`.

- Run `ls my_scripts`.

Your terminal should resemble:

```bash
$ mkdir my_scripts
$ mv sys_info.sh my_scripts/
$ ls my_scripts
sys_info.sh
```

Point out that now all we need to do is add our `my_scripts` directory to our `$PATH` so that bash will find it when it searches for commands.

Explain that if we want to assign a value to a variable in bash, we use the `VAR=VALUE` syntax.

In this case, to add a directory to our `$PATH`, we want to assign `PATH` to all of the directories it already has, _plus_ our new directory.

- Run `echo $PATH` again.

   ```bash
   $ echo $PATH
   /usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games:/snap/bin:/home/user/.local/bin
   ```

Copy the output with the right click.

- Type `PATH=/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games:/snap/bin:/home/user/.local/bin`.

Add your `my_scripts` directory.

- Type `PATH=/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games:/snap/bin:/home/user/.local/bin:/home/sysadmin/my_scripts`.

Explain that this will overwrite our `$PATH` variable with all of the directories it currently has, plus our new directory.

Point out that to make this easier, we can use the `$PATH` variable instead of copying its contents.

- Run `PATH=$PATH:/home/sysadmin/my_scripts`.

- Run `echo $PATH`.

You should see your appended path to the output:

```bash
$ echo $PATH
/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games:/snap/bin:/home/user/.local/bin:/home/sysadmin/my_scripts
```

Now run `sys_info.sh` directly:

```bash
$ sys_info.sh
```

Explain that if we wanted to make this a shorter command, we can shorten the length of the script name.

- Run `cd my_scripts`.

- Run `mv sys_info.sh sys`.

- Run `sys`.

Ask if there are any questions about creating a custom command or editing the `$PATH` variable.

#### Saving PATH to our `.bashrc`

Explain that just like creating aliases, variables are only good like this for the duration of our session. Once your window is closed, your `$PATH` will return to its default.

Explain that it is best practice to backup your `.bashrc` file before making any changes!

```bash
cp ~/.bashrc ./bashrc.bak
```

Explain that the good news is that we can save the path `PATH=$PATH:/home/sysadmin/my_scripts` to our `.bashrc`.

- Type `echo "PATH=$PATH:/home/sysadmin/my_scripts" >> ~/.bashrc`.

Point out that this is exactly how we added aliases to our .bashrc previously.

- Run `nano .bashrc`.

- Move to the bottom of the file and enter the new PATH variable.

   ```bash
   export PATH=$PATH:/home/sysadmin/my_scripts
   ```

Explain that here we want to use `export` to make this variable to _all_ processes across the system. If you don't use `export`, your `$PATH` variable may not always work.

Save and quit `nano`.

- Run your alias for reloading the .bashrc file.

- Run `rr`.

- Run `echo $PATH` to show your updated PATH.

Point out that creating custom scripts that you can use as custom commands like this is a valuable and useful skill to have at the command line. In the next activity, students will have a chance to do this on their own machine.

[<- Back to Module Contents](LessonPlan.md#module-day-1-contents)

---

### 12. Student Do: Custom Commands (0:20)

Explain the following to students:

- In the previous activity, you created your first bash script that contained a series of commands. This system audit script should prove helpful in saving you time during your audits.

- Now, we will continue to make this script more complex by adding a few commands from the first exercise.

- Then, you will save this script to a `scripts` directory and add that directory to your `$PATH` so you can call your script directly on the command line, from any directory.

Send the following files to students:

- [Activity File: Custom Command](Activities/12_Custom_Commands/Unsolved/Readme.md)

[<- Back to Module Contents](LessonPlan.md#module-day-1-contents)

---

### 13. Instructor Do: Custom Commands Review (0:10)

:bar_chart: Run a comprehension check poll before reviewing the activity. 

This activity turned our script into a custom command and added a script directory to the `$PATH` so that command can be called directly.

To complete this activity, they needed to do the following:

- Ensure that the script from the last activity runs as expected.

- Add the new commands listed in the instructions.

- Save the script in a ~/scripts directory.

- Add that ~/scripts directory to the `$PATH` variable.

- Run your script by calling its name only.

Use the following file to guide you through the review:

- [Solution Guide: Custom Command](Activities/12_Custom_Commands/Solved/Readme.md)

Answer any questions from the students before dismissing class.

[<- Back to Module Contents](LessonPlan.md#module-day-1-contents)

---

© 2023 edX Boot Camps LLC. Confidential and Proprietary. All Rights Reserved.
