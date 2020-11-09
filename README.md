# Bik_in_Paris

# BIK'IN PARIS - ETUDE DU TRAFFIC CYCLISTE

## PRESENTATION DU JEU DE DONNEES

<br>

L'objectif de notre étude est de réaliser une <b>analyse des données récoltées par des compteurs vélos</b> déployés par la mairie dans la ville de Paris afin de visualiser les horaires et les principales zones d’affluence.

Le jeu de données est constitué de <u>771 788 lignes et de 9 variables</u>: <em>Identifiant du compteur, Nom du compteur, Identifiant du site de comptage, Nom du site de comptage, Comptage horaire, Date et heure de comptage, Date d'installation du site de comptage, Lien vers la photo du site de comptage</em> et <em>Coordonnées géographiques</em>.

|    | Identifiant du compteur   | Nom du compteur                   |   Identifiant du site de comptage | Nom du site de comptage           |   Comptage horaire | Date et heure de comptage   | Date d'installation du site de comptage   | Lien vers photo du site de comptage                           | Coordonnées géographiques   |
|---:|:--------------------------|:----------------------------------|----------------------------------:|:----------------------------------|-------------------:|:----------------------------|:------------------------------------------|:--------------------------------------------------------------|:----------------------------|
|  0 | 100003096-SC              | 97 avenue Denfert Rochereau SO-NE |                       1.00003e+08 | 97 avenue Denfert Rochereau SO-NE |                  0 | 2019-09-01T06:00:00+02:00   | 2012-02-22                                | https://www.eco-visio.net/Photos/100003096/15765766519670.jpg | 48.83511,2.33338            |
|  1 | 100003096-SC              | 97 avenue Denfert Rochereau SO-NE |                       1.00003e+08 | 97 avenue Denfert Rochereau SO-NE |                  0 | 2019-09-01T03:00:00+02:00   | 2012-02-22                                | https://www.eco-visio.net/Photos/100003096/15765766519670.jpg | 48.83511,2.33338            |
|  2 | 100003096-SC              | 97 avenue Denfert Rochereau SO-NE |                       1.00003e+08 | 97 avenue Denfert Rochereau SO-NE |                  0 | 2019-09-01T04:00:00+02:00   | 2012-02-22                                | https://www.eco-visio.net/Photos/100003096/15765766519670.jpg | 48.83511,2.33338            |
|  3 | 100003096-SC              | 97 avenue Denfert Rochereau SO-NE |                       1.00003e+08 | 97 avenue Denfert Rochereau SO-NE |                 16 | 2019-09-01T09:00:00+02:00   | 2012-02-22                                | https://www.eco-visio.net/Photos/100003096/15765766519670.jpg | 48.83511,2.33338            |
|  4 | 100003096-SC              | 97 avenue Denfert Rochereau SO-NE |                       1.00003e+08 | 97 avenue Denfert Rochereau SO-NE |                  2 | 2019-09-01T05:00:00+02:00   | 2012-02-22                                | https://www.eco-visio.net/Photos/100003096/15765766519670.jpg | 48.83511,2.33338            |


Les variables qui serviront principalement à mener à bien notre analyse sont le <em>comptage horaire</em> (notre variable cible), la <em>date et heure du comptage</em> et les <em>coordonnées géographiques</em>.

Les données ont été récoltées de <b>septembre 2019 à septembre 2020</b>, et nous présente, pour chaque compteur, le nombre d'utilisateurs de vélibs qui sont passés devant ce compteur à chaque heure de cette année. 

Le prétraitement des données à été réalisé en plusieurs étapes à savoir:

 - Nous avons tout d'abord supprimé les valeurs manquantes grâce à la fonction dropna(). Nous avons opté pour la suppression des valeurs manquantes et non leur remplacement car elles ne correspondent qu’à 2% des données présentes dans notre jeu de données et ne possèdent donc pas de réel impact sur les résultats. Nous avons donc par la suite travaillé sur un jeu de données de 753 078 lignes.
 
 - Nous avons par la suite extrait l’heure, le jour de la semaine, le jour du mois, le mois et l’année de la variable <em>Date et heure de comptage</em> afin d'étudier la variation du comptage horaire en fonction de ces différentes variables.
 
 - Les jours étant automatiquement numérotés de 0 à 6, nous avons remplacé ces nombres par les jours de la semaine afin de permettre une interprétation plus facile des résultats.
 
 - Nous avons renommé la colonne <em>Comptage horaire</em> en <em>Comptage_horaire</em> pour faciliter le calcul du test statistique ANOVA
 
 - Enfin, nous avons extrait la longitude et la latitude des coordonnées géographiques afin de visualiser sur la carte de Paris présentée ci-dessous les zones où le comptage horaire a eu lieu.

### Emplacements géographiques des compteurs

![Image of Yaktocat](https://github.com/DataScientest/Bik_in_Paris/blob/main/carte_paris.png)

Cette carte géographique de la ville de Paris nous permet de déterminer les emplacements de chaque compteur mentionné dans notre jeu de données, ainsi que leur poids de comptage horaire représenté par la taille de chaque point. 

On constate que les compteurs comptabilisant le plus grand nombre d'utilisateurs de vélibs sont principalement ceux situés dans l’hypercentre autour de Châtelet, près des principales gares, en bord de Seine et autour du périphérique, notamment près des grandes Portes. 

<br/>
<br/>
Nous allons dans un premier temps présenter nos principales visualisations du Comptage horaire en fonction du temps afin d'en étudier les corrélations, puis dans un second temps procéder à des expérimentations de Machine Learning pour tenter de déterminer le modèle de prédiction le plus efficace.
