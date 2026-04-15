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

# Documentation API EcoleDirecte

## Caractéristiques communes

Toutes les requêtes authentifiées partagent les mêmes caractéristiques :

- **Méthode :** `POST`
- **Header :** `Content-Type: application/x-www-form-urlencoded`
- **Authentification :** `X-Token: <token>`
- **Corps :** `data=<JSON encodé en URL>`
- **ID élève :** `<id>`


## Notes

```http
POST /v3/eleves/<id>/notes.awp?verbe=get&v=6.17.0
Host: api.ecoledirecte.com
Content-Type: application/x-www-form-urlencoded
X-Token: <token>

data={"anneeScolaire":""}
```

```json
{
  "code": 200,
  "data": {
    "notes": [
      {
        "valeur": "14.5",
        "noteSur": "20",
        "libelleMatiere": "MATHEMATIQUES",
        "codePeriode": "A001",
        "coef": "2",
        "date": "2026-01-15",
        "commentaire": "Bon travail"
      }
    ]
  }
}
```


## Cahier de texte (Devoirs)

```http
POST /v3/Eleves/<id>/cahierdetexte.awp?verbe=get&v=4.98.0
Host: api.ecoledirecte.com
Content-Type: application/x-www-form-urlencoded
X-Token: <token>

data={}
```

```json
{
  "code": 200,
  "data": {
    "2026-04-15": [
      {
        "idDevoir": 98765,
        "matiere": "MATHEMATIQUES",
        "contenu": "RXhlcmNpY2VzIDEgYWwgNSBwYWdlIDQy",
        "effectue": false,
        "interrogation": false,
        "donneLe": "2026-04-14"
      }
    ]
  }
}
```


```markdown
# Marquer un devoir comme fait / non fait

## Marquer comme fait

```http
POST /v3/Eleves/<id>/cahierdetexte.awp?verbe=put&v=4.98.0
Host: api.ecoledirecte.com
Content-Type: application/x-www-form-urlencoded
X-Token: <token>

data={"idDevoirsEffectues":[98765],"idDevoirsNonEffectues":[]}
```

```json
{
  "code": 200,
  "message": "OK"
}
```

## Marquer comme non fait

```http
POST /v3/Eleves/<id>/cahierdetexte.awp?verbe=put&v=4.98.0
Host: api.ecoledirecte.com
Content-Type: application/x-www-form-urlencoded
X-Token: <token>

data={"idDevoirsEffectues":[],"idDevoirsNonEffectues":[98765]}
```

```json
{
  "code": 200,
  "message": "OK"
}
```

## Détail d'une journée

```http
POST /v3/Eleves/<id>/cahierdetexte/2026-04-15.awp?verbe=get&v=4.98.0
Host: api.ecoledirecte.com
Content-Type: application/x-www-form-urlencoded
X-Token: <token>

data={}
```

```json
{
  "code": 200,
  "data": {
    "matieres": [
      {
        "matiere": "MATHEMATIQUES",
        "aFaire": {
          "idDevoir": 98765,
          "contenu": "RXhlcmNpY2VzIDEgYWwgNSBwYWdlIDQy",
          "effectue": false,
          "documents": [
            {
              "id": 111,
              "libelle": "exercices.pdf"
            }
          ]
        }
      }
    ]
  }
}
```



## Messagerie (liste)

```http
POST /v3/eleves/<id>/messages.awp?typeRecuperation=received&itemsPerPage=100&verbe=get&v=4.98.0
Host: api.ecoledirecte.com
Content-Type: application/x-www-form-urlencoded
X-Token: <token>

data={}
```

```json
{
  "code": 200,
  "data": {
    "messages": {
      "received": [
        {
          "id": 112233,
          "subject": "Sortie scolaire",
          "date": "2026-04-10 14:30:00",
          "read": false,
          "from": {
            "nom": "DUPONT",
            "prenom": "Marie"
          },
          "files": [
            {
              "id": 222,
              "libelle": "autorisation.pdf"
            }
          ]
        }
      ]
    }
  }
}
```

## Messagerie (détail)

```http
POST /v3/eleves/<id>/messages/112233.awp?verbe=get&mode=destinataire&v=4.98.0
Host: api.ecoledirecte.com
Content-Type: application/x-www-form-urlencoded
X-Token: <token>

