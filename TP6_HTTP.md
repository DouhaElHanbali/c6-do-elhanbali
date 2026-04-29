# TP 6 - Le Protocole HTTP

## TP1 : Exploration avec les DevTools

### 1.1 Ouvrir les DevTools

![TP1_1-1](images/TP1_1-1.png)

### 1.2 Observer une requête simple

- Quel est le code de statut ?

  ![TP1_1-2_1](images/TP1_1-2_Q1.png)

  Réponse : 200

- Quels headers de requête sont envoyés ?

  ![TP1_1-2_2](images/TP1_1-2_Q2.png)

  Réponse : Accept, User-Agent, Accept-Language...

- Quel est le Content-Type de la réponse ?

  ![TP1_1-2_3](images/TP1_1-2_Q3.png)

  Réponse : application/json

### 1.3 Tester différentes méthodes

```
// GET
fetch('https://httpbin.org/get')
  .then(r => r.json())
  .then(console.log);
```

![TP1_1-3_GET](images/TP1_1-3_GET.png)

```
// POST
fetch('https://httpbin.org/post', {
  method: 'POST',
  headers: {'Content-Type': 'application/json'},
  body: JSON.stringify({name: 'John', age: 30})
})
  .then(r => r.json())
  .then(console.log);
```

![TP1_1-3_POST](images/TP1_1-3_POST.png)

### 1.4 Observer les codes de statut

#### Exercice :

| URL                    | Méthode | Code | Content-Type             |
| ---------------------- | ------- | ---- | ------------------------ |
| httpbin.org/get        | GET     | 200  | application/json         |
| httpbin.org/post       | POST    | 200  | application/json         |
| httpbin.org/status/201 | GET     | 201  | text/html; charset=utf-8 |

## TP2 : Maîtrise de cURL

### 2.1 Requête GET simple

- Quelle est la différence entre -i et -v ?

  Réponse :

  ![TP2_2-1_-i](images/TP2_2-1_-i.png)
  - `-i` : affiche les headers de réponse + le
    corps

  ![TP2_2-1_-v](images/TP2_2-1_-v.png)
  - `-v` : affiche tout (connexion, headers requête >, headers réponse <, corps)
    - Les lignes avec > = ce qu'on envoie
    - Les lignes avec < = ce qu'on reçoit
    - Les lignes avec \* = infos de connexion

### 2.2 Requête POST avec données

```
# Form data
curl -X POST -d "name=John&email=john@example.com" \
  https://httpbin.org/post
```

![TP2_2-2_F1](images/TP2_2-2_F1.png)

- Les données arrivent dans form, le champ json est null.
  C'est le format des vieux formulaires HTML (<form action="...">). Les données sont encodées comme clé=valeur&clé2=valeur2.

```
# JSON
curl -X POST \
  -H "Content-Type: application/json" \
  -d '{"name": "John", "email": "john@example.com"}' \
  https://httpbin.org/post
```

![TP2_2-2_F2](images/TP2_2-2_F2.png)

- Le Content-Type est bien _application/json_, mais json est null, car sur Windows CMD les guillemets " dans le -d ont mal passé — le JSON reçu n'était pas valide.

### 2.3 Headers personnalisés

![TP2_2-3](images/TP2_2-3.png)

- on ajoute nos propres headers à la requête. -H permet d'ajouter un header.

### 2.4 Suivre les redirections

![TP2_2-4](images/TP2_2-4.png)

- Sans -L : cURL s'arrête à la redirection (affiche le HTML 302)
- Avec -L : cURL suit toutes les redirections jusqu'à la destination finale

### 2.5 Télécharger un fichier

![TP2_2-5](images/TP2_2-5.png)

- o nom.ext → on peut choisir le nom du fichier
- O → le fichier garde son nom original de l'URL

### Exercice avancé

```
curl -X POST -H "Content-Type: application/json" \
-H "X-Custom-Header: MonHeader" \
-d "{\"action\": \"test\", \"value\": 42}" \
-i https://httpbin.org/post
```

![TP2_ExerciceAdv](images/TP2_ExerciceAdv.png)

## TP3 : API REST avec JavaScript

## TP4 : Analyse des Headers de Sécurité

## TP5 : Cache HTTP

## Exercices Récapitulatifs
