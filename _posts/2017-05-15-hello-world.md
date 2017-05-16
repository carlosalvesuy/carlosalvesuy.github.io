---
layout: post
title:  "Hello World!"
date:   2017-05-15 18:05:25 -0300
categories: hello world
author: "Carlos Alves"
comments: true
---

Hello World! From my new blog.

Let's start with a good ol' code.

```c
#include<stdio.h>
#include<string.h>

void
usage(void)
{
    /* Prints the usage information to the
     * standard error.
     */

    fprintf(stderr, "Usage: ./hello \n");
}


int
main(int argc, char *argv[])
{
    /* Asks for the name of the user and greets it
     * displaying a message in the standard output.
     * If no name is given, displays the default
     * greeting to the standard output.
     */

    char buf[BUFSIZ];

    puts("What is your name? ");

    if (fgets(buf, sizeof(buf), stdin) != NULL)
    {
        // remove trailing \n
        buf[strlen(buf) - 1] = '\0';

        if ( strlen(buf) == 0 )
            puts("Hello stranger!");
        else
            printf ("Hello %s!\n", buf);
    }

    return 0;
}
```
