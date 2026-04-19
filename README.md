# api.ecoledirecte.com
requetes possibles à l'api d'ecoledirecte

> [!warning]
> documentation non officielle
> Documentation uniquement des appels api de ecoledirecte -

> [!note]
> version anglais a venir et
> plus d'infos a venir.
> 
> Cette "documentation" n'est pas complète. utilise d'autre sources pour d'autes appels api.

## Sommaire

- [Format de l'api](#format-de-lapi)
- [Notes](#notes)
- [Cahier de texte](#cahier-de-texte)
     - [tous les devoirs](#tous-les-devoirs)
     - [jour spécifié](#cahier-de-textespecifié)
     - [marquer comme fait/non fait](#marquer-fait-ou-non-fait)
        - [marquer fait](#marquer-fait)
        - [marquer non fait](#marquer-non-fait)
- [pièces jointes](#pièce-jointe)
## format de l'api
les requetes ecoledirecte sont envoyés a ``https://api.ecoledirecte.com/`` en ``POST`` (pas GET
)

Toutes les requêtes partagent les mêmes caractéristiques :

- **Méthode** : `POST`
- **Header commun** : `Content-Type: application/x-www-form-urlencoded`
- **Authentification** : Header `X-Token: <token>`
- **Corps** : `data=<JSON encodé en URL>`
- **ID élève** : E123456

## notes
utilise
```url
api.ecoledirecte.com/v3/eleves/ID/notes.awp?verbe=get&v=4.98.0
```
requete:
```json
{
  "method": "POST",
  "scheme": "https",
  "authority": "api.ecoledirecte.com",
  "path": "/v3/eleves/ID/notes.awp?verbe=get&v=4.98.0",
  "Content-Type": "application/x-www-form-urlencoded",
  "X-Token": "abcde",
  "body": {
    "data": {"anneeScolaire": ""} //vide ou année scolaire actuelle
  }
}
```
reponse:
```json
{
    "code": 200,
    "token": "abcdefghijklmnopqrstuvwxyz1234567890",  //token (exemple)
    "host": "HTTP139",
    "data": {
        "foStat": "1001",
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
                "salleConseil": "SALLE CONSEIL 1",  //nom de la salle de conseil de classe
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
                                    "id": 1000, //id du prof
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
                            "nom":"M. Lampe"
                        }
                    ]
                },
            ]
        }
    }
}
```

- [Retour au sommaire](#Sommaire)
## cahier de texte
le cahier de texte sur le site charge plusieurs pages: 
   - viedelaclasse.awp
   - cahierdetexte.awp
   - manuelsNumeriques.awp

Je vais rester uniquement sur cahierdetexte.awp dans cette section
## tous les devoirs
utilise
```url
api.ecoledirecte.com/v3/Eleves/ID/cahierdetexte.awp?verbe=get&v=4.98.0
```

requete:
```json
{
  "method": "POST",
  "scheme": "https",
  "authority": "api.ecoledirecte.com",
  "path": "/v3/Eleves/ID/cahierdetexte.awp?verbe=get&v=4.98.0",
  "2FA-Token": "7654321",
  "Accept": "application/json, text/plain, */*",
  "Accept-Encoding": "gzip, deflate, br, zstd",
  "Accept-Language": "en-US,en;q=0.9",
  "Content-Length": 7,
  "Content-Type": "application/x-www-form-urlencoded",
  "Origin": "https://www.ecoledirecte.com",
  "Priority": "u=3, i",
  "Referer": "https://www.ecoledirecte.com/",
  "Sec-Fetch-Dest": "empty",
  "Sec-Fetch-Mode": "cors",
  "Sec-Fetch-Site": "same-site",
  "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/26.4 Safari/605.1.15",
  "X-Token": "1234567"
}
```
reponse
```json
{
  "code": 200,
  "token": "7654321",
  "host": "HTTP232",
  "data": {
    "2026-01-3": [ //pour quand, ici 2 devoirs pour le meme jour
      {
        "matiere": "FORTNITE", //nom d'affichage matiere
        "codeMatiere": "FN", //code matiere
        "aFaire": true,
        "idDevoir": 1,
        "documentsAFaire": false,
        "donneLe": "2026-01-01", //date ou le devoir a ete donné
        "effectue": false, //fait ou pas
        "interrogation": true, //eva ou pas
        "rendreEnLigne": false, //fonctionalitée "rendre en ligne"
        "tags": []
      },
      {
        "matiere": "FRANCAIS",
        "codeMatiere": "FRANC",
        "aFaire": true,
        "idDevoir": 2,
        "documentsAFaire": true,
        "donneLe": "2026-04-03",
        "effectue": false,
        "interrogation": false,
        "rendreEnLigne": false,
        "tags": []
      }
    ],
    "2026-02-04": [
      {
        "matiere": "MATHEMATIQUES",
        "codeMatiere": "MATHS",
        "aFaire": true,
        "idDevoir": 3,
        "documentsAFaire": true,
        "donneLe": "2026-02-06",
        "effectue": true,
        "interrogation": false,
        "rendreEnLigne": true,
        "tags": []
      }
    ],
  }
}
```


## cahier de texte(specifié)
obtenir les devoirs d'une periode spécifiée.
utilise
```url
api.ecoledirecte.com/v3/Eleves/ID/cahierdetexte/YYYY-MM-DD.awp?verbe=get&v=4.98.0
```

ID=1234 pour E1234

```json
{
  "method": "POST",
  "scheme": "https",
  "authority": "api.ecoledirecte.com",
  "path": "/v3/Eleves/ID/cahierdetexte/2026-05-04.awp?verbe=get&v=4.98.0",
  "2FA-Token": "7654321",
  "Accept": "application/json, text/plain, */*",
  "Accept-Encoding": "gzip, deflate, br, zstd",
  "Accept-Language": "en-US,en;q=0.9",
  "Content-Type": "application/x-www-form-urlencoded",
  "Origin": "https://www.ecoledirecte.com",
  "Priority": "u=3, i",
  "Referer": "https://www.ecoledirecte.com/",
  "Sec-Fetch-Dest": "empty",
  "Sec-Fetch-Mode": "cors",
  "Sec-Fetch-Site": "same-site",
  "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/26.4 Safari/605.1.15",
  "X-Token": "1234567",
  "body": "data={}"
}
```
réponse:
```json
{
  "code": 200,
  "token": "7654321",
  "host": "HTTP321",
  "data": {
    "date": "2026-02-04",
    "matieres": [
      {
        "entityCode": "MATHS",
        "entityLibelle": "MATHS",
        "entityType": "M",
        "matiere": "MATHEMATIQUES",
        "codeMatiere": "DNLHG",
        "nomProf": "Mme. Cercle",
        "id": 3,
        "interrogation": false,
        "blogActif": false,
        "nbJourMaxRenduDevoir": 0,
        "aFaire": {
          "idDevoir": 3,
          "contenu": "dmVuZXogZW4gY291cnMgc3Zw", //travail a faire en base64
          "rendreEnLigne": false,
          "donneLe": "2026-01-06",
          "effectue": false,
          "ressource": "",
          "documentsRendusDeposes": false,
          "ressourceDocuments": [],
          "documents": [
            {
              "id": 67,
              "libelle": "Cube.pdf",
              "date": "2026-01-06",
              "taille": 6031010, //taille du doc
              "type": "FICHIER_CDT",
              "signatureDemandee": false,
              "etatSignatures": [],
              "signature": {}
            },
            {
              "id": 69,
              "libelle": "Pavé-pas-droit.pdf",
              "date": "2026-01-06",
              "taille": 112541,
              "type": "FICHIER_CDT",
              "signatureDemandee": false,
              "etatSignatures": [],
              "signature": {}
            }
          ],
          "elementsProg": [],
          "liensManuel": [],
          "documentsRendus": [],
          "tags": [],
          "cdtPersonnalises": [],
          "contenuDeSeance": {
            "contenu": "",
            "documents": []
          }
        }
      }
    ]
  }
}
```
## marquer comme fait ou non fait
utilise
```url
api.ecoledirecte.com/v3/Eleves/<id>/cahierdetexte.awp?verbe=put&v=4.98.0
```
pour faire cela, on a besoin de l'identifiant du devoir et remplir avec celui ci fait ou non fait
> [!note]
> laisser l'autre champ vide
## marquer fait
Requete:
```json
{
  "method": "POST",
  "scheme": "https",
  "authority": "api.ecoledirecte.com",
  "path": "/v3/Eleves/<id>/cahierdetexte.awp?verbe=put&v=4.98.0",
  "Content-Type": "application/x-www-form-urlencoded",
  "X-Token": "<token>",
  "body": "data={\"idDevoirsEffectues\":[ID],\"idDevoirsNonEffectues\":[]}"
}
```
Reponse:
```json
{
  "code": 200,
  "message": "OK"
}
```
Le devoir est maintenant non fait (sur l'app, site et autres)

## marquer non fait
Requete:
```json
{
  "method": "POST",
  "scheme": "https",
  "authority": "api.ecoledirecte.com",
  "path": "/v3/Eleves/<id>/cahierdetexte.awp?verbe=put&v=4.98.0",
  "Content-Type": "application/x-www-form-urlencoded",
  "X-Token": "<token>",
  "body": "data={\"idDevoirsEffectues\":[],\"idDevoirsNonEffectues\":[ID]}"
}
```
Reponse:
```json
{
  "code": 200,
  "message": "OK"
}
```
Le devoir est maintenant non fait
- [Retour au sommaire](#Sommaire)
## pièce jointe
Récuperer la pièce jointe
> [!note]
> pièce jointe de mail, devoir ou vie scolaire
> recupère avec id

utilise telechargement.awp
```url
https://api.ecoledirecte.com/v3/telechargement.awp?verbe=get&fichierId=<ID fichier>&leTypeDeFichier=<type fichier>&v=4.98.0
```
Requete
```json
{
  "method": "POST",
  "scheme": "https",
  "authority": "api.ecoledirecte.com",
  "path": "/v3/telechargement.awp?verbe=get&fichierId=<ID_FICHIER>&leTypeDeFichier=<TYPE_FICHIER>&v=4.98.0",
  "2FA-Token": "7654321",
  "Accept": "application/json, text/plain, */*",
  "Content-Type": "application/x-www-form-urlencoded",
  "Origin": "https://www.ecoledirecte.com",
  "Referer": "https://www.ecoledirecte.com/",
  "X-Token": "1234567",
  "body": "data={\"forceDownload\":0}"
}
```
Réponse (en binaire):
```binary
0000000000000000000000000000000000000000
0000000000000000000000000000000000000000
0000000000000000000110000000000000000000
0000000000000000011111100000000000000000
0000000000000000001111111000000000000000
0000000000000000000011111000000000000000
0000000000000000000011110000000000000000
0000000000000000000000000000000000000000
0000000000000000000000110000000000000000
0000000000000000001111110000000000000000
0000000000000000000011111000000000000000
0000000000000000000100000000000000000000
0000000000000000000000000000000000000000
0000000000000000000000000000000000000000
0000000000000000000000000000000000000000
0000000000000000000000000000000000000000
0000000000000000000000000000000000000000
0000000000000000000000000000000000000000
0000000001000010110011011001110000000000
0000000000000000000000000000000000000000
0000000000000000000000000000000000000000
0000000000000000000000000000000000000000
0000000000000000000000000000000000000000
0000000000000000000000000000000000000000
0000000000000000000000000000000000000000
0000000000000000000000000000000000000000
0000000000000000000000000000000000000000
0000000000000000000000000000000000000000
0000000000000000000000000000000000000000
0000000000000000000000000000000000000000
0000000000000000000000000000000000000000
```



## Codes d'erreur

| Code | Signification |
|------|---------------|
| 200 | Succès |
| 403 | Token invalide/expiré |
| 404 | Ressource non trouvée |
| 500 | Erreur du serveur |

```json
{
  "code": 403,
  "message": "Token invalide ou expiré"
}
```
