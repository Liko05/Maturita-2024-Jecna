# Hypertextové schéma HTTP - hlavičky, HTTP autentifikace, HTTP2 - rozdíly oproti HTTP1.1. Webové služby

## HTTP (Hypertext  Transfer Protocol)

je internetovy protokol urceny pro komunikaci s WWW servery. Slouzi pro prenos hypertextovych dokumentu ve formatu HTML,
XML, i jinych typu souboru. Pouziva obvykle port TCP/80, verze 1.1 protokolu je definovana v RFC 2616. Spolecne s
elektronickou postou je HTTP nejvice pouzivanym protokolem, ktery se zaslouzil o obrovsky rozmach internetu.

Je vsak pouzivan i pro prenos dalsich informaci. Pomoci rozsireni MIME umi prenase jakykoli soubor (podobne jako
e-mail), pouziva se spolecne s formatem XML pro tzv. webove sluzby (spousteni vzdalenych aplikaci ) a pomoci aplikacnich
bran zpristupnuje i dalsi protokoly, jako je napr. FTP nebo SMTP.

Samotny protokol HTTP neumoznuje sifrovani ani zabezpeceni integrity dat. Pro zabezpeceni HTTP se casto pouziva TLS
spojeni nad TCP. Toto pouziti je oznacovano jako HTTPS.

## REQUEST metody

- GET: Pozadavek an uvedeny objekt se zaslanim pripadnych dat (promenne prohlizece, session id, ...) Vychozi metoda pri
  pozadavku na zobrazeni hypertextovych stranek, RSS feedu aj. Celkove nejpouzivanejsi.
- HEAD: Metoda podobna GET, avsak nepredava data. Poskytne pouze metadata o pozadovanem cili (velikost, typ, datum
  zmeny,...).
- POST: Odesila uzivatelska data na server. Pouziva se napriklad pri odeslani formulare na webu. S predanym objektem se
  pak zachazi podobne jako pri metode GET. Data muze odesilat i metoda GET, metoda POST se vsak pouziva pro prilis
  veliky objem dat (vic nez 512 bajtu, coz je velikost pozadavku GET), nebo pokud neni vhodne prenasena data zobrazit
  jako soucast URL (Data predavana metodou POST jsou obsazena v HTTP pozadavku)
- PUT: Nahraje data na server. Objekt je jmeno vytvareneho souboru. Pouziva se velmi zridka, pro nahravani dat na server
  se bezne pouziva FTP nebo SCP/SSH.
- DELETE: Smaze uvedeny objekt ze serveru. K tomu je zapotrebi jistych opravneni stejne jako u metody PUT.
- TRACE: Odesle kopii obdrzeneho pozadavku zpet odesilateli, takze klient muze zjisit, co na pozadavku meni nebo
  pridavaji servery, kterymi pozadavek prochazi.
- OPTIONS: Dotaz na server, jake podporuje metody.

| Request method | RFC      | Request has payload body | Response has payload body | Safe | Idempotent | Cacheable |
|----------------|----------|--------------------------|---------------------------|------|------------|-----------|
| GET            | RFC 9110 | Optional                 | Yes                       | yes  | yes        | yes       |
| HEAD           | RFC 9110 | Optional                 | No                        | Yes  | Yes        | Yes       |
| POST           | RFC 9110 | Yes                      | Yes                       | No   | No         | Yes       |
| PUT            | RFC 9110 | Yes                      | Yes                       | No   | Yes        | No        |
| DELETE         | RFC 9110 | Optional                 | Yes                       | No   | Yes        | No        |
| CONNECT        | RFC 9110 | Optional                 | Yes                       | No   | No         | No        |
| OPTIONS        | RFC 9110 | Optional                 | Yes                       | Yes  | Yes        | No        |
| TRACE          | RFC 9110 | No                       | Yes                       | Yes  | Yes        | No        |
| PATCH          | RFC 5789 | Yes                      | Yes                       | No   | No         | No        |

## HTTP hlavicky

Jedna se o list retezcu ktere obdrzi jak klient tak server pri HTTP komunikaci (request a response). Headers jsou
castokrat neviditelne pro klienta a jsou zpracovany a logovany jen server a klientskou aplikaci

- V HTTP 1.x jsou headers posilany az za request line nebo response line. Jsou ve formatu "key:value" jako plain text
  ukoncene za pomoci carrage return (CR) a line feed (LF) sequenci. Konec header je oznacen prazdnym polem co se znaci
  dvemi po sobe jdoucimi CR-LF pary. Nasledne pri prenosu jsou headers nahrazeny nekolika pseudo header fields kazdy
  zacinajici s :
