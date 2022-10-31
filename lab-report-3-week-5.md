# Week 5 Lab Report - Researching Commands

## Grep Commands

### **-c Option**

![!image](/images/grep-c1.png)

* In this first example, `-c` is being used to count the number of instances of the word `"emergency"` in the files of the `technical/911report` directory.
* This would be useful to collect useful information or data on how many times a certain keyword appears in a selection of text files. 

![image](/images/grep-c2.png)

* In this second example, the input is the same as the first example, but with the addition of the `-i` option.
* This ignores the case of the word provided to grep, which would often be useful to more accurately count the number of instances of a word, as it would account for capitalized words at the beginning of sentences.

![image](/images/grep-c3.png)

* In this third example, the `-c` command is used to search for the number of instances of the word `"mission"` in the files of the `technical/911report` directory.
* This shows another way `-c` could be useful for finding files that are of interest based on a keyword. For example, `technical/911report/chapter-13.5.txt` has 111 instances of the word `"mission"`, which may be of interest.

### **-C n Option**

![image](/images/grep-Cn1.png)

* In this first example, the `-C n` option is being used to print out lines containing the word `"emergency"` in addition to 1 line before that and 1 line after that. In this case, the `n` represents the number of lines before and after the line containing the search.
* This would be useful to gain context for the appearance of a word in a body of text. 

![image](/images/grep-Cn2.png)

* In this second example, the same command as above is used, but with the addition of the `-n` option, which states the line numbers of the lines that are outputted.
* This is useful because in addition to seeing the line containing the search and 1 line before and after, you can also see their line numbers, which can be used to quickly find them inside the actual text file. 

![image](/images/grep-Cn3.png)
* In this third example, `-C n` and `-n` are being used with the addition of `-w` in order to only search for exactly the word used for `grep`.
* This is useful because otherwise, `-C n` may print out too many unnecessary lines that do not match the search. 

### **Using -R With grep**

![image](/images/grep-R1.png)

* In this first example, `-R` is being used with `grep` in order to recursively travel through the directory `technical/911report/` for the word `"emergency"`.
* This is useful, as being able to recursively travel through a directory allows you to broadly search through all files and subdirectories inside the directory used for the search. 

![image](/images/grep-R2.png)
* In this second example, `-R` is once again used, but with `-c` added to the end to search for the number of times `"origin"` appears in the directory `technical/government`.
* This shows another reason why `-R` is useful since `technical/government` contains many subdirectories.

![image](/images/grep-R3.png)
* In this third example, `-R` is used with `-w` while the current directory is set to `technical`.
* This is useful since it allows grep to search through the entirety of `technical` for the word `"origin"` without having to specify a specific directory or pattern.
