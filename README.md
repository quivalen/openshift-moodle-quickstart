Moodle on OpenShift
======================

This git repository helps you get up and running quickly w/ a Moodle installation
on OpenShift.  The backend database is MySQL and the database name is the
same as your application name (using getenv('OPENSHIFT_APP_NAME')).  You can name
your application whatever you want.  However, the name of the database will always
match the application so you might have to update .openshift/action_hooks/build.


Running on OpenShift
----------------------------

Create an account at https://www.openshift.com and install the client tools (run 'rhc setup' first)

Create a php-5.4 application (you can call your application whatever you want)

    rhc app create moodle php-5.4 mysql-5.5 --from-code=https://github.com/quivalen/openshift-moodle-quickstart

That's it, you can now checkout your application at:

    http://moodle-$yournamespace.rhcloud.com

Username is admin and password is moodle

Note: When you upload plugins and themes, they'll get put into your OpenShift data directory
on the gear ($OPENSHIFT_DATA_DIR).  If you'd like to check these into source control, download the
plugins and themes directories and then check them directly into php/wp-content/themes, php/wp-content/plugins.

Notes
=====

GIT_ROOT/.openshift/action_hooks/deploy:
    This script is executed with every 'git push'.  Feel free to modify this script
    to learn how to use it to your advantage.  By default, this script will create
    the database tables that this example uses.

    If you need to modify the schema, you could create a file
    GIT_ROOT/.openshift/action_hooks/alter.sql and then use
    GIT_ROOT/.openshift/action_hooks/deploy to execute that script (make sure to
    back up your application + database w/ 'rhc app snapshot save' first :) )

Security Considerations
-----------------------
Consult the Moodle documentation for best practices regarding securing your moodle installation.  OpenShift
automatically generates unique secret keys for your deployment into wp-config.php, but you may feel more
comfortable following the Moodle documentation directly.
