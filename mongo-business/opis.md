# Opis NoSQL

1. Brak relacji
2. Brak stałej struktury danych
3. Open source
4. Rozproszona
5. Ostatecznie spójna
6. Dobrze skalowalna
7. Rozwijana przez największe internetowe firmy

# Spójność

1. Teoria CAP - bazy danych mogą mieć tylko 2 z tych 3 cech: spójność, dostępność, tolerancja podziału

2. NoSQL nie daje nam ACID: atomicity, consistency, isolation, durability

3. W zamian oferuje ostateczną spójność, która działą jak DNS propagation

# Zapytania

1. Brak języka zapytań
2. Do zapytań stosuje się programowanie proceduralne

# Sharding

1. Wzorzec, w którym osobne serwery utrzymują poszczególne części bazy
2. Partycje mogą być zduplikowane, więc replikacja jest wbudowana
3. Przydatne do trzymania danych blisko procesów biznesowych rozproszonych geograficznie.
