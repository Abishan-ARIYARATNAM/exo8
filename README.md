Lecture d’un fichier texte structuré
Contexte
Environnement de travail
Lecture “naïve” des données
Objectifs
Informations complémentaires
Doctests
Lecture structurée des données
Objectifs
Informations complémentaires
Doctests
Applications
Contexte
Un fichier texte est constitué de caractères imprimables (lettres, chiffres, ponctuation, caractères spéciaux, ...), c’est à dire représentés graphiquement par un glyphe. Par opposition, un fichier binaire est un fichier qui n’est pas interprétable directement sous forme de texte : une image, un son ou encore un autre fichier compressé.

Environnement de travail
Pour cet exercice, vous devez utiliser en priorité le fichier squelette ex08-meteo.py. IMPORTANT : Enregistrez le avec Right Click + Save Link As... pour conserver l’encodage.

Selon la convention de structuration des modules, ce fichier sera structuré en quatre parties :

Imports et définition des variables globales ;
Définition des fonctions secondaires ;
Définition de la fonction principale ;
Appel protégé de la fonction principale.
Les données utilisées pour cet exercice sont extraites de données publiques fournies par Météo France.

Elles sont stockées dans le fichier ex08-meteo-data-jan-2014.csv. Le fichier est encodé en utf8. IMPORTANT : Enregistrez le avec Right Click + Save Link As... pour conserver l’encodage.

Lecture “naïve” des données
Objectifs
L’objectif est d’écrire une fonction read_meteo_data() :

qui prend en argument un nom de fichier ;
et retourne son contenu sous la forme d’une liste de n chaines de caractères si le fichier comporte n lignes.
Vérifier le bon fonctionnement de la fonction en effectuant un appel depuis main() et en affichant la valeur de retour (les doctests de la fonction donnent des exemples d’appel et les valeurs de retour correspondantes).

Informations complémentaires
On parle ici de lecture “naïve” car on ne tire pas avantage de la structure des données contenues dans le fichier pour lequel:

la première ligne contient les 6 champs utilisés pour structurer les données :

le nom de la station ;
l’heure ;
le jour ;
le mois ;
l’année ;
la température exprimée en degrés Celsius.
les autres lignes du fichier contiennent les données proprement dites, séparées par des ;.

Ces informations devront être prises en compte “manuellement”.

Utiliser la construction with pour ouvrir ce fichier. Penser à préciser le mode d’ouverture (lecture ou écriture ?) et l’encodage ;

Compte tenu de la nature de l’objet à retourner, quelle est la méthode à utiliser ? read(), readline() ou readlines() ?

Doctests
Une fois la fonction opérationnelle pour quelques arguments, ET SEULEMENT DANS CE CAS, lancer les doctests dans un terminal.

$ python -m doctest ex08_meteo.py -v
La totalité des doctests doivent réussir.

Lecture structurée des données
Objectifs
Ecrire une fonction read_csv_meteo_data() :

qui prend en argument un nom de fichier ;
et retourne son contenu sous la forme d’une liste de n listes de m chaines de caractères si le fichier comporte n lignes de m données.
Vérifier le bon fonctionnement de la fonction en effectuant un appel depuis main() et en affichant la valeur de retour (les doctests de la fonction donnent des exemples d’appel et les valeurs de retour correspondantes).

Comparer le code des fonctions read_meteo_data() et read_csv_meteo_data(). Lequel vous paraît le plus concis ?

Informations complémentaires
Un fichier texte peut être structuré selon une convention qui facilite la lecture des données qu’il contient. Le format csv (Comma Separated Values) est très utilisé :

la version anglo saxonne utilise la virgule , comme délimiteur ;
en français, la virgule , est utilisée comme séparateur décimal et le délimiteur employé est le point virgule ;.
Le fichier meteo-jan-2014.csv est au format csv. On peut tirer partie de cette structuration pour améliorer un peu la lecture des données en retournant une structure plus simple à manipuler que celle obtenue dans l’exercice précédent. Pour cela, Python utilise le module csv.

Ne pas oublier d’importer le module csv qui n’est pas chargé au démarrage.

L’ouverture du fichier est identique à la version “naïve”.

Lors de l’utilisation de la fonction csv.reader(), penser à préciser le delimiter.

D’après la documentation de cette fonction, quel est l’objet retourné à la lecture de chaque ligne ?

D’après la consigne quel est le type de l’objet que doit retourner read_csv_meteo_data() ?

Doctests
Une fois la fonction opérationnelle pour quelques arguments, ET SEULEMENT DANS CE CAS, lancer les doctests dans un terminal.

$ python -m doctest ex08_meteo.py -v
La totalité des doctests doivent réussir.

Applications
L’objectif est d’écrire une fonction get_meteo_data_by_day() :

qui prend en argument les données lues par read_csv_meteo_data(), un nom de station et une date au format dd:mm:aaaa ;
et retourne la liste des températures pour la date et la station concernée.
Si les paramètres d’appel ne correspondent pas à des données présentes dans le fichier, la fonction doit retourner la liste vide. Le nom de la station passé en argument doit être insensible à la casse (minuscules/majuscules).

Au vu des données contenues dans meteo-jan-2014.csv, quelle est la taille de la liste attendue ?

Quelques indices :

la liste retournée par read_csv_meteo_data() ne contient elle que des données ?
la première idée est de rechercher la ligne du fichier qui correspond aux critères de recherche. N’est-il pas plus pratique d’écarter les lignes qui ne correspondent pas ?