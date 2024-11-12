# Linux-Process-API-fork-wait-exec-
Ex02-Linux Process API-fork(), wait(), exec()
# Ex02-OS-Linux-Process API - fork(), wait(), exec()
Operating systems Lab exercise
## REG NO:212223040029
# NAME: T DANUSH REDDY

# AIM:
To write C Program that uses Linux Process API - fork(), wait(), exec()

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux Process API - fork(), wait(), exec()

### Step 3:

Test the C Program for the desired output. 

# PROGRAM:
## C Program to print process ID and parent Process ID using Linux API system calls :
#include <stdio.h>
#include <sys/types.h>
#include <unistd.h>
int main(void)
{	      
	       pid_t process_id;
	    
	       pid_t p_process_id;
	      
      process_id = getpid();
	      
	       p_process_id = getppid();
	     


	      printf("The process id: %d\n",process_id);
	      printf("The process id of parent function: %d\n",p_process_id);
	      return 0; 
}



















##OUTPUT
![image](https://github.com/user-attachments/assets/62afe0a8-8f63-42a9-a6ef-aeaae493cbbf)














## C Program to create new process using Linux API system calls fork() and exit():
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
int main() {
    int pid;
    pid = fork();
    if (pid == -1) {
        perror("fork");
        exit(EXIT_FAILURE);
    }
    else if (pid == 0) {
        printf("I am child, my pid is %d\n", getpid());
        printf("My parent pid is: %d\n", getppid());
        exit(EXIT_SUCCESS);
    }
    else {
        printf("I am parent, my pid is %d\n", getpid());
        sleep(100);
        exit(EXIT_SUCCESS);
    }
    return 0;
}



##OUTPUT


![image](https://github.com/user-attachments/assets/ff5c10da-5b2a-4765-8c32-f823546effc4)

## C Program to execute Linux system commands using Linux API system calls exec() family:

#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>
int main() {
    pid_t pid = fork();
    if (pid < 0) {
        perror("Fork failed");
        exit(EXIT_FAILURE);
    } else if (pid == 0) {
        printf("This is the child process. Executing 'ls' command.\n");
        execl("/bin/ls", "ls", "-l", NULL); // Lists files in long format
        perror("execl failed");
        exit(EXIT_FAILURE);
    } else {
        int status;
        waitpid(pid, &status, 0); // Wait for the child to finish
        if (WIFEXITED(status)) {
            printf("Child process exited with status %d.\n", WEXITSTATUS(status));
        } else {
            printf("Child process did not exit normally.\n");
        }
        printf("Parent process is done.\n");
    }
    return 0;
}


##OUTPUT

![image](https://github.com/user-attachments/assets/71439880-9868-4ef4-949a-1e63aa4b74ce)


# RESULT:
The programs are executed successfully.
