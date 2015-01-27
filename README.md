THE GAME OF CODE UPDATES
========================

To allow mongodb commands first you need to install repositories on go-agent:

```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | sudo tee /etc/apt/sources.list.d/mongodb.list
sudo apt-get update
```



A command repository for Go
===========================

Introduction
------------
The newly introduced command repository hosts a selection of commands to help you get started
with various tools via [Go's custom command](http://support.thoughtworks.com/entries/22873043-go-s-custom-command).
This Readme describes syntax of a command and the structure of the repository.
For full documentation about Go's support for this feature, please see:

<http://www.thoughtworks.com/products/docs/go/current/help/command_repository.html>

Also check out these articles explaining how this can be used.

Introductory: [And you thought Go didn't support Maven, Nuget or Chef?](http://www.thoughtworks.com/insights/agile/and-you-thought-go-didnt-support-maven-nuget-chef-etc)

Advanced: [Use Go's new command repository to lookup your config scripts](http://www.thoughtworks.com/insights/blog/use-gos-new-command-repository-lookup-your-config-scripts)

Caution: Please do not change/add anything under the default repo on the Go server.
The directory will be deleted and re-created upon Go Server upgrade. Refer the above
link for setting up your own private command repository.

Version.txt
-----------
Go Server bundles a clone of the repository at <https://github.com/goteam/go-command-repo> by
default. The [version.txt](https://github.com/goteam/go-command-repo/blob/master/version.txt) file is meant to allow conditional overwriting of the repository during
server upgrades.

Command Syntax
--------------
A valid command file looks like this:

    <exec command="curl">
      <arg>-u</arg>
      <arg>user:password</arg>
      <arg>http://targeturl</arg>
    </exec>

It must be a valid .xml file ([escape](http://en.wikipedia.org/wiki/List_of_XML_and_HTML_character_entity_references#Predefined_entities_in_XML) special characters). The command attribute is mandatory. No other attributes are valid. Zero or more
arg child elements can be specified. No other child elements are allowed. One command file may only
contain one command.

Command Documentation
---------------------
Documentation is fully optional but it aids lookup and use if present. Here is the above command with
full documentation. Each item of documentation is key:value. Only whitespace characters may
precede a key. Value terminates with newline (no multi-line values). Descriptions longer than about 250
characters may get truncated in the admin GUI on the Go Server.

**note:** author refers to author of the command xml file, not the underlying tool :-)

    <!--
      name: curl
      description: curl is a command line tool for transferring data with URL syntax
      keywords: curl, wget, download, httpclient
      moreinfo: http://curl.haxx.se/docs/manpage.html
      author: Go Team
      authorinfo: http://support.thoughtworks.com/categories/20002778-go-community-support
    -->
    <exec command="curl">
      <arg>-u</arg>
      <arg>user:password</arg>
      <arg>http://targeturl</arg>
    </exec>
