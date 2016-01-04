# FTLDoc

Generates HTML documentation for FTL templates and macros.

* Original author: [chaquotay](https://github.com/chaquotay/ftldoc)
* Improvements: [nguillaumin](https://github.com/nguillaumin/ftldoc)

[![Build Status](https://travis-ci.org/nguillaumin/ftldoc.svg)](https://travis-ci.org/nguillaumin/ftldoc)

## Usage

    Usage: java -jar ftldoc.jar <options> file,file...

where:

* file = the templates (required)

and options are:

* -?     prints usage to stdout; exits (optional)
* -d <f> output directory (required)
* -h     prints usage to stdout; exits (optional)
* -help  displays verbose help information (optional)
* -tpl <f> alternative templates to use (optional)

## Maven dependencies

You'll need to install `jcmdline-1.0.1.jar` manually (Provided under `lib/` and available from [here](http://jcmdline.sourceforge.net/)):

`mvn install:install-file -Dfile=lib/jcmdline-1.0.1.jar -DgroupId=jcmdline -DartifactId=jcmdline -Dversion=1.0.1 -Dpackaging=jar`

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

You can use any `@` tags you want such as `@author`, or `@mytag`. These tags will be parsed and available in the template on the `macro` or `comment` objects (i.e. `macro.@author` ...).

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

## Custom templates

The generated doco is based on FreeMarker templates. There is a default set of templates provided but you can use your own.
To do so, use the `-tpl </path/to/tpl/folder` option. The folder must contains the following files:

* `file.ftl` : Used for a single `.ftl` file documentation.
* `index.ftl` : Index page (frameset).
* `index-all-cat.ftl` : Index of categories.
* `index-all-alpha.ftl` : Alphabetical index.
* `overview.ftl` : Overview (list of documented `.ftl` libraries).
* `filelist.ftl` : List of documented `.ftl` files (Left side of the frameset). 
