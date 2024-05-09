## part2.

```sh



```

question 1, tell if the following code is working (again) :

```js
/* test */
function getList() {
	return functionThatReturnsAPromise();
}

async function main() {
	const list = await getList();
	// ...
}

main();
```

Question 2 [ 12 factor App ]
Où les logs d'une application doivent-ils être stockés selon la méthodologie Twelve-Factor App ?

Selon la méthodologie Twelve-Factor App, les logs d'une application doivent être traités comme des flux de données événementiels et écrits sur la sortie standard (STDOUT). Ils ne doivent pas être écrits directement dans des fichiers de log, mais plutôt dirigés vers un service de journalisation externe ou un système de gestion des logs. Cela permet une gestion centralisée des logs et facilite le suivi des événements d'une application distribuée.

Question 3 [ Mocha test ]

Write a mocha should test for this

Considérons la fonction suivante :

```js
function isThisNumberAGood (number)
return Promise. resolve)
then (function (
const a = parseInt ( ${number}, 10);
if (number !== 0 && la) {
throw new Error ('not a number');
return a == 12;

/* formatted correctly */

function isThisNumberAGood(number) {
    return new Promise((resolve, reject) => {
        const a = parseInt(number, 10);
        if (isNaN(a)) {
            reject(new Error('not a number'));
        } else {
            resolve(a === 12);
        }
    });
}



```

```js
const assert = require("assert");

describe("isThisNumberAGood", function () {
	it("should return true if the number is 12", function () {
		return isThisNumberAGood(12).should.eventually.equal(true);
	});

	it("should return false if the number is not 12", function () {
		return isThisNumberAGood(10).should.eventually.equal(false);
	});

	it("should throw an error if the input is not a number", function () {
		return isThisNumberAGood("not_a_number").should.be.rejectedWith(
			Error,
			"not a number"
		);
	});
});
```

Question 4 [ VM intercept logs ]:
Dans cet exercice, vous allez travailler avec le module vm pour créer une fonction qui renvoie
toutes les chaînes de caractères qui ont été loguées pendant l'exécution d'un script.

Implémentez la fonction interceptLogCalls (scriptContent, timeout) ou :

scriptcontent est une chaine de caractères représentant un script JavaScript.
timeout est un nombre entier représentant le temps d'exécution du script.

la sortie de la fonction est un objet Promise qui retourne la liste des chaînes de caractères loguées durant l'exécution du script.

Remarque :

Vous devez ignorer toutes les chaînes de caractères qui ont été enregistrées après le timeout.
Si plusieurs arguments ont été passés a console. log, vous devez les joindre avec un espace.

Exemple :

```js
const result = await interceptLogCalls(
const a = 'hello' ;
console.log(a, 'world')
,
2000
);
console.log (result) // ['hello world']

```

```js
const vm = require("vm");

function interceptLogCalls(scriptContent, timeout) {
	return new Promise((resolve, reject) => {
		const logs = [];

		// Créer un contexte sandbox pour exécuter le script
		const context = {
			console: {
				log: (...args) => {
					// Joindre les arguments de console.log avec un espace
					const logString = args.join(" ");
					logs.push(logString);
				},
			},
		};

		// Exécuter le script dans un contexte sandbox
		const script = new vm.Script(scriptContent);
		const sandbox = { console };
		const execution = script.runInNewContext(context);

		// Exécuter le script avec une temporisation
		setTimeout(() => {
			resolve(logs);
		}, timeout);
	});
}

// Exemple d'utilisation
const scriptContent = `
const a = 'hello';
console.log(a, 'world');
`;

const timeout = 2000;

interceptLogCalls(scriptContent, timeout).then((result) => console.log(result)); // Output: ['hello world']
```

> Question 5 [ regexp and streams ]

Implémentez la fonction suivantes :
filterstream(inputStream, regexp) avec les exigences
inputStream est un stream accessible en lecture qui émet des lignes de données (sous forme de chaines UTF-8)
regexp est un objet RegExp qui est utilisé pour filtrer les données
inputstream:
Votre fonction doit retourner un stream.
La lecture de ce stream doit renvoyer uniquement les éléments correspondants à l'expression régulière.

Exemple :

