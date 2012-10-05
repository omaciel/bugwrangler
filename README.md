BugWrangler
===========

Introduction
------------

**BugWrangler** is a small tool I built to perform some queries against [Red Hat](http://redhat.com)'s [Bugzilla](https://bugzilla.redhat.com), though it could also be used against other Bugzilla installations, and provide me with reports and metrics. Right now it can output queries to standard output or generate a HTML file. The HTML format uses the awesome [Bootstrap](http://twitter.github.com/bootstrap/) project to provide a bit of styling.


Installation
------------

Installation is still manual:

1. Copy the `bugwrangler` file to your computer.
2. Install [python-bugzilla](http://pypi.python.org/pypi/python-bugzilla/0.6.2).
3. Make it executable.
4. Add it to your PYTHONPATH.

Usage
-----

    Usage: bugwrangler [options]

    Performs queries and actions against Red Hat's Bugzilla.

    Options:
      --version             show program's version number and exit
      -h, --help            show this help message and exit
      -b BUG_ID, --bug_id=BUG_ID
                            List of comma separated bug IDs.
      --product=PRODUCT     
      -q CONTACT, --qa_contact=CONTACT
      -a ASSIGNED, --assigned_to=ASSIGNED
                            Email of person assigned to work on bug.

      Bugzilla Login settings:
        Use the email and password to authenticate against Bugzilla.You may
        want to login to access any issues that may require authentication.

        -u USERNAME, --username=USERNAME
                            Valid Bugzilla username.
        -p PASSWORD, --password=PASSWORD
                            Valid Bugzilla password.

      Reporting options:
        All queries are displayed in the console unless you use this option to
        create a HTML formatted report.

        --html              

      Bugzilla STATUS options:
        Use any combination of the following status values: NEW, ASSIGNED,
        MODIFIED, ON_DEV, ON_QA, VERIFIED, POST, CLOSED

        -s STATUS, --status=STATUS
                            Bugzilla bug status.  [default: ON_QA]

      Date filtering:
        --start=START       Searches Bugzilla from start date.
        --end=END           Searches Bugzilla up to end date.

    Constructive comments and feedback can be sent to Og Maciel <omaciel at
    ogmaciel dot com>.

Examples
--------

All NEW [Katello](http://katello.org) bugs created since September 01, 2012

    $ bugwrangler --status NEW --product Katello --start 2012-09-01
    [834311] medium - Wrong Pool Id in "subscription-manager list --available" - <katello-qa-list@redhat.com> - NEW
    [843800] urgent - Syncronization raises an exception when package have a diffe - <katello-qa-list@redhat.com> - NEW
    [855279] medium - [RFE] add "description" field in "product status" CLI output - <katello-qa-list@redhat.com> - NEW
    [858209] unspecified - Thin reports a lots of avc: denied messages. - <katello-qa-list@redhat.com> - NEW

All Pulp bugs that have been either VERIFIED or CLOSED since October 01, 2012

    $ bugwrangler --status VERIFIED,CLOSED --product Pulp --start 2012-10-01
    [855380] unspecified - Owner information on copied and uploaded units are wrong - <pthomas@redhat.com> - VERIFIED
    [856775] unspecified - repo group member add/remove .adds/removes all the repos to/ - <pthomas@redhat.com> - CLOSED
    [858037] medium - DB validation fails for roles created before db version 2 - <pthomas@redhat.com> - VERIFIED
    [860800] unspecified - pulp doesnt handle errata spanning across multiple repos cas - <pthomas@redhat.com> - VERIFIED
    [862356] unspecified - User with non-UTF-8 characters in name causes task queue to  - <pthomas@redhat.com> - VERIFIED

All of the above Pulp bugs, which ones were closed between October 1 and October 2

    $ bugwrangler --status VERIFIED,CLOSED --product Pulp --start 2012-10-01 --end 2012-10-02
    [855380] unspecified - Owner information on copied and uploaded units are wrong - <pthomas@redhat.com> - VERIFIED
    [856775] unspecified - repo group member add/remove .adds/removes all the repos to/ - <pthomas@redhat.com> - CLOSED
    [858037] medium - DB validation fails for roles created before db version 2 - <pthomas@redhat.com> - VERIFIED

How many bugs have I verified so far for the Katello and CloudForms System Engine products, ever!

    $ bugwrangler --status VERIFIED,CLOSED --product "Katello,CloudForms System Engine" -q omaciel ATredhat DOT com | wc -l
    165

Get a nice looking report

    $ bugwrangler --status VERIFIED,CLOSED --product "Katello,CloudForms System Engine" -q omaciel ATredhat DOT com --html
    A report has been generated and can be found here: 20121005183811.html
    
A sample report can be found here: http://bit.ly/PYtfwS

Author
------

This software is developed by
Og Maciel http://ogmaciel.tumblr.com