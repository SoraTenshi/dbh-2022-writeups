# simplelogin

Die erste Web challenge und mit welcher man Login Daten bekommt. (username: "user" | password: "f45mSC4B5yZRzpoTE9")
Beim einloggen hab ich direkt mir die reponse header angeschaut.

```http
GET /index.php HTTP/1.1
Host: 071146b46e-web-simplelogin.dbhchallenge.net
Cookie: Session=04f8996da763b7a969b1028ee3007569eaf3a635486ddab211d512c85b9df8fb
Cache-Control: max-age=0
Sec-Ch-Ua: "Chromium";v="103", ".Not/A)Brand";v="99"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Windows"
Upgrade-Insecure-Requests: 1
User-Agent: \*
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-Dest: document
Referer: https://071146b46e-web-simplelogin.dbhchallenge.net/index.php
Accept-Encoding: gzip, deflate
Accept-Language: ja,en-US;q=0.9,en;q=0.8
Connection: close
```

nach einiger Zeit mit rumprobieren und allem moeglichen ist mir dann aufgefallen das der Session-Cookie ein immer einen hard gecodeden string: `04f8996da763b7a969b1028ee3007569eaf3a635486ddab211d512c85b9df8fb`

Nach einer kurzen Suche ist dann folgendes daraus entsprungen: ein sha256 hash welcher decoded zu 'user' entschluesselt wird.
Nun hab ich einfach mal probiert den session-cookie als sha256 gehashten "admin" zu ersetzen -> und es hat geklappt.
Nun wurde ich von der Seite als Admin begruesst und habe die Flag erhalten `DBH{e4c67197-68d0-4554-9771-245c68d9be49}`
