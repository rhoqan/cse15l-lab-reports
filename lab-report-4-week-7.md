# Week 7 Lab Report - Vim

## **Part 1**

**The task that I chose was the first task given:**

*In `DocSearchServer.java`, change the name of the `start` parameter of `getFiles`, and all of its uses, to instead be called `base`.*

**The series of keystrokes used to perform this was:**

`:%s/start/base/gc<Enter>yyyn` 

![image](/images/Vimlab1.png)

* The above image showcases the command that was used, which is `:%s/old/new/gc`, where `old` is the word that you want to replace with `new` at each location that it can be found.

* Here, the `gc` at the end indicates that you want to confirm each replacement.

* The first location of `start` in `DocSearchServer.java` is highlighted above, which is where the first replacement will happen.

* After typing this out, `<Enter>` is used to execute the command.

![image](/images/Vimlab2.png)

* The above image shows what happens after you press `<Enter>`.

* Text appears on the bottom where the command was typed, prompting whether or not to replace the highlighted word (which is `start`) with `base`.

* Typing any of the options shown will replace the highlighted word.

![image](/images/Vimlab3.png)

* The image above shows that the first appearance of `start` was replaced with `base` after I typed `y`.

* Now, it prompts whether or not to replace the second appearance of `start`.

![image](/images/Vimlab4.png)

* The image above shows that the second appearance of `start` was replaced with `base` after I typed `y`.

* Now, it prompts whether or not to replace the third appearance of `start`.

![image](/images/Vimlab5.png)

* While it is not shown since the cursor jumped to the fourth appearance of `start`, the third appearance of `start` was replaced after I typed `y`.

* Now, it prompts whether or not to replace the fourth and last appearance of `start`.

![image](/images/Vimlab6.png)

* Since replacing the fourth appearance of `start` would make the code for starting the server buggy, I typed `n` to not replace it with `base`.

* There is text at the bottom showing how many substitutions were made and how many lines those occurred on.

## **Part 2**

After performing the same editing task as Part 1 in the two ways suggested, I got the following results:

* Editing in VSCode and then using `scp` and `bash test.sh` took 1 minute and 56 seconds (116 seconds).
* Editing in Vim, saving and exiting, and then using `bash test.sh` took 1 minute and 9 seconds (69 seconds).

The only difficulty that occurred was when I was trying to open the file in Vim. I was prompted about an existing swap file and what I wanted to do with that, which took extra time to resolve.

Regarding the question of which method of editing that I prefer for editing a program that will be run remotely, I would probably prefer using Vim to do so for any tasks similar to this.

The process of using `scp` and `ssh` can be cumbersome, especially if I only need to edit one file. However, if I had a project or task that involved editing multiple files, editing on something like VSCode and then using `git` and GitHub Desktop would probably be more comfortable than using Vim on a remote server.

Overall, my current familiarity with more traditional text editors and IDE's is higher than with Vim, so that decreases my motivation to use it. However, I do find the commands available interesting, and think that they could potentially save significant time in some situations if I got more used to them.

