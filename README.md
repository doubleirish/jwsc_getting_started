# jwsc   Environment Setup
java web services in the cloud . Getting your environment setup. e.g vagrant, sdkman etc 

A Commmon Environment 
In previous labs a lot of time was spent by students on setting up their environment before they could write a single line of code. 
Depending on their Operating System , Mac, PC, Unix they might have to  use  sligtly different configuration or software versions and might also encounter issues local to a specific OS.  
To Simplify the setup we're using Vagrant and VirtualBox to create a Linux environment which is perconfigured with most of the tools you'll nee

This attached Vagrantfile provides a standard predefined java environment to help you get started faster.



##sdkman!
The included [sdkman](http://sdkman.io/) tool makes it easy to install and manage tools like maven, gradle and springboot-cli without worrying about PATHS and environmental variables.
In the old days to install a tool like maven or gradle you would have to do the following :-
 * find the tool on the web and download it
 * extract it into a directory 
 * possibly fix file permissions
 * add a XYZ_HOME environmental variable
 * add the XYZ_HOME\bin directory to your PATH variable
 * 
the sdkman utility simplfies all of the above  and also makes it easy to have multiple versions of tools like maven and gradle and easily switch between versions. This tool is already included in the attached Vagrantfile .

To install sdkman on a fresh system just paste the following in a linux terminal
```
curl -s "https://get.sdkman.io" | bash
```

This will install the sdk tool.
To use the tool create a new terminal window to activate the entry the installation
added to your ~/.bashrc file

To see all the candidate softwarre you can install type
```
sdk list
```

to install the latest version

```
sdk install candidate
```
e.g
sd install maven

Examples of commonly used command are below. The  full usage guide is at http://sdkman.io/usage.html

| sdk cmd  |  example | description  |
|---|---|---|
| sdk ls                             | sdk list                | show all candidate software you can install |
| sdk ls <candidate>                 | sdk ls maven            | show all versions of candidate software |
| sdk install <candidate>            | sdk install maven       | install the latest version  |
| sdk install <candidate>  [version] | sdk install maven 3.3.3 | install a specific verion of software    |
| sdk current                        |                         | show all software installed by sdk    |
| sdk use <candidate> <version>      | sdk use gradle 2.8      | switch to a differnt version of installed software  |
