# Debugging Programs

## By: Adhithya Ananthan
In this blog post I will go over places that I can improve the MarkdownParse program that we have been developing in CSE 15L. This post will look over two versions of MarkdownParse and will examine how it handles three edge cases. 


---
## Repo links

[My Repo Link](https://github.com/adhi0331/markdown-parser)

[Review Group Repo Link](https://github.com/ehsly/markdown-parser)

---

## JUnit Tests
![](/labreport4-screenshots/JunitTests.png)

These test cases were added to both my MarkdownParseTest.java and the group I was reviewing's MarkdownParseTest.java.

---
## Testing On My Implementation
![](/labreport4-screenshots/MyTestResults.png)

This is the terminal output for running the test on my implementation of MarkdownParse

---
## Testing On Review Group Implementation
![](/labreport4-screenshots/ReviewTestResults.png)

This is the terminal output for running the test on the group I was reviewing's implementation of MarkdownParse

---
## Snippet 1
Snippet 1 tested to see if code snippets affected getLinks ability to retrieve the links. From the images above we see that snippet 1 edge cases failed for both implementations. This bug can be fixed with some lines of code. We can get a substring of between the openBracket and closeBracket, then check to see if "`" is contained in the substring. If it is there then we won't add it to the return ArrayList. An example idea of the code is added below.

```
String toCheck = markdown.substring(openBracket, closeBracket);
if (toCheck.indexOf("`") != -1){
    currentIndex = closeBracket;
    continue;
}
```

---
## Snippet 2
Snippet 2 tested to see if any nested links affected the getLinks. Again, both implementations failed to account for this edge case. A fix for this edge cases is similar to the fix for snippet 1. We would have to take a substring from the openBracket and closeBracket, then check to see if there are any open brackets or close brackets within that substring. If there are then set currentIndex to the closeBracket index and continue through the next iteration. An example idea of the code is added below. 

```
String toCheck = markdown.substring(openBracket, closeBracket);
if (toCheck.indexOf("[") != -1 && toCheck.indexOf("]"){
    currentIndex = closeBracket;
    continue;
}
```

---
## Snippet 3
Snippet 3 tested to see if long lines of links and text affected getLinks ability to retrieve the links. Once again, both implementations failed to pass this edge case. Fixing this edge case might take a little more than just adding a couple of lines. There has to be some code that takes two substrings, one for the text inside the brackets and one for text inside the parentheses (the link). Then you would have to add some code that checks to see if there are any line breaks between any of those two substrings. If there aren't then add the link to the return ArrayList. Checking for line breaks may be as simple as importing a method from a java library of having to create a helper method. This is why this fix could be a little more complicated than the others. 