Voici le plan que j'ai proposé pour le projet : 



Projet : le design pattern Prototype
1. Introduction
Définition : le patron Prototype permet de créer de nouveaux objets en clonant un objet existant, sans dépendre de leur classe concrète.
Contexte : il est utile lorsque la création d'un objet est coûteuse, complexe ou exige une configuration initiale lourde.
Objectif : montrer comment le Prototype simplifie la duplication d'objets et améliore la flexibilité du code.
2. Problématique
Création lente ou complexe : certains objets demandent des initialisations lourdes, comme un accès à une base de données ou le chargement de ressources.
Couplage au type concret : le code client doit connaître la classe exacte pour instancier un objet.
Variantes nombreuses : on veut des objets proches, avec de petites différences (plannings, documents, configurations).
3. Principe du pattern
Clonage délégué à l'objet : chaque classe sait se copier elle-même via une méthode cloner().
Contrat commun : JavaScript n'a pas d'interface au sens strict. Une classe de base qui déclare cloner() joue ce rôle.
Copie maîtrisée par la classe : la méthode de clonage recrée l'objet et copie ses attributs, y compris les champs privés (#), puisqu'elle y a accès.
4. Structure
Prototype (classe de base) : déclare cloner().
PrototypeConcret : implémente le clonage, en copie superficielle ou profonde.
Client : demande la duplication sans connaître la classe concrète.
Registre de prototypes : stocke des modèles préconfigurés et fournit une copie à partir d'une clé.
5. Implémentation en JavaScript
Le projet est réalisé uniquement en JavaScript. On présente une seule implémentation, avec trois approches du clonage.
Approche 1 : classes concrètes avec clonage explicite
La classe de base Prototype déclare cloner().
Les classes concrètes héritent de Prototype et implémentent cloner() en copiant leurs attributs, y compris les structures imbriquées (tableaux, objets).
Démonstration : clonage d'une liste d'objets, puis vérification que les copies sont indépendantes des originaux.
Approche 2 : clonage générique avec structuredClone
cloner() s'appuie sur structuredClone pour copier l'objet en profondeur.
Limites à présenter : structuredClone ne conserve pas la classe (les méthodes sont perdues) et ne copie pas les fonctions.
Démonstration : comparaison avec l'approche 1, pour montrer pourquoi la copie doit rester sous le contrôle de la classe.
Approche 3 (cas avancé) : héritage prototypal natif
Object.create crée un objet qui délègue ses propriétés à un modèle.
Démonstration : la copie lit les propriétés du modèle tant qu'elle ne les redéfinit pas.
Point à signaler : la délégation est superficielle. Modifier un objet imbriqué du modèle modifie aussi les copies.
6. Cas d'usage
Plannings de travail : une semaine type clonée pour chaque semaine de l'année, puis adaptée (congés, remplacements).
Documents administratifs : une liasse vierge clonée pour chaque client.
Objets métier complexes : ordres financiers contenant un client, un compte et des parts.
7. Registre de prototypes
Stockage : modèles prédéfinis, par exemple « Semaine standard », « Période estivale » ou « Garde de nuit renforcée ».
Utilisation : le client récupère un clone à partir d'une clé.
Avantage : centralisation et réutilisation des configurations.
8. Avantages et inconvénients
Avantages
Découplage du code client par rapport aux classes concrètes.
Performance : évite des initialisations coûteuses.
Flexibilité : création rapide de variantes.
Inconvénients
Clonage profond complexe à implémenter correctement.
Références partagées difficiles à maîtriser.
Effort de mise en œuvre : chaque classe doit gérer son propre clonage.
9. Mini-projet : planification des gardes d'une caserne de pompiers (JavaScript)
Le problème réel : une caserne planifie des semaines entières de gardes. Chaque semaine suit un modèle type (mêmes postes, mêmes horaires, même répartition des équipes), mais doit être adaptée aux congés et aux remplacements. Recopier la structure à la main pour chaque semaine est long et source d'erreurs.
Fonctionnement du système
Un modèle de semaine type est créé une seule fois, avec ses jours, ses gardes et ses équipes.
Le système clone ce modèle pour chaque semaine, puis applique les modifications propres à chacune.
Un registre de prototypes stocke plusieurs modèles : « Semaine standard », « Période estivale », « Garde de nuit renforcée ».
Démonstration prévue
Clonage superficiel (le piège) : les équipes partagées entre les copies changent partout à la fois.
Clonage profond (la correction) : modifier une garde dans une semaine ne touche plus les autres.
Comparaison de performance : générer 52 semaines en reconstruisant chaque semaine, puis en clonant le modèle. Le benchmark doit être fiable, avec un nombre suffisant d'itérations et un chargement des effectifs simulé. Si l'écart est faible, prévoir une autre démonstration.
Attendus techniques couverts
Classe de base Prototype déclarant cloner(), héritée par la classe Semaine.
Plusieurs prototypes et un registre accessible par clé.
Clonage superficiel et clonage profond démontrés.
Cas d'usage métier : la caserne elle-même.
Précautions
Utiliser des données fictives (noms et identifiants inventés) pour la confidentialité.
Limiter le périmètre à deux ou trois écrans : modèles, planning de la semaine, comparaison.
10. Conclusion
Le Prototype est utile lorsque les objets sont coûteux ou complexes à créer et qu'ils se ressemblent beaucoup.
Il réduit le couplage avec les classes concrètes et améliore la réutilisation des configurations.
Il impose en revanche une gestion rigoureuse de la copie profonde, sous peine de partager involontairement des données.
Sources
Refactoring Guru, Prototype : https://refactoring.guru/fr/design-patterns/prototype
Refactoring Guru, Prototype en Java, exemple : https://refactoring.guru/fr/design-patterns/prototype/java/example
Wikibooks, Patrons de conception / Prototype : https://fr.wikibooks.org/wiki/Patrons_de_conception/Prototype
Éditions ENI, Le pattern Prototype : https://www.editions-eni.fr/livre/design-patterns-en-java-descriptions-et-solutions-illustrees-en-uml-2-et-java-5e-edition-les-23-modeles-de-conception-9782409037603/le-pattern-prototype
Invivoo, Prototype design pattern : https://invivoo.com/blog/prototype-design-patterns
Université de Lorraine (Telecom Nancy), Prototype pattern : https://gibson-pages.telecomnancy.univ-lorraine.fr/francois.charoy/complement/designpatterns/prototypepattern/
GeeksforGeeks, Prototype design pattern : https://www.geeksforgeeks.org/system-design/prototype-design-pattern/

