# MSFconsole Fundamentals

+ Before we can start using the Metasploit Framework for penetration testing, we need to get an understanding of how to use MSFconsole.

+ The Metasploit Framework Console (MSFconsole) is an easy-to-use all in one interface that provides you with access to all the functionality of the Metasploit Framework.

+ We will be utilizing MSFconsole as our primary MSF interface for the rest of the course.

**Note**: All we imaging, concerning penetration testing, can be done with the metasploit framework, and for this task we will always choose the MSFconsole above any other metasploit framework platform. It is our command center for this matter. From the msfconsole we can search modules, load modules, configure them, execute them, search for payloads, manage sessions, etc.

## What you Need to Check

1. How to search for modules.
2. How to select modules.
3. How to configure module options & variables.
4. How to search for payloads.
5. Managing sessions.
6. Additional functionality.
7. Saving your configuration.

## MSF Module Variables

+ MSF modules will typically require information like the target & host IP address and port in order to initiate a remote exploit/connection.

+ These options can be configured through the use of MSF variables.

+ MSFconsole allows you to set both local variable values or global variable values.

## MSF Module Variables

| Variable | Purpose                                                                                                                    |
| -------- | -------------------------------------------------------------------------------------------------------------------------- |
| LHOST    | This variable is used to store the IP address of the attacker’s system.                                                    |
| LPORT    | This variable is used to store the port number on the attacker’s system that will be used to receive a reverse connection. |
| RHOST    | This variable is used to store the IP address of the target system/server.                                                 |
| RHOSTS   | This variable is used to specify the IP addresses of multiple target systems or network ranges.                            |
| RPORT    | This variable stores the port number that we are targeting on the target system.                                           |

**Note**: LPORT and LHOST are commonly required on modules that will receive a remote shell connection from the target. However the come with default values which are good enough for a first connection. However, remember that when you open multiple connections, you require to change the port every time you start a new session in metasploit.

## Notes from the practical demonstration

- Run `help` command to get a complete description of what you can do.

- Run `version` to get current version of the msfconsole. Note the framework and the console are different things so two versions are displayed.

- Run `show all` to show all modules. Run `show exploits` if you want to limit the search to only exploit modules and you can do this with any type of module in the metasploit framework.

- You can get some information about a specific command by running `$COMMAND -h`.

- To search for a specific pattern we can use the command `search $PATTERN`.

- If we want to select a module, we can just copy the name of the module from the output of the previous command like this: `use $MODULE_FULL_NAME` or using the `#` identifier `use $ID`. When selecting the module, the prompt will change to the type of module we are using and the full name of the module. For example: `moduletype(this/is/the/name)` it will mean is active.

- To check the options of a module, run `show options` with the module selected.

- To set any options, we can run the command `set $VARIABLE_NAME`. We can check again by running `show options` again. If we want to set a variable globally, so it can be used by any other module while we are using the msfconsole, we can run the command `setg $VARIABLE_NAME`.

- Once the options are set as you like, just type `run` or `exploit` to execute the module.

**Note**: The actions could be cancelled at any time by typing ctrl+c on the terminal running msfconsole.

- We can exit a module using the command `back`. The msfconsole will stop using the module.

- `search` is a command that can be used with options. We can look for cve, type, platform and we can sort. For example: `search cve:2017 type:exploit platform:windows` if we add a minus sign we can filter out that option, for example `search cve:2017 type:exploit platform:-windows` will filter out windows.

**Note**: When using an exploit module, the payload will be default to a version of meterpreter. This payload can be changed further on, from an x64 to an x86 shell if needed, or changing it to a simple reverse shell if that is the case.

- To view and manage sessions, we can use the `sessions` command. It will list the sessions with its session id, and it will help us navigate between sessions and so on.

**Note**: At the moment, we shouldn't have any session running, this is mostly useful after exploitation.

- We can also perform some banner grabbing using the command `connect`. For example: `connect $TARGET_IP $TARGET_PORT`. This is useful during the information gathering phase.
