# DotNet

Remarques introductives : le cours ENI et très en retard sur la réalité du terrain et ce qui vous sera présenté diffèrera sensiblement du contenu des supports.

Le cours sera présenté avec les anciennes syntaxes, mais les TP seront actualisé.

Langage encore "OOP" que java. Présenté comme étant plus concis que le java dont il est (officieusement) forké. Date de 2001, et windows only jusqu'en 2017 (<= version 4.8) où il est passé open source et est devenu multiplateforme (>= 5).

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



