Description
===========
BruteBuster is a simple, pluggable Django app that can help you protect against password bruteforcing attempts.

The module overrides the default authenticate() function from django.contrib.auth, so it provides automated protection both for your custom login pages and for the admin login page.

Each block is applied against a unique username/IP address combination. In this way, bruteforcing attempts coming from a different IP address would not prevent the original user from logging in.

Installation
------------
1. Install the BruteBuster module to your Python path
```
#easy_install django-brutebuster
```
To verify that the Python module is available, you can run the Django shell and check the value of BruteBuster.version:
```
$python manage.py shell
(InteractiveConsole)
>>> import BruteBuster
>>> print BruteBuster.version
0.1
```
If you don't see any errors, then congrats! The hard part is over.

2. Add BruteBuster to your INSTALLED_APPS list in settings.py
3. Add BruteBuster.middleware.RequestMiddleware to your MIDDLEWARE_CLASSES in settings.py
4. Run python manage.py syncdb to add the BruteBuster table to your database
5. That's it! Don't forget to restart your server, if needed.

Operation
---------
If everything is working properly, you should see a Failed attempts table in the Django admin interface. Whenever a failed login is detected, the Failures counter for the respective Username/IP address combo is incremented. If the counter goes over a certain threshold (called BB_MAX_FAILURES), login attempts for this User and IP are blocked until BB_BLOCK_INTERVAL (minutes) passes without a failed login.

The default BB_MAX_FAILURES value is 5, and the default BB_BLOCK_INTERVAL is 3 (minutes). Both values can be overridden in settings.py.

Display
-------
All active blocks will have a 'Blocked' column set to True in the Failed Attempts table in the Django admin.

Block removal
-------------
The easiest way to remove a block is to delete the corresponding line from the Failed Attempts table. It is completely safe to remove data from this table (the worst that could happen is to remove some existing block)

Future
------
Found some bug? Got a suggestion? Need a feature that's not present yet? In any case we would love to hear back from you. You can use the contact form, or simply throw us an email at office () mtr-design.com.
