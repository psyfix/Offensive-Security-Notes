### Initial Foothold
```
Always use more then one tool when you are stuck! eg. dirb, feroxbuster and ffuf.

Always google what you see when you are stuck. Whether that is the name of a directory or file / or a the name of string in the nmap response. Google it and put exploit afterwards.

Always try a recursive directory search with feroxbuster.

Always try a directory search with extensions relating the web technology eg. php.

Always try a different wordlist. Try raft large words too or common.txt, directory-list-2.3-big.txt

Always check default credentials for any technology you see running!.

When looking at files in the folder viewer application make sure to turn on hidden files to show them.
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
```