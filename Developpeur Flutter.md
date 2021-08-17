# Developpeur Flutter

## Notice d'information

La Mater Tech recrute un développeur Flutter qui travaillera premièrement dans le développement de la plateforme MyStore (qui deviendra plus tard Genuka) en version mobile, dans un second temps, il sera amené à réaliser d'autres applications mobile pour le compte de l'entreprise La Mater, Inc. ou sur demande de La Mater Tech. 

Afin de tester les compétences en design et intérgation d'API, ainsi que de la structuration et la propreté du code, nous avons mis en place ce teste technique.

**Important !!**  
Les informations relatives à ce test doivent rester confidentielles. Le résultat obtenu et les informations fournies restent la propriété intellectuelle et légale de l'entreprise La Mater, Inc.

## Enoncé de l'exercice

En 1 semaine maximum, vous devrez réaliser une mini application avec les pages suivantes : 
1. Page de connexion
2. Page d'inscription
3. Liste des produis
4. Détail d'un produit

Ce sont là les 4 pages minimum requises. Vous avez la possibilité de développer d'autres pages, si vous le souhaitez; celà sera considéré comme un bonus. Néanmoins, ce sont ces 4 pages qui seront surtout notées.
Ainsi, l'évaluation portera sur : 
- le respect du design proposé,
- la vitesse de réalisation du projet, 
- la structure du code et sa propreté, 
- Votre manière de "commiter" votre code et d'utiliser Git.


