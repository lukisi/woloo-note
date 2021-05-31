# Annotazioni

### Learn TypeScript recipe

*   Learn JavaScript: the guide at the Mozilla Web Docs is a good starting point  
    [link](https://developer.mozilla.org/docs/Web/JavaScript/Guide)
*   Introduction to TypeScript for JavaScript Programmers (typescriptlang.org docs)  
    [link](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html)
*   Introduction to TypeScript for OOP Programmers (typescriptlang.org docs)  
    [link](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-oop.html)
*   Read the Handbook from start to finish  
    [link](https://www.typescriptlang.org/docs/handbook/intro.html)

# JavaScript

## Variables

JavaScript è case-sensitive e usa il set di caratteri Unicode.  
E.g. `let Früh = "foobar";`

Il carattere `;` separa le istruzioni. È opzionale a fine riga, ma
è buona prassi metterlo.

Si possono dichiarare variabili in 3 forme:

*   `var` - Declares a variable, optionally initializing it to a value.
*   `let` - Declares a block-scoped, local variable, optionally initializing it to a value.
*   `const` - Declares a block-scoped, read-only named constant.

*Nota:* esiste una forma di dichiarare una variabile e valorizzarla con il
valore di un membro di una struttura. Si chiama *Destructuring Assignment*.  
For example, `let { bar } = foo`. This will create a variable named `bar` and assign to it the value corresponding to the key of the same name from our object `foo`.

Se si assegna un valore ad una variabile non dichiarata si crea una
*undeclared global variable*. For example, `x = 42`. Javascript lo consente
ma è prassi sconsigliata.

### Variable scope

Se dichiaro una variabile con `var` fuori da qualsiasi funzione essa
è globale a tutto il codice.

Se dichiaro una variabile con `var` dentro una funzione essa è locale
a quella funzione.  
Il suo scope **non** è limitato ad un blocco di codice (ad esempio al
blocco di codice eseguito in una istruzione `if`).

Per limitare lo scope ad un blocco di codice si può usare la
keyword `let` (introdotta nel ECMAScript 2015).

*Nota:* le variabili (locali o di funzione) possono essere dichiarate
dopo il loro uso. In questo caso sono *undefined* fino al punto in
cui sono dichiarate, anche se sono inizializzate. Si chiama
*Variable Hoisting*.

Le variabili globali sono in effetti proprietà del cosidetto *global object*.

Nelle pagine web il global object è `window`. Quindi posso usare la
sintassi `window.varname` per accedere alla variabile globale `varname`.

### Tipi primitivi

Ci sono 7 tipi primitivi e poi gli oggetti.

*   *Boolean*. true and false.
*   *null*. A special keyword denoting a null value.
*   *undefined*. A top-level property whose value is not defined.
*   *Number*. An integer or floating point number. For example: 42 or 3.14159.
*   *BigInt*. An integer with arbitrary precision. For example: 9007199254740992.
*   *String*. A sequence of characters that represent a text value. For example: "Howdy"
*   *Symbol* (new in ECMAScript 2015). A data type whose instances are unique and immutable.

### Oggetti e funzioni

Si può pensare ad un oggetto come un contenitore di valori.  
Una funzione è un oggetto `Function` (non si usa il termine istanza e il
termine classe, è sempre un oggetto). Si può
pensare a una funzione come una procedura che la script può eseguire.

## Literals

**Arrays**

*   `[]` - un array vuoto
*   `['mela', 'pera', , 'pinolo']` - un array con 4 elementi.  
    L'elemento 2 (il terzo) è `undefined`.
*   `['mela', 'pera', 'pinolo',]` - un array con 3 elementi.  
    La virgola finale viene ignorata.

**Boolean**

*   `false` - falso
*   `true` - vero

**Number e BigInt**

*   Un numero se non inizia con `0` è interpretato in base 10.
*   Se inizia con `0` o `0o` o `0O` è interpretato in base 8.
*   Se inizia con `0x` o `0X` è interpretato in base 16.
*   Se inizia con `0b` o `0B` è interpretato in base 2.

Esempi:

```
0, 117, -345, 123456789123456789             (decimal, base 10)
015, 0001, -0o77, 0o777777777777             (octal, base 8)
0x1123, 0x00111, -0xF1A7, 0x123456789ABCDEF  (hexadecimal, "hex" or base 16)
0b11, 0b0011, -0b11, 0b11101001010101010101  (binary, base 2)
```


**Floating-point**

*Può* comprendere:

*   A decimal integer which can be signed (preceded by "+" or "-"),
*   Un punto decimale ("."),
*   A fraction (another decimal number),
*   An exponent. Cioè "e" o "E" seguito da un intero, which can be signed (preceded by "+" or "-").

*Deve* avere almeno una cifra; *deve* avere un punto decimale oppure una "e" (o "E").

More succinctly, the syntax is:

```
[(+|-)][digits].[digits][(E|e)[(+|-)]digits]
```

Esempi:

```
3.1415926
-.123456789
-3.1E+12
.1e-23
```

**Objects**

Un *object literal* si rappresenta dentro parentesi graffe (`{}`)
come una lista di 0 o più coppie chiave-valore.

La chiave, cioè il nome del membro dell'oggetto, può essere un qualsiasi
literal di stringa o di numero.  
Se si tratta di un valido identifier
(cioè inizia per carattere o `_` o `$` e in seguito può avere anche numeri)
allora può essere scritto senza apici; inoltre può essere acceduto
anche con la forma `varoggetto.nomemembro`.  
Altrimenti (se ad esempio si usa un numero come chiave, oppure una stringa
che inizia con un numero) può essere acceduto solo con la
forma `varoggetto[<literal>]`.

Il valore può essere qualsiasi dato, anche un altro oggetto.

```js
var sales = 'Toyota';
var car = { myCar: 'Saturn', special: sales };

console.log(car.myCar);   // Saturn
console.log(car.special); // Toyota

var car2 = { manyCars: {a: 'Saab', b: 'Jeep'}, 7: 'Mazda' };

console.log(car2.manyCars.b); // Jeep
console.log(car2[7]); // Mazda

var unusualPropertyNames = {
  '': 'An empty string',
  '!': 'Bang!'
}
console.log(unusualPropertyNames.'');   // SyntaxError: Unexpected string
console.log(unusualPropertyNames['']);  // An empty string
console.log(unusualPropertyNames.!);    // SyntaxError: Unexpected token !
console.log(unusualPropertyNames['!']); // Bang!
```

**Stringhe**

Possono essere racchiuse senza differenze tra apici o virgolette.

Un literal di tipo stringa non è tecnicamente un oggetto String. Ma
è buona prassi usarli. Dove serve un oggetto String la conversione
da un literal avviene in automatico e dopo l'uso l'oggetto viene rimosso.

```js
'foo'
"bar"
'1234'
'one line \n another line'
"John's cat"
```

Se si vuole usare un po' di sintassi nelle stringhe si hanno a disposizione i
*template literal* e anche i *tagged templates*. Si usano con i backtic.

```js
// Basic literal string creation
`In JavaScript '\n' is a line-feed.`

// Multiline strings
`In JavaScript, template strings can run
 over multiple lines, but double and single
 quoted strings cannot.`

// String interpolation
var name = 'Bob', time = 'today';
`Hello ${name}, how are you ${time}?`

let myTag = (str, name, age) => `${str[0]}${name}${str[1]}${age}${str[2]}`;
let [name, age] = ['Mika', 28];
myTag`Participant "${ name }" is ${ age } years old.`;
// Participant "Mika" is 28 years old.
```

## Control flow

**block statement** - non definisce uno scope per le variabili dichiarate
con `var`. Solo `let` e `const` dichiarano variabili block-scoped.

```js
{
    statement;
    statement;
    statement;
}
```

**if** - vedi
[Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean#description)
for an explanation of what evaluates to true and false.

```js
if (/*boolean expr*/) {
    dothis();
} else if () {
    dothat();
} else {
    donothing();
}
```

**switch** - Viene valutata l'espressione. Se il valore è fra quelli
indicati in un `case` il controllo passa allo statement sotto. Altrimenti
se esiste un `default` il controllo passa allo statement sotto. Altrimenti
esce dal blocco.  
Il caso `default` può essere anche messo prima del fondo, ma è prassi metterlo
in fondo.  
Se non si incontra un `break` il controllo prosegue. Se si incontra un `break`
si esce dal blocco.

```js
switch (expression) {
  case label_1:
    statements_1
    [break;]
  case label_2:
    statements_2
    [break;]
    …
  default:
    statements_def
    [break;]
}
```

**try...throw...cacth...finally** - Qualsiasi tipo di dato può essere
lanciato con uno statement `throw`; tuttavia esistono questi
standard types specifically created for this purpose:
[ECMAScript exceptions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error#error_types),
[DOMException](https://developer.mozilla.org/en-US/docs/Web/API/DOMException)
e [DOMError](https://developer.mozilla.org/en-US/docs/Web/API/DOMError).  
Ci può essere solo un blocco `catch`.
Il `catchID` esiste come identifier
solo nel blocco catch.

```js
openMyFile();
try {
  writeMyFile(theData); // This may throw an error
} catch(catchID) {
  handleError(catchID); // If an error occurred, handle it
} finally {
  closeMyFile(); // Always close the resource
}
```

### loops

**for(initial;check;increment) ...** - simile al C.

**do ... while(expr)** - eseguito almeno una volta, condizione valutata
alla fine.

**while(expr) ...** - condizione valutata
all'inizio.

**label...break...continue** -
lo statement `break` fa uscire dal blocco più interno (while, do-while, for, or switch) oppure da quello segnato con una label. Lo statement `continue`
passa alla prossima iterazione, anche qui con una opzionale label.

**for...in...** - assegna ad una variabile tutte le properties *enumerabili*
di un oggetto.

**for...of...** - assegna ad una variabile tutti i valori di un
oggetto che è *iterable*.

Esempio:

```js
const arr = [3, 5, 7];
arr.foo = 'hello';

for (let i in arr) {
   console.log(i); // logs "0", "1", "2", "foo"
}

for (let i of arr) {
   console.log(i); // logs 3, 5, 7
}
```

## Functions

La dichiarazione/definizione di una funzione in Javascript
in uno `statement`
è fatta con la sintassi:

*   keyword `function`
*   nome della funzione
*   fra parentesi lista di parametri
*   fra parentesi graffe blocco della funzione.

Esempio:

```js
function square(number) {
  return number * number;
}
```

Al momento della chiamata di una funzione gli argomenti sono
passati ai parametri *by value*. I dati di tipo primitivo sono
copiati, ma gli oggetti/array non sono copiati.

Un altro modo di definire una funzione è in una `expression`
con questa sintassi:

*   keyword `function`
*   *opzionale* nome della funzione - La funzione può restare anonima
    e la variabile che viene valorizzata può essere usata per
    chiamare la funzione. Comunque, il nome può essere dichiarato
    sia per permettere la ricorsività sia per avere un identificativo
    utile durante il debugging.
*   fra parentesi lista di parametri
*   fra parentesi graffe blocco della funzione.

Esempio:

```js
const square = function(number) { return number * number }
var x = square(4) // x gets the value 16

const factorial = function fac(n) { return n < 2 ? 1 : n * fac(n - 1) }
console.log(factorial(3))
```

Definendo una funzione come espressione è possibile definire
funzioni in base a condizioni, definire funzioni che sono
membri di ogggetti (*metodi*), ecc.

Esempi:

```js
var myFunc;
if (num === 0) {
  myFunc = function(theObject) {
    theObject.make = 'Toyota';
  }
}
```

Le funzioni sono visibili in uno *scope* come le variabili (cioè
l'intero programma o solo dentro un'altra funzione).  
Le funzioni definiscono un loro *scope* (all'interno dello scope
globale o quello di un'altra funzione).

Le funzioni definite come statement (ma non quelle definite
come expression) possono anche
essere definite dopo il loro uso, purché siano nello stesso scope.
Si dice *hoisted*.

Una funzione è a tutti gli effetti un oggetto. Si veda l'oggetto
[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function).
Tra i suoi metodi c'è `apply` che può essere usato per chiamare una
funzione in modo flessibile/dinamico.

### closures

Una funzione `outer` definisce uno scope per le variabili dichiarate
al suo interno. Sicché non sono accessibili dal suo esterno. Abbiamo
una sorta di *encapsulation*.  
Ora consideriamo una funzione `inner` definita dentro la funzione `outer`.
Essa ha accesso alle variabili definite in `outer` (oltre che
a quelle definite al suo interno e anche alle globali).  
Se la funzione `inner` è definita come espressione e assegnata
ad una variabile che sopravvive dopo la conclusione della funzione
`outer` allora viene creata una *closure*, cioè tutte le variabili
locali alla funzione `outer` dovranno sussistere anche dopo l'uscita
della funzione `outer` perché potranno essere utilizzate dalla funzione
`inner` che può essere chiamata tramite la variabile suddetta.

Faccio un esempio:

```js
var getNumber;
var addNumber;
var initNumber = function() {
    var theNumber = 0;
    getNumber = function() {
        return theNumber;
    }
    addNumber = function(inc) {
        theNumber += inc;
    }
}
initNumber();
console.log(getNumber());  // logs 0
addNumber(3);
console.log(getNumber());  // logs 3
addNumber(2);
console.log(getNumber());  // logs 5
```

La chiamata alla funzione `initNumber` inizializza a 0 `theNumber`
e valorizza le due funzioni *closures*. Solo per mezzo di queste
due funzioni `getNumber` e `addNumber` sarà possibile accedere in
lettura e in modifica a quel valore.

### oggetto arguments

La funzione che è in esecuzione in un dato momento può accedere
con la keyword `arguments` ad un oggetto con caratteristiche simili
ad un array:

*   `arguments[0]` - il primo argomento
*   `arguments.length` - il numero di argomenti

In questo modo posso passare ad una funzione più argomenti di quelli
che sono i parametri definiti nella firma.

### parameters

Tutti i parametri definiti nella firma hanno un valore di default
che se non specificato è `udefined`. Quindi posso sempre passare
meno argomenti di quelli
che sono i parametri definiti nella firma.

Posso indicare nella firma un valore di default diverso per ogni
parametro, anche se non sono gli ultimi parametri.

Esempio:

```js
function f(x = 1, y) {
  return [x, y]
}

f()   // [1, undefined]
f(2)  // [2, undefined]
```

Infine posso indicare come ultimo parametro un "*rest parameters*"
che conterrà un array con tutti gli argomenti passati in più
rispetto ai parametri definiti nella firma. La sintassi è:

```js
function myFun(a,  b, ...manyMoreArgs) {
    return manyMoreArgs;
}
myFun(1,2,3,4,5);   // [ 3, 4, 5 ]
```

### arrow function

Una funzione può essere definita in modo molto succinto con
l'operatore freccia così:

```js
var f1 = s => s.length;
console.log(f1("ciao")); // 4

var f2 = (a,b) => {console.log(a+b);}
f2(2,3); // 5
f2("ciao ", "mondo"); // ciao mondo
```

Si può notare che se l'unica istruzione del blocco è il valore da restituire
si può fare a meno delle parentesi graffe. E se c'è un solo parametro da
passare alla funzione si può fare a meno delle parentesi tonde.

Oltre alla brevità, le arrow function hanno come pecularità che
non definiscono un loro `this`.

### funzioni predefinite

JavaScript ha diverse funzioni top-level incluse nel framework:

*   eval()
*   uneval()
*   isFinite()
*   isNaN()
*   parseFloat()
*   parseInt()
*   decodeURI()
*   decodeURIComponent()
*   encodeURI()
*   encodeURIComponent()

## Operatori

Uso classico degli operatori binari e unari.

`**` eleva a potenza.

Se si usano gli operatori di comparazione su due operandi che non sono
dello stesso tipo Javascript cerca di fare un cast, di solito verso
un tipo *Number*. Se si vuole una stretta comparazione senza casting
bisogna usare `===` e `!==`.

Gli operatori aritmetici *tendono* a considerare i diversi tipi come
numerici e restituire valori *float*. Esempi:

```js
> "1" / "2"
0.5
> "1" / "2" == 1 / 2
true
> 1 / 2 == 1.0 / 2.0
true
```

Caso particolare il `+`. Come operatore unario davanti a una
stringa la converte in numero. Come operatore binario dopo una
stringa converte in stringa l'operando successivo e fa una
concatenazione. Esempi:

```js
> +"45"
45
> "45"
'45'
> "45"-3
42
> "45"+2
'452'
> +"45"+2
47
```

Gli operatori di assegnazione restituiscono un valore, quindi
si possono avere istruzioni concatenate che vanno interpretate
da destra verso sinistra, come queste:

```js
w = z = x = y;
// equivalent to
w = (z = (x = y));
// or
x = y; z = y; w = y
```

```js
z += x *= y;
// is equivalent to
z += (x *= y);
// or (except without the tmp)
tmp = x * y; x *= y; z += tmp;
```

### delete

L'operatore `delete` elimina una property da un oggetto.

**TODO** ....

# TypeScript

TypeScript è un linguaggio *transpiled*, cioè il compilatore `tsc` genera
un altro linguaggio (non codice macchina nativo) che in questo caso è
JavaScript e quindi viene interpretato.

Un valido codice JavaScript è anche un codice TypeScript (può essere passato
al comando `tsc`).

## Transpiler

Il comando `tsc nomefile.ts` legge il file TypeScript e genera un file
`nomefile.js`. Nel fare questa operazione controlla che i tipi definiti
siano usati correttamente.

Oltre a fare questo controllo per generare il file JavaScript che verrà
in ultima analisi interpretato ed eseguito da una VM (nodejs ad esempio
o un browser) il transpiler viene sfruttato dagli IDE per fornire tool
di aiuto alla programmazione come autocompletion, errori evidenziati, ecc.

Anche se ci sono errori, di norma il transpiler genera comunque il codice
JavaScript, assumendo che il programmatore sa il fatto suo. A meno che non
si voglia evitare con il flag `--noEmitOnError`.

Quando si produce il file `.js` tutte le definizioni dei tipi sono
rimosse. Una definizione di un tipo non modifica il comportamento a
run-time, ma solo aiuta nel fare i check a compile-time.

Inoltre di solito il transpiler fa anche un *downleveling*: cioè se incontra
codice che è stato introdotto in JavaScript (o ECMAScript, o ES) in una
versione recente cerca di produrre codice equivalente che funzioni bene
anche su una VM compatibile solo con una versione più vecchia.  
Per default cerca di aderire alla ES3. Si può cambiare se si pensa che
il runtime sarà di sicuro più recente, e.g. `--target es2015`.

Altri flag interessanti nel file `tsconfig.json`:

*   `noImplicitAny` - errore se il tipo di una variabile non è dichiarato
    e viene inferred come `any`.
*   `strictNullChecks` - controlla possibili usi di variabili a `null`
    o `undefined`.

## static type checking

Il principale valore aggiunto di TypeScript è il type system. Che viene
controllato (*checked*) al compile time.

Oltre ai tipi primitivi di JavaScript (che però non sono dichiarati alla
definizione di una variabile):  
`boolean`  
`bigint`  
`null`  
`number`  
`string`  
`symbol`  
`undefined`  
il TypeScript aggiunge:  
`any` (allow anything)  
`unknown` (ensure someone using this type declares what the type is)  
`never` (it’s not possible that this type could happen)  
`void` (a function which returns undefined or has no return value).

## Variabili

Posso dichiarare il tipo di una variabile così:

```ts
let name : string = "Carl";
```

## Funzioni

La firma di una funzione:

```ts
function getMult(op1 : number, op2 : number): number {
    ...
}
```

## Interfacce

Si può definire una interfaccia per specificare quali siano i tipi dei
membri (le chiavi) di un oggetto; e poi assegnare un oggetto congruo
ad una variabile definita per contenere quella interfaccia.

```ts
interface User {
  name: string;
  id: number;
}

let user: User = {
  name: "Hayes",
  id: 0,
};
```

## Classi

Si può definire una classe. Se è congrua con una interfaccia
si può usare con una variabile del tipo della interfaccia.

```ts
interface User {
  name: string;
  id: number;
}

class UserAccount {
  name: string;
  id: number;

  constructor(name: string, id: number) {
    this.name = name;
    this.id = id;
  }
}

const user: User = new UserAccount("Murphy", 1);
```

## Tipi composti

### Unioni

La keyword `type` con l'operatore unione `|` permette di creare un
tipo che, assegnato ad una variabile, elenca i possibili valori che può
assumere.

```ts
type MyBool = true | false;
type WindowStates = "open" | "closed" | "minimized";
type LockStates = "locked" | "unlocked";
type OddNumbersUnderTen = 1 | 3 | 5 | 7 | 9;
```

L'operatore unione `|` può essere usato **anche** per dichiarare una variabile
che può contenere uno fra diversi tipi.

```ts
function wrapInArray(obj: string | string[]) {
  if (typeof obj === "string") {
    return [obj];
  } else {
    return obj;
  }
}
```

### typeof

L'operatore `typeof` (del JavaScript, vedi
[doc](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof))
restituisce una stringa in base al tipo di una variabile.  
*Nota:* con un array l'operatore typeof restituisce "object", per
vedere se è un array si può usare `Array.isArray(a)`.

### Generics

Un esempio di classe che usa generics è `Array`. Se non si specifica il tipo può
contenere elementi di qualsiasi (any) valore.

```ts
type StringArray = Array<string>;
type NumberArray = Array<number>;
type ObjectWithNameArray = Array<{ name: string }>;
```

Possiamo anche noi definire un tipo che fa uso di generics.

```ts
interface Backpack<Type> {
  add: (obj: Type) => void;
  get: () => Type;
}

// This line is a shortcut to tell TypeScript there is a
// constant called `backpack`, and to not worry about where it came from.
declare const backpack: Backpack<string>;

// object is a string, because we declared it above as the variable part of Backpack.
const object = backpack.get();

// Since the backpack variable is a string, you can't pass a number to the add function.
backpack.add(23);  // errore dal type checker in compilazione
```

## type system strutturale

Abbiamo detto che in fase di compilazione (transpiling in effetti)
il TypeScript controlla la coerenza dei tipi. Ma non usa un type
system stretto, bensì uno basato sulla forma degli oggetti.

Un oggetto è considerato assegnabile ad una variabile di un certo tipo
se possiede tutti i membri di quel tipo.

```ts
interface Point {
  x: number;
  y: number;
}

function logPoint(p: Point) {
  console.log(`${p.x}, ${p.y}`);
}

// logs "12, 26"
const point = { x: 12, y: 26 };
logPoint(point);

const point3 = { x: 21, y: 55, z: 89 };
logPoint(point3); // logs "21, 55"

const rect = { x: 33, y: 3, width: 30, height: 80 };
logPoint(rect); // logs "33, 3"

const color = { hex: "#187ABF" };
logPoint(color);
// Error: Argument of type '{ hex: string; }' is not assignable to parameter of type 'Point'.
//        Type '{ hex: string; }' is missing the following properties from type 'Point': x, y
```

# Handbook

## primitivi

I tipi primitivi di JavaScript (che saranno usati come building blocks)
più frequentemente usati sono `string`, `number` e `boolean`.  
Il TypeScript usa queste stesse keyword (le stringhe che sarebbero restituite dall'operatore
`typeof` di JavaScript) per indicare questi tipi.  
*Nota* con la maiuscola iniziale sono altre cose che raramente useremo nel nostro codice.

## array

Un array che contenga un certo tipo si definisce con `number[]`. Si può usare anche
`Array<number>` che vedremo meglio con i generics.

*Nota*: Note that `[number]` is a different thing; refer to the section on tuple types.

## any

Una variabile dichiarata come `any` può contenere di tutto. Può avere qualsiasi membro,
anche esso sarà di tipo `any`. Quindi questo pezzo di codice non produrrà alcun errore
nel type checking al compile time:

```ts
let obj: any = { x: 0 };
// None of the following lines of code will throw compiler errors.
// Using `any` disables all further type checking, and it is assumed 
// you know the environment better than TypeScript.
obj.foo();
obj();
obj.bar = 100;
obj = "hello";
const n: number = obj;
```

## funzioni

Si può specificare il tipo dei parametri di una funzione e anche il tipo
del valore di ritorno, sia per una funzione normale, sia per una funzione
anonima, sia per una arrow-function.

```ts
function getMult(op1 : number, op2 : number): number {
    ...
}
```

Nel caso di una funzione anonima, usata in un certo contesto, il transpiler potrebbe
inferire questi tipi.

```ts
// No type annotations here, but TypeScript can spot the bug
const names = ["Alice", "Bob", "Eve"];

// Contextual typing for function
names.forEach(function (s) {
  console.log(s.toUppercase());  // <--- emits a error, since it knows that s:string
});

// Contextual typing also applies to arrow functions
names.forEach((s) => {
  console.log(s.toUppercase());  // <--- emits a error, since it knows that s:string
});
```


# Angular

Per avere versioni più recenti di nodejs, typescript e npm ho creato un
conatiner `agata` configurato per usare X11 del mio host, sul quale ho installato
questi pacchetti con snap.

Installa `node` con snap e questo fornisce anche `npm`.  
Aggiorna `npm` con `sudo npm install -g npm`.  
Non installare `typescript` con snap perché non funziona.  
Non installate `node-typescript` con apt perché poi installerebbe anche `nodejs`.  
Installa `typescript` con `npm`.

```bash
luca@dell:~$ lxc launch ubuntu:20.04 --profile default --profile x11 agata
luca@dell:~$ lxc exec agata -- sudo --user ubuntu --login
...
ubuntu@agata:~$ ... sudo apt full-upgrade -y ...
ubuntu@agata:~$ sudo apt install gnome-terminal
...
ubuntu@agata:~$ sudo snap login luca.dionisi@gmail.com
ubuntu@agata:~$ snap install --classic node
ubuntu@agata:~$ sudo npm install -g typescript
ubuntu@agata:~$ snap install --classic code
ubuntu@agata:~$ 
ubuntu@agata:~$ npm -v
6.14.13
ubuntu@agata:~$ tsc -v
Version 4.3.2
ubuntu@agata:~$ node -v
v14.17.0
ubuntu@agata:~$ code -v
1.56.2
054a9295330880ed74ceaedda236253b4f39a335
x64
ubuntu@agata:~$ 
```

Ora segui il corso Angular di Schwarzmuller. Se non si aggiorna il `npm` come
detto sopra, l'installazione di `@angular/cli` potrebbe non funzionare.


