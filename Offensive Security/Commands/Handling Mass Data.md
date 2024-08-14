
```
Cut

Sed

Awk

cat targets.txt| cut -f2 -d\ | sort -u | while read ip;do echo host $ip;done| sh -x 2>&1 |tee scriptout.blah

└─# cat targets.txt | cut -f2 -d " " | sort -u | while read ip;do echo host $ip;done                                                                                                        

grep http targets.txt|awk {'print $5"://"$2":"$4"/"'}|tr -d \(|tr -d \)|tr -d \?|sed "s|ssl/http|https|g"|sed -e "s/-proxy//"|sed -e "s/-alt//"|sed -e "s/radan-//"|sed "s/httpss/https/"

sed 's/apple/orange/g' input.txt > output.txt

sed -i 's/apple/orange/g' input.txt
```