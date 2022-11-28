# Week 9 Lab Report - Grading Script

## **Grading Script Used**

```
set -e

rm -rf student-submission
git clone $1 student-submission

FILE="student-submission/ListExamples.java"

if [ -f "$FILE" ]
then
    echo "$FILE does exist."
else
    echo "$FILE does not exist."
    echo "Grade: 0 points"
    exit
fi


cp TestListExamples.java ./student-submission

set +e

javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar student-submission/*.java 2> error.txt

set -e

if [ -s error.txt ]
then
    echo "$(cat error.txt)"
    echo "Did not compile, Grade: 0 points"
        exit
fi

set +e

cd ./student-submission
java -cp .:../lib/hamcrest-core-1.3.jar:../lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples > testerror.txt    


echo "$(cat testerror.txt)"

grep -i "failure" testerror.txt > grep.txt

set -e

if [ -s grep.txt ]
then
    echo "Failed tests, so Grade: 0 points"
    exit
else
    echo "Grade: Full Points!"
    exit
fi
cd ..
```

## Three Examples of Using Grading Script

![image](/images/lab5fullpoint.png)

![image](/images/lab5nocompile.png)

![image](/images/lab5testfail.png)

## **Script Trace**
The student submission used was https://github.com/ucsd-cse15l-f22/list-methods-signature

*Note: [] means there was no stdout/stderr*

Line 1: `set -e`
* Stdout: `[]`
* Stderr: `[]`
* Exit Code: 0

Line 2: `rm -rf student-submission`
* Stdout: `[]`
* Stderr: `[]`
* Exit Code: 0

Line 3: `git clone $1 student-submission`
* Stdout: `[]`
* Stderr: `Cloning into 'student-submission'...`
* Exit Code: 0

Line 4: `if [ -f "$FILE" ]`
* For this if statement, the condition is true because `-f` checks for if `ListExamples.java` file exists within `student-submission/`. It does exist, so the condition is true.

Line 6: `echo "$FILE does exist."`
* This runs in the `then` branch of the if statement
* Stdout: `student-submission/ListExamples.java does exist.`
* Stderr: `[]`
* Exit Code: 0

Line 12: `cp TestListExamples.java ./student-submission`
* Stdout: `[]`
* Stderr: `[]`
* Exit Code: 0

Line 13: `set +e`
* Stdout: `[]`
* Stderr: `[]`
* Exit Code: 0

Line 14: `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar student-submission/*.java 2> error.txt`
* Stdout: `[]`
* Stderr: `student-submission/TestListExamples.java:18: error: incompatible types: List<String> cannot be converted to StringChecker      
        String s = ListExamples.filter(strs, new ContainsDStringChecker()).get(0);
                                       ^
Note: Some messages have been simplified; recompile with -Xdiags:verbose to get full output
1 error`
* Exit Code: 1

Line 15: `set -e`
* Stdout: `[]`
* Stderr: `[]`
* Exit Code: 0

Line 16: `if [ -s error.txt ]`
* For this if statement, the condition is true because `-s` in this case checks to see if the contents of `error.txt` are not empty. Since there is a compile error, `error.txt` is not empty.

Line 18: `echo "$(cat error.txt)"`
* This runs in the `then` branch of the if statement.
* Stdout: `student-submission/TestListExamples.java:18: error: incompatible types: List<String> cannot be converted to StringChecker
        String s = ListExamples.filter(strs, new ContainsDStringChecker()).get(0);
                                       ^
Note: Some messages have been simplified; recompile with -Xdiags:verbose to get full output
1 error`
* Stderr: `[]`
* Exit Code: 0

Line 19: `echo "Did not compile, Grade: 0 points"`
* This runs in the `then` branch of the if statement.
* Stdout: `Did not compile, Grade: 0 points`
* Stderr: `[]`
* Exit Code: 0

Line 20: `exit`
* This runs in the `then` branch of the if statement.
* Stdout: `[]`
* Stderr: `[]`
* Exit Code: 0
