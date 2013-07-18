---
layout: post
title: "Emacs reminder"
categories: [coding, emacs]
tags: [emacs, nifty]
---
{% include JB/setup %}

I find myself doing branches from tags released by the maven plugin on a parent pom.
This requires that I do the update from the released <version>x.y</version> to <version>x.y.z-SNAPSHOT</version>
on all sub-poms of the maven project.

Small emacs to take all pom.xmls from current directory and replace the version in all of them

>M-x find-name-dired RET
Enter directory to search
>\[directory\]
Enter file pattern
>pom.xml

* Press 't' to mark all found files

* Press 'Q' to perform query-replace on all marked files

* Proceed as normal query-replace, press Y to perform change on all files without further prompting