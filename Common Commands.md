#### Common Commands

- grep

Grep is a tool that will find certain patterns or words in one or more files.you can think of grep as the “search” tool built-in to the command line

  ```bash
# Must use sudo because this file is protected
# The -i flag will make my search case insensitive 
sudo grep -i "zach" /etc/passwd # zach:x:1000:1000:Zach,,,:/home/zach:/bin/bash
  ```
  we could also search by a regular expression.
  ```bash
# Must use sudo because this file is protected
sudo grep --color -E "^[a-z]{3}:" /etc/passwd
  ```
 or in this way:
   ```bash
sudo cat /etc/passwd | grep --color -E "^[a-z]{3}:"
  ```
  #### awk and sed
  These tools are considered text editors because they can find and replace parts of a file or files.
  - Sed

  Sed is a “stream editor” (looks at each line character by character).It is great for little find and replace operations across one or more files
  - Awk <br/>
 
  Awk considered a computationally complete programming language and is catered more towards large data that is delimiter separated
  <br/>
 For simple text transformations (like find/replace), use sed. <br/>
 For simple formatting transformations, use awk <br/>
 For complex formatting/text transformations, use awk <br/> <br/>
 I wanted to replace all the commas with spaces instead. <br/>
  
  
  ```bash
  #original data
  #Date,Open,High,Low,Close,Adj Close,Volume
#2018-11-06,201.919998,204.720001,201.690002,203.770004,203.061493,31882900
#If I add the -i flag to the command, it will edit the file.

  sed -i 's/,/ /g' AAPL.csv
  
  #modified data
  #Date Open High Low Close Adj Close Volume
#2018-11-06 201.919998 204.720001 201.690002 203.770004 203.061493 31882900
  ```
     
 we can look to awk to do some better summarization, I just want to see the date, open, and volume. To get that, I can use awk.
  
  ```bash
      #original data
      #Date,Open,High,Low,Close,Adj Close,Volume
      #2018-11-06,201.919998,204.720001,201.690002,203.770004,203.061493,31882900

      awk -F " " ' BEGIN { print "Date\t\tPrice\t\tVolume" }; NR > 1 { print $1 "\t" $2 "\t" $7 } ' aapl.csv

      #modified data
      #Date            Price           Volume
      #2018-11-06      201.919998      31882900

  ```
  
 another way to implementation :
  
 creat a file called awk-example.sh and plac the above command in it with better formatting:
  
  ```bash
       # This is an awk comment
      # Before processing any text, we want to set the FS variable (what our file is separated by), 
      # the OFS variable (what our output is separated by), and then print a header for our output.
      BEGIN {
              # Notice how each line is ended with a semicolon -- similar to C programming language
              FS=" ";
              OFS="\t";
              print "Date\t\tPrice\t\tVolume";
      };# NR > 1 means that we only want to print the following bracket enclosed values for lines that are greater
      # than line 1.  In other words, we are omitting the first line.
      NR > 1 {
              # We want to print the first, second, and seventh value in each line.
              print $1, $2, $7;
      };
  ```
  run this file like so:
   ```bash
# Outputs the same thing as 
# awk -F " " ' BEGIN { print "Date\t\tPrice\t\tVolume" }; NR > 1 { print $1 "\t" $2 "\t" $7 } ' aapl.csv
# This reads the awk-example.sh file and executes it against aapl.csv
awk -f awk-example.sh aapl.csv
  ```
  
  
  
