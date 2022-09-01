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

Les annotations de Java on leur équivalent en dotNet avec les **[ attributs ]** qui s'écrivent entre "[ ]".  

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

Par défault, le fw propose de créer les modalités d'authentification et d'activer Docker.

1. Creation d'un builder d'application web
2. Configuration app
3. Construction app
4. Run

DotNet fourni un système de pipeline et de middleware pour gérer l'avant et l'après exécution d'une requête.  

**Razor** : équivalent de Thymeleaf ou Twig.

#### Controller
ViewData (préférer celui ci) ou ViewBag permettent de transférer des données entre M-V en dehors des besoins liés à la page (*e.g.* liste externe).

On peut définir précisément une route pour chaque action pour prévoir par exemple des accès par id.

#### View et syntaxe Razor
Les fichiers cshtml fonctionneront comme une classe.  
Aussi les variables déclarées y resteront accessibles, des méthodes peuvent y être créees etc...  
Les @ de début de vue vont permettre de passer des atrtibuts, des usings...  
Le plus souvent on passera ainsi des listes d'objets en tant que models.  
```
Toutes les vues auront du model : 
    - déclaration : @ model.blabla
    - utilisation : @ Model.blabla
```

Le fw permet de créer automatiquement les controllers pour un objet/ViewModel qui proposera autmatiquement les actions d'affichage en GET et la partie POST pour modification et récupération des informations.

Les vues partielles permettent de mutualiser des éléments entre plusieurs vues. Il s'agit d'une vue non-soumise au layout et est forcément préfixée par un "_" et sont liées à une modèle.
``` csharp
@await this.Html.PartialASync.("_ClassName", this.Model) 
```

Validation : se fera avec des attributs.

Structuration des projets DotNet
Les différentes couches d'une solution seront séparées en projets.
Clic droit sur un projet et ajouter référence de projet.

Injection de dépendance : se fera **uniquement dans les controllers**
L'utilisation ne se fera pas en annotation avec  @Autiwired et @Services mais en utilsiant dans Program.cs :

``` csharp
builder.Services.AddTransient<NomDuService>();
builder.Services.AddSingleton<SingletonService>();
```

### Entity Framework
ORM : Object Relational Mapping permet la liaison entre les tables de données et les classes.

Différentes approches possibles : 
- Database First : si la db existe déjà. Permettra de générer les modèles à partir des données pré-existantes.
- Model First : déprécié
- Code First : Génération de la db à partir du code c# (80% des projets)

#### DbContext
Objet représentant notre base de donnée. Contiendra tous les champs, les relations et la définition de la chaine de connexion dans App.conf/Json.
Classe abstraite qui devra être héritée.

- DbSet : représente les données d'une table sous forme d'énumérable.
- Linq pour manipuler le slistes
- SaveChanges pour enregistrer les changements

<br>

1. Créer un projet
2. Ajouter les dépendances NuGet : 
    - MSEntityFrameworkCore
    - Provider spécifique de la base de donnée (SqlLite à mettre par défaut)
    - .Design pour le design sql des migrations
3. Création classe Context héritant de DbContext
4. Création d'entités (modèles de db)  
    Par défaut, EF prendra Id comme la PK.
    Gestion des nullable : expliciter la gestion des nullables de la façon suivante avec l'annotation "Required":
    ``` csharp
    [Required]
    public string Nom {get ; set}
    ```
5. Création d'un DbSet dans Context
    ``` csharp
    public DbSet<Personne> Personne => this.Set<Personne>();
    ```
    N.B. Le type Set disposera des méthodes LinQ (IEnum) et SaveChanges()
6. Dans Program.cs : création d'une instance de Context
7.  ``` csharp
    await context.Database.EnsureCreatedAsync();
    ```


#### Async Await
Par défaut, les codes sont synchrones. Dans le cas d'un traitement long, l'étape la plus longue conditionnera la longueur du programme. Il s'agira en général des appels aux services externes impliquant une certaine variabilité environnementale (réseau ,API etc...)

