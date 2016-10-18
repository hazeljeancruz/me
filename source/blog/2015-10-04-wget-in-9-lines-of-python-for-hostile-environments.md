---
title:	'wget in 9 lines of Python For Hostile Environments'
author: "Wojciech Adam Koszek"
abstract:
address: "Menlo Park, CA"
description: "wget implementation for environments such as Synology DSM distribution, where wget doesn't have HTTPS support."
tags:	article
read:	2015-10-05
published: true
layout:	layout_book
ads:
- 
spellcheck-allow:
- "github"
- "synology"
- "Gists"
---

HTTPS seems to be everywhere these days, including GitHub. It’s great to
see the security of the Web improved, but sometimes this comes at a
cost. Recently I wanted to actually fetch and test my own repository for
bootstrapping my storage box from Synology:

[https://github.com/wkoszek/synology](https://github.com/wkoszek/synology)

The DS214play model which I have comes with the `wget` program without
HTTPS, so doing a command line bootstrapping is difficult. This is one
of this weird chicken-and-egg problems we sometimes experience, and to
test my software releases published on GitHub, I wrote this simple
thing, which lets me fetch the release and do further bootstrapping and
testing:

<script src="https://gist.github.com/wkoszek/48b4ac725664d324c9d5.js"></script>

Oh, and GitHub Gists are HTTPS too, so to actually get it, I had to
transfer the content through PasteBin;

~~~shell
wget -O - 'http://pastebin.com/raw.php?i=PcbNtyh9' | tr 'r' ' ' > wget2
chmod 755 wget2
./wget2 https://github.com/wkoszek/synology/archive/0.0.4.zip
~~~

Why like that? Well in the middle of testing it, I learned that:
[Pastebin adds DOS new-line separators at the end snippets](http://www.koszek.com/blog/2015/10/05/pastebin-adds-dos-newline-on-snippet/)
