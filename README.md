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
    "token": "abcdefghijklmnopqrstuvwxyz1234567890",  //token (exemple)
    "host": "HTTP139",
    "data": {
        "foStat": "1001",  //jsp sa sert a quoi
        "periodes": [
            {
                "idPeriode": "A001",  //Identifiant peridode, utilisé pour savoir quelle note est ou
                "codePeriode": "A001",
                "periode": "1er Trimestre", //nom du trimestre
                "annuel": false,
                "dateDebut": "2025-09-02",  //debut trimestre
                "dateFin": "2025-11-21",  //fin trimestre
                "examenBlanc": false,
                "cloture": true,  //si le trimestre est en cours
                "dateConseil": "2025-12-04",  //date conseil de classe
                "heureConseil": "17:45",  //heure conseil de classe
                "salleConseil": "SALLE CONSEIL 1",  //jsp
                "moyNbreJoursApresConseil": -1,
                "ensembleMatieres": {
                    "dateCalcul": "",
                    "nomPP": "M. Patapim",
                    "nomCE": "",
                    "decisionDuConseil": "",  
                    "disciplines": [
//CAS SPECIAL, DEUX PROFS
                        {
                            "id": 1, //id de la note
                            "codeMatiere": "FN",  //code de la matière (mathematiques=math, espagnol=ESP)
                            "codeSousMatiere": "",
                            "discipline": "FORTNITE",
                            "coef": 1, //coefitient
                            "effectif": 0,
                            "rang": 0,
                            "groupeMatiere": false,
                            "idGroupeMatiere": 0,
                            "option": 0,
                            "sousMatiere": false,
                            "saisieAppreciationSSMat": false,
                            "professeurs": [
                                {
                                    "id": 1000, //id du prof, plus grand = prof plus recent, peut determiner quel prof est arivé avant qui
                                    "nom": "Mme Raider."
                                },
                                {
                                    "id": 100,
                                    "nom": "M deux."
                                }
                            ]
                        },
                        {
                            "id": 2,
                            "codeMatiere": "MATHS",
                            "codeSousMatiere": "",
                            "discipline": "MATHEMATIQUES",
                            "coef": 1,
                            "effectif": 0,
                            "rang": 0,
                            "groupeMatiere": false,
                            "idGroupeMatiere": 0,
                            "option": 0,
                            "sousMatiere": false,
                            "saisieAppreciationSSMat": false,
                            "professeurs": [
                                {
                                    "id": 67,
                                    "nom": "Mme Cercle."
                                }
                            ]
                        }
                    ],
                    "disciplinesSimulation": []  //fin des arguments
                }
            },
         {
                "idPeriode": "A999Z",
                "codePeriode": "A999Z",
                "periode": "Année",
                "annuel": true,
                "dateDebut": "2025-09-02",
                "dateFin": "2026-06-30",
                "examenBlanc": false,
                "cloture": false,
                "moyNbreJoursApresConseil": -1,
                "ensembleMatieres": {
                    "dateCalcul": "",
                    "nomPP": "M. Patapim.",
                    "nomCE": "",
                    "decisionDuConseil": "",
                    "disciplines": [
//encore une fois, je n'en ai absolument AUCUNE idée pourquoi
                        {
                            "id": 1,
                            "codeMatiere": "FN", 
                            "codeSousMatiere": "",
                            "discipline": "FORTNITE",
                            "coef": 1, //coefitient
                            "effectif": 0,
                            "rang": 0,
                            "groupeMatiere": false,
                            "idGroupeMatiere": 0,
                            "option": 0,
                            "sousMatiere": false,
                            "saisieAppreciationSSMat": false,
                            "professeurs": [
                                {
                                    "id": 1000,
                                    "nom": "Mme Raider."
                                },
                                {
                                    "id": 100,
                                    "nom": "M deux."
                                }
                            ]
                        },
                        {
                            "id": 2,
                            "codeMatiere": "MATHS",
                            "codeSousMatiere": "",
                            "discipline": "MATHEMATIQUES",
                            "coef": 1,
                            "effectif": 0,
                            "rang": 0,
                            "groupeMatiere": false,
                            "idGroupeMatiere": 0,
                            "option": 0,
                            "sousMatiere": false,
                            "saisieAppreciationSSMat": false,
                            "professeurs": [
                                {
                                    "id": 67,
                                    "nom": "Mme Cercle."
                                }
                            ]
                        }
                    ],
                    "disciplinesSimulation": []  //fin des arguments
                }
            },
 ],
//les vraies notes
        "notes": [
            {
                "id": 1,
                "devoir": "Fortnite battle royale chapitre 7 saison 1",
                "codePeriode": "A001",
                "codeMatiere": "FN",
                "libelleMatiere": "Fortnite",
                "codeSousMatiere": "Fort",
                "typeDevoir": "Interrogation",
                "enLettre": false,
                "commentaire": "",
                "uncSujet": "",
                "uncCorrige": "",
                "date": "2025-09-08",
                "dateSaisie": "2025-09-27",
                "coef": "1",
                "noteSur": "20",
                "valeur": "19,5",
                "valeurisee": false,
                "nonSignificatif": false,
                "moyenneClasse": "",  //activable par l'etablissement
                "minClasse": "", //activable par l'etablissement
                "maxClasse": "", //activable par l'etablissement
                "elementsProgramme": [
                    {
                        "descriptif": "faire un top 1",
                        "idElemProg": 1,
                        "valeur": "4",  //1=non atteints / 2=partielement atteints / 3=atteints  /  4=depassés
                        "cdt": false,
                        "idCompetence": 671,
                        "idConnaissance": 0,
                        "libelleCompetence": "Gagner une game sur BATTLE ROYALE",
                        "afc": 0
                    }
                ]
            },
            {
                "id": 2,
                "devoir": "Pi",
                "codePeriode": "A001",
                "codeMatiere": "MATHS",
                "libelleMatiere": "MATHEMATIQUES",
                "codeSousMatiere": "",
                "typeDevoir": "Interrogation",
                "enLettre": false,
                "commentaire": "",
                "uncSujet": "",
                "uncCorrige": "",
                "date": "2025-09-12",
                "dateSaisie": "2025-09-12",
                "coef": "0.25",
                "noteSur": "20",
                "valeur": "-42,5",
                "valeurisee": false,
                "nonSignificatif": false,
                "moyenneClasse": "", //activable par l'etablissement
                "minClasse": "", //activable par l'etablissement
                "maxClasse": "", //activable par l'etablissement
                "elementsProgramme": [
                    {
                        "descriptif": "faire des additions",
                        "idElemProg": 2,
                        "valeur": "1",
                        "cdt": false,
                        "idCompetence": 672,
                        "idConnaissance": 0,
                        "libelleCompetence": "additioner",
                        "afc": 1
                    },
                    {
                        "descriptif": "Calculer et soustraire",
                        "idElemProg": 1793,
                        "valeur": "1",
                        "cdt": false,
                        "idCompetence": 673,
                        "idConnaissance": 0,
                        "libelleCompetence": "Nombres et calculs",
                        "afc": 1
                    }
                ]
            },
  ],
        "parametrage": {
            "couleurEval1": "#ff0000",
            "couleurEval2": "#ffc000",
            "couleurEval3": "#0070c0",
            "couleurEval4": "#00b050",
            "libelleEval1": "", //texte en base64, enlevé pour des raisons de vie privée
            "libelleEval2": "", //texte en base64, enlevé pour des raisons de vie privée
            "libelleEval3": "", //texte en base64, enlevé pour des raisons de vie privée
            "libelleEval4": "", //texte en base64, enlevé pour des raisons de vie privée
            "affichageMoyenne": false, //activable par l'etablissement, moyenne ELEVE
            "affichageMoyenneDevoir": false, //activable par l'etablissement, moyenne ELEVE
            "affichagePositionMatiere": false,
            "affichageOngletCompetence": 1,
            "affichageNote": true,
            "affichageCompetence": true,
            "affichageEvaluationsComposantes": false,
            "affichageGraphiquesComposantes": true,
            "modeCalculGraphiquesComposantes": "eval",
            "affichageCompNum": false,
            "libelleEvalCompNum1": "", //texte en base64, enlevé pour des raisons de vie privée
            "libelleEvalCompNum2": "", //texte en base64, enlevé pour des raisons de vie privée
            "libelleEvalCompNum3": "", //texte en base64, enlevé pour des raisons de vie privée
            "affichageAppreciation": false,
            "coefficientNote": true,
            "colonneCoefficientMatiere": false,
            "noteGrasSousMoyenne": false,
            "noteGrasAudessusMoyenne": false,
            "libelleDevoir": true,
            "dateDevoir": true,
            "typeDevoir": true,
            "noteUniquementPeriodeCloture": false,
            "notePeriodeReleve": false,
            "notePeriodeAnnuelle": false,
            "notePeriodeHorsP": false,
            "libellesAppreciations": [
                "Appréciation générale"
            ],
            "appreciationsParametrage": [
                {
                    "code": "APP1",
                    "id": 1,
                    "nbMaxCaractere": 200,
                    "libelle": "Appréciation générale"
                }
            ]
        },
        "LSUN": {
            "A001": [
                {
                    "cdt": false,
                    "codeMatiere": "FN",
                    "libelleMatiere": "FORTNITE",
                    "isFirstOfMatiere": true,
                    "nbElemProgMatiere": 5,
                    "codeSousMatiere": "",
                    "libelleSousMatiere": "",
                    "isFirstOfSousMatiere": false,
                    "nbElemProgSousMatiere": 0,
                    "libelleElementProgramme": "Jouer",
                    "idElemProg": 1,
                    "valeur": "4",
                    "afc": 0,
                    "professeurs": [
                        {
                            "id": 1234,
                            "nom": "M. Lampe"
                        }
                    ]
                },
            ]
        }
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
