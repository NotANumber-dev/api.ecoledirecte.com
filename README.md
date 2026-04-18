# api.ecoledirecte.com
requetes possibles à l'api d'ecoledirecte

> [!warning]
> documentation non officielle
> Documentation uniquement des appels api de ecoledirecte -

> [!note]
> version anglais a venir
> plus d'infos a venir
> Cette "documentation" n'est pas complète. utilise d'autre sources pour d'autes appels api.


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
