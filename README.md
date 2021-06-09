filetime_from_git: A Plugin for Pelican
====================================================

[![Build Status](https://img.shields.io/github/workflow/status/pelican-plugins/filetime_from_git/build)](https://github.com/pelican-plugins/filetime_from_git/actions)
[![PyPI Version](https://img.shields.io/pypi/v/pelican-filetime_from_git)](https://pypi.org/project/pelican-filetime_from_git/)
![License](https://img.shields.io/pypi/l/pelican-filetime_from_git?color=blue)

Use Git commit to determine page date

If the blog content is managed by git repo, this plugin will set articles'
and pages' `metadata['date']` according to git commit.

The date is determined via the following logic:

* if a file is not tracked by Git, or a file is staged but never committed
  - metadata['date'] = filesystem time
  - metadata['modified'] = filesystem time
* if a file is tracked, but no changes in staging area or working directory
  - metadata['date'] = first commit time
  - metadata['modified'] = last commit time
* if a file is tracked, and has changes in stage area or working directory
  - metadata['date'] = first commit time
  - metadata['modified'] = filesystem time

When this module is enabled, `date` and `modified` will be determined
by Git status; no need to manually set in article/page metadata. And
operations like copy and move will not affect the generated results.

Installation
------------

This plugin can be installed via:

    python -m pip install pelican-filetime_from_git

Usage
-----

If you don't want a given article or page to use the Git time, set the
metadata to `gittime: off` to disable it.

### Other options

`GIT_HISTORY_FOLLOWS_RENAME` (default `True`)

You can also set `GIT_HISTORY_FOLLOWS_RENAME` to `True` in your pelican config to 
make the plugin follow file renames i.e. ensure the creation date matches
the original file creation date, not the date is was renamed.

`GIT_GENERATE_PERMALINK` (default `False`)

Use in combination with permalink plugin to generate permalinks using the original
commit sha 

`GIT_SHA_METADATA` (default `True`)

Adds sha of current and oldest commit to metadata

`GIT_FILETIME_FROM_GIT` (default `True`)

Enable filetime from git behaviour

### Content specific options

Adding metadata `gittime` = `False` will prevent the plugin trying to setting filetime for this
content.

Adding metadata `git_permalink` = `False` will prevent the plugin from adding permalink for this
content.

### FAQ

Q. I get a `GitCommandError: 'git rev-list ...'` when I run the plugin. What's up?

Be sure to use the correct gitpython module for your distros git binary.
Using the `GIT_HISTORY_FOLLOWS_RENAME` option to `True` may also make your problem go away as it uses
a different method to find commits.

Contributing
------------

Contributions are welcome and much appreciated. Every little bit helps. You can contribute by improving the documentation, adding missing features, and fixing bugs. You can also help out by reviewing and commenting on [existing issues][].

To start contributing to this plugin, review the [Contributing to Pelican][] documentation, beginning with the **Contributing Code** section.

[existing issues]: https://github.com/pelican-plugins/filetime_from_git/issues
[Contributing to Pelican]: https://docs.getpelican.com/en/latest/contribute.html

License
-------

This project is licensed under the AGPL-3.0 license.
