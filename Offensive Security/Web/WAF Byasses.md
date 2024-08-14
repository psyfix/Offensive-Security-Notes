When JSON serializes an object it will decode and escape any unicoded characters. When the payload is originally parsed this first bypasses the WAF, it then is serialized by JSON and the payload is executed.

![Accept-Encoding: Zip, deflate 
Accept-Language: 
ateDetails" "in ut": 
Eden 
Unicode escape waf 
[https://trustfoundry.net/bypassing-wafs-with-json-unicode-escape-sequences/](https://trustfoundry.net/bypassing-wafs-with-json-unicode-escape-sequences/)

[https://github.com/0xInfection/Awesome-WAF](https://github.com/0xInfection/Awesome-WAF)

Depending on the technology stack of the website payloads can be encoded in many different types.

[https://soroush.secproject.com/downloadable/request-encoding-to-bypass-web-application-firewalls.pdf](https://soroush.secproject.com/downloadable/request-encoding-to-bypass-web-application-firewalls.pdf)

For Example UTF-32 is processed by python / Django, so encoding a payload in UTF-32 may bypass the waf and be executed by the application.

Unicode converter:

[https://convertcodes.com/unicode-converter-encode-decode-utf/](https://convertcodes.com/unicode-converter-encode-decode-utf/)

Encoding converter / [https://www.jdoodle.com/python-programming-online/](https://www.jdoodle.com/python-programming-online/)

import urllib

def paramEncode(params="", charset="IBM037", encodeEqualSign=False,

encodeAmpersand=False, urldecodeInput=True, urlencodeOutput=True):

    result = ""

    equalSign = "="

    ampersand = "&"

    if encodeEqualSign:

        equalSign = equalSign.encode(charset)

    if encodeAmpersand:

        ampersand = ampersand.encode(charset)

    params_list = params.split("&")

    for param_pair in params_list:

        param, value = param_pair.split("=")

        if urldecodeInput:

            param = urllib.unquote(param).decode('utf8')

            value = urllib.unquote(value).decode('utf8')

        param = param.encode(charset)

        value = value.encode(charset)

    if urlencodeOutput:

        param = urllib.quote_plus(param)

        value = urllib.quote_plus(value)

    if result:

        result += ampersand

    result += param + equalSign + value

    return result

print(paramEncode("=hello"))