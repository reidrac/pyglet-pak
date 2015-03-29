Quick and simple way of packaging pyglet games for Linux and Mac.

This is a personal backup; consider the code public domain (all but
the AVBin libraries that are LGPL).

You may need a `__main__.py` (executable) in the root of your game
code. For example:

	#!/usr/bin/env python

	import pyglet
	from game import Main

	if __name__ == "__main__":
		main = Main()
		pyglet.app.run()

And the directory structure would be:

    game/
	pyglet/
	__main__.py

Also you may want to patch pyglet so `resource.get_script_home` returns
the parent directory of the script being run. This is because the file
being run is *inside* a ZIP file and what we want is the actual
directory containing the ZIP file.

You can take that into account when using `resource.get_script_home`, so
why patch pyglet? Because pyglet will try to load avbin from the `lib/`
directory in the same path the script is running, but it won't work if
that's a ZIP file.

You could also fake a frozen app by adding `sys.frozen` property with
value `windows_exe` in your `__main__.py` before importing pyglet; or
anything like that, just check `resource.get_script_home` implementation!

Juan J. Martínez <jjm@usebox.net>

