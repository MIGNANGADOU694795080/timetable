// Question 03
SET ECHO OFF
SET MARKUP HTML ON SPOOL ON
SPOOL emploi_temps_TIPAM2.HTML
SELECT DISTINCT T.jourCoursDate as jours ,
                  C.intituleCourt ||'('||C.codeCours||')' as cours ,
                    C.credits as credits_cours,
                    'trimestre'|| C.periodeAcademiqueIdTrim  as periode_trimestrielle,
                    ce.specialiteNomSpec || cd.classNiveauidNiveau as specialite,
                    T.tranche ||'heures' as tranche_horaire
FROM Cours C
JOIN Typehoraire T
ON C.codeCours= T.crsCodeCours
JOIN Jourcours j
ON J.dateJourCours=T.jourCoursDate
JOIN Coursdeclasse cd
ON  T.crsCodeCours=cd.crsCodeCours
JOIN Classe ce
ON ce.specialiteNomSpec=cd.classSpecialiteNomspec
INNER JOIN ClassePeriodeacademique ca
ON C.periodeAcademiqueIdTrim=ca.PERIODEACADEMIQUEIDTRIM
WHERE ce.specialiteNomSpec='TIPAM'
AND   cd.classNiveauidNiveau=002
    ORDER BY CASE T.jourCoursDate  WHEN 'lundi' THEN T.jourCoursDate END ASC,
             CASE T.jourCoursDate  WHEN 'mardi' THEN T.jourCoursDate END ASC,
             CASE T.jourCoursDate  WHEN 'mercredi' THEN T.jourCoursDate END ASC,
             CASE T.jourCoursDate  WHEN 'jeudi' THEN T.jourCoursDate END ASC,
             CASE T.jourCoursDate  WHEN 'vendredi' THEN T.jourCoursDate END ASC,
             CASE T.jourCoursDate  WHEN 'samedi' THEN T.jourCoursDate END ASC; 
--ORDER BY T.jourCoursDate ASC;
SPOOL OFF
SET MARKUP HTML OFF
SET ECHO ON




SELECT DISTINCT T.jourCoursDate as jours ,C.intituleCourt ||'('||C.codeCours||')' as cours ,
C.credits as credits_cours,'trimestre'|| C.periodeAcademiqueIdTrim  as periode_trimestrielle,
ce.specialiteNomSpec || cd.classNiveauidNiveau as specialite,
T.tranche ||'heures' as tranche_horaire
FROM Cours C
JOIN Typehoraire T
     ON C.codeCours= T.crsCodeCours
JOIN Jourcours j
     ON J.dateJourCours=T.jourCoursDate
JOIN Coursdeclasse cd
     ON  T.crsCodeCours=cd.crsCodeCours
JOIN Classe ce
     ON ce.specialiteNomSpec=cd.classSpecialiteNomspec
INNER JOIN ClassePeriodeacademique ca
     ON C.periodeAcademiqueIdTrim=ca.PERIODEACADEMIQUEIDTRIM
WHERE ce.specialiteNomSpec='&specialite'
AND cd.classNiveauidNiveau=&niveau
and C.PERIODEACADEMIQUEIDTRIM=1

CASE 
ORDER BY 
(
    CASE T.jourCoursDate
        When 'lundi' THEN 1
        When 'mardi' THEN 2
        When 'mercredi' THEN 3
        When 'jeudi' THEN 4
        When 'Vendredi' THEN 5
        else 5
    END
)ASC;