data={}
```

```json
{
  "code": 200,
  "data": {
    "id": 112233,
    "subject": "Sortie scolaire",
    "content": "Q29uZmlybWF0aW9uIGRlIGxhIHNvcnRpZQ==",
    "date": "2026-04-10 14:30:00",
    "from": {
      "nom": "DUPONT",
      "prenom": "Marie"
    },
    "files": [
      {
        "id": 222,
        "libelle": "autorisation.pdf"
      }
    ]
  }
}
```


## Carnet de correspondance

```http
POST /v3/eleves/<id>/eleveCarnetCorrespondance.awp?verbe=get&v=4.98.0
Host: api.ecoledirecte.com
Content-Type: application/x-www-form-urlencoded
X-Token: <token>

data={}
```

```json
{
  "code": 200,
  "data": {
    "correspondances": [
      {
        "type": "Observation",
        "contenu": "RWxjbGlhbnQgc3VyIGxlIHRyYXZhaWw=",
        "dateCreation": "2026-04-01 10:15:00",
        "auteur": {
          "nom": "MARTIN",
          "prenom": "Jean"
        },
        "isSignatureDemandee": true,
        "urlFichier": "https://api.ecoledirecte.com/fichiers/333"
      }
    ]
  }
}
```

## Vie scolaire

```http
POST /v3/eleves/<id>/viescolaire.awp?verbe=get&v=4.98.0
Host: api.ecoledirecte.com
Content-Type: application/x-www-form-urlencoded
X-Token: <token>

data={}
```

```json
{
  "code": 200,
  "data": {
    "absencesRetards": [
      {
        "typeElement": "Absence",
        "displayDate": "Lundi 5 Avril",
        "libelle": "Absence matinée",
        "justifie": true,
        "motif": "Rendez-vous médical"
      }
    ],
    "sanctionsEncouragements": [
      {
        "typeElement": "Encouragement",
        "libelle": "Travail soigné",
        "date": "2026-04-07"
      }
    ]
  }
}
```

## Timeline

```http
POST /v3/eleves/<id>/timeline.awp?verbe=get&v=4.98.0
Host: api.ecoledirecte.com
Content-Type: application/x-www-form-urlencoded
X-Token: <token>

data={}
```

```json
{
  "code": 200,
  "data": [
    {
      "titre": "Réunion parents-professeurs",
      "soustitre": "Remise des bulletins",
      "contenu": "RV le 25 avril",
      "date": "2026-04-25"
    }
  ]
}
```

## Téléchargement de pièce jointe

```http
POST /v3/telechargement.awp?verbe=get&fichierId=<idFichier>&leTypeDeFichier=PIECE_JOINTE&v=4.98.0
Host: api.ecoledirecte.com
Content-Type: application/x-www-form-urlencoded
X-Token: <token>

data={"forceDownload":0,"anneeMessages":"2025-2026"}
```

*Réponse : Fichier binaire (PDF, image, vidéo, etc.)*

## Espace de travail

```http
POST /v3/E/<id>/espacestravail.awp?verbe=get&typeModule=espaceTravail&v=4.98.0
Host: api.ecoledirecte.com
Content-Type: application/x-www-form-urlencoded
X-Token: <token>

data={}
```

```json
{
  "code": 200,
  "data": [
    {
      "id": "ESPACE_001",
      "titre": "Classe de 4ème",
      "resume": "RXNwYWNlIGRlIHRyYXZhaWw=",
      "estMembre": true,
      "cloud": true
    }
  ]
}
```

## Codes d'erreur

| Code | Signification |
|------|---------------|
| 200 | Succès |
| 403 | Token invalide ou expiré |
| 404 | Ressource non trouvée |
| 500 | Erreur interne du serveur |

```json
{
  "code": 403,
  "message": "Token invalide ou expiré"
}
```
