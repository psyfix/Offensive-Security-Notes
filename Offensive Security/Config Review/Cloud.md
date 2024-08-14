###### Scout Suite
```
#Installation
$ virtualenv -p python3 venv
$ source venv/bin/activate
$ pip install scoutsuite
$ scout --help

python scout.py aws --access-keys --access-key-id <AKIAIOSFODNN7EXAMPLE> --secret-access-key <wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY> --no-browser --quiet --report-dir /home/kali/<client>/
```

###### Cloud Sploit
```
https://github.com/parsa-epfl/cloudsuite

#Setting up configuration
cp config.js /home/kali/<client>/

AWS:
{
  access_key: process.env.AWS_ACCESS_KEY_ID || ' KEYS HERE ',
  secret_access_key: process.env.AWS_SECRET_ACCESS_KEY || ' SECRET KEY HERE',
}

./index.js --cloud=aws --config=/home/kali/<client>/config.js --csv /home/kali/<client>/output.csv

```