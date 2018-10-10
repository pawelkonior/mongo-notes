# Shell

Shell jest powloka pozwalajaca na dostep do instancji serwera Mongo. W calosci uzywa JS (mimo, ze sama baza jest napisana w C++). Jest to zwiazane z rodowodem i popularnoscia MongoDB, ktora wziela sie z wielkich ilosci danych pochodzacych z aplikacji internetowych.

```bash
mongod
```

- mongod odpala serwer MongoDb (deamon)
- bez parametrow domyslnie uzywa /data/db lokalizacji
- jezeli /data/db nie istnieje lub nie ma praw zapisu, to sypnie bledem
- domyslny port to 27017

```bash
mongod --dbpath ~/data/rs1 --port 27017
```

- --dbpath - definiuje miejsce na dysku, gdzie dane beda zapisywane
- ~/ w systemach UNIXowych oznacza katalog domoy, na windowsie nalezy uzyc C:\ itd.
- --port definiuje, na ktorym porcie zostanie uruchomiony serwer, mozna wybrac dowolny, ktory nie jest uzywany.