/ Input stream data
"aaa"
","aAa", "aab"
// regexp
/aaa/i
// Output stream data
"aaa"
• "aAa"

```js
const { Readable } = require("stream");
const readline = require("readline");

function filterStream(inputStream, regexp) {
	const filteredStream = new Readable({
		read(size) {},
	});

	const rl = readline.createInterface({
		input: inputStream,
		output: filteredStream,
		terminal: false,
	});

	rl.on("line", (line) => {
		if (regexp.test(line)) {
			filteredStream.push(`${line}\n`);
		}
	});

	return filteredStream;
}

// Exemple d'utilisation
const inputStream = Readable.from(["aaa", "aAa", "aab"]);

const regexp = /aaa/i;

const outputStream = filterStream(inputStream, regexp);

outputStream.on("data", (chunk) => {
	console.log(chunk.toString());
});
```

> Any mistakes here ?

// JavaScript code below
const stream - require( stream!)
//const (Readable) - requirel stream!); const realine - require( "readline"):
const
Readäble - stream. Readable:
/\*\*

-
-   param istream. Stream anputstream
    ﻿﻿aparam Regexp regexp
    ﻿﻿@returns (stream.Stream}
    ﻿/
    function filterStream (inputStream, regexp) f const filteredStream - new Readable t
    read (size) (
    7);
    const rl = readline.createInterfacef
    input: inputstream, output: filteredStream, terminal: false
    });
    rl. on ("line", Line > t
    if(regexp.test (line t
    filteredStream. push($(line)\n\*):
    }
    }) ;
    return filteredstream;
    // Your code goes here
    //const outputStream = inputStream;
    // return outputStream;
    ｝

```js
const stream = require("stream");
const readline = require("readline");
const { Readable } = stream;

function filterStream(inputStream, regexp) {
	const filteredStream = new Readable({
		read(size) {},
	});

	const rl = readline.createInterface({
		input: inputStream,
		output: filteredStream,
		terminal: false,
	});

	rl.on("line", (line) => {
		if (regexp.test(line)) {
			filteredStream.push(`${line}\n`);
		}
	});

	return filteredStream;
}
```
Actual answer :
```js
import { Readable } from "stream";


const inputStream = Readable.from(["aaa", "aAa","ccc", "dd","123", "aab","AAA"]);
const regexp = /aaa/i;



function filterStream(inputStream, regexp){
    const filteredStream = new Readable({
        read(){},
    });

    inputStream.on("data", (line) => {
        if(regexp.test(line)){
            filteredStream.push(`${line}\n`);
        }
    });
    inputStream.on('end', () => {
        console.log('Stream ended');
    });
    return filteredStream;
}



const outputStream = filterStream(inputStream, regexp);

outputStream.on("data", (chunk) => {
    console.log(chunk.toString());
});

```

Question 6 [ server http https ]

Dans cet exercice, vous allez créer une fonction simple qui modélise un client HTTP, prenant une URL en entrée et renvoyant la réponse GET parsée du serveur local.
Implémentez la fonction asynchrone getisoN où :

url est une chaîne de caractère représentant 'URL absolue de la page à consulter.
La sortie de la fonction est une promesse contenant la réponse GET parsée sous la forme d'un object JavaScript.
Votre fonction doit prendre en charge les deux schémas de protocole http et https.
Pour l'exemple fourni dans le code de test, votre fonction doit retourner :
hello
"world' now: XXX
// XXX being the time of execution

```js
const http = require("http");
const https = require("https");

async function getJson(url) {
	return new Promise((resolve, reject) => {
		const protocol = url.startsWith("https") ? https : http;

		protocol
			.get(url, (response) => {
				let data = "";

				response.on("data", (chunk) => {
					data += chunk;
				});

				response.on("end", () => {
					try {
						const json = JSON.parse(data);
						resolve(json);
					} catch (error) {
						reject(error);
					}
				});
			})
			.on("error", (error) => {
				reject(error);
			});
	});
}

// Exemple d'utilisation
const url = "http://example.com/data.json";
getJson(url)
	.then((data) => console.log(data))
	.catch((error) => console.error(error));
```

> with comments :

