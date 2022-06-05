# Using VIMDIFF

## By Adhithya Ananthan

In this post I will explain how I used the vimdiff command to find differences in the outputs of two implementations of markdownparse. vimdiff is very helpful for being able to notice differencees between files without having to manually look through them.

---

In lab 9 we created two results.txt files, one containing the outputs for the TA's implementation of markdown parse and anothere containing our group's implementation of markdown parse. We can use vimdiff to compare the two files. 

![](/cse15l-lab-reports/labreport5-screenshots/vimdiff.png)

Above we can see what vimdiff looks like when comparing the two files. From this we can see that the test case for 32.md and 342.md are different. 

[Link for 32.md](https://github.com/adhi0331/cse15l-lab-reports/blob/main/labreport5-screenshots/32.md)

[Link for 342.md](https://github.com/adhi0331/cse15l-lab-reports/blob/main/labreport5-screenshots/342.md)

Lets dive into each test case

---
## Test 32.md

From looking at the [Common Markdown Site](https://spec.commonmark.org/dingus/) we can see that the expected out is...

```
[]
```

Lets compare each implementation's output

![](/cse15l-lab-reports/labreport5-screenshots/running32mine.png)

This is our groups implementation.

![](/cse15l-lab-reports/labreport5-screenshots/running32tutor.png)

And this is the TA's implementation.

From these pictures we can see that our group's implementation is incorrect and TA's is correct. Though Markdown highlights "foo" to be a link, the link is not a valid link hence it should be included in the output. Let's look at what needs to be added to the groups MarkdownParse.java to fix the error.

![](/cse15l-lab-reports/labreport5-screenshots/32fix.png)

In this long if block we see that we did not check to see if the link contains ". This is what causes the program to add a link when it shouldn't. Adding a statement such as `link.contains("\"")` will make sure the invalid link does not get added. Also, we could make this if block a function called `isValid()` which will return a boolean based on whether the link is valid.

---
## Test 342.md

We can see that the exepcted output is

```
[]
```
from looking at [Common Markdown Site](https://spec.commonmark.org/dingus/) .

Lets compare the two implementations one more time.

![](/cse15l-lab-reports/labreport5-screenshots/running342mine.png)

This is our group's implementation.

![](/cse15l-lab-reports/labreport5-screenshots/running342tutor.png)

And this is the TA's implementation.

We can see that the roles reversed this time. The TA's implementation was incorrect as it returned a link, whereas our group's implementation was correct. Let's see what needs to be fixed in the TA's MarkdownParse.java.

![](/cse15l-lab-reports/labreport5-screenshots/342fix.png)

It seems that this if statement does not check whether backticks are in the potential link. This is why the program adds the link to the list when it shouldn't. A potential fix would be to add some statement to ensure backticks are not in the link similar to the other ones used in the if statement. 


---
## Conclusion

In conclusion, vimdiff is very helpful in finding differences between files. In this cases we were able to find differences in outputs for over a thousand of test cases. Such skill will be important in the real worold where we might need to compare files efficiently.



