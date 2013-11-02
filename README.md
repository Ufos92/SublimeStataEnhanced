# Sublime Stata 13

* Version 1.0.0
* Date: November 1, 2013

This package basic support for Stata and comes with:

* (*All versions of Stata*) Language definition for `.do` and `.ado` files 
* (*Stata 13, OS X only*) A build system for Stata files
* (*Stata 13, OS X only*) The following command (available via the command palette and with keyboard shortcuts):
	* Send current line or selection to Stata: `super+enter`


## Background

This is a modified version of [Steve Harris's Stata package](https://github.com/docsteveharris/stata). Because of scripting limitations in Stata < 12, his version relied on creating temporary `.do` files to pass commands to Stata. Stata 13 added fancy new AppleScript commands (specifically `DoCommand` and `DoCommandAsync`) that allow for scripted commands and eliminate the need for temporary files. Because of that, this package is far simpler and than other Sublime Text packages.


## Known issues

* This package is hardcoded to use StataSE. If your version of Stata in `/Applications/` is named something else ("Stata", "StataMP", "StataIC", etc.), you'll need to change the name from "StataSE" in two places:
	* `Stata.sublime-build`
	* `text_2_stata.py`
* Stata *really* hates running comments in the command window. Inline comments like `*`, `\\`, and `\* ... \*` will often result in errors when running lines individually. This is a limitation with Stata. Comments are allowed in `.do` files, but not really in the command window (see [this](http://www.stata.com/statalist/archive/2010-12/msg00372.html)). So skip commented lines if you run lines individually.


## Roadmap and wish list

* This only works on OS X since all commands rely on `osascript`. Adding Windows support would be cool (Stata 13 on Windows [has support for automation APIs](http://www.stata.com/automation/)).
* Using a package-wide variable for the name of Stata (e.g. "StataSE") would be nice as well, eliminating the need to manually edit the plugin.
* In the build file, the `osascript ...` command works, but gives the following error: `error "No result was returned from some part of this expression." number -2763`. The plugin currently fixes that by wrapping the command in `try` and `end try` commands. It would be nice to not have to do that, though.