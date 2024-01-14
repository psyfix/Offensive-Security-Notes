### Initial Foothold
```
Always use more then one tool when you are stuck! eg. dirb, feroxbuster and ffuf.

Always google what you see when you are stuck. Whether that is the name of a directory or file / or a the name of string in the nmap response. Google it and put exploit afterwards.

Always try a recursive directory search with feroxbuster.

Always try a directory search with extensions relating the web technology eg. php.

Always try a different wordlist. Try raft large words too or common.txt, directory-list-2.3-big.txt

Always check default credentials for any technology you see running!.

When looking at files in the folder viewer application make sure to turn on hidden files to show them.

Look at the files infront of you. They are not just there for no reason.

Check nmap for common namnes to add to hosts file.

Check burp for passive requests being made in the background on a web application.

Map application for potential application manual vulnerabilties like fileuploads and forms.

Google function unusual function names in code, maybe there is a weakness or exploit.
```

### Exploiting
```
Always try different versions of the same exploit.

```
### Priv Esc

```
Any password always spray on the current users on the sytem.

Is the executable or script you have privileges to run as root modifiable? OR can you write to that directory and overwrite the file instead?

When you are compiling binaries for kernel exploits make sure to compile the right architecture 32/64!

Look at wildcards in the sudo -l command and in general usually it means you can touch anything you want by manipulating the command.

RUN Rebeus KERBEROAST AND ASEPROAST.
```