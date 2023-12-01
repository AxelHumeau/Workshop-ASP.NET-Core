# Découverte d'ASP.NET-Core

## Introduction

Lorsque vous aurez besoin de chercher des informations, je vous invite à aller sur la documentation Microsoft (https://learn.microsoft.com/fr-fr/aspnet/core/?view=aspnetcore-7.0) 

Sauf si précision, les classes, interfaces, propriétés et méthodes doivent être publiques. 

## Prérequis
Vous devriez avoir installé Visual Studio sur Windows ou Mac (et pas VS Code) ou installé Rider (de la suite JetBrains) 

Pour Rider, quelques différences peuvent être présente car le sujet a été fait avec Visual Studio en tête.

Je recomande Visual Studio si vous souhaitez faire le workshop suivant.

Pour Visual Studio, installé le workload "ASP.NET and web development" avec au moins ".NET 6.0 Runtime" dans les Composants individuels

## Exercice 1 : Créer un projet ASP.NET Core  

Avant de commencer à développer notre application, il faut créer le projet. 

Créez donc un projet d’application web ASP.NET Core (Model-View-Controller), en sélectionnant .NET 6.0 pour la version de .NET. Pour le nom de la solution, mettez « Todo », tandis que pour le projet, mettez « Todo.Web ». 

Vous pouvez maintenant appuyer sur Build pour lancer l’application. 

## Exercice 2 : Architecture des services 

Le principe des services est d’avoir une classe réutilisable à différents endroits du code, le but étant de pouvoir notamment utiliser les services dans les controllers (le code pour contrôler les pages) et bien séparer le code. 

Créez donc un second projet nommé « Todo.Services » dans la solution, cette fois de type Class Library, créez ensuite un dossier « Classes », « Interfaces » et « Models » à l’intérieur. 

## Exercice 3 : Le modèle 

Le modèle est la classe dénuée de méthode qui sera lié à une vue lors de l’affichage de celle-ci. Dans notre cas, le modèle sera la classe représentant nos to-dos. 

Créez donc une classe nommée « TodoViewModel » dans le dossier « Models » de « Todo.Web ». Celle-ci doit avoir les propriétés suivantes : 

  - Un id, doit être un nombre 

  - Un nom, doit être une chaine de caractère* 

  - Une description, doit être une chaine de caractère* 

  - Une date de fin, doit être une date* 

  - Une date de création, doit être une date 

*Ces propriétés doivent être obligatoire lors de la validation de modèle, ajoutez donc les attributs correspondants (cherchez sur la documentation). 

## Exercice 4 : Créations des pages 

### Les vues 

Les vues sont les pages affichés dans notre application web, elles sont chacune lié à un modèle. Les vues avec ASP.NET Core sont des Razor Views, celle-ci ont la particularité d’utiliser la syntaxe Razor, qui leur permet d’utiliser les Tag Helpers et du code C# dans le code HTML (plus d’info dans la documentation). 

Créez 5 vues (Razor View) dans un nouveau dossier « Todo » dans « Views » : 

  - ListeTodo.cshtml, le modèle doit être IEnumerable\<TodoViewModel\>, son but sera de boucler dans l’énumérable et afficher un aperçu de l’ensemble des TodoViewModel. 
La vue devra aussi contenir un lien déclenchant l’action « AjouterTodo » du controller « TodoController » et chaque aperçu de Todo devra avoir lien vers les détails (action « DetailsTodo » du même controller). 

  - AjouterTodo.cshtml, le modèle doit être TodoViewModel, son but sera d’ajouter des to-dos grâce à des formulaires. La vue devra avoir un lien de retour vers la liste de to-dos et afficher un message lorsque le formulaire n’est pas validé.  

  - DetailsTodo.cshtml, le modèle doit être TodoViewModel, son but sera d’afficher toutes les informations de la to-do ainsi que le temps restant. La vue devra avoir un lien de retour vers la liste de to-dos. 

  - SupprimerTodo.cshtml, le modèle doit être TodoViewModel, son but sera d’afficher les détails de la to-do avant de proposer de la supprimer. 

  - ModifierTodo.cshtml, le modèle doit être TodoViewModel, son but sera d’afficher les informations de la to-do dans un formulaire afin de la modifier (pensez à quelles informations doivent être modifiable). 

Pour l’ensemble de ces vues, n’hésitez pas à chercher des informations sur la documentation. 

Vous pouvez donner le style que vous voulez à ces vues. 

### Le controller  

Les controllers sont le centre d’une application web ASP.NET Core, ce sont eux qui vont appeler les différents services pour récupérer des informations qu’il va ensuite formatter dans une classe (un modèle) et vont enfin charger une page (une vue) avec ce modèle (d’où Model-View-Controller ou MVC). 

Pour commencer, créez un controller dans le dossier « Controllers » de « Todo.Web », nommé le « TodoController » 

Vous y verrez une méthode « Index », cette méthode est une action du controller. Basé sur cette action, créez 8 méthodes : 

  - ListeTodo 
    Paramètre : aucun 
    Pour l’instant renvoie une vue avec un IEnumerable<TodoViewModel> vide pour modèle. 


  - DetailsTodo 
    Paramètre : un id (nombre) 
    Pour l’instant renvoie une vue avec une to-do avec des informations de test pour modèle. 


  - AjouterTodo (GET*) 
    Paramètre : aucun 
    Renvoie une vue avec une to-do avec aucune valeur pour ses propriétés. 
 

  - AjouterTodo (POST*) 
    Paramètre : TodoViewModel 
    Pour l’instant ne fait qu’effectuer une validation de modèle et renvoyer une vue avec une to-do avec aucune valeur pour ses propriétés. 
 

  - SupprimerTodo (GET*) 
    Paramètre : un id (nombre) 
    Pour l’instant renvoie une vue avec une to-do avec des informations de test pour modèle. 


  - SupprimerTodo (POST*) 
    Paramètre : TodoViewModel 
    Pour l’instant effectue une validation de modèle et redirige vers la liste de to-dos. 
 

  - ModifierTodo (GET*) 
    Paramètre : un id (nombre) 
    Renvoie une vue avec une to-do avec aucune valeur pour ses propriétés. 
    

  - ModifierTodo (POST*) 
    Paramètre : TodoViewModel 
    Pour l’instant ne fait qu’effectuer une validation de modèle et renvoyer une vue avec une to-do avec aucune valeur pour ses propriétés. 

*désigne la méthode HTML, pensez à utiliser les attributs correspondants. 

### La barre de navigation 

C’est bien d’avoir ajouté des pages mais c’est mieux de pouvoir y accéder sans avoir à taper manuellement l’url. 

Ajoutez dans la barre de navigation (dans Todo.Web/Views/Shared/_Layout.cshtml) un menu déroulant nommé « To-do » comprenant des liens déclenchant les actions d’ajout et de liste. 

Vous devrez pouvoir maintenant accéder à vos pages depuis n’importe où sur le site. 

## Exercice 5 : le service 

Le service va nous permettre de récupérer les informations requises par nos pages. 

### Le modèle 

Du fait de notre architecture, on ne peut pas avoir la même classe pour désigner nos to-dos car cela provoquera des dépendances circulaires. Pour contrer ça, créez une classe « TodoDetails » dans le dossier « Todo.Services/Models » avec les mêmes propriétés que « TodoViewModel », sans les attributs de validation. 

### L’interface 

Créez une interface « ITodoService » dans le dossier « Todo.Services/Interfaces » composée des méthodes suivantes : 

  - GetAllTodos 
    Paramètres : aucun 
    Retour : IEnumerable<TodoDetails> 


  - GetTodo 
    Paramètres : id (nombre) 
    Retour : TodoDetails 


  - AddTodo 
    Paramètres : model (TodoDetails) 
    Retour : TodoDetails 


  - EditTodo 
    Paramètres : model (TodoDetails) 
    Retour : TodoDetails 


  - DeleteTodo 
    Paramètres : model (TodoDetails) 
    Retour : booléen 

## Le stockage 

Pour enregistrer nos to-dos, il va falloir les stocker. Pour cela nous utiliseront un fichier JSON nommé « todos.json » situé dans un nouveau dossier « data » à l’intérieur de « Todo.Web/wwwroot » contenant uniquement « [{}] ». 

Installez ensuite le package Nuget « Newtonsoft.Json ». 

## Le service 

Tout d’abord, créez une classe « TodoService » implémentant l’interface créée plus tôt. 

Ensuite, implémentez les méthodes en lisant, en écrivant, et surtout en sérialisant et désérialisant le contenu JSON de todos.json en TodoDetails (pensez au cas où il n’y a pas encore de to-dos). 

Plus d’infos sur la sérialisation et la désérialisation avec Newtonsoft : http://www.newtonsoft.com/json/help/html/serializingjson.htm 

## L’utilisation dans les controllers 

C’est bientôt fini, plus qu’à utiliser notre service dans notre controller ! Pour cela il faut d’abord qu’il soit disponible… Heureusement, ASP.NET Core a une fonctionnalité nommée l’injection de dépendance. 

Commencer par ajouter dans « Program.cs » notre service avec notre interface un tant que « Transient ». 

Vous pouvez maintenant demander une instance de ITodoService lors de la création de votre controller. 

(Voir la documentation sur l’injection de dépendances.) 

Une fois cela fait nous pouvons presque utiliser notre service. Il nous manque juste un moyen pour convertir nos TodoDetails en TodoViewModel, créez donc 2 méthodes privées dans ce but. 

Vous pouvez maintenant utiliser le service pour compléter les actions du controller (attention à bien définir un id unique et la date de création lors de la création de to-dos). 

Essayez votre application, si tout fonctionne, bravo, vous avez terminé ce workshop (il y a quelques bonus si vous voulez aller plus loin), sinon, corriger vos erreurs en revenant sur les précédents exercices (oubliez pas la doc !). 

## Bonus 

Voici quelques propositions de bonus : 

  - Ajouter des messages de validation/erreur 

  - Ajouter différentes catégories de to-dos 

  - Trier les to-dos dans la liste (par nom, par date de fin, par date de création) 

  - Styliser l’application web (css, javascript) 
