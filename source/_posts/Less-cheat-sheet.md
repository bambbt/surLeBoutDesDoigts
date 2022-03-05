---
title: Less cheat sheet
date: 2022-03-05 14:12:45
tags : [Terminal, Shell, Cheat sheets]
categories:
 - [Unix, Command]
---


**less** is a command line utility that displays the contents of a file or a command output, one page at a time. It is similar to **more**, but has more advanced features and allows you to navigate both forward and backward through the file.

**less** loading time is faster because it does read the whole file before display it like an editor like nano, vim would do it.
So it is recommended to use it with large files. Like application logs etc..

To use it type in:

``less [OPTIONS] filename``

Here some command that can be used while less is displaying the content of a file.


Search  | |
--------|---------------------------------------------------------------------
```/``` | search for a pattern which will take you to the next occurrence.
```?``` | search for a pattern which will take you to the previous occurrence.
```n``` | for next match in forward
```N``` | for previous match in backward

Navigation    | |
--------------|--------------------------------------------------------------
```SPACE```   | forward one window
```b```       | backward one window
```d```       | forward half window
```u```       | backward half window
```j```       | navigate forward by one line
```10j```     | 10 lines forward.
```k```       | navigate backward by one line
```10k```     | 10 lines backward.
```G```       | go to the end of file
```g```       | go to the start of file
```q or ZZ``` | exit the less pager

Other          | |
---------------|-----------------------------------------------------------------
```F```        | simulate tail -f inside less pager
```ma```       | mark the current position with the letter ‘a’,
```‘a```       | go to the marked position ‘a’.
```&pattern``` | display only the matching lines, not all.
```v```        |using the configured editor edit the current file.
```CTRL+G```   |  show the current file name along with line, byte and percentage statistics.
