## Some questions.
```sh



```

> question 1, tell if the following coede is working : 

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

> answer 1 :

```js

function getList() {
  // This function returns a promise (functionThatReturnsAPromise)
  return functionThatReturnsAPromise();
}

async function main() {
  // Await the result of getList, which returns a promise
  const list = await getList();
  // Once getList promise resolves, continue with further processing...
}
// Call main function to start the asynchronous execution
main();

```

> Question 2 : "Votre entreprise possède 2 produits basés sur Node.js, le premier destiné à l'Italie (avec 2000 utilisateurs actifs par jour) et le second destiné à l'Angleterre (avec 1000 utilisateurs par jour). Ces produits fonctionnent avec les mêmes codebases Node.js et Express.js API, mais avec des localisations différentes.

Un jour, votre entreprise a acheté des serveurs pour 24 CPU au total dans des datacenters en Allemagne.

Votre tâche consiste à scaler horizontalement l'application Node.js afin de consommer pleinement tous les CPU de ce serveur. Que devez-vous faire ?" 


> Question 3 : 

"Quel sera la sortie du code suivant ?
```js
const buffer = Buffer.alloc(7, 'Hello');
console.log(buffer.toString() + '*')"

```

> Question 4 :

"Considérez ces deux options :

Option #1
```DOCKER
FROM node:12-alpine3.12

RUN mkdir /app
ADD package.json /app/package.json
ADD package-lock.json /app/package-lock.json
WORKDIR /app
RUN npm ci --only=production

ADD . /app

EXPOSE 3000

ENTRYPOINT ["node","index.js"]
```


Option #2

FROM node:12-alpine3.12

RUN mkdir /app
ADD . /app
WORKDIR /app
RUN npm ci --only=production

EXPOSE 3000

ENTRYPOINT ["node","index.js"]

Quelle option permet d'augmenter les performances du système CI/CD, en supposant qu'elle génère une image Docker plusieurs fois par heure?"


Answer 4 :

L'Option #1 est plus performante pour le système CI/CD, surtout si l'image Docker est générée plusieurs fois par heure. Cela est dû à l'ordre des instructions dans le Dockerfile :

Dans l'Option #1, les instructions ADD package.json /app/package.json et ADD package-lock.json /app/package-lock.json sont exécutées avant la copie de l'ensemble du répertoire avec ADD . /app. Cela signifie que si le contenu de package.json ou package-lock.json n'a pas changé, le cache de l'image Docker peut être réutilisé lors de la création de l'image, ce qui réduit le temps nécessaire pour construire l'image.
En revanche, dans l'Option #2, tout le répertoire est ajouté à l'image avant l'exécution de npm ci --only=production. Cela signifie que même si seuls les fichiers package.json ou package-lock.json ont changé, l'étape npm ci doit être réexécutée, ce qui peut entraîner une perte de temps.




> Question 5 : 
"Vous avez une base de données MySQL contenant des articles et le code Express.js suivant :
```js
// get the client
const mysql = require('mysql2')
const validator = require('validator')

// create the connection to database
const connection = mysql.createConnection({
host: 'localhost',
user: 'root',
database: 'test'
})
app.get('/post/:title', function (req, res, next) {
const title = req.params.title;
if (validator.isEmpty(title)) {
return res.render('404.html');
}
connection.query('SELECT * FROM posts WHERE title = ' + title, function (err, result) {
if (err) {
return next(err);
}
res.render('post.html', result);
})
})

```


Des hackers ont envoyé une demande à :

GET http://example.org/post/1;DROP ALL TABLES;

et la base de données a exécuté la requête suivante :

SELECT * FROM posts WHERE title = 1; DROP ALL TABLES;

Quelle est la meilleure stratégie pour éviter ces attaques ?"

Answer 5 :

Pour éviter ce type d'attaque, vous pouvez utiliser des requêtes paramétrées ou des requêtes préparées. Dans le code Express.js fourni, la requête SQL est construite en concaténant la variable title directement dans la chaîne de requête :

