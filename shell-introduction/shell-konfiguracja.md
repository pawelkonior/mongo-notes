# Shell konfiguracja

W mongo shell mozemy używać niemal całego Javascriptu, główne funkcjonalności, które nie działają to pobieranie plików z zewnętrznych serwerów. (np. fetch, XmlHTTPRequest).

---

W mongo shell Javascipt służy do ułatwienia nam pracy, dlatego istotne jest zorganizowanie sobie odpowiednich narzędzi.

Powinniśmy sobie stworzyć zestaw narzędzi (helpers), które będziemy reużywać. Narzędzia tego typu możemy zapisać w plikach nazwa_pliku.js, a następnie możemy je załadować w zależności od potrzeby.

```js
load("sciezka_do_pliku/nazwa_pliku.js");
// sprawdzanie czy nasza funkcja jest dostępna (bez nawiasów okrągłych na końcu)
typeof nazwa - funkcji;
// undefined - nie jest dostępna, źle wczytaliśmy
// function - możemy używać
```

Od tego momentu, możemy używać wszystkich funkcji znajdujących się w podanym pliku.

Jak wyznaczyć ścieżkę do naszego pliku z Javascriptem?

```bash
run("pwd") //działa tylko na system UNIX-like
run("ls", "-l", "/home/uzytkownik/mongo-helpers/") // funkcja run pozwala wywoływać różne skrypty na domyślnej powłoce systemu (np. bash)
```

Jednak ładowanie plików do każdej sesji w mongo shell staje się męczące, dlatego możemy zautomatyzować ten proces tworząc plik .mongorc.js w katalogu domowym komputera.

```js
// .mongorc.js
print("Witaj mój Panie"); //spowoduje, że mongo shell będzie witał nas odpowiednią wiadomością
```

Jeżeli .mongorc.js istnieje w katalogu domowym to domyślnie będzie uruchamiany z każdą sesją. Jeżeli nie chcemy, aby w nowej sesji zostały użyte funkcjonalności z .mongorc.js:

```bash
mongod --norc //wyłączy mongorc
```

Mongorc nie musi służyć tylko do dodawania naszego zestawu funkcji, jest to dobre miejsce na konfiguracje, np. jaki edytor powinien domyślnie zostać użyty przy edytowaniu kodu:

```js
EDITOR = "/usr/bin/vim"; //vim na unix-like systemach, edytor musi istnieć w systemie, abyśmy go mogli użyć
```

Mongorc funkcjonalność, która nas zabezpiecza przed usunięciem bazy, bądź kolekcji:

```js
// wyrażenie funkcyjne, które zostanie wywołane, jeżeli użytkownik spróbuje usunąć baze
const messageForUser = () => {
  print("nie rób tego");
};

//usuwanie bazy
db.dropDatabase = DB.prototype.dropDatabase = messageForUser;
//usuwanie kolekcji
DBCollection.prototype.drop = messageForUser;
//usuwanie indexu
DBCollection.prototype.dropIndex = messageForUser;
```
