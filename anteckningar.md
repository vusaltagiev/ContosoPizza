HTTP REPL-verktyget i terminalen. Här är en stegen:

1. "För att köra i terminalen öpppna ett nytt terminal och skriv httprepl" - Detta startar HTTP REPL-verktyget, som är ett lättviktigt, plattformsoberoende kommandoradsverktyg som används för att göra HTTP-begäranden.

2. "http://localhost:{PORT}" - Ersätt {PORT} med portnumret där din applikation körs. Detta kommando ansluter HTTP REPL till din applikation.

3. "ls" - Detta kommando listar alla tillgängliga routes i din applikation.

4. "cd {Filnamn}" - Ersätt {Filnamn} med namnet på den route du vill navigera till. Detta kommando ändrar katalog till den angivna routen.

5. "get" - Detta kommando skickar en GET-begäran till den aktuella routen.
   




Valfritt: Testa det färdiga webb-API:et med KOMMANDORADEN HTTP REPL
Öppna den befintliga httprepl terminalen igen eller öppna en ny integrerad terminal från Visual Studio Code genom att välja Terminal>Ny terminal på huvudmenyn.

Om du öppnade en ny terminal ansluter du till webb-API:et genom att köra följande kommando:

.NET CLI

Kopiera
httprepl https://localhost:{PORT}
Du kan också köra följande kommando när som helst medan HttpRepl det körs:

.NET CLI

Kopiera
connect https://localhost:{PORT}
Gå till slutpunkten genom att Pizza köra följande kommando:

.NET CLI

Kopiera
cd Pizza
Kör följande kommando för att se de nya åtgärderna i Pizza-API:et:

.NET CLI

Kopiera
ls
Föregående kommando visar utdata från tillgängliga API:er för Pizza slutpunkten:

Output

Kopiera
    https://localhost:{PORT}/Pizza> ls
    .      [GET|POST]
    ..     []
    {id}   [GET|PUT|DELETE]
Gör en POST begäran om att lägga till en ny pizza i HttpRepl med hjälp av följande kommando:

.NET CLI

Kopiera
post -c "{"name":"Hawaii", "isGlutenFree":false}"
Föregående kommando returnerar den nyligen skapade pizzan:

Output

Kopiera
HTTP/1.1 201 Created
Content-Type: application/json; charset=utf-8
Date: Fri, 02 Apr 2021 23:23:09 GMT
Location: https://localhost:{PORT}/Pizza?id=3
Server: Kestrel
Transfer-Encoding: chunked

{
    "id": 3,
    "name": "Hawaii",
    "isGlutenFree": false
}
Uppdatera den nya Hawaii pizzan till en Hawaiian pizza med en PUT begäran med hjälp av följande kommando:

.NET CLI

Kopiera
put 3 -c  "{"id": 3, "name":"Hawaiian", "isGlutenFree":false}"
Föregående kommando returnerar följande utdata som indikerar att det lyckades:

Output

Kopiera
HTTP/1.1 204 No Content
Date: Fri, 02 Apr 2021 23:23:55 GMT
Server: Kestrel
Kontrollera att pizzan har uppdaterats genom att köra GET åtgärden igen med hjälp av följande kommando:

.NET CLI

Kopiera
get 3
Föregående kommando returnerar den nyligen uppdaterade pizzan:

Output

Kopiera
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Date: Fri, 02 Apr 2021 23:27:37 GMT
Server: Kestrel
Transfer-Encoding: chunked

{
    "id": 3,
    "name": "Hawaiian",
    "isGlutenFree": false
}
Vårt API kan också ta bort den nyligen skapade pizzan genom åtgärden DELETE om du kör följande kommando:

.NET CLI

Kopiera
delete 3
Föregående kommando returnerar ett 204 No Content resultat för lyckat resultat:

Output

Kopiera
HTTP/1.1 204 No Content
Date: Fri, 02 Apr 2021 23:30:04 GMT
Server: Kestrel
Kontrollera att pizzan har tagits bort genom att köra GET åtgärden igen med hjälp av följande kommando:

.NET CLI

Kopiera
get
Föregående kommando returnerar de ursprungliga pizzorna som resultat:

Output

Kopiera
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Date: Fri, 02 Apr 2021 23:31:15 GMT
Server: Kestrel
Transfer-Encoding: chunked

[
    {
        "id": 1,
        "name": "Classic Italian",
        "isGlutenFree": false
    },
    {
        "id": 2,
        "name": "Veggie",
        "isGlutenFree": true
    }
]