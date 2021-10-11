# MSDS610
​
This repository will show you how to efficiently use the terminal to quickly summarize data without having to write a python script or open jupyter notebook.
​
​
### Introduction
As data scientists, we spend a lot of time trying to understand and work with data.  We need quick ways to preview data or make it easier to work with, and this is where streams come in handy.  Streams are input and output connections between a program and its environment.  Using streams is a way to combine commands together to make more  powerful commands so data can be quickly analyzed.
​
This repository will discuss the 3 main components of streams:  Standard Input, Standard Output, and Standard Error; then, it will summarize these concepts through an example.
Redirection refers to a stream is controlled.  A stream can be reirrected to achieve different results.
​
​
### Standared Input
Standard input stream carries data from a user to a program.  When standard input stream is not redirected, it will read input from the terminal.  
​
To redirect standard input, use the '<' symbol.  The example below redirects the input to the cat command to use the text file 'foo.txt' instead of standard input.
EX:  <code>$ cat \< foo.txt</code>
​
​
### Standard Output
Standard output writes data generated by a program or a command. When the standard output stream is not redirected, it will output text to the terminal.
​
To redirect standard output, use the '>' symbol. The example below redirrects the output of ls to a file 'bar.txt' instead of the default output in the terminal.
EX:  <code>$ ls > bar.txt</code>
​
​
## Frequently used commands
Now, we are going to introduce a few common terminal commands and show some examples to get started using streams and I/O redirection.
<code>$ wc output.csv</code>
​
The | symbol is used to pass the standard output of one program to the standard input of another program.
<code>$ grep 'sales' output.csv | wc </code> 
​
What if we want to save the result of the command to a file?  Use redirection!
<code>$ grep 'sales' output.csv | wc > result.txt </code>  
​
​
### Standard Error
Standard error is where errors are written that are generated by a failed program.  Similar to standard output, the default output for standard error is the terminal.
​
<code>$ pdftotext test.txt > greatness.txt </code>  
​
​
### Streams and Redirection with csvkit
To combine some of the items discussed above, I will walk through a longer example of using a stream with csvkit.  
​
To install and get started with csvkit, which is a program that can be used to process csv files using UNIX commands, use brew install.<code>$ brew install csvkit</code>
​
<code>csvcut -c 3 -e latin1 file.csv | tail +2 | sort | uniq -c | sort -r -n | head -5 > out.txt</code>
​
Here are the steps to walk through this long command stream:  
1.  There are 3 starting arguments passed into the csvcut command.  
    -  -c 3: tells csvcut to look at 3rd column of csv file
    - -e latin1: tells csvcut to use ‘latin 1’ encoding
    - file.csv:  is the input csv file
2.  The output of #1 is then piped into the tail command; 'tail +2' tells the program to start at the 2nd row of the file and go to the end
3.  The output of #2 is then piped into the sort command; the results are sorted in ascending order by default.
4.  The output of #3 is then piped into the unique command; 'unique -c' eliminates duplicates and returns unique results with a count added.  (Note, the -c is the argument to add the count.)
5.  The output of #4 is then piped into another sort command.  This time 'sort -r -n' includes arguments to sort in reverse order by number.  In this case the sorting will be based on the count added in the previous step with the 'unique -c' command.
6.  The output of #5 is then piped into the head command to get the top 5 results.
7.  The final step redirects the output to a txt file to save for easy reference later.
