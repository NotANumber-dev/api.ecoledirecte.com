# api.ecoledirecte.com
requetes possibles à l'api d'ecoledirecte

> [!warning]
> documentation non officielle

> [!note]
> version anglais a venir


## format de l'api
les requetes ecoledirecte sont envoyés a ``https://api.ecoledirecte.com/`` en ``POST`` (pas GET
)

Toutes les requêtes partagent les mêmes caractéristiques :

- **Méthode** : `POST`
- **Header commun** : `Content-Type: application/x-www-form-urlencoded`
- **Authentification** : Header `X-Token: <token>`
- **Corps** : `data=<JSON encodé en URL>`
- **ID élève** : E123456
