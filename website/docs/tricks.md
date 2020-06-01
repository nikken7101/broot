
## `dcd` : Deep fuzzy cd

When you want to cd to a deep directory, using `br` is fast and easy enough:

* you type `br` (and `enter`)
* you type the name of the deep folder (or part of it)
* you check the right line is selected
* you do `alt-enter`
* you're done

But when you frequently go to a few specific places, you may prefer a shortcut.

As broot can be driven by commands, you can define this function:

	# deep fuzzy cd
	function dcd {
		br --only-folders --cmd "$1 :cd"
	}

(paste this for example in your .bashrc)

This is the *"I'm feeling lucky"* of broot, you can use it to directly jump to directories you know, when you don't need the interactive search of br.

Example:

![dcd ruleset](../img/20190122-dcd_rulset.png)

## focus a new directory but keep the current filter

When you hit `enter` on a directory, it's focused and the filter is reset.

If you want to keep the filter, for example to search deeper, you may use `:focus` instead.

Similarly, `:back` keeps can be used in place of `esc` to keep the filter when going to the previous state.

## Going from a fixed search to an exact one

Let's assume you type `too` to search for some files. You might have got too many matches including some where the letters aren't consecutive.

You may switch to an exact search by just adding `/`, which changes the fuzzy pattern to a regular expression.

Or if you realize you want to match `tOo` too, then you make it case insensitive by adding an i: `too/i`.

## Run an script or program from broot

If your system is normally configured, just doing `alt`-`enter` on an executable will close broot and executes the file.

## Change standard file opening

When you hit enter on a file, broot asks the system to open the file. It's usually OK but you might wish to change that, for example when you're on a server without xdg-open or equivalent.

Here's an example of configuration changing the behaviour on open:

```toml
[[verbs]]
invocation = "edit"
key = "enter"
execution = "$EDITOR {file}"
apply_to = "file"
```

(the `apply_to` line ensures this verb isn't called when the selected line is a directory)


## Git Status

If you want to start navigating with a view of the files which changed, you may do

    br -gc :gs

Then just hitting the `esc` key will show you the normal unfiltered broot view.

(note: this isn't equivalent to `git status`. Most notably, removed files aren't displayed)

From there you may use the `:gd` verb (`:git_diff`) to open the selection into your favourite dif viewer.