- V HTTP2 A HTTP3 ktere pouzivaji binarni protocol jsou headers zakodovany do jednoho HEADERS a 0 a vic CONTINUATION
  frames za pouziti HPACK (komprese v HTTP2) nebo QPACK (komprese v HTTP3).

Header nazvy jsou case sensitive o jejich standarizaci se stara IETF(the Internet Engineering Task Force) v RFC 9110 and

9111. Nestandartni header nazvy be se meli oznacovat prefixem "X-".
      Value headru muze obsahovat kvalitu ktera se nasledne pouziva pri vyjednavani se serverem. Napr: Accept-Language:
      de;
      q=1.0, en; q=0.5

Velikost header primo omezuje webserver jako je napriklad Apache 2.3. Kde je omezena velikost request na 8,190 bytes.
Muze byt maximalne 100 header fields in a single request.

| Name            | Description                                                                                                          | Example                                                                                           | Status              | Standard       |
|-----------------|----------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|---------------------|----------------|
| Accept-Language | List of acceptable human languages for response.                                                                     | Accept-Language: en-US                                                                            | Permanent           | RFC 9110       |
| Authorization   | Authentication credentials for HTTP authentication.                                                                  | Authorization: Basic QWkdadj2313j123zsdadjawDDJAKD==                                              | Permanent           | RFC 9110       |
| Cache-Control   | Used to specify directives that must be obeyed by all caching mechanisms along the request-response chain.           | Cache-Control: no-cache                                                                           | Permanent           | RFC 9111       |
| Content-Length  | The length of the request body in octets (8-bit bytes).                                                              | Content-Length: 348                                                                               | Permanent           | RFC 9110       |
| Content-Type    | The Media type of the body of the request (used with POST and PUT requests).                                         | Content-Type: application/x-www-form-urlencoded                                                   | Permanent           | RFC 9110       |
| Cookie          | An HTTP cookie previously sent by the server with Set-Cookie (below).                                                | Cookie: $Version1;Skin=new;                                                                       | Permanent: standard | RFC 2965, 6265 |
| Date            | The date and time at which the message was originated (in "HTTP-DATE" format as defined by RFC 9110; HTTP Semantics) | Date: Tue, 15 Nov 1994 08:12:31 GMT                                                               | Permanent           | RFC 9110       |
| Forwarded       | Disclose original information of a client connectiong to a web server through an HTTP proxy.                         | Forwarded: for=192.0.2.60;proto=http;by=203.0.113.43 Forwarded: for=192.0.2.43, for=198.51.100.17 | Permanent           | RFC 7239       |
| From            | The email address of the user making the request.                                                                    | From: user@example.com                                                                            | Permanent           | RFC 9110       |
| Host            | The domain name of the server and port number on which the server is listening.                                      | Host: en.wikipedia.org:8088                                                                       |                     |                |

## Autentifikace

Oba tyto dva typy by meli byt pouzity vyhradne pres HTTPS s TLS sifrovani a validnim SSL certifikatem. Jako odpoved
pokud se neoveri by mel prijit status code 401 unauthorized.

## Basic

Muzeme zajistit zapomoci header Authentization pomoci basic access authentication metody. Kde muzeme posilat jmeno a
heslo. Header Authorization: Basic `<credentials>` kde credentials jsou Base64 sifrovany ID a password spojeny dohromady
za pomoci":".

Napr: `Authorization: Bearer <token> `

## HTTP 1.1

Jedna se o plaintextovy protocol.

### Client request

```
GET / HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-GB,en;q=0.5
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Server response
HTTP/1.1 200 OK
Date: Mon, 23 May 2005 22:38:34 GMT
Content-Type: text/html; charset=UTF-8
Content-Length: 155
Last-Modified: Wed, 08 Jan 2003 23:11:55 GMT
Server: Apache/1.3.3.7 (Unix) (Red-Hat/Linux)
ETag: "3f80f-1b6-3e1cb03b"
Accept-Ranges: bytes
Connection: close

<html>
  <head>
    <title>An Example Page</title>
  </head>
  <body>
    <p>Hello World, this is a very simple HTML document.</p>
  </body>
</html>
```

## HTTP 1.1 vs HTTP 2

