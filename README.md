# edqm-sync
https://standardterms.edqm.eu/

## EDQM Api Authentication Tips

Two headers should be put into the http request

- Date
  - compatible with RFC 7231 Date/Time Formats
  - usually like **Mon, 20 Jul 2015 08:00:00 GMT**
- X-STAPI-KEY
  - consist of two part **Login|Signature**(the | is just a string value not operator)
  - Login
    - email address which login into edqm website
  - Signature
    - StringToSign = HTTP-Verb + "&" + URI + "&" + HOST + "&" + Date
      - HTTP-Verb
        - http request method
        - usually like GET、POST
      - URI
        - http request uri
        - exclude scheme、host from url
        - for example if the url is **https://standardterms.edqm.eu:443/standardterms/api/v1/domains**, the true uri is **/standardterms/api/v1/domains**
      - HOST
        - http request host
        - constant, should be **standardterms.edqm.eu**
      - Date
        - same with the Date header as above
      - &
        - just a string value not operator
    - 22 last characters of Base64( HMAC-SHA512( YourSecretAccessKey, StringToSign ) )
      - you need to sign **StringToSign** with **YourSecretAccessKey** using HMAC-SHA512
      - then encoded with Base64
      - finally keep the last 22 characters of the base64 result

` If you have any other questions about european edqm like data or structure or other pharmacovigilance terminology questions,contact with my email huoyexiangyu@gmail.com
