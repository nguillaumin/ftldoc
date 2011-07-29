# FTLDoc

Generates HTML documentation for FTL templates and macros.

* Original author: [chaquotay](https://github.com/chaquotay/ftldoc)
* Improvements: [nguillaumin](https://github.com/nguillaumin/ftldoc)

## Usage

    Usage: java -jar ftldoc.jar <options> file,file...

where:

* file = the templates (required)

and options are:

* -?     prints usage to stdout; exits (optional)
* -d <f> output directory (required)
* -h     prints usage to stdout; exits (optional)
* -help  displays verbose help information (optional)

## Maven dependencies

You'll need to install `jcmdline-1.0.1.jar` manually (Available from [here](http://jcmdline.sourceforge.net/)):

`mvn install:install-file -Dfile=jcmdline-1.0.1.jar -DgroupId=jcmdline -DartifactId=jcmdline -Dversion=1.0.1 -Dpackaging=jar`

## Comment syntax

The comments to process must start with a `<#---` tag (3 dashes). This is to mimic the Javadoc behaviour where a `/*` is a standard comment, but `/**` is a Javadoc comment.

### Macro comments

The first sentence of the comment (until the first dot) will be used a short description in the summary table.

Macro parameters should be indicated using `@param <name> <description>`.

HTML is permitted within comments.

Example:

```
<#---
	Does fancy stuff.
	
	<p>And does it well !</p>
	
	@param fist The first parameter.
	@param second The second parameter, a <code>boolean</code>.
-->
<#macro MyMacro first="" second=false>
    ...
<#/macro>
```

### Global comment

A global comment for a given `.ftl` file can be written at the top of the file. The first comment found that isn't followed by a `<#macro />` is considered the global comment.

### Categories

Macro can be put in categories. To embed a group of macros in a category, use the `@begin` and `@end` tags.

```
<#-- @begin Menu handling -->

<#---
    ...
-->
<#macro MainMenu> ... </#macro>

<#---
    ...
-->
<#macro SubMenu> ... </#macro>

<#-- @end -->
```