javascript

connection.query('SELECT * FROM `posts` WHERE `title` = ' + title, function(err, result) {

Cela rend votre application vulnérable aux attaques par injection SQL. Pour éviter cela, vous devriez utiliser des requêtes paramétrées comme ceci :

javascript

connection.query('SELECT * FROM `posts` WHERE `title` = ?', [title], function(err, result) {

Avec cette approche, les valeurs des paramètres sont transmises séparément de la requête SQL, ce qui rend l'injection SQL impossible car les paramètres sont traités de manière sécurisée par la bibliothèque de base de données.



> Question 6 :



"Vous souhaitez créer une application Node qui retourne la racine carrée du nombre passé en argument :
```bash

node square.js 9
3

```
Par quoi doit-on remplacer  ???  dans le code suivant pour que l'application fonctionne comme attendu ?

```js
const math = require('mathjs')

const result = math.sqrt( ??? )

console.log(result)"

```


>Answer 6 :
```js
const math = require('mathjs');

const result = math.sqrt(process.argv[2]);

console.log(result);

```

> Question 7 : 

"Que retourne ce script ?
```js
const EventEmitter = require('events');

class MyEmitter extends EventEmitter {}

const myEmitter = new MyEmitter();
myEmitter.on('event', function(a,b) {
console.log(a, b, this === myEmitter);
});
myEmitter.emit('event', 'a')"


```

> Answer 7 :

Ce script crée une instance de MyEmitter, une classe qui étend EventEmitter du module events de Node.js. Ensuite, il attache un écouteur d'événements à l'événement 'event' avec la méthode on(). L'écouteur d'événements est une fonction anonyme qui prend deux arguments a et b et qui imprime a, b, et this === myEmitter dans la console. Enfin, il émet l'événement 'event' avec la méthode emit() en passant 'a' comme argument.

Lorsque l'événement est émis, la fonction anonyme attachée à l'écouteur d'événements est appelée avec 'a' comme premier argument. Elle imprime ensuite 'a', undefined (car il n'y a pas de deuxième argument passé lors de l'émission de l'événement), et true (car this === myEmitter est vrai dans le contexte de la fonction de rappel attachée à myEmitter).

Ainsi, la sortie de ce script sera :

javascript
Copy code
a undefined true



> Question 8 :

"Dans cet exercice, vous devez implémenter la fonction `createEE` qui crée une instance EventEmitter capable d'émettre des données à un intervalle défini.

`createEE` prend en entrée `opts`, un objet option. `opts` contient les propriétés suivantes :
- `opts.fn` : une fonction synchrone. La sortie de la fonction doit être émise avec l'événement `data`.
- `opts.interval` : l'intervalle, en millisecondes, entre les événements `data`.
- `opts.signal` : un objet `AbortSignal` à utiliser pour émettre un événement `close` et arrêter l'émission de données.

Notes :
- Si une erreur se produit lors de l'appel de la fonction `fn`, l'erreur doit être émise avec l'événement `error`.
- Le premier événement doit être émis immédiatement après la création de l'EventEmitter."


Constrains : to be added


the function should be made following this constrains :
```js
// JavaScript code​​​​​​‌​​‌​‌​​‌‌‌​‌​​‌​‌‌​‌‌​​‌ below
var EventEmitter = require("events");

/**
 *
 * @param {object} opts
 * @param {any} opts.fn
 * @param {number} opts.interval
 * @param {AbortSignal} opts.signal
 * @returns {EventEmitter}
 */
const createEE = ({ fn, interval, signal }) => {
    const e = new EventEmitter();

    return e;
};



```

```js
const EventEmitter = require("events");

/**
 *
 * @param {object} opts
 * @param {any} opts.fn
 * @param {number} opts.interval
 * @param {AbortSignal} opts.signal
 * @returns {EventEmitter}
 */
const createEE = ({ fn, interval, signal }) => {
    const e = new EventEmitter();

    const intervalId = setInterval(() => {
        try {
            const result = fn();
            e.emit('data', result);
        } catch (error) {
            e.emit('error', error);
        }
    }, interval);

    signal.addEventListener('abort', () => {
        clearInterval(intervalId);
        e.emit('close');
    });

    try {
        const result = fn();
        e.emit('data', result);
    } catch (error) {
        e.emit('error', error);
    }

    return e;
};

/* provided test */
im going to test the createEE function using the follwogin test , do you see any issue with it ?
let counter = 0;
const ac = new AbortController();

// emitter should emit
// in `data` events: 1, 2, 3, 4
// then emit `close` event
const e = createEE({
    fn: () => {
        return ++counter;
    },
    interval: 300,
    signal: ac.signal,
});

e.on("data", console.log);
e.on("close", () => console.log("closed"));

setTimeout(() => {
    console.log("stopping after 1 second");
    ac.abort();
}, 1000);

```


>Question 9 :

The text extracted from the provided HTML is:

"Dans cet exercice, vous allez utiliser le module cluster pour interagir avec des processus enfants (workers).

Un worker a été implémenté à l'emplacement `workerPath`. Il utilise une logique de calcul lourde pour le CPU. Le worker attend le message d'entrée du processus cluster primaire. Il calcule ensuite le résultat et le renvoie.

Votre objectif est d'implémenter la fonction asynchrone `doCalculations(inputs, workerPath)` qui envoie les entrées au worker et retourne les résultats du calcul.
- `inputs` est une liste contenant la ou les chaînes de caractères à envoyer.
- `workerPath` est une chaîne de caractères représentant le chemin du fichier du worker.
- Votre fonction doit renvoyer un objet `Promise` qui se résout en un tableau de résultats.
- Les calculs doivent être exécutés en parallèle.
- L'ordre entre les entrées et les sorties doit être préservé."

rewrite your answer according to the following constrains :
```js
// JavaScript code​​​​​​‌​​‌​‌​​‌‌‌​‌​​‌​‌‌​‌‌​​‌ below
const cluster = require("cluster");

/**
 *
 * @param {string[]} inputs
 * @param {string} workerPath
 * @returns {Promise<Array<string | number>} calculation results returned from workers
 */
async function doCalculations(inputs, workerPath = "/tmp/deps/worker") {
    // Your code goes here
    const result = []; // = calculate(inputs)

    return result;
}

//it will be tested with :

doCalculations(['hello', 'world']).then(console.log).catch(console.error)


```

```js


const { Worker, isMainThread, parentPort, workerData } = require('worker_threads');
const { promisify } = require('util');
const { resolve } = require('path');

/**
 * Function to perform heavy CPU calculations using worker threads.
 * @param {Array<string>} inputs List of strings to send to workers for calculation.
 * @param {string} workerPath Path to the worker file.
 * @returns {Promise<Array<string | number>>} Promise that resolves to an array of results.
 */
async function doCalculations(inputs, workerPath = "worker.js") {
    if (isMainThread) {
        return new Promise((resolve, reject) => {
            const workerPromises = inputs.map(input => {
                return new Promise((resolve, reject) => {
                    const worker = new Worker(resolve(workerPath), { workerData: input });
                    worker.on('message', resolve);
                    worker.on('error', reject);
                    worker.on('exit', (code) => {
                        if (code !== 0)
                            reject(new Error(`Worker stopped with exit code ${code}`));
                    });
                });
            });

            Promise.all(workerPromises)
                .then(resolve)
                .catch(reject);
        });
    } else {
        // Worker thread
        const calculate = (input) => {
            // Perform heavy CPU calculations based on input
            return input.toUpperCase();
        };

        parentPort.postMessage(calculate(workerData));
    }
}

// Example usage:
doCalculations(['hello', 'world'])
    .then(console.log)
    .catch(console.error);


```


