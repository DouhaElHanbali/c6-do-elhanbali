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

- Les données arrivent dans _form_, le champ _json_ est null.
  C'est le format des vieux formulaires HTML (_<form action="...">_). Les données sont encodées comme _clé=valeur&clé2=valeur2_ .

```
# JSON
curl -X POST \
  -H "Content-Type: application/json" \
  -d '{"name": "John", "email": "john@example.com"}' \
  https://httpbin.org/post
```

![TP2_2-2_F2](images/TP2_2-2_F2.png)

- Form data : données dans "form", Content-Type: application/x-www-form-urlencoded
- JSON : données dans "json", Content-Type: application/json
- La différence = le format d'encodage des données envoyées

### 2.3 Headers personnalisés

![TP2_2-3](images/TP2_2-3.png)

- on ajoute nos propres headers à la requête. -H permet d'ajouter un header.

### 2.4 Suivre les redirections

![TP2_2-4](images/TP2_2-4.png)

- Sans -L : cURL s'arrête à la redirection (affiche le HTML 302)
- Avec -L : cURL suit toutes les redirections jusqu'à la destination finale

### 2.5 Télécharger un fichier

![TP2_2-5](images/TP2_2-5.png)

- o nom.ext : on peut choisir le nom du fichier
- O : le fichier garde son nom original de l'URL

### Exercice avancé

```
curl -X POST -H "Content-Type: application/json" \
-H "X-Custom-Header: MonHeader" \
-d "{\"action\": \"test\", \"value\": 42}" \
-i https://httpbin.org/post
```

![TP2_ExerciceAdv](images/TP2_ExerciceAdv.png)

## TP3 : API REST avec JavaScript

## 3.1 GET basique

![TP3_3-1](images/TP3_3-1.png)

- _fetch(url)_ : envoie la requête GET
- _await_ : attend la réponse avant de continuer
- _response.json()_ : convertit la réponse en objet JS
- _try/catch_ : si ça plante, on attrape l'erreur

## 3.2 POST - Créer une ressource

![TP3_3-2](images/TP3_3-2.png)

- _method: 'POST'_ : on crée une nouvelle ressource
- _headers Content-Type: application/json_ : on dit au serveur qu'on envoie du JSON
- _body: JSON.stringify(data)_ : on convertit l'objet JS en texte JSON
- _response.ok_ : vérifie que le status est entre 200-299
- Le serveur répond avec l'objet créé + id: 101 généré automatiquement

## 3.3 PUT - Modifier une ressource

![TP3_3-3](images/TP3_3-3.png)

- on modifie entièrement l'article avec _id: 1_. _PUT_ = remplace tout l'objet.

## 3.4 DELETE - Supprimer une ressource

![TP3_3-4](images/TP3_3-4.png)

- method: _'DELETE'_ → on supprime la ressource avec id: 1
- _response.ok_ retourne true si status\* 200-299, suppression réussie
- Remarque _.then(console.log);_ j'ai l'ajouté jsut pour voir le résultat dans la console.

## Exercice pratique

```
async function fetchWithRetry(url, options, maxRetries) {
    for (let i = 1; i <= maxRetries; i++){
        const response = await fetch(url, options);
        if (response.status >= 500){
            await new Promise(resolve => setTimeout(resolve, 1000));
            continue;
        } else {
            return response;
        }
    }
    throw new Error (`Échec après ${maxRetries} tentatives`);
}
```

![TP3_ExercicePrat](images/TP3_ExercicePrat.png)

## TP4 : Analyse des Headers de Sécurité

## 4.1 Vérifier les headers d'un site

![TP4_4-1](images)

## 4.2 Analyser avec Security Headers

![TP4_4-2](images)

## Exercice

![TP4_Exercice](images)

## TP5 : Cache HTTP

## Exercices Récapitulatifs
