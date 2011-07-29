FTLDoc
======

Generates HTML documentation for FTL templates and macros.

Usage
-----

    Usage: java -jar ftldoc.jar <options> file,file...

where:

* file = the templates (required)

and options are:

* -?     prints usage to stdout; exits (optional)
* -d <f> output directory (required)
* -h     prints usage to stdout; exits (optional)
* -help  displays verbose help information (optional)

Maven dependency
----------------

You'll need to install `jcmdline-1.0.1.jar` manually (Available from [here](http://jcmdline.sourceforge.net/)):

`mvn install:install-file -Dfile=jcmdline-1.0.1.jar -DgroupId=jcmdline -DartifactId=jcmdline -Dversion=1.0.1 -Dpackaging=jar`
