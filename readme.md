# The Web In Depth 

## HTTP Request 
    (GET/POST/ETC) something we're very familiar with. A bit of a refresher on the format of the HTTP Request

    verb/resource/locator http/1.1/ header1  

    Request Headers

    host: indicates the desired host handling the request. 
    accept: indicates what MIME types are accepted by the client. (JSON, XML, etc)
    cookie: passes cookie data 
    referer: pages leading to this request. (Not found in HTTPS on the origin)
    Authorization: used for basic auth.     


## Cookies

    cookies are key-value pairs of data that are sent from the server and reside on the client for a fixed time 

### Cookie security:
    cookies can be read by any subdomain of the origin domain. For example, .example.com, cookies can be read by any subdomain such as example.com. 

    REMEMBER to follow the hiearchy: 
        test.example.com can set cookies for foo.test.example.com and example.com but not test2.example.com   

    Two flags to know for cookies
        secure: The cookie will only be accessible to HTTPS pages
        httponly: cookie cannot be read by javascript

    These flags are indicated on the set-cookie header that passes them in the first place. 

## HTML 
    
    Geneerally HTML when there is a discrepancy between parsing it normally and then parsing with an intermediary and third party, it implies an area of vulnerability. 


## Content Sniffing

    