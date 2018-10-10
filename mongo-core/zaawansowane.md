# Mongo zaawansowane rozwiązania:

---

## CRUD zaawansowny

# C - insert

```js
db.user.insertOne({ name: "Paweł" });
```

- automatycznie zostanie wstawione pole \_id, jeżeli nie przekazaliśmy własnego
- \_id jest wstawiane z użyciem funkcji ObjectId(), który musi być unikalny. ObjectId składa się z timestamp, machine name(hash), pid (process id), increment, co daje nam 16.777.216 niepowtarzalnych id na sekunde na jeden proces.
- ponieważ timestamp jest pierwszą częścią ObjectId, oznacza to automatyczne sortowanie po dacie.

```js
insertMany(); // przyjmuje tablice dokumentów

db.user.insertMany([
  {
    name: "Paweł"
  },
  {
    name: "Jacek"
  }
]);
```

- wysyłanie tysięcy dokumentów w jednej procedurze może być wyraźnie szybsze
- gdy chcemy pobrać dane z np. MySQL powinniśmy użyć mongoimport, zamiast insertMany()
- jednym wsadem możemy przesłać 48MB danych
- jeżeli pojawi się error podczas tworzenia dokumentów, to wszystkie instrukcje po nim nie będą miały miejsca, gdyż domyślny tryb dodawania danych jest z flagą ordered insert. Można to zmodyfikować używając unordered insert, wtedy tylko rzeczy, które powodują error nie znajdą się w kolekcji

```js
// zapisze wszystkie unique dokumenty
db.user.insertMany(
  [
    {
      name: "Paweł"
    },
    {
      name: "Paweł"
    },
    {
      name: "Jacek"
    }
  ],
  { ordered: false }
);
```

**Walidacja dokumentów**

1. MongoDB robi minimalne sprawdzenie danych, które będą dodawane.
2. Wszystkie dokumenty muszą być mniejsze niż 16MB
3. Sprawdzenie wielkości dokumentu można wykonać funkcją Object.bsonsize(doc), wynik jest w bajtach.

## R - delete

deleteOne(), deleteMany() -> pierwszy parametr to filter, działa na dokumentach kolekcji.

Usunięcie kolekcji drop();

```js
db.user.drop();
```

## U - update

replaceOne(), updateOne(), upadateMany(), dla wszystkich pierwszy parametr to filter. updateOne(), updateMany() -> 2 parametr to modyfikator, replaceOne() -> parametr to dokument.

Powyższe operacje używają zasad:

- ostatni wygrywa
- operacje są atomiczne

Update posiada specjalne operatorami, które są kluczami, za pomocą, których można stworzyć bardziej złożone operacje takie jak dodawanie, usuwanie kluczy, modyfikowanie tablic i osadzonych dokumentów.

Operatory rozpoczynają swoją nazwę od $.

```js
{
  "url": "opi.com",
  "pageviews": 200
}

db.analytics.updateOne({"url": "opi.com"}, {"$inc": {"pageviews": 1}})
```

1. $set -> ustawia wartość pola, jeżeli pole nie istnieje, zostanie utworzone. Przydatny przy zmianie struktury dokumentu, może również zmieniać typ danych.

2. $unset -> usuwa pole z dokumentu

3. $inc -> zwiększa wartość o podaną. Może być użyty tylko z integer, long, doubrle

4. $push -> dodaje element na koniec tablicy w dokumencie

5. $pop -> usuwa element z końca tablicy w dokumencie.

6. $addToSet -> dodaje element jeżeli nie istnieje (not redundand);

7. $pull -> usuwa element z tablicy, wg podanych kryteriów, a nie na podstawie pozycji jak np. $pop.

**Operatory** posiadają modyfikatory. Np. $each, $ne, $sort, $slice. Modyfikatory również rozpoczynają swoją nazwę od $. Ich główną zaletą jest możliwośc łączenia w łańcuch.

**Upsert** - specjalny rodzaj update. Jeżeli element nie zostanie znaleziony na podstawie filtra zostanie utworzony. Dzięki czemu nie musimy sprawdzać całej bazy w poszukiwaniu elementu i dopiero dodawać jeżeli nie istnieje.

```js
db.analytics.updateOne(
  { url: "/university" },
  { $inc: { pageviews: 1 } },
  { upsert: true }
);
```

---

Czasami potrzebujemy coś znaleźć w celu wykonania operacji na tym, dlatego funkcje są pomocne:

```js
findOneAndDelete();
findOneAndReplace();
findOneAndUpdate();
```
