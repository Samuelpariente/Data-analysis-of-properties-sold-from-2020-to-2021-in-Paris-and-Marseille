# Data-analysis-of-properties-sold-from-2020-to-2022-in-Paris-and-Marseille-

Langage Python – Rapport Projet TD 9 et 10 ![](Aspose.Words.476ec148-4115-4cee-a66b-472225a57c1b.001.png)

*Par Pariente Samuel, Maurice Edouard, Ortega Marius ![](Aspose.Words.476ec148-4115-4cee-a66b-472225a57c1b.002.png)*

I-  Introduction 

Dans le cadre des TD 9 et 10 de Langage Python, notre objectif était d’analyser les données de valeurs foncières françaises des années 2020 et 2021 grâce à la bibliothèque Pandas. Au cours de notre analyse, nous avons été amenés à utiliser d’autres bibliothèques dont nous ferons mention plus tard dans le rapport. Pour vous présenter notre travail, nous parlerons ainsi de la structure du notebook Jupyter, de son contenu et des bibliothèques et sources de données tierces que nous avons utilisé pour le concevoir. Dans un second temps, nous détaillerons l’implémentation de notre application Django qui répertorie les résultats de notre travail sous forme d’un site.  

II-  Structure du Notebook Jupyter 

Au début de notre travail, nous avons réalisé que la base de données des demandes de valeurs foncières de 2021 contenait plusieurs valeurs nulles ou inutilisables. En effet, quand on regarde les 5 premières valeurs et les 5 dernières on remarque déjà que des colonnes ne sont remplit que de valeurs nulles. On a commencé par supprimer les colonnes avec beaucoup de valeurs nulles et qui ne nous intéressent pas pour notre étude. Il s’agissait de Code type local, No disposition, Type de voie, No voie, Nombre pièce principales, No plan, Code postal, voie et nombre de lots. Pour s’assurer qu’il n’y a pas de colonnes avec trop de valeurs nulles, nous avons utilisé algorithme qui supprime automatiquement les lignes avec plus de la moitié des valeurs égales à nulle.  

Enfin débarrassé des colonnes avec trop de valeurs nulles ou inutiles pour notre étude, nous avons remarqué un autre problème. Certaines valeurs ne sont pas du bon type. Par exemple, Valeur Foncière est composé de données chiffrées, mais elles sont toutes de type string. On convertit donc ces valeurs. Pour ne pas fausser l’espérance et la variance de la colonne Valeur Foncière, nous avons décidé de les remplacé par la moyenne des valeurs de cette colonne. Cela nous évite d’avoir des données nulles qui perturberont les graphiques. Cependant, nous observons qu’il n’y a pas que Valeur foncière qui a ces valeurs nulles pouvant fausser nos graphiques. Deux autres colonnes ont ce même problème. Pour chacune, on utilise une méthode différente pour nettoyer ses données. Dans le cas de Nature culture, on remplace les nulles par une valeur pour les identifier. Dans le cas de Sélection, la colonne regroupe des données qualitatives. On ne peut donc pas remplacer ses nulles par une moyenne. On les remplace alors par des valeurs aléatoires choisis dans son jeu de donnés ce qui permet de ne pas modifier le comportement global du set de données. 

Enfin, on modifie le format des dates de « jj-mm-aaaa » en « mm-jj-aaaa » puisque les librairies dont nous avons fait usage utilisent ce second format.  

A l’issue de ces traitements, nous avons une base de données nettoyée et utilisable. 

Après cette étape, nous organisons notre analyse en plusieurs catégories. Elles sont structurées dans un sens logique pour aller de l’analyse la plus générale (France entière) au cas le plus précis (Communes et départements). Premièrement, nous visualisons des graphiques expliquant la situation sur le territoire français dans sa globalité. Ce sont des analyses à l’échelle nationale qui se veulent le plus général possible. Elles servent surtout d’introduction et de remise en contexte. Ensuite, nous affichons quelques graphiques par région en prenant en compte certaines communes aux données importantes. Après cela, nous réalisons une étude comparative entre les départements. Elle nous permet de visualiser la situation immobilière de chacun des départements tout en la comparant avec le reste de la France. Après cela, nous réalisons une étude approfondie de deux villes françaises. Il s’agit de Paris et de Marseille. Dans les deux cas, nous commençons par une étude générale de la ville, pour avancer vers une comparaison entre arrondissements. Enfin, nous concluons en faisant une comparaison avec les données de 2020 sur l’échelle nationale, départementale, mais aussi sur les valeurs foncières des arrondissements parisien entre 2020 et 2021.  

III-  Structure de l’application Django 

Notre projet Django est composé de 7 applications ayant chacune des thématiques. Nous les répertorions dans le tableau suivant : 



|Nom de l’application |Path |Fonction dans le projet |
| - | - | - |
|graphiqueLib |graph/ |Page d’accueil de notre site. On peut accéder aux différentes applications depuis celle-ci.  |
|all2021 |all2021/ |Page répertoriant nos résultats sur des données de la France entière en 2021. |
|comp2020 |comp2020/ |Page répertoriant les comparaisons entre les données de 2020 et celles de 2021. |
|mapParis |mapParis/ |Page contenant une carte dynamique de paris agrémentée d’informations. |
|marseille |marseille/ |Page répertoriant nos résultats sur des données de Marseille en 2021. |
|paris |paris/ |Page depuis laquelle sont accessible les deux applications en rapport avec Paris. Soit ‘parisOthers’ et ‘mapParis’. |
|parisOthers |parisOthers/ |Page répertoriant nos résultats sur des données de Paris en 2021 excepté la carte dynamique mentionnée plus haut. |
***Note importante :  ![](Aspose.Words.476ec148-4115-4cee-a66b-472225a57c1b.003.png)***

Afin de lancer notre site, vous devez taper l’adresse suivante dans votre moteur de rechercher : 

[http://localhost:8000/graph/ ](http://localhost:8000/graph/)

Dans l’optique de mieux se représenter la structure visible côté utilisateur, nous vous proposons ci- après un diagramme résumant quelles pages sous accessible à partir d’une autre : 

![](Aspose.Words.476ec148-4115-4cee-a66b-472225a57c1b.004.jpeg)

IV-  Conclusion 

En conclusion, nous tenions à vous présenter les différents problèmes auxquels nous avons fait face et la répartition du travail au sein de l’équipe. 

Au cours de notre projet, nous avons fait face à deux problématiques majeures : 

- La taille de la base de données : 

En effet, le volume de données étant plus que conséquent, avec plus de 3 millions de lignes de données. Nous avons été confrontés à une impossibilité. En effet, utiliser des boucles de afin de traverser la base de données provoquait des temps de calculs bien trop élevés. Toute fois nous avons pu surmonter ce problème en nettoyant la base de données ainsi qu’en utilisant les fonctions optimisées préexistantes dans pandas. 

- L’utilisation de Django : 

Dans un second temps Django fut un défi car cela impliquait de comprendre en un laps de temps très réduit un nouveau Framework relativement complexe. Toutefois, nous avons réussi à fournir un site entièrement fonctionnel avec l’aide des tutoriels en ligne et sur dvo. 

Pour finir nous estimons la répartition du travail dans le tableau suivant : 



||X ||Samuel Pariente |Marius Ortega |Edouard Maurice |
| :- | - | :- | - | - | - |
||Pourcentage de participation ||33 % |33% |33% |

