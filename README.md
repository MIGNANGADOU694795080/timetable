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

Question 05
CREATE VIEW emploisdetemps AS 
SELECT DISTINCT C.codeCours, T.jourCoursDate  FROM Cours C
JOIN Typehoraire T
ON C.codeCours= T.crsCodeCours
JOIN Jourcours J
ON J.dateJourCours=T.jourCoursDate
JOIN Coursdeclasse cls
ON  T.crsCodeCours=cls.crsCodeCours
JOIN Classe Cl
ON cl.specialiteNomSpec=cls.classSpecialiteNomspec
WHERE T.jourCoursDate 
IN ('lundi','mardi','mercredi','jeudi','vendredi','samedi');

4. SELECT courCodeCours FROM Etudiantdeclasse WHERE etudiantMatricule =&matricule;

5. script de l'emploi de temps
SET ECHO OFF
SET MARKUP HTML ON SPOOL ON
SPOOL emploi_temps_TIPAM2.HTML
SELECT DISTINCT T.jourCoursDate as jours ,
                  C.intituleCourt ||'('||C.codeCours||')' as cours ,
                    C.credits as credits_cours,
                    'trimestre'|| C.periodeAcademiqueIdTrim  as periode_trimestrielle,
                    ce.specialiteNomSpec || cd.classNiveauidNiveau as specialite,
                    T.tranche ||'heures' as tranche_horair


alter table etudiant add password varchar(50);
update etudiant set password = ora_hash(matricule) where matricule = valeur;

alter table enseignants add password varchar(50);
update enseignants set password = ora_hash(matricule) where matricule = valeur

CREATE VIEW Question3 AS
SELECT DISTINCT C.codeCours, T.jourCoursDate,T. TRANCHE,C.VOLUMEH FROM Cours C
JOIN Typehoraire T
ON C.codeCours= T.crsCodeCours
JOIN Jourcours J
ON J.dateJourCours=T.jourCoursDate
JOIN Coursdeclasse cls
ON T.crsCodeCours=cls.crsCodeCours
JOIN Classe Cl
ON cl.specialiteNomSpec=cls.classSpecialiteNomspec
WHERE T.jourCoursDate
 IN ('lundi','mardi','mercredi','jeudi','vendredi','samedi') AND cls.classNiveauidNiveau=001;

 SELECT * FROM Question3
ORDER BY T.jourCoursDate ASC;
SPOOL OFF
SET MARKUP HTML OFF
SET ECHO ON