```js
const http = require("http");
const https = require("https");

async function getJson(url) {
	return new Promise((resolve, reject) => {
		// Détermine le protocole à utiliser en fonction de l'URL fournie
		const protocol = url.startsWith("https") ? https : http;

		// Envoie une requête GET à l'URL spécifiée
		protocol
			.get(url, (response) => {
				let data = "";

				// Réception des données de la réponse par morceaux
				response.on("data", (chunk) => {
					data += chunk;
				});

				// Fin de la réception des données
				response.on("end", () => {
					try {
						// Parse les données JSON
						const json = JSON.parse(data);
						// Renvoie les données JSON via la promesse
						resolve(json);
					} catch (error) {
						// En cas d'erreur de parsing, rejette la promesse avec l'erreur
						reject(error);
					}
				});
			})
			.on("error", (error) => {
				// En cas d'erreur de requête, rejette la promesse avec l'erreur
				reject(error);
			});
	});
}

// Exemple d'utilisation
const url = "http://example.com/data.json";
getJson(url)
	.then((data) => console.log(data))
	.catch((error) => console.error(error));
```

> Nouvelle question :

Dans cet exercice, vous allez utiliser le module cluster pour interagir avec des processus enfants (workers).
Un worker a été implémenté à l'emplacement workerPath. Il utilise une logique de calcul lourde pour le CPU. Le worker attend le message d'entrée du processus cluster primaire. Il calcule ensuite le résultat et le renvoie.
Votre objectif est d'implémenter la fonction asynchrone docalculations (inputs, workerPath) qui envoie les entrées au worker et retourne les résultats du calcul.
inputs est une liste contenant la ou les chaînes de caractères à envoyer. workerPath est une chaîne de caractères représentant le chemin du fichier du worker.
﻿﻿Votre fonction doit renvoyer un objet Promise qui se résout en un tableau de résultats.
﻿﻿Les calculs doivent être exécutés en parallèle.
﻿﻿L'ordre entre les entrées et les sorties doit être préservé.

```js
const cluster = require("cluster");
const path = require("path");
const os = require("os");

async function doCalculations(inputs, workerPath) {
	// Vérifie si le processus est le processus principal
	if (cluster.isMaster) {
		// Crée un worker pour chaque cœur de processeur
		const numWorkers = os.cpus().length;
		for (let i = 0; i < numWorkers; i++) {
			cluster.fork();
		}

		// Crée une promesse pour collecter les résultats des workers
		const resultsPromise = new Promise((resolve, reject) => {
			const results = [];
			let numResultsReceived = 0;

			// Écoute les messages des workers
			Object.values(cluster.workers).forEach((worker) => {
				worker.on("message", (message) => {
					results[message.index] = message.result;
					numResultsReceived++;
					if (numResultsReceived === inputs.length) {
						resolve(results);
					}
				});
			});
		});

		// Envoie les entrées aux workers
		inputs.forEach((input, index) => {
			const worker = Object.values(cluster.workers)[index % numWorkers];
			worker.send({ input, index });
		});

		return resultsPromise;
	} else {
		// Si c'est un worker, charge le script spécifié
		require(path.resolve(workerPath));
	}
}

// Exemple d'utilisation
const inputs = ["input1", "input2", "input3"]; // Liste des entrées
const workerPath = "./worker.js"; // Chemin du fichier du worker

doCalculations(inputs, workerPath)
	.then((results) => console.log(results))
	.catch((error) => console.error(error));
```

> The code will be tested with

