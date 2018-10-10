# Javascript podstawy

Javascript to implementacja standardu ECMA SCRIPT. Obecna wersja to 2018. Niestety nie wszysktie nowe funkcjonalnosci działają, gdyż jest to zależne od srodowiska, na którym uruchamiamy Javascript. W mongo shell jest to V8.

---

## Tworzenie zmiennych

```js
var nazwa_zmiennej = "wartosc";
let nazwa_zmiennej = "wartosc";
const nazwa_zmiennej = "wartosc":
```

var - starsza wersja tworzenia zmiennych, zasieg funkcyjny, moze zostac ponownie zadeklarowana, moze zostac ponownie zainicjalizowana, jest hoistowana.

let - nowy sposob deklarowania zmiennych w JS, zasieg blokowy, moze zostac ponownie zadeklarowana, nie moze byc ponownie zainicjalizowana, nie jest hoistowana.

const - nowy sposob deklarowania zmiennych (stalych) w JS, zasieg blokowy, nie mozna ponownie zadeklarowac ani zainicjalizowac, (typy referencyjne moga byc modyfikowane, referencja nie moze zostac zmieniona), nie jest hoistowana.

## Hoisting

Przenoszenie deklaracji funkcji oraz deklaracji zmiennych stworzonych za pomoca var na poczatek aktualnego zasiegu.

```js
console.log(zmienna);
var zmienna = 1;

//bedzie przetworzone jako:
var zmienna;
console.log(zmienna);
zmienna = 1;
```

## Zasieg

Zasieg definiuje, gdzie zmienne i deklaracje funkcji sa widoczne (dostepne)

Funkcyjny:

```js
function name() {
  // zasieg funkcyjny obowiazuje w tych klamerkach, tworza go tylko funkcje
}
```

Blokowy:

```js
{
  // zasieg blokowy tworzony jest przez dowolna pare klamerek
}

if (1) {
  // zasieg blokowy
}

for (let i = 0; i < 10; i++) {
  //zasieg blokowy
}
```

## Warunki

Glownym narzedziem do sprawdzania warunkow w JS jest wyrazenie if oraz operator trojkowy, switch.

```js
const warunek = true;
const warunek2 = true;

if (warunek) {
  //kod jezeli prawda
} else {
  //kod jezeli nieprawda
}

if (warunek) {
  //prawda dla warunku
} else if (warunek2) {
  //prawda dla warunek2
} else {
  //jezeli w ogole falsz
}

warunek ? console.log("prawda") : console.log("falsz");
```

## Petle

Uzywane jezeli mamy do przetworzenia wiele elementow, for, for in, for of, while, do while.

```js
// for(inicjalizacja, warunek, inkrement){
//kalkulacje
//}

for (let i = 0; i < 10; i++) {
  // zrob cos
}
```

## Funkcje

Funkcje to podstawa JS, do dyspozycji mamy funkcje nazwane, wyrazenia funkcyjne, funkcje anonimowe, funkcje strzalkowe (arrow function). Funkcje moge przyjmowac argumenty (arguentem moze byc wszystko, nawet inne funkcje)

Funkcja:

```js
//deklaracja
function nazwa(parametr) {
  //kalkulacje
  return "xwrocic mozna cokolwiek";
}
//wywolanie
nazwa("argument");
```

Wyrazenie funkcyjne, uzywa funkcji anonimowej przypisanej do zmiennej:

```js
//deklaracja
const dodaj = function(parametr) {
  return "zwroc cos";
};
//wywoalanie
dodaj("argument");
```

Arrow function:

```js
//jeden parametr
const dodaj = parametr => {
  return "cos";
};

//brak parametrów
const dodaj = () => {
  return "cos";
};

//2+ parametrow
const dodaj = (parametr1, parametr2) => {
  return "cos";
};

//niejawny return, jezeli miescimy sie w 1 linijce to nie musimy pisac retrun i tak wartosc zostanie zwrocona
const dodaj = () => "cos";
```

## Closures/domkniecia (C.E.V.E., backpack)

Domkniecie to dostep do zmiennej spoza aktualnego zasiegu w momencie wywolania.

```js
function sentence(city) {
  return function(name) {
    return `Mam na imie ${name}, pochodze z ${city}`;
  };
}

//wywolanie:
const s1 = sentence("Warszawa");
const res1 = s1("Pawel");
const res2 = s1("Jacek");
```

## Klasy

Klasy to lukier skladniowy, czyli klasy w rozumieniu obiektowym nie istnieja, natomiast je symulujemy.

```js
//deklaracja klasy
class Auto {
  //kluczowa funkcja, uruchamiana zawsze kiedy tworzymy nowa instancje (egzemplarz klasy)
  constructor(silnik) {
    //property klasy mozna deklarowac tylko przez konstruktor
    this.silnik = silnik;
  }

  //funkcje (metody) klasy mozna deklarowac w ciele klasy
  getEngineName() {
    return this.silnik;
  }
}

//tworzenie egzemplarza:
const bmw = new Auto("v8");
bmw.getEngineName();
```

## Generatory:

Generator to zautomatyzowany iterator. Iterator to funkcja, która wie w jaki sposob przetwarzac dane.

Generator to funkcja, ktora oznaczamy gwiazdka, posiada slowo kluczowe yield.

Yield to return na sterydach, zwraca wartosc i pauzuje generator dokladnie w tym miejscu, w ktorym znajduje sie yield.

```js
function *flow(){
  let a  = 10;
  a = yield 5;
  yield a + 10;
}

const f = flow();
f.next(); // value: 5
f.next(25): // value: 35
f.next(); // value undefined
```

## JS paradygmaty

JS jest jezykiem wieloparadygmatowym, mozna w nim prograowac funkcyjne oraz obiektowow.

Programowanie funkcyjne - w skrócie oparte na pure function, czyli funkcji w rozumieniu matematycznym, ten sam input, ten sam output, brak side efektow

Programowanie obiektowe - w skrócie oparte o klasy i obiekty, (enkapsulacja, polimorfizm, dziedzczenie, itd.)
