## part2.
```sh



```

> question 1, tell if the following code is working (again) : 

```js
/* test */
function getList ( ) {
  return functionThatReturnsAPromise ( )
}

async function main ( ) {
  const list = await getList ( )
  // ...
}

main ( )


```


> Où les logs d'une application doivent-ils être stockés selon la méthodologie Twelve-Factor App ?

Selon la méthodologie Twelve-Factor App, les logs d'une application doivent être traités comme des flux de données événementiels et écrits sur la sortie standard (STDOUT). Ils ne doivent pas être écrits directement dans des fichiers de log, mais plutôt dirigés vers un service de journalisation externe ou un système de gestion des logs. Cela permet une gestion centralisée des logs et facilite le suivi des événements d'une application distribuée.



> Write a mocha should test for this 

Considérons la fonction suivante :


```js
function isThisNumberAGood (number)
return Promise. resolve)
then (function (
const a = parseInt ( ${number}, 10);
if (number !== 0 && la) {
throw new Error ('not a number');
return a == 12;
```

```js
const assert = require('assert');

describe('isThisNumberAGood', function() {
  it('should return true if the number is 12', function() {
    return isThisNumberAGood(12).should.eventually.equal(true);
  });

  it('should return false if the number is not 12', function() {
    return isThisNumberAGood(10).should.eventually.equal(false);
  });

  it('should throw an error if the input is not a number', function() {
    return isThisNumberAGood('not_a_number').should.be.rejectedWith(Error, 'not a number');
  });
});


```


