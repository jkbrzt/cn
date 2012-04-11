#!/usr/bin/env python
"""
github.com/jkbr/cn

"""
import os
import sys
import datetime


host = 'google.com' if len(sys.argv) != 2 else sys.argv[1]
gui_alert_delta = datetime.timedelta(seconds=5)
title = 'Server reachable'
ping_command = """
bash -c '
while ! ping -c 1 "{host}" &> /dev/null; do
    echo -n .
    sleep 1
done;
'
 """

start = datetime.datetime.now()
result = os.system(ping_command.format(host=host))


if result is not 0:
    sys.exit(result)


ping_took = datetime.datetime.now() - start
needs_gui_alert = ping_took > gui_alert_delta
message = 'Pinged {host} after {seconds} seconds.'.format(
    seconds=ping_took.seconds,
    host=host
)


print('\n%s\n\a' % message)


try:
    import gntp.notifier
except ImportError:
    pass
else:
    notifier = gntp.notifier.GrowlNotifier('CN', ['info', 'error'])
    notifier.register()
    notifier.notify(
        noteType='info',
        title=title,
        description=message,
        sticky=needs_gui_alert
    )
    sys.exit(0)


if needs_gui_alert:
    try:
        import Cocoa
    except ImportError:
        pass
    else:
        Cocoa.CFUserNotificationDisplayAlert(
            0, 3, 0, 0, 0,
            title,
            message,
            "OK",
            None, None, None
        )