Sur le plan fonctionnel, ces pages permettront à un utilisateur de se connecter/s'inscrire à la plateforme MyStore (une documentation d'API sera fournie plus bas). Une fois l'utilisateur connecté, les produits et collections de l'entreprises seront affiché sur la page 3 (liste des produits). Lorsque l'utilisateur cliquera sur un produit, il aura la page de détail. du produit avec les variantes qui s'afficheront (dans l'exemple, la seule variante est "Taille" et les valeurs sont S, M, L M et L ayant des frais additionnels de 200 FCFA et 400 FCFA)

### Pages à réaliser (Disponible sur Figma : https://r.lamater.net/r/flutter_test_figma)
![](https://filemanager.lamater.net/lamater/Tech/Recrutement/Test%20Flutter/Page%20Inscription.png)
![](https://filemanager.lamater.net/lamater/Tech/Recrutement/Test%20Flutter/page%20Connexion.png)
![](https://filemanager.lamater.net/lamater/Tech/Recrutement/Test%20Flutter/Liste%20des%20produits%20de%20l'entreprise.png)
![](https://filemanager.lamater.net/lamater/Tech/Recrutement/Test%20Flutter/D%C3%A9tail%20d'un%20produit.png) 


### Livrables attendus 

- Un fichier APK à envoyer via Whatsapp au (+237 6 95 76 25 95)
- Le lien du repository GitHub / GitLab privé (vous devrez ajouter le compte @wdjopa pour que nous puissions avoir accès)

### Durée du projet : 1 Semaine maximum à partir du jour d'envoi de ce document

-----------------

## Documentation API MyStore pour le test


> La racine de l'URL est : https://dashboard.mystore.lamater.net/api/2021-05

### Register / Inscription (Page 1)

Pour enregistrer un nouvel utilsiateur, 
**Type de requete** : POST
**Route**: /clients/register
**Body**: 
```JSON
{
        "email": "",
        "tel": "",
        "firstname": "",
        "surname" : "",
        "password": ""
}
```

**Reponse**
-- En cas de succès -> 201
Avec le contenu suivant : 
```JSON
{
  "user": {
    "firstname": "",
    "surname": "",
    "email": "",
    "tel": "",
    "sex": null,
    "birth_date": null,
    "other": null,
    "updated_at": "2021-08-14T07:36:48.000000Z",
    "created_at": "2021-08-14T07:36:48.000000Z",
    "id": 540
  },
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1N....cUx7-sw"
}
```
Donc après l'inscription, si vous le souhaitez, vous pouvez directement aller à la page 3.      
-- En cas d'erreur -> 400
Avec le contenu suivant : 
```JSON
{
  "status": "error",
  "message": {
    "email": {
      "Unique": [
        "clients"
      ]
    },
    "tel": {
      "Unique": [
        "clients"
      ]
    }
  }
}
```

### Login / Connexion (Page 2)

Pour connecter un utilisateur existant, 
**Type de requete** : POST
**Route**: /clients/login
**Body**: 
```JSON
{
        "email": "",
        "password": ""
}
```

**Reponse**
-- En cas de succès -> 201
Avec le contenu suivant : 
```JSON
{
  "user": {
    "firstname": "",
    "surname": "",
    "email": "",
    "tel": "",
    "sex": null,
    "birth_date": null,
    "other": null,
    "updated_at": "2021-08-14T07:36:48.000000Z",
    "created_at": "2021-08-14T07:36:48.000000Z",
    "id": 540
  },
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1N....cUx7-sw"
}
```
    
-- En cas d'erreur -> 400
Avec le contenu suivant : 
```JSON
{
  "code": "INVALID_CREDENTIALS",
  "status": "error",
  "special": "Le mot de passe est incorrect.",
  "message": "Identifications de connexion invalides"
}
```


### Liste des produits (Page 3)

Ici vous aurez besoin d'afficher la liste de tous les produits de l'entreprise Ritual Café.

#### Lister les collections

Une collection peut etre vue comme une catégorie. Elle comporte un attribut "produits" qui est une liste de produits. 
Ainsi pour chaque catégorie, vous avez la liste des produits associés

**Type de requete** : GET
**Route**: /companies/430/collections
**Body**: 
```JSON
{
  "data": [
    {  
      "id": 117,
      "name": "Vins",
      "description": null,
      "entreprise_id": 2,
      "parent_collection_id": 112,
      "created_at": "2021-04-25T06:16:37.000000Z",
      "updated_at": "2021-04-25T06:16:37.000000Z",
      "produits": [
        {
          "id": 2735,
          "name": "Carla David",
          "description": "<p>Est dolore excepteur.sdsfgdfgsdfgsdfg<\/p>",
          "stocks": 62,
          "temps_preparation": 177,
          "editable": 0,
          "available": 1,
          "infiniteStocks": 0,
          "comparaison_price": 445,
          "price": 994,
          "entreprise_id": 64,
          "created_at": "2021-07-04T10:40:08.000000Z",
          "updated_at": "2021-07-04T10:43:30.000000Z",
          "slug": null,
          "code": null,
          "pivot": {
            "collection_id": 117,
            "product_id": 2735
          },
          "medias": [
            {
              "link": "https:\/\/dashboard.mystore.lamater.net\/storage\/2545\/Group-2-(1).png",
              "collection_name": "default",
              "collection": {
                "id": 3,
                "name": "default",
                "description": null,
                "entreprise_id": 2,
                "created_at": "2021-02-10T11:46:50.000000Z",
                "updated_at": "2021-02-10T11:46:50.000000Z"
              },
              "thumb": "https:\/\/dashboard.mystore.lamater.net\/storage\/2545\/conversions\/Group-2-(1)-thumb.jpg"
            }
          ],
          "tags": [
            {
              "id": 11,
              "name": "Poisson",
              "description": null,
              "created_at": "2020-05-28T14:43:59.000000Z",
              "updated_at": "2020-05-28T14:43:59.000000Z",
              "slug": null,
              "order_column": 0,
              "type": null,
              "pivot": {
                "product_id": 2735,
                "tag_id": 11
              }
            }
           
          ],
          "collections": [
            "Poulets\/Frites",
            "Desserts",
            "Plats"
          ],
          "variants": [],
          "avis": []
        }
      ],
      "medias": [
        {
          "link": "https:\/\/bucket-my-store.s3.eu-west-3.amazonaws.com\/2434\/vins-cote-rotie.jpg",
          "collection_name": "default",
          "collection": {
            "id": 3,
            "name": "default",
            "description": null,
            "entreprise_id": 2,
            "created_at": "2021-02-10T11:46:50.000000Z",
            "updated_at": "2021-02-10T11:46:50.000000Z"
          }
        }
      ],
      "parent": null
    }
    ],
    "links": {
        "first": "https:\/\/dashboard.mystore.lamater.net\/api\/2021-05\/companies\/2\/collections?page=1",
        "last": "https:\/\/dashboard.mystore.lamater.net\/api\/2021-05\/companies\/2\/collections?page=2",
        "prev": null,
        "next": "https:\/\/dashboard.mystore.lamater.net\/api\/2021-05\/companies\/2\/collections?page=2"
    },
    "meta": {
        "current_page": 1,
        "from": 1,
        "last_page": 2,
        "path": "https:\/\/dashboard.mystore.lamater.net\/api\/2021-05\/companies\/2\/collections",
        "per_page": 10,
        "to": 10,
        "total": 20
    }
}
```

#### Lister les produits

À partir d'une categorie(collection), on a des informations essentielles sur un produit tel que le nom (name), le prix (price), la description (description), les tags (tags), les variantes (variants), les avis (avis) et plusieurs autres champs.
À partir de la collection, il vous sera possible d'avoir les informations nécessaires pour réaliser la page produit (Page 4)


---------------------

## Rappel 
Le but n'est pas de faire une application ecommerce complète. Nous souhaitons voir votre capacité à reproduire une IHM, voir la manière dont vous structurez votre code et vos différents commit pour évaluer votre utilisation de l'outil Git.

