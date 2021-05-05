# Annotazioni

# Javascript

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




