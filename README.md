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

## Notes
requete:
```http
POST /v3/eleves/<id>/notes.awp?verbe=get&v=6.17.0
Host: api.ecoledirecte.com
Content-Type: application/x-www-form-urlencoded
X-Token: <token>

data={"anneeScolaire":""}
```
reponse:
```json
{
  "code": 200,
  "data": {
    "notes": [
      {
        "valeur": "0",
        "noteSur": "100",
        "libelleMatiere": "MATHEMATIQUES",  //nom d'affichage de la matière
        "codePeriode": "A001",  //trimestre A001 = trimestre 1, A002 = trimestre 2, A003 = trimestre 3
        "coef": "67",
        "date": "2026-01-15",
        "commentaire": "Confonds pi avec le périmètre d'un rectangle"
      }
    ]
  }
}
```


## Cahier de texte (Devoirs)
Obtenir TOUS les devoirs
```http
POST /v3/Eleves/<id>/cahierdetexte.awp?verbe=get&v=4.98.0
Host: api.ecoledirecte.com
Content-Type: application/x-www-form-urlencoded
X-Token: <token>

data={}
```
reponse
```json{
  "code": 200,
  "data": {
    "2026-04-15": [
      {
        "idDevoir": 1,
        "matiere": "MATHEMATIQUES",
        "effectue": false,  //fait ou pas fait
        "interrogation": false
      }
    ],
    "2026-04-16": [
      {
        "idDevoir": 2,
        "matiere": "HISTOIRE-GEOGRAPHIE",
        "effectue": true,
        "interrogation": true   /eva ou pas
      },
      {
        "idDevoir": 3,
        "matiere": "PHYSIQUE-CHIMIE",
        "effectue": false,
        "interrogation": false
      }
    ]
  }
}
```

obtenir les devoirs d'une periode spécifiée 

```http
POST /v3/Eleves/<id>/cahierdetexte/<date>.awp?verbe=get&v=4.98.0
```
date est variable, par exemple 2026-04-15
<br>reponse
```http
{
  "code": 200,
  "data": {
    "matieres": [
      {
        "matiere": "MATHEMATIQUES",
        "aFaire": {
          "idDevoir": 1,
          "contenu": "RmFpcmUgbGVzIGV4ZXJjaWNlcyBkZSBsYSBwYWdlIDI1IGEgbGEgcGFnZSAyNDgu", //travail a faire encodé en base64
          "effectue": false,
          "documents": [
            {
              "id": 111, //id de la piece jointe
              "libelle": "exercices.pdf" //nom du fichier en piece jointe
            }
          ]
        }
      }
    ]
  }
}
```
# Marquer un devoir comme fait / non fait
## Marquer comme fait
pour faire cela, on a besoin de l'identifiant du devoir et remplir avec celui ci fait ou non fait
```http
POST /v3/Eleves/<id>/cahierdetexte.awp?verbe=put&v=4.98.0
Host: api.ecoledirecte.com
Content-Type: application/x-www-form-urlencoded
X-Token: <token>

data={"idDevoirsEffectues":[ID],"idDevoirsNonEffectues":[]}
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

data={"idDevoirsEffectues":[],"idDevoirsNonEffectues":[ID]}
```

```json
{
  "code": 200,
  "message": "OK"
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
          "id": 112233, //id du message
          "subject": "Sortie scolaire",
          "date": "2026-04-10 14:30:00", //date et heure
          "read": false, //lu ou non lu, les enseignants peuvent voir cela également.
          "from": {
            "nom": "SAHUR",
            "prenom": "Tung tung"
          },
          "files": [
            {
              "id": 222, //id de la puece jointe
              "libelle": "autorisation.pdf" //pieces jointes
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
POST /v3/eleves/<id>/messages/<ID>.awp?verbe=get&mode=destinataire&v=4.98.0
Host: api.ecoledirecte.com
Content-Type: application/x-www-form-urlencoded
X-Token: <token>

data={}
```
id est l'identifiant du message (112233 comme exemple)
```json
{
  "code": 200,
  "data": {
    "id": 112233,
    "subject": "Sortie scolaire",
    "content": "VmVuZXogc3Zw", //contenu du message en base 64
    "date": "2026-04-10 14:30:00",
    "from": {
      "nom": "SAHUR",
      "prenom": "Tung tung"
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
        "type": "Observation",  //listerai les types plus tard
        "contenu": "Sm91ZSBhIGZvcnRuaXRlIGVuIGNvdXJz", //correspondance en base 64
        "dateCreation": "2026-04-01 10:15:00", //date et heure
        "auteur": {
          "nom": "west",
          "prenom": "Mason"
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
