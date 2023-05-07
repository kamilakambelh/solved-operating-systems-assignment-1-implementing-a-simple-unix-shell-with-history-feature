Download Link: https://assignmentchef.com/product/solved-operating-systems-assignment-1-implementing-a-simple-unix-shell-with-history-feature
<br>
This project consists of designing a <strong>C program</strong> to serve as a shell interface that accepts user commands and then executes each command in a separate process. This project can be completed on any Linux, UNIX, or Mac OS X system. A shell interface gives the user a prompt, after which the next command is entered. The example below illustrates the prompt <em>osh&gt;</em> and the users next command: <em>cat prog.c</em>. (This command displays the file <em>prog.c</em> on the terminal using the UNIX <em>cat</em> command.)

One technique for implementing a shell interface is to have the parent process first read what the user enters on the command line (in this case, <em>cat prog.c</em>), and then create a separate child process that performs the command. Unless otherwise specified, the parent process waits for the child to exit before continuing. However, UNIX shells typically also allow the child process to run in the background, or concurrently. To accomplish this, we add an ampersand <em>(</em><em>&amp;)</em> at the end of the command. Thus, if we rewrite the above command as <em>osh&gt; cat prog.c &amp;</em>

the parent and child processes will run concurrently. The separate child process is created using the <em>fork() </em>system call, and the users command is executed using one of the system calls in the <em>exec()</em> family (as described in the textbook). A <strong>C</strong> program that provides the general operations of a command-line shell is supplied in section 3 below. The main() function presents the prompt <em>osh&gt;</em> and outlines the steps to be taken after input from the user has been read. The <em>main()</em> function continually loops as long as should_run equals 1; when the user enters exit at the prompt, your program will set should_run to 0 and terminate.

This project is organized into two parts: (1) creating the child process and executing the command in the child, and (2) modifying the shell to allow a history feature.

<h1>1.         Creating a Child Process</h1>

The first task is to modify the main() function in the skeleton program shell.c (see below) so that a child process is forked and executes the command specified by the user. This will require parsing what the user has entered into separate tokens and storing the tokens in an array of character strings (args in shell.c). For example, if the user enters the command ps -ael at  the osh&gt; prompt, the values stored in the args array are:

args[0]  =  “ps” args[1] = “-ael” args[2]

= NULL

This args array will be passed to the execvp() function, which has the following prototype: execvp(char *command, char *params[]);

Here, command represents the command to be performed and params stores the parameters to this command. For this project, the execvp() function should be invoked as execvp(args[0], args). Be sure to check whether the user included an &amp; to determine whether or not the parent process is to wait for the child to exit.

<h1>2.         Creating a History Feature</h1>

The next task is to modify the shell interface program so that it provides a history feature that allows the user to access the most recently entered commands. The user will be able to access up to 10 commands by using the feature. The commands will be consecutively numbered starting at 1, and the numbering will continue past 10. For example, if the user has entered  35 commands, the 10 most recent commands will be numbered 26 to 35. The user will be able to list the command history by entering the command history at the osh&gt; prompt.  As  an example, assume that the history consists of the commands (from most to least recent):  ps, ls -l, top, cal, who, date The command history will output:

6 ps

5 ls -l

4 top

3 cal

2 who

1 date

Your program should support two techniques for retrieving commands from the command history:

<ol>

 <li>When the user enters !!, the most recent command in the history is executed.</li>

 <li>When the user enters a single ! followed by an integer N, the Nth command in the history is executed.</li>

</ol>

Continuing our example from above, if the user enters !!, the ps command will be performed; if the user enters !3, the command cal will be executed. Any command executed in this fashion should be echoed on the users screen. The command should also be placed in the history buffer as the next command. The program should also manage basic error handling. If there are no commands in the history, entering !! should result in a message No commands in history. If there is no command corresponding to the number entered with the single !, the program should output ”No such command in history.”

<h1>3.         shell.c</h1>

/* Name:

ID:

Teammate name(s):

*/

#include &lt;stdio.h&gt;

#include &lt;unistd.h&gt;

#define MAX LINE 80 /* The maximum length command */ int main(void){ char *args[MAX LINE/2 + 1]; /* command line arguments */ int should run = 1; /* flag to determine when to exit program */ while (should run) { printf(“osh&gt;”); fflush(stdout);

/**

<ul>

 <li>After reading user input, the steps are:</li>

 <li>(1) fork a child process using fork()</li>

 <li>(2) the child process will invoke execvp()</li>

 <li>(3) if command included &amp;, parent will not invoke wait() * (4) if command is quit, the shell should exit</li>

 <li>Explain your steps as comments in the code itself.</li>

</ul>

*/ } return 0; }