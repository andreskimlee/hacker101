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

## HTML Parsing
    
    Geneerally HTML when there is a discrepancy between parsing it normally and then parsing with an intermediary and third party, it implies an area of vulnerability. 

    Most browsers will pick up on mistakes for user error and these sometimes present as vulnerability. 

## Content Sniffing

### Mime sniffing 
    
    A Browser will often not look at the content type header that the server is passing but also the contents of the page. If the majority of the page is read as hmtl, it'll be parsed at html 

    Imagine you have a site with a file upload function for profile pictures 

    if that file contains enough html to trigger the sniffing heuristics an attacker could upload a picture and then link it to other victims. 

    This is why most services use separate domains to host the pictures (AWS S3)

### Encoding Sniffing 

    Encoding is also picked up by browsers. if you dont specify for example an encoding for html document. the browser will apply heuristic to determine it. If you are able to control the way the browser decodes text you may be able to alter the parsing. 

    The takeaway here is you should always specify the encoding on the header so you know what the browser will be encoding it. So that the server and client dont have a discrepancy. 

    Also specify MIME Types

### Same-Origin Policy 

    is how browsers restricts a number of security-critical features 

        -what domains you can contact via XMLhttprequest 
        -Acess to the dom across separate windows/frames 

    Origin Matching
        -protocol must match (HTTP/HTTPS) no crossing boundraries
        - port numbers must match 
        -domain names must be an exact match

### CORS

    is still very new but enables some risky situations. in essence you are allowed to make xmlhttprequests to domains outside of your origin. An origin is for example http://example.com. It must match http and the whole domain.

    special headers signify where the request originates from what custom headers are added, etc 
    its also possible to pass the remaining domains cookies allowing attackers to potentially compromise loggined in users
    Due to how recent it is security issues and vulnerabilities are still largely unexplored. 

### CSRF

    Cross site request forgery is when an attacker tricks a victim into going to a page controlled by the attacker which then submits data to the target site as the victim. 

    A good example of this, imagine you had a  bank account and when you log into your account it submits an API request once you are loggedin by the hacker to submit for a transfer. This is CSRF. Preventitive measures generally include ways to detect origin. CSRF Tokens are tied to user session. (Embedded in forms) 


    How To Mitigate :

        POST request should check to see if CSRF token matches the CSRF token generated from the user session.   
        doesnt work with get requests but get requests anyway you dont expect a change in state. 

    How NOT to mitigate: 


# XSS 

    XSS (cross site scripting) is easily the most common bug you will counter

    Reflected XSS - input from the user is directly returned to the browser permitting injection of arbitrary content
    Stored XSS - input from the user is stored on the server and returned later without proper escaping. 
    DOM XSS - input from a user is inserted into a page's dom without proper handling enabling insertion of arbitrary nodes.

    