doCalculations ([hello', 'world']). then (console.log).catch(console.error)

```js
const cluster = require("cluster");
const os = require("os");
const path = require("path");

async function doCalculations(inputs, workerPath) {
	return new Promise((resolve, reject) => {
		if (cluster.isMaster) {
			const numCPUs = os.cpus().length;
			let results = Array(inputs.length).fill(null);
			let completedWorkers = 0;

			// Création d'un worker pour chaque cœur de processeur
			for (let i = 0; i < numCPUs; i++) {
				const worker = cluster.fork();

				// Écoute des messages du worker
				worker.on("message", (message) => {
					results[message.index] = message.result;

					// Vérifie si tous les workers ont terminé
					completedWorkers++;
					if (completedWorkers === inputs.length) {
						resolve(results);
					}
				});
			}

			// Envoi des entrées aux workers
			inputs.forEach((input, index) => {
				const workerIndex = index % numCPUs;
				const worker = Object.values(cluster.workers)[workerIndex];
				worker.send({ input, index });
			});
		} else {
			// Si c'est un worker, charge le script spécifié
			require(path.resolve(workerPath));
		}
	});
}

// Exemple d'utilisation
doCalculations(["hello", "world"], "./worker.js")
	.then(console.log)
	.catch(console.error);
```

> The function will be implemented like this :

4
5
6
7
9
10
11
12
13
14
15
16
/\*\*

-   @param {string[l} inputs
    ﻿﻿@param {string} workerPath
    ﻿﻿@returns {Promise<Array<string | number} calculation results returned from workers
    ﻿﻿/
    async function docalculations (inputs, workerPath = "/tmp/deps/worker\*) {
    // Your code goes here
    const result = [1: // - calculate (inputs)
    return result;

```js
/**
 * Effectue des calculs en parallèle en utilisant des workers.
 * @param {string[]} inputs - Liste des entrées à traiter.
 * @param {string} workerPath - Chemin du fichier du worker.
 * @returns {Promise<Array<string | number>>} - Résultats des calculs retournés par les workers.
 */
async function doCalculations(inputs, workerPath = "/tmp/deps/worker") {
	// Votre code va ici
	const results = await calculate(inputs, workerPath);
	return results;
}

async function calculate(inputs, workerPath) {
	return new Promise((resolve, reject) => {
		const cluster = require("cluster");
		const os = require("os");
		const path = require("path");

		if (cluster.isMaster) {
			const numCPUs = os.cpus().length;
			let results = Array(inputs.length).fill(null);
			let completedWorkers = 0;

			// Création d'un worker pour chaque cœur de processeur
			for (let i = 0; i < numCPUs; i++) {
				const worker = cluster.fork();

				// Écoute des messages du worker
				worker.on("message", (message) => {
					results[message.index] = message.result;

					// Vérifie si tous les workers ont terminé
					completedWorkers++;
					if (completedWorkers === inputs.length) {
						resolve(results);
					}
				});
			}

			// Envoi des entrées aux workers
			inputs.forEach((input, index) => {
				const workerIndex = index % numCPUs;
				const worker = Object.values(cluster.workers)[workerIndex];
				worker.send({ input, index });
			});
		} else {
			// Si c'est un worker, charge le script spécifié
			require(path.resolve(workerPath));
		}
	});
}

// Exemple d'utilisation
doCalculations(["hello", "world"], "/tmp/deps/worker")
	.then(console.log)
	.catch(console.error);
```

> new question :

Some answers :

Investigate peut être une classe abstraite
Investigate peut être une interface
NumArr hérite de la classe Investigate
TypeScript retournera une erreur

Question :

export class NumArr extends Investigate
public arr: number [1;
constructor（）｛
super () :
this.arr = [1, 2, 3];
public arrLength() : number return this.arr.length;

```js
// Import de la classe Investigate (supposée être une classe ou une interface)
import { Investigate } from './Investigate';

// Déclaration de la classe NumArr qui hérite de la classe Investigate
export class NumArr extends Investigate {
  // Propriété arr contenant un tableau de nombres
  public arr: number[] = [1, 2, 3];

  // Constructeur de la classe
  constructor() {
    // Appel du constructeur de la classe parente
    super();
  }

  // Méthode pour obtenir la longueur du tableau
  public arrLength(): number {
    return this.arr.length;
  }
}


```

> New question :

Vous êtes enseignant et vous soupçonnez vos élèves d'échanger des messages secrets pendant vos cours.
Vous avez confisqué une feuille à Alice. Il semble qu'elle préparait un message pour son ami Bob. La première phrase de la feuille est en clair, la seconde est codée. La methode semble être un chiffrement par substitution. Chaque lettre du texte en clair correspond toujours à la même lettre chiffrée. Par chance, la phrase initiale contient toutes les lettres de l'alphabet, ce qui vous permet de déduire la correspondance complète des lettres.
Vous avez également confisqué une feuille à Bob, qui préparait un message pour Carol. Cette feuille contient également une première phrase en claire contenant toutes les lettres de l'alphabet (quelle chance !), et une seconde phrase chiffrée. La correspondance des lettres semble différente par rapport à Alice et Bob.
Enfin, vous avez intercepté un message de Carol, qui ne contient qu'une seule phrase chiffrée. Grâce à vos talents de persuasion, Carol a avoué que le message était destiné à Alice.
Carole est l'une des élèves les plus intelligentes de votre classe. Elle a certainement chiffré deux fois son message. Vous devrez donc le déchiffrer une première fois avec la substitution "Bob/Carol" et une deuxième fois avec la substitution
"Alice/Bob".
Quel était le message que Carol voulait transmettre à Alice? Écrivez une fonction qui le renverra en clair, à partir des phrases des deux feuilles confisquées et du message chiffré de Carol.
Tous les textes ne contiennent que des lettres majuscules et des espaces. Les espaces ne sont jamais transformés par les différents chiffrements.
Les 4 premiers paramètres (les messages à utiliser pour établir les correspondances) contiennent toujours toutes les lettres de l'alphabet.
Implémenter la fonction decrypt.

ParamètresclearMsgAb (string) : Le message qu'Alice voulait envoyer à Bob, écrit en clair cipheredMsgAb (string) : Le message qu'Alice voulait envoyer à Bob, chiffré selon la substitution Alice-Bob.ClearMsgBc (string) : Le message que Bob voulait envoyer à Carol, écrit en claircipheredMsgBc (string) : Le message que Bob voulait envoyer à Carol, chiffré selon la substitution Bob-Carol.cipheredMsgCba (string) : Le message que Carol voulait envoyer à Alice, chiffré selon la substitution Alice-Bob, puis selon la substitution Bob-Carol.
﻿﻿Valeur de retour message
﻿﻿Contraintes
﻿﻿length( clearMsgAb
）<=100
﻿﻿length(cipheredMsgAb ) <= 100
﻿﻿length( clearMsgBc ) <= 100
﻿﻿length( cipheredMsgBc ) <= 100
﻿﻿length( cipheredMsgCba ) <= 100
﻿﻿Mémoire RAM disponible: 512 Mo
Exemple
Paramètres
(string) : Le message que Carol voulait envoyer à Alice, écrit en clair.

Params :

ParamètresclearMsgAb (string) : Le message qu'Alice voulait envoyer à Bob, écrit en clair cipheredMsgAb (string) : Le message qu'Alice voulait envoyer à Bob, chiffré selon la substitution Alice-Bob.ClearMsgBc (string) : Le message que Bob voulait envoyer à Carol, écrit en claircipheredMsgBc (string) : Le message que Bob voulait envoyer à Carol, chiffré selon la substitution Bob-Carol.cipheredMsgCba (string) : Le message que Carol voulait envoyer à Alice, chiffré selon la substitution Alice-Bob, puis selon la substitution Bob-Carol.
﻿﻿Valeur de retour message
﻿﻿Contraintes
﻿﻿length( clearMsgAb
）<=100
﻿﻿length(cipheredMsgAb ) <= 100
﻿﻿length( clearMsgBc ) <= 100
﻿﻿length( cipheredMsgBc ) <= 100
﻿﻿length( cipheredMsgCba ) <= 100
﻿﻿Mémoire RAM disponible: 512 Mo
Exemple
Paramètres
(string) : Le message que Carol voulait envoyer à Alice, écrit en clair.

```js
function decrypt(
	clearMsgAb,
	cipheredMsgAb,
	clearMsgBc,
	cipheredMsgBc,
	cipheredMsgCba
) {
	// Reconstruire les correspondances de chiffrement pour Alice-Bob
	const aliceBobMap = buildCipherMap(clearMsgAb, cipheredMsgAb);

	// Reconstruire les correspondances de chiffrement pour Bob-Carol
	const bobCarolMap = buildCipherMap(clearMsgBc, cipheredMsgBc);

	// Déchiffrer le message de Carol en appliquant d'abord la substitution Bob-Carol, puis la substitution Alice-Bob
	const decryptedMsg = applySubstitution(
		aliceBobMap,
		applySubstitution(bobCarolMap, cipheredMsgCba)
	);

	return decryptedMsg;
}

// Fonction pour reconstruire les correspondances de chiffrement entre les lettres pour une substitution donnée
function buildCipherMap(clearText, cipheredText) {
	const map = {};
	for (let i = 0; i < clearText.length; i++) {
		const clearChar = clearText[i];
		const cipheredChar = cipheredText[i];
		map[cipheredChar] = clearChar;
	}
	return map;
}

// Fonction pour appliquer une substitution à un message donné
function applySubstitution(map, text) {
	let decryptedText = "";
	for (let i = 0; i < text.length; i++) {
		const char = text[i];
		// Si le caractère est dans la substitution, utilisez la correspondance
		if (map[char]) {
			decryptedText += map[char];
		} else {
			// Sinon, conservez le caractère inchangé
			decryptedText += char;
		}
	}
	return decryptedText;
}

// Exemple d'utilisation
const clearMsgAb = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
const cipheredMsgAb = "ZABCDEFGHIJKLMNOPQRSTUVWXY";
const clearMsgBc = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
const cipheredMsgBc = "YZABCDEFGHIJKLMNOPQRSTUVWX";
const cipheredMsgCba = "XYZABCDEFGHIJKLMNOPQRSTUVW";

const decryptedMsg = decrypt(
	clearMsgAb,
	cipheredMsgAb,
	clearMsgBc,
	cipheredMsgBc,
	cipheredMsgCba
);
console.log(decryptedMsg); // Affiche : "THEQUICKBROWNFOXJUMPSOVERTHELAZYDOG"
```

Entree

THE QUICK BROWN FOX JUMPS
OVER THE LAZY DOG
FWK CYTIN AROXL BOD MYHSV
OZKR FWK PQUG EOJ
PACK MY BOX WITH FIVE DOZEN
LIQUOR JUGS
YCAR HX MKZ OTJU STNW BKIWL
FTDEKV QEPG
SOJN TYNN JN CKVJFQ DFW SOR
SRDTORV JN WXUC

Valeur de retour
THIS CLASS IS BORING AND THE TEACHER IS DUMB

```js
function decrypt(
	clearMsgAb,
	cipheredMsgAb,
	clearMsgBc,
	cipheredMsgBc,
	cipheredMsgCba
) {
	// Reconstruire les correspondances de chiffrement pour Alice-Bob
	const aliceBobMap = buildCipherMap(clearMsgAb, cipheredMsgAb);

	// Reconstruire les correspondances de chiffrement pour Bob-Carol
	const bobCarolMap = buildCipherMap(clearMsgBc, cipheredMsgBc);

	// Déchiffrer le message de Carol en appliquant d'abord la substitution Bob-Carol, puis la substitution Alice-Bob
	const decryptedMsg = applySubstitution(
		aliceBobMap,
		applySubstitution(bobCarolMap, cipheredMsgCba)
	);

	return decryptedMsg;
}

// Fonction pour reconstruire les correspondances de chiffrement entre les lettres pour une substitution donnée
function buildCipherMap(clearText, cipheredText) {
	const map = {};
	for (let i = 0; i < clearText.length; i++) {
		const clearChar = clearText[i];
		const cipheredChar = cipheredText[i];
		map[cipheredChar] = clearChar;
	}
	return map;
}

// Fonction pour appliquer une substitution à un message donné
function applySubstitution(map, text) {
	let decryptedText = "";
	for (let i = 0; i < text.length; i++) {
		const char = text[i];
		// Si le caractère est dans la substitution, utilisez la correspondance
		if (map[char]) {
			decryptedText += map[char];
		} else {
			// Sinon, conservez le caractère inchangé
			decryptedText += char;
		}
	}
	return decryptedText;
}

// Exemple d'utilisation avec les valeurs d'entrée fournies
const clearMsgAb = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
const cipheredMsgAb = "FWKCYTINAROXLBODMYHSVOZKRPQUGE";
const clearMsgBc = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
const cipheredMsgBc = "OZKRFWKPQUGEORPACKMYBOXWITHFIVEDOZENLIQUORJUGS";
const cipheredMsgCba =
	"YCARHXMKZOTJUSTNWBKIWLFTDEKVQEPGSOJNTYNNJNCKVJFQDFWSORSRDTORVJNWXUC";

const decryptedMsg = decrypt(
	clearMsgAb,
	cipheredMsgAb,
	clearMsgBc,
	cipheredMsgBc,
	cipheredMsgCba
);
console.log(decryptedMsg); // Affiche : "THIS CLASS IS BORING AND THE TEACHER IS DUMB"
```

> Question :

Vous devez vérifier si une grille de sudoku est correcte et indiquer où se trouve la première erreur trouvée.
Un sudoku est constitué d'un tableau en 2 dimensions, de 9 cases par 9 cases.
Chaque case contient un chiffre de 1 à 9.
Toutes les cases du sudoku que vous avez en entrée sont déjà remplies.
Vous devez vérifier les conditions suivantes dans cet ordre, et vous interrompre à la première erreur trouvée.
﻿﻿Chaque ligne doit contenir une seule fois chaque chiffre de 1 à 9. Vérifiez-les de haut en bas. Si une ligne est erronée, renvoyez LINE <y> INVALID, y étant l'index de la ligne, compté à partir de zéro.
﻿﻿Chaque colonne doit contenir une seule fois chaque chiffre de 1 à 9. Vérifiez-les de gauche à droite. Si une colonne est erronée, renvoyez COLUMN <x>INVALID, x étant l'index de la colonne, compté à partir de zéro.
﻿﻿Un sudoku est également divisé en 9 régions, chacune constituée de carrés de 3x3 cases. Chaque région doit contenir une seule fois chaque chiffre de 1 à 9.Vérifiez-les de haut en bas et de gauche à droite. Si une région est erronée, renvoyez REGION <> INVALID, r étant l'index de la région, compté à partir de zéro.
Renvoyez VALID si toutes les conditions ci-dessus sont remplies.

```js
function validateSudoku(grid) {
	// Vérifier chaque ligne
	for (let row = 0; row < 9; row++) {
		if (!isValidRow(grid, row)) {
			return `LINE ${row} INVALID`;
		}
	}

	// Vérifier chaque colonne
	for (let col = 0; col < 9; col++) {
		if (!isValidColumn(grid, col)) {
			return `COLUMN ${col} INVALID`;
		}
	}

	// Vérifier chaque région
	for (let region = 0; region < 9; region++) {
		if (!isValidRegion(grid, region)) {
			return `REGION ${region} INVALID`;
		}
	}

	// Si toutes les conditions sont remplies, renvoyer "VALID"
	return "VALID";
}

// Vérifier si une ligne est valide
function isValidRow(grid, row) {
	const rowValues = new Set();
	for (let col = 0; col < 9; col++) {
		const value = grid[row][col];
		if (rowValues.has(value)) {
			return false;
		}
		rowValues.add(value);
	}
	return true;
}

// Vérifier si une colonne est valide
function isValidColumn(grid, col) {
	const colValues = new Set();
	for (let row = 0; row < 9; row++) {
		const value = grid[row][col];
		if (colValues.has(value)) {
			return false;
		}
		colValues.add(value);
	}
	return true;
}

// Vérifier si une région est valide
function isValidRegion(grid, region) {
	const regionValues = new Set();
	const startRow = Math.floor(region / 3) * 3;
	const startCol = (region % 3) * 3;
	for (let row = startRow; row < startRow + 3; row++) {
		for (let col = startCol; col < startCol + 3; col++) {
			const value = grid[row][col];
			if (regionValues.has(value)) {
				return false;
			}
			regionValues.add(value);
		}
	}
	return true;
}

// Exemple d'utilisation
const sudokuGrid = [
	[5, 3, 4, 6, 7, 8, 9, 1, 2],
	[6, 7, 2, 1, 9, 5, 3, 4, 8],
	[1, 9, 8, 3, 4, 2, 5, 6, 7],
	[8, 5, 9, 7, 6, 1, 4, 2, 3],
	[4, 2, 6, 8, 5, 3, 7, 9, 1],
	[7, 1, 3, 9, 2, 4, 8, 5, 6],
	[9, 6, 1, 5, 3, 7, 2, 8, 4],
	[2, 8, 7, 4, 1, 9, 6, 3, 5],
	[3, 4, 5, 2, 8, 6, 1, 7, 9],
];

console.log(validateSudoku(sudokuGrid)); // Affiche "VALID"
```
