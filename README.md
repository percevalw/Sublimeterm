SublimeTerm
===========

[![Build Status](https://travis-ci.org/percevalw/Sublimeterm.svg?branch=master)](https://travis-ci.org/percevalw/Sublimeterm) [![codecov](https://codecov.io/gh/percevalw/Sublimeterm/branch/master/graph/badge.svg)](https://codecov.io/gh/percevalw/Sublimeterm)

*STILL IN DEVELOPMENT*

SublimeTerm is a plugin for Sublime Text that allows you to run a shell in your editor.

VI and other readline-intensive programs (iPython, PSQL, ...) should run fine.

![](https://raw.githubusercontent.com/percevalw/Sublimeterm/master/doc/demo.gif)

## How does it work ?

This plugin acts as a standard [terminal emulator](https://en.wikipedia.org/wiki/Terminal_emulator). It is is highly multi-threaded, to avoid blocking SublimeText while waiting for the shell 'answer'. The communication with the process is made using [standard streams](https://en.wikipedia.org/wiki/Standard_streams) and Python's subprocess library.

**Input**

When you write something to the screen, the diff between the old and the new content is detected through analysis of the cursor position.

This input is translated into [ANSI Control Sequences](https://en.wikipedia.org/wiki/ANSI_escape_code) (ex: backspace becomes \x08 character, up-arrow becomes \x08[A etc) and sent to the shell (or any other program we want to communicate with) using the standard input.


**Output**

Once the program has finished processing our input, it replies using the standard output and error channels with other ANSI Control Sequences. Those are way more complicated than the input since they control color, cursor position, line-erasals etc.

Actually, they can be decoded using a [finite state machine](https://en.wikipedia.org/wiki/Finite-state_machine) and translated to actions to do in the tab. Those actions are in fact run on a virtual screen, whose content is diffed to only correct on the real screen what has really changed. We could replace the whole screen every time the program replies one of our input but this would make the user experience way slower.

## What is next ?
There is no roadmap for this project.

Colors are still missing but I'm working on it.

Some parts are still a bit to slow to offer a seamless terminal emulation to the user. C can be a good option to speed these up a bit.