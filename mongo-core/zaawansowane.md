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
