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
- Classe *Program*
- Method *Main*
- Classe *Console*

Le DotNet est organisé en Solution (.sln) contenant plusieurs projets. On va considérer qu'une application sera une solution.
- NameSpace = Package (java)
- Visbilité : private/public/protected/internal valable uniquement pour le projet.
- .WriteLine = println.
    ``` csharp
    cw tab tab
    ```

Utilisation de la flèche pleine : lancement w/ début, flèche vide w/o débug.
En DotNet, on peut définit des modes de complilation différents. Le mode realease (vs. debug) ne permet pas de débugger.

### Bases du C#
PascalCase pour les fichiers.

Les getters et setters sont auto-implémentés
``` csharp
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
``` csharp
Personne personne = new Personne {Nom = "MARTIN", Prenom = "JEAN"};
```

Création de classe : se placer sur le projet/ajouter/classe