| HTTP/1.1                                                                                                    | HTTP/2                                                                     |
|-------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------|
| It works on the textual format. Plain text                                                                  | It works on the binary protocol. binary                                    |
| There is head of line blocking that blocks all the request behind it until it the response does not receive | It allows multiplexing so one TCP connection is used for multiple requests |
| It uses requests resource Inlining for use getting multiple pages                                           | It uses PUSH frame by server that collects all multiple pages              |
| It compresses data by itself.                                                                               | It uses HPACK for data Compression.                                        |

### HTTP2 je vyvinut na SPDY protokolu:

#### Povinne funkcionality

- Multiplexove spojeni: SPDY podporuje neomezeny pocet soubeznych toku dat skrze jedine TCP spojeni. Efektivita spojeni
  je maximalizovana, protoze jsou jednotlive dotazy posilany zaroven. Snizi se tim take pocet TCP spojeni k jednomu web
  serveru.
- Priorita dotazovani: S multiplexem je spojen problem priority. Pri pomalem spojeni muze dojit k zadrzeni paketu, ktere
  klient nutne potrebuje. SPDY implementuje prioritu dotazu (urovne 0 az 7), ktera tento problem efektivne resi.
- Komprimace hlavicek: Komprimace hlavicek je vzdy zapnuta a snizuje se tim pocet odeslanych dat. Hlavicky jsou vzdy
  komprimovany pomoci komprese zlib.

#### Nepovine funkcionality

- Server push: Na rozdil od HTTP, muze sam server zacit odesilat data. V hlavicce preda klientovi informaci, ze zacne
  odesilat data, ktea si klient jeste nevyzadal. Toto opatreni muze znacne zrychlit nacitani stranek, ktere klient jeste
  nenavstivil. Pokud ma jiz klient data v pameti pak je odeslani zbytecne, rozhodnuti o odeslani dat nalezi jenom
  serveru, jelikoz protokol neposkytuje informace o datech ktera jsou ulozena u klienta.
- Server hint: Server ma moznost, misto aktivniho odesilani dat, pouze informovat klienta o potrebnych datech. Klient
  pak muze rychleji zareagovat vlastnim dotazem. Pri pomalem spojeni klient rychleji zjisti, ktera data potrebuje, jeste
  pred tim nez by se mu stahl predchozi dotaz.

### HTTP2 HPACK

V HTTP/2 jsou hlavicky ve formatu binarnich ramu, ktere obsahuji nazev a hodnotu jednotlivyxh poli. HPACK je pouzivan k
redukci redundance a snizeni velikosti prenasenych dat pri komunikaci. Pri kompresi HPACK vyuziva nasledujici techniky:

- Staticka tabulka: HPACK obsajike statickou tabulku, ktera obsahuje nejbezneji pouzivane hlavicky, jako napriklad "
  Content-Type" nebo "Accept-Encoding". Tyto hlavicky jsou predem zakodovany a jsou k dispozici jak na strane klienta,
  tak na strane serveru.
- Dynamicka tabulka: HPACK udrzuje take dynamickou tabulku, ve ktere jsou ulozeny nedavno pouzite hlavicky. Tato tabulka
  je vymenna mezi klientem a serverem a umoznuje zakodovani hlavicek, ktere nejsou obsazeny ve staticke tabulce.
- Huffmanovo kodovani: HPACK pouziva Huffmanovo kodovani pro zakodovani casto pouzivanych retezcu. Tato technika snizuje
  velikost prenasenych dat zakodovanim casto se vyskytujicich znaku do kratsich binarnich kodu

## Webove sluzby

- Sluzba nabizena elektronickym zarizenim jinemu elektronickemu zarizeni, komunikujici spolu pres internet
- Sluzba bezici na pocitaci, poslouchajici pro requesty na urcitem portu pres interent

Vetsinou obsahuji object-oriented web-based interface do databazoveho serveru, vyuzito napriklad dalsim web serverem
nebo pomoci mobilni aplikace. Mnoho spolecnosti ktere poskytuji data v HTML formatu budou take poskytovat tyto data ve
forme XML nebo JSON na jejich serverech.

Existuji i jine zpusoby pro komunikaci s webovou sluzbou: Je jim napriklad komunikace podle filosofie CRUD(Create, read,
update, delete) realizovane typicky jako Representational State Transfer (REST), ktery v provedeni nad protokolem HTTP
vyuziva prave ctyr jeho metod (POST,GET,PUT,DELETE). Aby bylo mozno s daty na serveru pracovat, tato ctyri volani
vystavene sluzby staci.

webserver: Apache, Nginx, node express (jenom jako proxy)
nginx resi sifrovani apod.
pouziva se REST API pro predavani dat
http methody
SSL/TLS

## Status codes

[MDN DOCS](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)