- Toutes les méthodes utilsiées dans l'EF sont asynchrones.
- Toute méthode doit retourner une Task<>
- Spécifie un async en début
- Peut gérer autant d'await que souhaité.


#### Migrations
Problèmatique importante de la gestion des mises à jour sous forme de migration.
- Ajout migration : Add-Migration NOM
- Appliquer migration : Uptade-Database
- Annuler migration : Uptade-Database -TargetMigration PRECEDENTE_MIGRATION
- Générer script de maj : Update-Database -Script

#### Relations entre entités
Les liens sont crées en ajoutant l'attribut à la classe.
On peut ajouter le mot clef virtua lavant le type si on demande du lazy loading (vs. eager loading)

Ex.
``` powershell
dotnet tool install dotnet-ef -g
```
Toute migration contient 2 méthodes : Up and Down.

#### CRUD
Dans un DbSet on retrouvera par défaut un Find(int id) mais qui est peu utilsiée irl.
``` csharp
DbSet<Personne> personne
var personne = context.Personne.Find(1);
```
Création d'enttié : 
- création d'instance de Personne
- Ajout au DbSet
- SaveChanges()

Modification d'entité :
- Récupérer l'entité (Find)
- Modifier l'attribut
- SaveChanges()

Génération de controller + View avec EF.

#### Fluent API
- Annotation : règle de modele. Ne permet pas toutes les modifications.
- Fluent API : design pattern utilisable pour configurer des entités par code.
    - EF va par défaut mettre les tables au pluriel.
    - Définir des noms de colonne
    - Exclure un champ de la db

-Les relations : permet de configurer les relations.

#### Loading
3 façons de charge :
- LazyLoading (default)
- ExplicitLoading (lourd et peu utilisé)
- Eager : context.ObjectInclude(o => o.atrtibut) permet d'inclure des sous-objets d'une entité.
Par défault les objets seront chargés sans leurs relations. 

#### Gestion des ressources
La porté d'une connexion sera limitée à une méthode par exemple en utilsiant : using var context = new LoadingContext().
Using s'assurera de la fermeture de la connexion à l'échéance de la méthode.

#### Etat EntityState
Enumération contenant les statuts d'une entité : Added, Unchanged, Modified, Deleted, Detached.

#### Notes TP Final Dojo
Connexion provider
``` json
Server=170SE3-9Q205M2;Database=Dojo;User Id=sa;Password=Pa$$w0rd;
```

``` powershell
dotnet ef migrations add <nom_de_la_migration> -p <chemin_du_projet_dal>
dotnet ef migrations add Creation -p ..\DotNet.06.TP5Dojo.Dal\
dotnet ef database update
```

```csharp
 <ItemGroup>
    <PackageReference Include="Microsoft.EntityFrameworkCore" Version="6.0.8" />
    <PackageReference Include="Microsoft.EntityFrameworkCore.Design" Version="6.0.8">
      <PrivateAssets>all</PrivateAssets>
      <IncludeAssets>runtime; build; native; contentfiles; analyzers; buildtransitive</IncludeAssets>
    </PackageReference>
    <PackageReference Include="Microsoft.EntityFrameworkCore.SqlServer" Version="6.0.8" />
    <PackageReference Include="Microsoft.EntityFrameworkCore.Tools" Version="6.0.8">
      <PrivateAssets>all</PrivateAssets>
      <IncludeAssets>runtime; build; native; contentfiles; analyzers; buildtransitive</IncludeAssets>
    </PackageReference>
    <PackageReference Include="Microsoft.VisualStudio.Web.CodeGeneration.Design" Version="6.0.8" />
  </ItemGroup>
```

Pour rendre les services injectables, il va falloire créer des méthodes d'extension dans les couches 
public static DalExtensions
public static void AddServices (this.IServiceCollection services)
add corresponding services originally in program

## API
### Définition
L'API s'adressera à une machine au lieu de l'humain.
Le format d'envoi des données n'est pas figé, mais le dominé par le JSON.  
Les controlleurs hériteront de ControllerBase et attribués par [ApiController]  
Les objets seront par défaut renvoyés en Json.  
Swagger pour tester à la Postman.