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

### 2.1 Réponse :

- Quelle est la différence entre -i et -v ?

  Réponse :

  ![2.1_cmd_-i](images)
  - `-i` : affiche les headers de réponse + le
    corps

  ![2.1_cmd_-i](images/TP2_Q2-1_-i.png)
  - `-v` : affiche tout (connexion, headers requête >, headers réponse <, corps)
    - Les lignes avec > = ce qu'on envoie
    - Les lignes avec < = ce qu'on reçoit
    - Les lignes avec \* = infos de connexion

## TP3 : API REST avec JavaScript

## TP4 : Analyse des Headers de Sécurité

## TP5 : Cache HTTP

## Exercices Récapitulatifs
