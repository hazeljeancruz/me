---
title:	'Subtle difference between FreeBSD, MacOSX and Linux printf'
author: "Wojciech Adam Koszek"
klayout: post
description: >
  Things you'll find when you try to write a substitute for one of the most
  basic and rudimentar pieces of UNIX C API. Treat it as "lessons learned"
  from implementing `mini_printf`.
address: "Menlo Park, CA"
tags:
- "software engineering"
- "freebsd"
read:	2015-10-28
published: true
image: http://layered.typepad.com/antidote_to_burnout/images/2007/10/06/4b14310b020017cf.gif
keywords:
- programming
- development
- printf
- unix
ads:
-
spellcheck-allow:
- "refactored"
- "repeatability"
- "testbench"
- "PRNG"
---

I'm working on polishing my `mini_printf` implementation and making a final,
verified and documented code release, and the thing I made work in the past
and something that stopped working when I moved to MacOSX was a randomized
stress-test.

[https://github.com/wkoszek/mini_printf](https://github.com/wkoszek/mini_printf)

It's pretty neat: it uses its own PRNG generator to achieve repeatability
and uses its numbers to construct randomized format strings which are then
played against OSes `printf()` and my `mini_printf()` API. Both versions are
later compared. I exposed a lot of bugs in `mini_printf` that way, of which
all have been fixed.

So anyway: I refactored `mini_printf` to the state where I can show it to
other people. I also made the stress-test work on MacOSX, and I could play
1,000,000 random format string patterns with 0 failures in couple of
seconds. But the same code failed miserably on Linux. 

It looks like my stressing testbench found a usability problem between
Linux and MacOSX printf. Problem shows up when you decide to use
unsupported format string specifier. While Linux leaves the `%` signs,
MacOSX doesn't propagate them to the string. I guess I'll have to find a way
to elegantly solve it, and preferably without any `#defines`.

## Program


	wk:/w/repos/mini_printf> cat p.c
	#include <stdio.h>

	int
	main()
	{
		printf("%k%k%k\n");
	}

## Linux

	vagrant@vagrant-ubuntu-trusty-64:/vagrant/mini_printf$ ./p
	%k%k%k

## MacOSX and FreeBSD
	wk:/w/repos/mini_printf> ./p
	kkk
