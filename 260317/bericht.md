# Arbeitsbericht

- Datum: 17.3.2026
- Thema: [Arbeitsbericht Curl beim Notenmanagent](https://www.franzmatejka.at/htl/doc/ITSI_2_linux/14_curl.html)
- Name: Alexander Schauer
- Klasse: 3AHITS
- Fach: SYTB

# Übersicht

- Browser Developer Tool

# Erklärung Developer Tool

- mit f12 kommt man in die Developer Tools und auf der Leiste oben kann man den Network Tab auswählen
- Hier sieht man alle Netzwerk Zugriffe (Vorallem GET und POST requests es gibt aber auch DELETE und PUT requests)
- wenn man einen request in der Kommandozeile haben will kann man in dem Network Tab auf den request Rechtsklick drücken und dann Copy Value > Copy as cURL und dann kann man es einfach in die Kommandozeile pasten und sieht den Output
- wenn der response vom Server ein JSON ist handelt es sich um Daten die mit JavaScript in die Website eingebaut werden
- wenn man die JSON Response vom cURL in jq pipped dann sieht man die Daten strukturierter

```
┌──(kali㉿kali)-[~]
└─$ curl 'https://notenmanagement.htl-braunau.at/rest/api/Klassen' -H 'User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0' -H 'Accept: */*' -H 'Accept-Language: en-US,en;q=0.5' -H 'Accept-Encoding: gzip, deflate, br' -H 'Referer: https://notenmanagement.htl-braunau.at/schueler/home' -H 'Sec-Fetch-Dest: empty' -H 'Sec-Fetch-Mode: cors' -H 'Sec-Fetch-Site: same-origin' -H 'authorization: bearer y3t_UnDTdZZof7oyKsHfTGh1zi9oJgavpcptorgQURf9wLB0A8yO24B6ll1_rYgL2KFLVpgXFj820xJTz26iqekQ7T8UumZjSb-vVdZ4y6CqaAc2d9Fv87z836IRmDjrxz1czSLO7OuDXM_iPWmxBm7wUjJctQwASGH_7dPadXb9NL3hGE6oVtK7qXPuPNyJNF3QDbZ5AHQwOd5Vw7yyDXdMkKf5C7SYwJvBdAP-wMsVN3PWiffocY3vozSHVhQRXhQy3_FjzgYv5f35hFQGN0W1MhLPaC88Z3o31xwcbniygSl3SQ4kUhy90jP4BHDl7oUambp-9_AVPXRSrh-Pru8N2K1EC8MZMf8-_QOSupMMVGXefLtV1XOY460xm-1qZWvrWTvi9SKg96o-BH1aZE6wVX_l7MZQJh4rOmiLdEVa8lxenpAt-ZFUik5FRiMKv05F5p8uNIdsQtC8jcsCeNEdFDWnXHsqcnz8kHXgdZu59IKMt-Llir6c5jbVQ7eqGXb63UJav_gi6IKAxUgIbVC5X-vkF3mpbBmSRkKi39GbvU0ubBwmwCTEKREGf6c-gYmZ5xxgGcFgdTMadAdHmgJXgHG6jk18BtuoIO3GFOipn6igWe2YQd59qfGsjUJXrH0B0MRr_km7dcnUn9a2ZQ' -H 'Connection: keep-alive' -H 'Cookie: _ga_7HXBEWYXMN=GS2.1.s1773731574$o1$g1$t1773732396$j60$l0$h0; _ga=GA1.1.2034133895.1773731575; _ga_MKKQL10FVQ=GS2.1.s1773731575$o1$g1$t1773732396$j60$l0$h0; _gcl_au=1.1.81027.1773731575; _gid=GA1.2.1051782231.1773731575; cookieconsent_status=dismiss; .AspNet.Cookies=miPguEoceIZoSNO5Xh2OTCMxwEfBAMdi83EeGTBmUUIKzCiurzbslAHqknekjyj_St5QMLVa7u7nYsjiJxQXC359vKrQHt8EFfzfJf-zrAuKd-1TFXVaxpr1jpCam1-YQvWxzjeDcdJx5lEh4XbcGpUvrixaL6V8quL0DBtEG8YyVWsqTsQ-hETy-nNfD2lO2kpUpxMgY0f7UVuw6QaS-aWuWfXFNqSAd9x1GbYDvD8fC5zvf1PN9qXjWKzl7lGE_O_y33f8PWBeTDN0iX2Ozoyz_5gtCE6bcQrCBe-htAXj5ERka5EuvlSOmyzXIVQ6Xh1ITYhW50rxmR5DBTE9pZfu5yHiOtokRDZyZM8qqiPsvzMaxLsBgJb_mcZZFqPPGJ64JJ9lFozuUUR_-4o1v5T3nlxFtbCq6QnVZFpF2u5Tp0mA1xDo_CuSLyVxGxnLLcGhz0IbCEGVTG6YTazNqsef0LaUzlCUzMrnzB13i89suyGjJ4Pg4SLk4PlsK5GR' -H 'TE: trailers' | jq
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   638  100   638    0     0  12499      0 --:--:-- --:--:-- --:--:-- 12760
[
  {
    "Name": "1AFELC"
  },
  {
    "Name": "1AHELS"
  },
  {
    "Name": "1AHETS"
  },
  {
    "Name": "1AHITS"
  },
  {
    "Name": "1AHME"
  },
  {
    "Name": "1BHELS"
  },
  {
    "Name": "1BHME"
  },
  {
    "Name": "2AFELC"
  },
  {
    "Name": "2AHELS"
  },
  {
    "Name": "2AHETS"
  },
  {
    "Name": "2AHITS"
  },
  {
    "Name": "2AHME"
  },
  {
    "Name": "2BHELS"
  },
  {
    "Name": "2CHELS"
  },
  {
    "Name": "3AFELC"
  },
  {
    "Name": "3AHELS"
  },
  {
    "Name": "3AHET"
  },
  {
    "Name": "3AHITS"
  },
  {
    "Name": "3AHME"
  },
  {
    "Name": "3BHELS"
  },
  {
    "Name": "3BHME"
  },
  {
    "Name": "3CHELS"
  },
  {
    "Name": "4AFELC"
  },
  {
    "Name": "4AHELS"
  },
  {
    "Name": "4AHET"
  },
  {
    "Name": "4AHITS"
  },
  {
    "Name": "4AHME"
  },
  {
    "Name": "4BHELS"
  },
  {
    "Name": "4CHELS"
  },
  {
    "Name": "5AHELS"
  },
  {
    "Name": "5AHET"
  },
  {
    "Name": "5AHITS"
  },
  {
    "Name": "5AHME"
  },
  {
    "Name": "5BHELS"
  },
  {
    "Name": "5BHME"
  },
  {
    "Name": "5CHELS"
  }
]
```