A simple CLI tool that periodically tries to ping google.com (or the host provided)
and displays a notification once the server is reachable.

Usage:

    cn [host]


On Mac OS, a Growl notification is displayed if the `gntp` package is available (`pip install gntp`).
If not, then a Cocoa dialog is shown instead.

Use cases:

    1. When you want to know when you are back online (`cn`).
    2. When you are restarting a server and want to know when it's up again (`cn server`).

That's it.
