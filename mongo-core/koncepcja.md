# Kocnepcja

## Dokumenty

Dane w MongoDb sa zapisywane jako dokumenty (documents). Documents to JSON-like obiekt.

JSON - javascript object notation.

- sklada sie z klamerek (definiuje obiekt)
- par klucz wartosc
- klucz musi byc w cudzyslowach
- wartosc musi byc w cudzyslowach jezeli jest tekstem (string)
- pary sa oddzielane przecinkami
- klucz w obrebie jednego obiektu nie moga sie powtarzac

```js
{
  "klucz": "wartosc",
  "klucz2": "wartosc",
  "klucz3": 10,
  "klucz4": [1, 2, 3],
  "klucz4": {
    "klucz": "warosc",
    "klucz2": {
      //itd
    }
  }
}
```

JSON - tworca Douglas Crockford (kluczowa osoba w swiecie JS).

Sprawdzenie poprawnosci JSON:
[JSON validator](https://jsonlint.com/)

Zasady:

- wielkosc liter ma znaczenie
- typ danych ma znaczenie
- kolejnosc danych ma znaczenie

```js
//typ
{
  "count": 5
}
{
  "count": "5"
}

//wielkosc liter
{
  "count": 5
}
{
  "Count": 5
}

//kolejnosc, 2 rozne dokumenty
{
  "x": 1,
  "y": 2
}
{
  "y": 2,
  "x": 1
}
```

## Kolekcje (collections)

Dokumenty sa grupowane w kolekcje. Kolekcje moga miec dynamic schemas (dynamiczna strukture). Kolekcje sa identyfikowane przez nazwe.

Nazwa:

- tekst UTF-8
- bez pustego string ("")
- bez \0 (null)
- kropka na poczatku jest zarezerwowana dla wewnetrznych kolekcji
- $ nie powinno sie uzywac, bo operatory i modyfikatory korzystaja z tej konwencji

## Podkolekcje (subcollection):

Uzywane jako przestrzen nazw (namespace). np. shop.customers, shop.products itd.

- sa uzywane np w GridFS (protokol przechowywania duzych plikow)

## Bazy danych

Sluza do grupowania kolekcji, jedna instancja mongo moze zawierac wiele baz. Kazda baza ma:

- wlasne zasady dostepu
- osobny plik na dysku

Nazewnictwo:

- string UTF-8
- brak pustego stringa ("")
- generalnie alphanumeric ASCII
- wielkosc liter ma znaczenie
- dobrze jest uzywac malych liter
- maksymalnie 64bytes
- zarezerwowane nazwy: admin, local, config

Bazy wbudowane:
admin - autoryzacja
local - dane dla pojedynczego serwera mongo, nie jest replikowana
config - sharder mongo cluster, kazdy shard ma tutaj swoje dane.
