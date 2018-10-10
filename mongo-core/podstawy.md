# Mongo podstawy

Po połączeniu z bazą mamy dostępne zmienne i funkcje wbudowane w mongo shell.

## db

```js
db;
//test
//zawsze pokazuje aktualnie używaną bazę
```

Shell posiada wbudowany dodatek, który pozwala nam używać pewnych funkcjonalności, które nie są poprawnym Javascript. Zostało to zrobione po to, aby ludzie migrujący z baz SQL mogli łatwo odnaleźć się w nowym środowisku.

```js
use nazwa_bazy
//przełączy na baze nazwa_bazy
```

## Podstawowe operacje

---

## Create

Aby dodać dokument do naszej kolekcji możemy użyć insertOne(), insertMany();

```js
//tworzymy dokument (obiekt JSON-like)
const doc = {
  name: "Pawel",
  surname: "Konior"
};

//dodajemy do kolekcji user w bazie, którą aktualnie używamy
db.user.insertOne(doc);

//sprawdzamy, czy się dodało
db.user.findOne();
```

## Read

Odczytywanie danych z bazy możemy zrealizować za pomocą find() i findOne()

```js
//szukamy pierwszego pasującego dokumentu do warunku przekazanego w parametrze funkcji findOne(), jeżeli nie przekażemy nic to zostanie zwrócony pierwszy element.
db.user.findOne();
```

## Update

W celu zmodyfikowania istniejącego elementu możemy użyć updateOne(), która wymaga conajmniej 2 argumentów. Pierwszy to kryteria do znalezienia elementu, który chcemy zmodyfikować, drugi argument to nowy dokument

```js
db.user.update(
  {
    name: "Paweł"
  },
  ($set: { name: "Paweł Paweł" })
);
```

## Delete

Usuwanie realizujemy za pomocą deletOne(), deleteMany(), które usuwa dokument z kolekcji na zawsze.

```js
db.user.deleteOne({ name: "Pawel" });
```

## CRUD

Funkcje insertOne() (C), findOne() (R), insertOne() (U), deleteOne() (D) - dają nam pełną implementacje CRUD (create, read, update, delete).

Jeżeli chcemy stworzyć nowy dokument - insertOne(), insertMany()

Jeżeli chcemy odczytać jakiś dokument - find(), findOne()

Jeżeli chcemy zmodyfikować dokument - updateOne(), updateMany()

Jeżeli chcemy usunąć dokument - deleteOne(), deleteMany()

## Typy danych:

# JSON:

1. null
2. boolean
3. numeric
4. string
5. array
6. object

# Javascript:

1. null
2. boolean
3. number
4. string
5. object
6. symbol
7. undefined

# Mongo JSON-like dokument (BSON) pola:

1. **null**: reprezentuje wartość null (nic) oraz wartość nie istniejącą. {"name": null}
2. **boolean**: true, false. {"name": true}
3. **number**: domyślnie 64 bajtowa liczba zmiennoprzecinkowa. {"age": 35.4}

```js
{"age": NumberInt("30")} // 4 bajty
{"age": NumberLong("30000")} //8 bajtów
// powyższe metody pozwalają zaoszczędzić miejsca w bazie do przechowywania danych.
```

4. **string**: UTF-8
5. **date**: 64 bitowa liczba reprezentująca ilość milisekund liczonych od początku epoki Unixa (1 styczeń 1970). Strefa czasowa jest nie zapisywana, w tej kwestii dobrze jest użyć dodatkowego property w dokumencie. Czas brany jest z urządzenia, na których jest uruchomiony serwer.
6. **regular expression**: używa wyrażeń regularnych z Javascript, czyli standardu PCRE (Perl compatible regular expressions). {"name": /[A-Z]/i}
7. **array**: zbiór danych. {"hobbies": ["alcohol", "drugs", "javascript"]}
8. **object id**: 12 bajtowy ID dla dokumentu.
9. **binary data**: literał tekstowy zawierający bajty. Nie można go modyfikować z poziomu shella. Jedyny sposób na zapisanie znaków spoza UTF-8.
10. **code**: możliwość zapisywania Javascriptu jako wartości dla pola. {"name": function(){//ciało funkcji}}
