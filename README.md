# PRÉSENTATION
Le Data Access Object (DOA) est un modèle de programmation qui permet à un serveur de traiter des requêtes d'accès aux données de différentes Bases De Données (DB).

Lorsque le serveur reçoit des requêtes, le DAO s'occupe de les traduire avant de les envoyer au bon format, peu importe la DB choisie.

# INSTALLATION
- Import de la librairie (chemin vers le fichier `DAO.js`)

`const DAO = require('path/to/DAO')`

- Instanciation d'une nouvelle DB dans une variable (chemin vers la DB)

SQLite
```js
const db = new DAO.SQLite('/path/to/database')
```
MongoDB
```js
const db = new DAO.MongoDB('/path/to/database')
```
Redis
```js
const db = new DAO.Redis('/path/to/database')
```
# UTILISATION

`db` : Instance du DAO lié à la Base De Données ciblée

`'target'` : Collection MongoDB / Table SQL / Clé Redis

`element` : Objet JavaScript a récupérer / insérer / mettre à jour

`id` : ID de l'Objet JavaScript à obtenir / supprimer

`callback` : Traitement à effectuer une fois les valeurs récupérées

- create(`'target'`, `element`) ajoute un élement à la cible 
```js
let new_element = {}
db.create('example', new_element)
```
- getAll(`'target'`, `callback()`) retourne toutes les données de la cible
```js
db.getAll('example', elements => {
    console.log(elements)
})
```
- getById(`'target'`, `id`, `callback()`) retourne la donnée correspondant à l'ID dans la cible
```js
db.getById('example', element.id, element => {
    console.log(element)
})
```
- update(`'target'`, `element`) modifie une donnée dans la cible
```js
updated_element.key = new_value
db.update('example', updated_element)
```
- delete(`'target'`, `id`) retire une donnée de la cible
```js
db.delete('example', element.id)
```
- seed(`'target'`, `elements`) remplie la cible avec une liste d'éléments
> **ATTENTION** cette méthode réinitialise la cible, et ne doit être utilisée que pour des tests
```js
db.seed('example', elements)
```

> Toutes les méthodes peuvent prendre une fonction de `callback` en dernier paramètre pour pouvoir gérer les réponses des requêtes, et les erreurs peuvent être gérées avec `try` et `catch`

# CONVENTIONS
- 1 Feature = 1 Branche = 1 Merge Request
- Méthodes = camelCase
- Variable = snake_case
- Commit & Branches = EN
- Documentation = FR
- Requêtes SQL en majuscules