# Shell uruchomienie

Shell jest powłoką pozwalająca na dostęp do instancji serwera Mongo. W całości uzywa JS (mimo, ze sama baza jest napisana w C++). Jest to związane z rodowodem i popularnoscia MongoDB, która wzieła się z wielkich ilości danych pochodzących z aplikacji internetowych.

```bash
mongod
```

- mongod odpala serwer MongoDb (deamon)
- bez parametrów domyślnie uzywa lokalizacji /data/db
- jezeli /data/db nie istnieje lub nie ma praw zapisu, to sypnie błędem
- domyślny port to 27017

```bash
mongod --dbpath ~/data/rs1 --port 27017
```

- --dbpath - definiuje miejsce na dysku, gdzie dane beda zapisywane
- ~/ w systemach UNIXowych oznacza katalog domowy, na windowsie nalezy uzyć C:\ itd.
- --port definiuje, na którym porcie zostanie uruchomiony serwer, mozna wybrac dowolny, ktory nie jest aktualnie uzywany.
