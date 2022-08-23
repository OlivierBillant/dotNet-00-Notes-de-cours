# DotNet

Remarques introductives : le cours ENI et très en retard sur la réalité du terrain et ce qui vous sera présenté diffèrera sensiblement du contenu des supports.

Le cours sera présenté avec les anciennes syntaxes, mais les TP seront actualisé.

Langage encore "OOP" que java. Présenté comme étant plus concis que le java dont il est (officieusement) forké. Date de 2001, et windows only jusqu'en 2017 (<= version 4.8) où il est passé open source et est devenu multiplateforme (>= 5).
Permettra de faire de bas niveau car permet de faire du C nativement.

Une relase majeure annuelle et toute les versions paires seront LTS.

dotNet est un "écosystème" permettant d'utiliser plusieurs langages (C#, vb.NET). Le FW web ASP.NET était utilisé jusque dans les années 2010. On utilise depuis ASP.CORE. La mobilité sera gérée via Xamarin. N.B. Xamarin est remplacé par MAUI qui restent très proche (syntaxe identique, philisphie similaire...), les différences sont essentiellement techniques.

## Installation de Visual Studio Community 2022.

Nombreux modules disponibles. Liste des modules à installer :

- Dev Web avec ASP.NET

## Introduction

Les fichers C# se terminent par :

```
file-name.cs
```

La doc est la msdn.
La compilation en C# diffère un peu du java. La compilation se fera en IL : intermediate langage, proche de l'Assembler qui sera interprété par la machine. La compilation est ainsi un peu plus longue mais gagnera lors de l'éxécution.

Plusieurs artéfacts seront générés :

- .exe/.dmg
- .dll : library

### Premier projet

Une **application console** sera composée de :

- Classe _Program_
- Method _Main_
- Classe _Console_

Le DotNet est organisé en Solution (.sln) contenant plusieurs projets. On va considérer qu'une application sera une solution.

- NameSpace = Package (java)
- Visbilité : private/public/protected/internal valable uniquement pour le projet.
- .WriteLine = println.
  ```csharp
  cw tab tab
  ```

Utilisation de la flèche pleine : lancement w/ début, flèche vide w/o débug.
En DotNet, on peut définit des modes de complilation différents. Le mode realease (vs. debug) ne permet pas de débugger.

### <ins>Bases du C#</ins>

PascalCase pour les fichiers.

Les getters et setters sont auto-implémentés

```csharp
public string nom {
    get {return nom;}
    set {nom = value;}
    }
```

Les constructeurs seront utilisés pour toutes les classes. Un vide sera défini par défaut et sera remplacé dès lors que l'on en définira un.

```
int et string sont des classes.
```

Exemple d'instanciation :

```csharp
Personne personne = new Personne {Nom = "MARTIN", Prenom = "JEAN"};
```

Création de classe : se placer sur le projet/ajouter/classe

Raccourcis : prop tab tab / propg

Par défaut toutes les classes créees ont une valeur nulle.

En DotNet, les classes sont passées par références. Toutefois les structures seront par défaut non-nullable et tout peut-être rendu nullable par le "?".

<br>

#### Héritage et Interface

Pas d'héritage multiple.
L'héritage comme l'implémentation d'interface passera pas ":"

```csharp
public abstract class Peluche : Jouet
```

Pour ouvrir une classe à la modification, il faudra l'overrider.

La convention veut qu'une interface commence par un **i majuscule**.

Pas de convention sur les classes abstraites. Peuvent être notées A, mais rien de consensuel.

Mot clef **base** remplace **super** pour appeler les méthodes ou attributs parents.

<br>

#### Types génériques

Type pouvant exploiter une autre type. En java, les types génériques ne sont valables que jusqu'à la compilation.

```csharp
public class Generique<T>
{
    private T attribut;

    public void Methode(TParametre)
    {
        TVariable
    }
}
```

On peut forcer une contrainte sur le type du générique en utilisant

```csharp
internal interface IAnimal<T> where T : INourriture
```

<br>

#### Les collections : List

On utilisera essentiellement la List. Permettra toutes les modifications dynamiques.

Les HashSet empêchent la duplication d'éléments.
Les dictionnaires seront un ensemble de clef/valeur

<br>

#### Les records

Sont en lecture seules et sont concus pour faciliter le transfèrt de données.

<br>

#### Methodes d'extension

Méthodes statiques permettant d'ajouter des comportements à une classe existante.
Sont notées par une petite flèche vers le bas sur le cube dans la liste des méthodes.  
Le **this** est la caractéristique de ces méthodes.

```csharp
public static class Extension
{
    public static int Add(this int a, int b)
    {
        return a + b;
    }
}
```

<br>

#### Les fonctions : Func

Toute méthode en DotNet doit commencer par une majuscule.

<br>

#### Les actions : Action

Similaires aux fonctions, ne retournent rien.

Dans les deux cas : prennent jusqu'à 16 paramètres max.

On peut overrider les opérateurs mathématiques et ceux de cast. Cela permettra par exemple d'additionner deux classes entre elles avec un "+".

<br>

#### Interpolation de chaine

```csharp
 $"Rectangle de longueur {Longueur} et de largeur {Largeur}\n Aire : {Aire()} \n Perimetre {Perimetre()}\n";
```

<br>

#### Line Break

On peut utiliser Environment.NewLine en lieu et place de \n afin d'adapter le retour chariot à l'OS de destination.

<br>

### <ins> LINQ - Streams </ins>

**L**anguage **IN**tegrated **Q**uery
Ensemble d'outils pour traiter et manipuler des collections.

Deux syntaxes possibles :

- requête (proche SQL)
- méthode (lambda)

Méthodes permettant de récupérer des éléments :

- First et FirstOrDefault
- Where : equivalent de Filter en stream va filtrer sur une condition
- Distinct
- Skip/Take : utilisés pour la pagination de tableau (ex. dans une lsite de 10 éléments, chaque page faisant 2 élements, pour accéder à la page 2 on skip 2 éléments et on take les deux suivants)
- Select : selectionner un attribut d'une liste. Va transformer une liste de personne en liste d'int si on select sur l'age par exemple. - SelectMany : permet d'applatir une sous-liste
  -GroupBy : renvoi une liste groupée par une clef.

Méthodes permettant de trier des éléments :

- OrderBy
- Vérifier des conditions All et Any
- Transformaer une collection : select et selectMany
- Count

La plutpart des méthodes LINQ renvoient des enumérables et seront donc largement chainable pour faire des requêtes plus poussées. Les méthodes **Then** et **ThenBy** vont faciliter ces enchainements. Plus exactement, c'est un Iterator qui est retournée et qui est un objet qui **va servir** à itérer.

```
Autrement dit, la requête ne sera "construite" que lorsqu'elle est utilisée par la suite (e.g. dans un foreach).
```

N.B. Toutes ces méthodes reposent sur des boubles qui vont parcourir les listes et seront donc d'autant plus lourdes que la liste sera longue.

**Tuple** : datastruct non définie permettant de passer un ensemble de données sans avoir à créer une classe. Beaucoup utilisé pour les retours de méthodes.

<br>

## Développement Web en ASP.NET

### Structure du projet Web
On retrouvera les désormais classiques :
- Models
- Views
- Controllers

Auquel s'ajoutent : 
- Content : ressources
- Program.cs : classe de démarrage
- Web.config : le serveur est désormais embarqué dans le fw (similaire spring)

```
N.B. Tous les projets écrits en dotNet s'exécuteront nativement.
```

