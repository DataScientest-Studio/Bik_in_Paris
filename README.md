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

![carte_paris](https://github.com/DataScientest/Bik_in_Paris/blob/main/carte_paris.png)

Cette carte géographique de la ville de Paris nous permet de déterminer les emplacements de chaque compteur mentionné dans notre jeu de données, ainsi que leur poids de comptage horaire représenté par la taille de chaque point. 

On constate que les compteurs comptabilisant le plus grand nombre d'utilisateurs de vélibs sont principalement ceux situés dans l’hypercentre autour de Châtelet, près des principales gares, en bord de Seine et autour du périphérique, notamment près des grandes Portes. 

<br/>
<br/>
Nous allons dans un premier temps présenter nos principales visualisations du Comptage horaire en fonction du temps afin d'en étudier les corrélations, puis dans un second temps procéder à des expérimentations de Machine Learning pour tenter de déterminer le modèle de prédiction le plus efficace.

## DATA VISUALISATION ET ANALYSES STATISTIQUES

### Visualisation du comptage horaire selon le mois

#### Visualisation du comptage horaire par mois grâce à un barplot


![comptage_mois2](https://github.com/DataScientest/Bik_in_Paris/blob/main/comptage_mois2.png)

Cette première visualisation nous permet de constater que les mois de juin, juillet et septembre sont ceux qui connaissent le plus grand nombre de comptage horaire avec un moyenne située autour de 80: nous pouvons le justifier par le fait que les utilisateurs font davantage de vélo en été puisque le beau temps le permet, alors que la baisse du mois d'août s'explique plutôt par les départs en vacances. 

Mars, avril et novembre connaissent au contraire le plus petit nombre d’utilisateurs de vélibs, avec des moyennes de comptage horaire s'élevant respectivement à 30, 10 et 35. Concernant les mois de mars et d'avril, cela s’explique par la <u>crise sanitaire dû au Covid-19 et au confinement</u> qui a eu lieu. Quant au mois de novembre, cela s'explique plus simplement par la baisse de température qui désincite les utilisateurs à se déplacer en vélo.

Nous constatons également une forte affluence inhabituelle pendant les mois de décembre et de janvier, malgré la baisse des températures, qui aurait donc logiquement provoqué une baisse de l’affluence des vélibs. Il s'agit en réalité de la période de <u>grève illimitée SNCF</u> qui a débuté le 5 décembre 2019 et qui a obligé les Parisiens à utiliser d'autres modes de transport dont les vélibs.

#### Visualisation du comptage horaire d'un compteur en fonction de la date

Dans cette section, nous avons sélectionné un compteur situé en zone de forte affluence, au "89 boulevard de Magenta NO-SE".

Nous analysons alors l’affluence sur trois lundis de périodes différentes :
 - Le <u>lundi 9 décembre 2019</u> : lors des grèves SNCF 
 - Le <u>lundi 18 novembre 2019</u> : journée classique
 - Le <u>lundi 23 mars 2020</u> : lors du début du confinement

![comptage_9dec2](https://github.com/DataScientest/Bik_in_Paris/blob/main/comptage_9dec2.png) 
On constate que le comptage horaire de cette journée de début de grève SNCF est très élevé, dépassant 500 comptages par heure en heure de pointe, contre une moyenne habituelle de 135 pour les mêmes horaires. 
![comptage_18nov](https://github.com/DataScientest/Bik_in_Paris/blob/main/comptage_18nov.png)
Lors de ce lundi classique de travail, durant un mois de novembre où l’utilisation mensuelle est dans la moyenne, on constate que l’utilisation du compteur se situe autour de 300 en heure de pointe et autour de 100 durant le reste de la journée.
![comptage_23mars2](https://github.com/DataScientest/Bik_in_Paris/blob/main/comptage_23mars2.png) 
Notre dernier jour sélectionné est le premier lundi du confinement suite au Covid-19. On constate alors une très faible utilisation de vélos, sans différence notable entre les heures creuses et heures de pointe. L’utilisation moyenne du compteur se situe autour de 50.

#### Etude de la corrélation entre le comptage horaire et le mois par le test ANOVA


|          |     df |      sum_sq |        mean_sq |      F |   PR(>F) |
|:---------|-------:|------------:|---------------:|-------:|---------:|
| mois     |      1 | 3.45443e+07 |    3.45443e+07 | 4688.8 |        0 |
| Residual | 753076 | 5.54821e+09 | 7367.4         |  nan   |      nan |


La p-value (PR(>F)) est nulle, ce qui confirme que les mois ont un impact significatif sur la pratique du vélo.

Nous pouvons alors conclure de ces premières visualisations ainsi que de notre test ANOVA que l'utilisation des vélibs varie fortement selon la saison et les évènements (grève, confinement, vacances...) survenant dans la ville de Paris. 

### Visualisation du comptage horaire selon le jour de la semaine


![comptage_semaine1](https://github.com/DataScientest/Bik_in_Paris/blob/main/comptage_semaine1.png)

On constate que les vélos sont utilisés de manière homogène chaque jour de la semaine avec une moyenne de comptage horaire qui se situe autour de 60. 

Le comptage horaire nous permet également de conclure que les vélibs sont moins utilisés les week-ends. En effet, le comptage horaire moyen le samedi s'élève à 40 environ et à près de 50 pour le dimanche. 

Cette différence entre la semaine et le week-end nous amène à l'hypothèse que l'utilisation des vélibs varie en fonction des activités professionnelles et scolaires des habitants de la ville.


#### Etude de la corrélation entre le comptage horaire et le jour par le test ANOVA

|          |     df |      sum_sq |        mean_sq |       F |   PR(>F) |
|:---------|-------:|------------:|---------------:|--------:|---------:|
| jour     |      6 | 6.87764e+07 |    1.14627e+07 | 1565.52 |        0 |
| Residual | 753071 | 5.51398e+09 | 7322           |  nan    |      nan |

La p-value (PR(>F)) est nulle, cela confirme que le jour de la semaine a un effet statistique significatif sur le comptage horaire.

Ainsi, nous pouvons conclure de cette deuxième analyse ainsi que du test de corrélation ANOVA que l'utilisation des vélibs varie également en fonction de la période de la semaine. Les utilisateurs de vélibs semblent davantage utiliser les vélibs lors des journées de travail plutôt que pour leur loisirs en week-end.



### Visualisation du comptage horaire selon l’heure de la journée

#### Visualisation du comptage horaire moyen selon l’heure de la journée

![comptage_heure](https://github.com/DataScientest/Bik_in_Paris/blob/main/comptage_heure.png)

On constate que les vélos sont utilisés majoritairement durant les heures de pointe, c’est à dire de 8h à 10h ainsi que de 18h à 20h.
Une moyenne de 110 utilisateurs par heure sont comptabilisés entre 8h et 10h et une moyenne de 135 utilisateurs entre 18h et 20h.

Le reste de la journée indique une moyenne relativement stable et située autour de 70 comptages par heure alors que le graphique affiche sans surprise une baisse progressive par heure du nombre d'utilisateurs à partir de 20h et jusqu'au lendemain matin.

#### Visualisation du comptage horaire de chaque jour de la semaine

![comptage_heure_barplot4](https://github.com/DataScientest/Bik_in_Paris/blob/main/comptage_heure_barplot4.png) 

Cette visualisation nous permet d'avoir une vision des moyennes de comptage horaire de chaque journée de la semaine et du week-end. 

On constate ainsi que les conclusions tirées grâce au graphique précédent sont dûes au jour de semaine uniquement, puisque les samedi et dimanche suivent une variation différente car ne connaissant pas de pic lors des heures de pointe. Cependant cette visualisation n'étant pas des plus lisibles, nous présentons également ci-dessous une visualisation représentant un graphique par jour de semaine.

#### Visualisation du comptage horaire pour chaque jour de la semaine et selon l'heure
<br/>

![comptage_heure_par_jour7](https://github.com/DataScientest/Bik_in_Paris/blob/main/comptage_heure_par_jour7.png) 

Ce graphique, qui présente chaque jour de semaine dans l'ordre, nous permet d'avoir une vision du comptage horaire par jour, et ainsi de mieux de nous rendre compte de la différence notable de variation entre la semaine et le week-end. 

Nous constatons encore une fois une très forte utilisation des vélos de 8h à 10h et de 18h à 20h uniquement du lundi au vendredi, pouvant aller jusqu'à 1200 passages d'utilisateurs de vélibs par heure sur ces horaires pour certains compteurs. Durant les autres plages horaires de la semaine, le comptage horaire semble uniforme.

En week-end, le comptage horaire semble également uniforme entre le samedi et le dimanche. On observe une hausse progressive du nombre de passages de vélib jusqu'à atteindre en moyenne 700 passages autour de 18h avant de connaître une baisse progressive jusquau lendemain. 

Le comptage horaire varie donc de manière nettement différente entre la semaine et le week-end.


#### Etude de la corrélation entre le comptage horaire et l’heure par le test ANOVA

|          |     df |      sum_sq |        mean_sq |       F |   PR(>F) |
|:---------|-------:|------------:|---------------:|--------:|---------:|
| C(heure) |     23 | 1.24848e+09 |    5.42816e+07 | 9431.09 |        0 |
| Residual | 753054 | 4.33428e+09 | 5755.6         |  nan    |      nan |

La p-value (PR(>F)) est nulle, cela confirme que l'heure a un effet statistique significatif sur le comptage horaire.

Ainsi, nous pouvons tirer de ces visualisations de comptage horaire ainsi que du test ANOVA la conclusion que la période de la journée enraîne une variation notable sur l'utilisation de vélibs, puisqu'on parvient à nettement différencier les heures de départ et de retour du lieu de travail ainsi que les périodes plus calmes telles que la nuit.

## Conclusion sur ces visualisations
<br/>

Notre étude nous invite à utiliser les variables heure, jour et mois qui ont toutes trois un effet statistique très prononcé sur le comptage horaire pour anticiper les demandes des utilisateurs. La régularité du comptage horaire (renseigné toutes les heures sur le jeu de données) ainsi que la précision du lieu où se trouve chaque compteur nous permettent de livrer une analyse avec une certaine précision mais comportant toutefois des limites.

En effet, les compteurs étant situés à des emplacements précis et ne couvrant pas la totalité de la capitale comme nous pouvons le constater sur notre carte d'introduction, cela ne nous permet pas de conclure sur les zones de forte ou de faible affluence.
Aussi, l’exploitation de la variable mois peut s’avérer limitée pour visualiser le comportement du comptage horaire car les données ne représentent qu’une seule année. 

Un autre aspect important de cette analyse est la <b>présence de biais:</b> notamment la grève de transport et le confinement dû au Covid-19 qui, étant des évènements inhabituels, ne permettent pas de généraliser notre analyse sur les années suivantes.

<br/>

# MODELISATION PAR MACHINE LEARNING
## Introduction au Machine Learning
<br />
<br />
Nous allons à présent procéder à des expérimentations de Machine Learning: anticiper le comptage horaire pour un jour et une heure de la semaine. 
Nous devrons ici utiliser des <b>méthodes de Régression</b> puisque nous avons uniquement des variables quantitatives à notre disposition. 

Pour mener à bien notre résolution de problème de Machine Learning, nous utilisons les variables listées ci-dessous:
 - <em>Identifiant du compteur</em>, pour garder l’identité des compteurs liés à chaque comptage horaire
 - <em>Comptage horaire</em>, qui est notre variable cible et qui nous sera donc essentielle pour la suite de notre analyse
 - <em>Date et heure de comptage</em> qui contient l’année, le mois, le jour et l’heure de chaque ligne de comptage horaire et qui nous sera d’une grande utilité pour préciser notre analyse

Nous mettons ainsi volontairement de côté les variables ci-dessous: 
 - <em>Nom du compteur, Identifiant du site de comptage</em> et <em>Nom du site de comptage</em> qui sont redondantes avec la variable gardée  <em>Identifiant du compteur</em>
 - <em>Date d’installation du site de comptage</em>, qui ne nous sert pas dans notre analyse
 - <em>Lien vers photo du site de comptage</em>, qui donne un lien URL et n’apporte donc aucune information utile pour la suite de notre analyse
 - <em>Cordonnées géographiques</em>, ne nous étant pas utile non plus pour résoudre notre problème de Machine Learning.

## Preprocessing de données

<br />
<br />
Avant de démarrer nos expérimentations, nous procédons au preprocessing de nos données.

Tout d’abord, nous commençons par <b>extraire le mois, le jour du mois, le jour de la semaine</b> (allant de 0 à 6 et représentant pour chaque journée, le jour de la semaine associé) ainsi que <b>l’heure</b> de notre variable <em>Date et heure de comptage</em>. 

Nous créons ensuite une boucle à l’aide des variables <em>Comptage horaire</em> et <em>Date et heure de comptage</em> afin d’extraire, pour chaque ligne de comptage horaire, le comptage des heures précédant cette dernière et enregistré sous chacune des variables <em>comptage_h-X</em>. La <b>fenêtre horaire</b> que l’on voudra observer sera défini par une variable fenêtre que l’on programmera successivement sur 3, 5 et 7 afin d’observer le modèle qui nous donne les résultats les plus pertinents.

Nous procédons par la suite à une nouvelle suppression des valeurs manquantes afin de ne pas freiner la suite de notre analyse.

En procédant à l’extraction de nos variables cibles et explicatives, nous sélectionnons donc en tant que variable cible le <b><em>comptage horaire</em></b> et en tant que variables explicatives, celles listées ci-dessous:

 - <em>Identifiant du compteur</em>
 - <em>Weekday, mois</em> et <em>heure</em>
 - Les variables <em>comptage_h-X</em>

Voici ci-dessous un extrait des variables que nous utilisons pour la suite de notre rapport, avec une fenêtre ajustée à 5:
<br />
<br />

|        | Identifiant du compteur   |   Comptage_horaire |   weekday |   mois |   heure |   comptage_h-1 |   comptage_h-2 |   comptage_h-3 |   comptage_h-4 |   comptage_h-5 |
|-------:|:--------------------------|-------------------:|----------:|-------:|--------:|---------------:|---------------:|---------------:|---------------:|---------------:|
| 131937 | 100042374-109042374       |                109 |         2 |      8 |      16 |             57 |             78 |            257 |              0 |             42 |
| 496725 | 100056041-SC              |                 53 |         0 |      8 |      13 |             88 |             29 |             11 |             55 |             25 |
| 471396 | 100056038-SC              |                 13 |         4 |      1 |      20 |            100 |             35 |             52 |            179 |             40 |
| 357255 | 100047548-104047548       |                  7 |         6 |      5 |       8 |             10 |             18 |             26 |             22 |             44 |
| 572754 | 100056326-103056326       |                  4 |         3 |      1 |      23 |              4 |             17 |              7 |              2 |              1 |
  
  
<br />
<br />
Nous avons enfin procédé au découpage de notre jeu de données en données d’entraînement et de test. Nous souhaitons ici utiliser comme données d’entraînement les données correspondants aux <b>21 premiers jours de chaque mois</b> (ou aux 3 premières semaines) et comme données de test, les données survenants après le 21ème jour de chaque mois. Nous utilisons cette méthode pour avoir des données d’entraînement et de test gardant une certaine cohérence temporelle, contrairement au train_test_split qui sélectionnerait des données de manière aléatoire et donc non pertinentes. 


## Exprérimentation Machine Learning
<br/>
<br/>
Nous avons sélectionné pour notre expérimentation trois méthodes de Machine Learning:

 - <b>La Régression linéaire</b>
 - <b>Le Gradient Boosting Regressor</b>
 - <b>Le Random Forest Regressor</b>


### Régression Linéaire
<br/>

Après avoir fait varier la fenêtre sur différentes valeurs à savoir 3, 5 et 7, le modèle a été instancié puis entraîné sur l'ensemble d'entraînement (X_train et y_train). Par la suite, a été déterminé respectivement : 
 - L’erreur moyenne absolue du jeu d’entraînement (MAE train)
 - L’erreur moyenne absolue du jeu de test (MAE test)
 - L’erreur relative du jeu de test (=MAE sur le jeu de test / comptage moyen)

Observons à présent les résultats pour chacune des fenêtres:


#### Fenêtre = 3

MAE train: 21.49480241855504   
MAE test: 20.391301560019645

Relative test error: 0.35931435011831153


#### Fenêtre = 5

MAE train: 21.405109067699964  
MAE test: 20.33467288956354

Relative test error: 0.3582412759011802


#### Fenêtre = 7

MAE train: 21.374116427049746  
MAE test: 20.31097360560857


Relative test error: 0.35781520803226163

<br/>

<u>Observations:</u> La Regression linéaire nous montre que les résultats entre les différentes fenêtres considérées sont presque égaux. Par ailleurs, ces résultats obtenus nous laissent penser que la performance du modèle ne varie pas selon les différentes valeurs que l'on attribue au comptage horaire des heures précédentes.

<br/>

### Gradient Boosting Regressor
<br/>

Tout comme pour la Régression linéaire, nous faisons varier la fenêtre sur 3, 5 puis 7. En suivant le même entraînement que précédemment et en instanciant cette fois le GradientBoostingRegressor, voici les résultats que nous obtenons:


#### Fenêtre = 3

GBR MAE train 15.102000435778786  
GBR MAE test 14.177302213047787

GBR Relative test error: 0.249817703696755

#### Fenêtre = 5

GBR MAE train 15.10200043577875  
GBR MAE test 14.177302213047744

GBR Relative test error: 0.24981770369675424

#### Fenêtre = 7

GBR MAE train 15.102000435778768  
GBR MAE test 14.177302213047767

GBR Relative test error: 0.24981770369675466

<br/>

<u>Observations:</u> Les résultats du Gradient Boosting Regressor sont meilleurs que ceux de la Regression Linéaire. La MAE train et la MAE test présentent un très faible écart, ce qui signifie a priori que l'apprentissage est bon. Par ailleurs, on ne constate aucune différence notable entre les fenêtres 3, 5 et 7, cela nous amène à la conclusion que la performance du modèle ne varie pas significativement selon la visibilité que l'on donne à l'algorithme pour chaque comptage horaire.

<br/>

### Random Forest Regressor
<br/>

Comme précédemment, afin de faire varier les résultats, nous faisons varier la fenêtre horaire destinée à ajuster les prédictions du modèle sur 3, 5 puis 7. 

<u>Pour chaque fenêtre:</u>

Après avoir instancié notre modèle, nous testons les <b>hyperparamètres</b> suivants:
 - n_estimators: [100,300,500], 
 - max_depth: [2,11,20],
 - min_samples_split: [2,50,100],
 - min_samples_leaf: [1,50,100]}

Par la suite nous utilisons la classe <b>GridsearchCV</b> pour sélectionner l’ensemble de paramètres ayant la meilleure performance moyenne sur l’ensemble des échantillons.

Après avoir sélectionné les paramètres les plus pertinents avec la fonction best_params_, nous les appliquons au modèle et observons la <b>MAE (Mean Absolute Error)</b> de ce modèle optimal avec:
 - L’erreur moyenne absolue du jeu d’entraînement
 - L’erreur moyenne absolue du jeu de test
 - L’erreur relative du jeu de test (=MAE sur le jeu de test / comptage moyen)

<br/>
Ce modèle s'avère être particulièrement long à exécuter. Notre fichier contenant 753 058 lignes après suppression des valeurs manquantes, nous avons calculé le temps nécessaire pour entraîner le modèle sans prendre en compte les paramètres: 451.52 secondes, soit <b>plus de 7 minutes</b>. 

Cela nous amènerait donc à <b>un temps de 50h pour entraîner ce modèle avec le GridSearchCV et donc en prenant en compte chacun des hyperparamètres que nous souhaitions tester</b>. Nous pouvons donc en conclure que Scikit Learn n'est pas le modèle adapté pour ce type de calcul.

<br/>

### Visualisation de notre meilleur modèle: Gradient Boosting Regressor
<br/>

Dans cette dernière partie, nous allons afficher une visualisation nous permettant d'observer l'efficacité du modèle nous ayant apporté les meileurs scores: le Gradient Boosting Regressor. 

Nous choisissons de faire apparaître une visualisation sur un compteur: "89 boulevard de Magenta NO-SE" et une date: le jeudi 28 novembre 2019, date non biaisée.

Nous ajustons ensuite notre fenêtre de comptage horaire sur 7, notre ajustage le plus large testé précédemment. Puis nous définissons à nouveau nos données d'entraînement contenant toutes les données de notre dataset mis à part celles que nous cherchons à prédire, et nos données de test correspondant à celles du compteur et de la date choisis. Après avoir entraîné notre modèle puis après avoir fait notre prédiction, nous obtenons la visualisation suivante:

![predictions3](https://github.com/DataScientest/Bik_in_Paris/blob/main/visu-predictions3.png) 

Cette visualisation nous permet d'observer que le modèle du Gradient Boosting Regressor nous donne des prédictions fiables lors des heures creuses mais ne permet pas de prédire avec précision le comptage horaire durant les heures de pointe. La différence entre le comptage horaire réel et les prédictions possède pour ces heures là une différence au moins égale à 50 comptages. Par ailleurs on observe également que les prédictions affichent en heure de pointe un résultat toujours inférieur au comptage réel. Cela est dû aux variations trop fortes du comptage horaire sur les heures de pointe entre chaque journée qui rend les prédictions moins fiables.

Nous ne pouvons donc pas conclure que ce modèle soit particulièrement performant en semaine étant donné les fortes variations qui adviennent chaque matin et soir. 

<br/>

Nous allons à présent visualiser les prédictions faites sur un jour de week-end afin de comparer nos résultats avec ceux du jour de semaine obtenus précédemment. En suivant le même procédé que celui développé plus haut, voici la visualisation obtenue:

![predictions](https://github.com/DataScientest/Bik_in_Paris/blob/main/visu-predictions-samedi.png)  

La tendance générale reste globalement semblable entre les prédictions et la réalité, mais nous ne pouvons pas pour autant conclure que la prédiction soit particulièrement fiable: les prédictions faites par le modèle présentent un écart souvent supérieur à 50 comptages durant la journée et pouvant aller jusqu'à plus de 150 comptages d'écartssur certaines heures.

Ainsi, nous pouvons conclure que malgré des prédictions parfois fidèles à la réalité, le modèle du Gradient Boosting Regressor n'est pas pour autant un modèle complètement fiable et ne parvient pas à donner une prédiction semblable au comptage horaire réel.

<br/>

## Conclusion sur le Machine Learning

<br/>

Nous pouvons conclure de nos expérimentations que le Gradient Boosting Regressor semble nous apporter de meilleurs résultats que la Régression Linéaire pour notre problème de Machine Learning. Pourtant, malgré ces résutats plus encourageants, la visualisation des prédictions faites grâce à ce modèle du Gradient Boosting Regressor en semaine nous montre ses limites: la prédiction faite est certes fiable sur les heures creuses mais beaucoup moins sur les heures de pointe. En week-end, les prédictions faites restent également peu fiables et montrent des disparités avec la réalité.

Aussi, nos changements de fenêtres entraînés sur 3, 5 puis 7 nous permettent de conclure que le modèle n'est pas plus ou moins performant selon la visibilité qu'on lui donne sur les comptages horaire des heures précédentes. 

Aussi, nous constatons que le GridSearchCV n'est pas une méthode efficace pour résoudre notre problème de Machine Learning sous Scikit Learn avec un fichier contenant un nombre important de données. Il serait donc préférable d'utiliser le framewok Pyspark pour entraîner ce modèle. 
