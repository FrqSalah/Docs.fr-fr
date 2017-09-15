---
title: "Migration d’ASP.NET Core 1.x vers la version 2.0"
author: scottaddie
description: "Cet article présente les prérequis et la plupart des étapes courantes nécessaires pour la migration d’un projet ASP.NET Core 1.x vers ASP.NET Core 2.0."
keywords: ASP.NET Core, migration
ms.author: scaddie
manager: wpickett
ms.date: 08/01/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: migration/1x-to-2x/index
ms.openlocfilehash: c14e7d61e8b353c18fc4a4f2bf3658069982bad5
ms.sourcegitcommit: e832a9b9f41a8b26a8c88edfd8fc35b8bfd97d5d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="migrating-from-aspnet-core-1x-to-aspnet-core-20"></a>Migration d’ASP.NET Core 1.x vers ASP.NET Core 2.0

Par [Scott Addie](https://github.com/scottaddie)

Dans cet article, nous allons vous montrer comment mettre à jour un projet ASP.NET Core 1.x existant vers ASP.NET Core 2.0. La migration de votre application vers ASP.NET Core 2.0 vous permet de tirer parti de [nombreuses nouvelles fonctionnalités et améliorations des performances](https://go.microsoft.com/fwlink/?linkid=854094). 

Les applications ASP.NET Core 1.x existantes sont basées sur des modèles de projet propres à la version. Les modèles de projet et le code de démarrage qu’ils contiennent évoluent en même temps que le framework ASP.NET Core. Outre le framework ASP.NET Core, vous devez aussi mettre à jour le code de votre application.

<a name="prerequisites"></a>

## <a name="prerequisites"></a>Prérequis
Consultez [Bien démarrer avec ASP.NET Core](xref:getting-started).

<a name="tfm"></a>

## <a name="update-target-framework-moniker-tfm"></a>Mettre à jour le Moniker du Framework cible
Les projets ciblant .NET Core doivent utiliser le [Moniker du Framework cible](/dotnet/standard/frameworks#referring-to-frameworks) d’une version supérieure ou égale à .NET Core 2.0. Recherchez le nœud `<TargetFramework>` dans le fichier *.csproj* et remplacez son texte interne par `netcoreapp2.0` :

[!code-xml[Main](../1x-to-2x/samples/AspNetCoreDotNetCore2.0App/AspNetCoreDotNetCore2.0App/AspNetCoreDotNetCore2.0App.csproj?range=3)]

Les projets ciblant le .NET Framework doivent utiliser le Moniker du Framework cible d’une version supérieure ou égale à .NET Framework 4.6.1. Recherchez le nœud `<TargetFramework>` dans le fichier *.csproj* et remplacez son texte interne par `net461` :

[!code-xml[Main](../1x-to-2x/samples/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App.csproj?range=4)]

> [!NOTE]
> .NET Core 2.0 offre une surface d’exposition beaucoup plus grande que .NET Core 1.x. Si vous ciblez le .NET Framework uniquement car il manque des API dans .NET Core 1.x, le ciblage de .NET Core 2.0 fonctionnera sans doute.

<a name="global-json"></a>

## <a name="update-net-core-sdk-version-in-globaljson"></a>Mettre à jour la version du SDK .NET Core dans global.json
Si votre solution s’appuie sur un fichier [*global.json*](https://docs.microsoft.com/dotnet/core/tools/global-json) pour cibler une version spécifique du SDK .NET Core, mettez à jour sa propriété `version` de façon à utiliser la version 2.0 installée sur votre ordinateur :

[!code-json[Main](../1x-to-2x/samples/AspNetCoreDotNetCore2.0App/global.json?highlight=3)]

<a name="package-reference"></a>

## <a name="update-package-references"></a>Mettre à jour les références de package
Le fichier *.csproj* dans un projet 1.x répertorie chaque package NuGet utilisé par le projet.

Dans un projet ASP.NET Core 2.0 ciblant .NET Core 2.0, une seule référence de [métapackage](xref:fundamentals/metapackage) dans le fichier *.csproj* remplace la collection de packages :

[!code-xml[Main](../1x-to-2x/samples/AspNetCoreDotNetCore2.0App/AspNetCoreDotNetCore2.0App/AspNetCoreDotNetCore2.0App.csproj?range=9-11)]

Toutes les fonctionnalités d’ASP.NET Core 2.0 et d’Entity Framework Core 2.0 sont incluses dans le métapackage.

Les projets ASP.NET Core 2.0 ciblant le .NET Framework doivent continuer à référencer des packages NuGet spécifiques. Mettez à jour l’attribut `Version` de chaque nœud `<PackageReference />` vers la version 2.0.0.

Par exemple, voici la liste des nœuds `<PackageReference />` utilisés dans un projet ASP.NET Core 2.0 standard qui cible le .NET Framework :

[!code-xml[Main](../1x-to-2x/samples/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App.csproj?range=9-22)]

<a name="dot-net-cli-tool-reference"></a>

## <a name="update-net-core-cli-tools"></a>Mettre à jour les outils CLI .NET Core
Dans le fichier *.csproj*, mettez à jour l’attribut `Version` de chaque nœud `<DotNetCliToolReference />` vers la version 2.0.0.

Par exemple, voici la liste des outils CLI utilisés dans un projet ASP.NET Core 2.0 standard qui cible .NET Core 2.0 :

[!code-xml[Main](../1x-to-2x/samples/AspNetCoreDotNetCore2.0App/AspNetCoreDotNetCore2.0App/AspNetCoreDotNetCore2.0App.csproj?range=13-17)]

<a name="package-target-fallback"></a>

## <a name="rename-package-target-fallback-property"></a>Renommer la propriété PackageTargetFallback
Le fichier *.csproj* d’un projet 1.x utilise un nœud et une variable `PackageTargetFallback` :

[!code-xml[Main](../1x-to-2x/samples/AspNetCoreDotNetCore1.1App/AspNetCoreDotNetCore1.1App/AspNetCoreDotNetCore1.1App.csproj?range=5)]

Renommez le nœud et la variable `AssetTargetFallback` :

[!code-xml[Main](../1x-to-2x/samples/AspNetCoreDotNetCore2.0App/AspNetCoreDotNetCore2.0App/AspNetCoreDotNetCore2.0App.csproj?range=5)]

<a name="program-cs"></a>

## <a name="update-main-method-in-programcs"></a>Mettre à jour la méthode Main dans Program.cs
Dans les projets 1.x, la méthode `Main` de *Program.cs* ressemble à ceci :

[!code-csharp[Main](../1x-to-2x/samples/AspNetCoreDotNetCore1.1App/AspNetCoreDotNetCore1.1App/Program.cs?name=snippet_ProgramCs&highlight=8-19)]

Dans les projets 2.0, la méthode `Main` de *Program.cs* a été simplifiée :

[!code-csharp[Main](../1x-to-2x/samples/AspNetCoreDotNetCore2.0App/AspNetCoreDotNetCore2.0App/Program.cs?highlight=8-11)]

L’adoption de ce nouveau modèle 2.0 est vivement recommandée, et elle est obligatoire pour que des fonctionnalités de produit telles que les [migrations Entity Framework Core](xref:data/ef-mvc/migrations) fonctionnent. Par exemple, l’exécution de `Update-Database` à partir de la fenêtre de la Console du Gestionnaire de Package ou de `dotnet ef database update` à partir de la ligne de commande (sur des projets convertis vers ASP.NET Core 2.0) génère l’erreur suivante :

```
Unable to create an object of type '<Context>'. Add an implementation of 'IDesignTimeDbContextFactory<Context>' to the project, or see https://go.microsoft.com/fwlink/?linkid=851728 for additional patterns supported at design time.
```

<a name="view-compilation"></a>

## <a name="review-your-razor-view-compilation-setting"></a>Passer en revue votre paramètre de compilation de vue Razor
La vitesse de démarrage d’application et la taille des bundles publiés ont une importance capitale pour vous. Pour ces raisons, la [compilation de vue Razor](xref:mvc/views/view-compilation) est activée par défaut dans ASP.NET Core 2.0.

L’affectation de la valeur true à la propriété `MvcRazorCompileOnPublish` n’est plus nécessaire. Vous pouvez supprimer la propriété du fichier *.csproj*, sauf si vous désactivez la compilation des vues.

Quand vous ciblez le .NET Framework, vous devez toujours référencer explicitement le package NuGet [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation) dans votre fichier *.csproj* :

[!code-xml[Main](../1x-to-2x/samples/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App.csproj?range=15)]

<a name="app-insights"></a>

## <a name="rely-on-application-insights-light-up-features"></a>S’appuyer sur les fonctionnalités de mise en évidence d’Application Insights
La configuration sans effort de l’instrumentation des performances d’application est importante. Vous pouvez maintenant vous appuyer sur les nouvelles fonctionnalités de mise en évidence [d’Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview) disponibles dans les outils Visual Studio 2017.

Par défaut, les projets ASP.NET Core 1.1 créés dans Visual Studio 2017 ajoutaient Application Insights. Si vous n’utilisez pas le SDK Application Insights directement, en dehors de *Program.cs* et *Startup.cs*, effectuez les étapes suivantes :

1. Supprimez le nœud `<PackageReference />` suivant du fichier *.csproj* :
    
    [!code-xml[Main](../1x-to-2x/samples/AspNetCoreDotNetCore1.1App/AspNetCoreDotNetCore1.1App/AspNetCoreDotNetCore1.1App.csproj?range=10)]

2. Supprimez l’appel de méthode d’extension `UseApplicationInsights` de *Program.cs* :

    [!code-csharp[Main](../1x-to-2x/samples/AspNetCoreDotNetCore1.1App/AspNetCoreDotNetCore1.1App/Program.cs?name=snippet_ProgramCsMain&highlight=8)]

3. Supprimez l’appel d’API côté client Application Insights du fichier *_Layout.cshtml*. Il comprend les deux lignes de code suivantes :

    [!code-cshtml[Main](../1x-to-2x/samples/AspNetCoreDotNetCore1.1App/AspNetCoreDotNetCore1.1App/Views/Shared/_Layout.cshtml?range=1,19)]

Si vous utilisez le SDK Application Insights directement, continuez à le faire. La version 2.0 du [métapackage](xref:fundamentals/metapackage) inclut la dernière version d’Application Insights. Par conséquent, une erreur de passage à une version antérieure de package s’affiche si vous référencez une version antérieure.

<a name="auth-and-identity"></a>

## <a name="adopt-authentication--identity-improvements"></a>Adopter les améliorations d’authentification / identité
ASP.NET Core 2.0 offre un nouveau modèle d’authentification, et plusieurs modifications importantes ont été apportées à ASP.NET Core Identity. Si vous avez créé votre projet avec l’option Comptes d’utilisateur individuels activée, ou si vous avez ajouté manuellement l’authentification ou Identity, consultez [Migrating Authentication and Identity to ASP.NET Core 2.0 (Migration de l’authentification et de l’identité vers ASP.NET Core 2.0)](xref:migration/1x-to-2x/identity-2x).

## <a name="additional-resources"></a>Ressources supplémentaires
- [Changements importants dans ASP.NET Core 2.0](https://github.com/aspnet/announcements/issues?page=1&q=is%3Aissue+is%3Aopen+label%3A2.0.0+label%3A%22Breaking+change%22&utf8=%E2%9C%93)