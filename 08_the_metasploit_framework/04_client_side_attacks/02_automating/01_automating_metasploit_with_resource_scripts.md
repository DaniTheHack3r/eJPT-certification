# Automating Metasploit with Resource Scripts

+ Metasploit resource scripts are a great feature of MSF that allow you to automate repetitive tasks and commands.

+ They operate similarly to batch scripts, whereby, you can specify a set of Msfconsole commands that you want to execute sequentially.

+ You can the load the script with Msfconsole and automate the execution of the commands you specified in the resource script.

+ We can use resource scripts to automate various tasks like setting up multi handlers as well as loading and executing payloads.

**Note**: We can essentially automate any action we can perform with the msfconsole using resource scripts.

## Laboratory

For this technical demonstration we won't need a lab environment. We can follow along using a simple kali virtual machine.

- We will start by listing all prepackaged resource scripts. We can do this by running ls on `/usr/share/metasploit-framework/scripts/resource/`. You will se that they come with the syntax `resource_script_name.rc`.

- We can open one of these resource scripts like any other text file with a code editor like vim, code or nano. You will notice that it contains some documentation, and the commands that run sequentially are written in ruby.

- We will automate the process of setting up a multihandler. The steps to perform this action manually would be:
    + Starting up msfconsole.
    + Selecting `multi/handler` auxiliary module.
    + Setting up the payload, and LHOST and LPORT options.
    + Running the multihandler

**Note**: You could run the handler as a job in the background with -j.

- Now from the terminal, create a new rc file called `handler.rc`. You can create it wherever you want. And then, you can add the commands you usually use when you want to perform a certain task. For example, when setting a handler, we can add the following content to the resource script:

```
    use multi/handler
    set PAYLOAD windows/meterpreter/reverse_tcp
    set LHOST X.X.X.X
    set LPORT 1234
    run
```

**Note**: The important thing here, is that you need to add the commands you use from the first command to the last, in order from top to bottom.

- Save the script and fire up the msfconsole with the following option `msfconsole -r handler.rc`. This will automate the commands and start up the msfconsole as well. You will notice the multi handler will be waiting the connection as if you did it manually.

- Now we will make another example using the tcp portscan module. We will add the following content to the resource script:

```
    use auxiliary/scanner/portscan/tcp
    set RHOSTS X.X.X.X
    run
```
- Save the script and fire up the msfconsole with the following option `msfconsole -r portscan.rc`. This will show us the exact same results as if we run it from inside the msfconsole.

- Now we will try another simple example where we will execute several unrelated commands. Start by creating a file called `db_status.rc` with the following contents:

```
    db_status
    workspace
    workspace -a Test
```

- Save and then execute it by typing `msfconsole -r db_status.rc` and it should show the database status, list all workspaces and create a new workspace called Test. You can delete the workspace afterward.

- We can also execute Resource Script from within the msfconsole. Start up the msfconsole and run `resource ~/path/to/resource/script`.

- We can also create Resource Scripts from the msfconsole automatically. This can be achieved by initializing a new msfconsole session, and run the commands we want to save later. For example: `use auxiliary/scanner/portscan/tcp`, `set RHOSTS X.X.X.X` and `run`. Then, we can save the commands and create a new RC file by running `makerc ~/path/to/new/resource/script` from inside the msfconsole. It will display how many commands will be saved when creating it and the output file should contain this:

```
    use auxiliary/scanner/portscan/tcp
    set RHOSTS X.X.X.X
    run 
```
