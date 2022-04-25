# Debugging Techniques

## By: Adhithya Ananthan
In this blog post I will examine how I used java debugger and JUNIT to fix bugs I had with the program MarkdownParse.java. This program takes a markdown file as an input and returns the links of a markdown file as the output. During the week 3 and 4 labs our lab team was tasked with fixing the initial file to be able to accomdate for various edge cases. I will further explain 3 of the edge cases we fixed in this blog post.

---

## Memory Overload

![](/lab2report-files/Symptom1.png)

The first symptom that was tackled was a memory overload. The file that caused this error can be viewed [*here*](/lab2report-files/myFile1.md). This symptom occured due to the extra empty lines after the links. To fix this issue I used the java debugger to see the values of each index as it goes through the while loop. I found out that the program causes an infinite loop because when parsing at the end of the input string (markdown) openBracket eventually gets a value of -1. To fix the issue I added an if statement which causes the program to break out of the while loop when openBracket equals -1. The change can be viewed below. 

![](/lab2report-files/Symptom1Fix.png)

---

## When end ")" is removed

![](/lab2report-files/Symptom2.png)

This symptom occurs when the end ")" is removed from the link. It results in an incorrect output of printing multiple links. The file that caused this error can be found [*here*](/lab2report-files/myFile2.md). This error occurs because the program finds the next end bracket which is on the next link. It then gets the entire string and adds it to the list. To fix this issue I decided to add an if statement where it only adds the link if the substring between openParen + 1 and closeParen does not have parentheses and brackets. Doing so elimanted the invalid links in the markdown files. The changes can be found below. 

![](/lab2report-files/Symptom2Fix.png)

---

## Text Between Markdown Links

![](/lab2report-files/Symptom3.png)

This symptom occurs when there is text between the "]" and "(" of a link in a markdown file. The file that caused this error can be found [*here*](/lab2report-files/myFile3.md). In theory it should not print out the link since there is text between the two strings therefore making it an invalid string. This error occured because the program searches for the next "(" after the "]" instead of checking to see if "(" occurs right after "]". In order to fix this issue I added an if statement to see if closeBracket + 1 does not equal openParen. If it doesn't the program will break out of the while loop. Doing so prevented any invalid links from being read and caused the program to stop reading the file. The changes can be found below. 

![](/lab2report-files/Symptom3Fix.png)

---

# Wrapup

Debugging a program is a very important aspect of the programming process. In these labs I was able to gain a better understanding of debugging programs. Using tools like JUNIT and java debugger can help us deal with various edge cases and improve our programs. 