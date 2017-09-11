---
title: "Bien démarrer avec des pages Razor dans ASP.NET Core avec Visual Studio Code"
author: rick-anderson
description: "Bien démarrer avec des pages Razor dans ASP.NET Core à l’aide de Visual Studio Code"
keywords: "ASP.NET Core,pages Razor,génération de modèles automatique,Entity Framework Core,EF,EF Core,base de données,mac,macOS,Visual Studio Code,Code"
ms.author: riande
manager: wpickett
ms.date: 8/27/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: aspnet-core
uid: tutorials/razor-pages-vsc/razor-pages-start
ms.openlocfilehash: aa39de71addb2499af6d322db6da0ec635c54970
ms.sourcegitcommit: d9ec19e5452af83648074db5d96c0a0f4f9e7f9a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-razor-pages-in-aspnet-core-with-visual-studio-code"></a><span data-ttu-id="77ef8-104">Bien démarrer avec des pages Razor dans ASP.NET Core avec Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="77ef8-104">Getting started with Razor Pages in ASP.NET Core with Visual Studio Code</span></span>

<span data-ttu-id="77ef8-105">De [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="77ef8-105">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="77ef8-106">Ce didacticiel décrit les principes fondamentaux liés à la génération d’une application web de pages Razor dans ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="77ef8-106">This tutorial teaches the basics of building an ASP.NET Core Razor Pages web app.</span></span> <span data-ttu-id="77ef8-107">Nous vous recommandons d’effectuer l’étape [Présentation des pages Razor](xref:mvc/razor-pages/index) avant de commencer ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="77ef8-107">We recommend you complete [Introduction to Razor Pages](xref:mvc/razor-pages/index) before starting this tutorial.</span></span> <span data-ttu-id="77ef8-108">L’utilisation de pages Razor est la méthode recommandée pour générer l’IU d’applications web dans ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="77ef8-108">Razor Pages is the recommended way to build UI for web applications in ASP.NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77ef8-109">Prérequis</span><span class="sxs-lookup"><span data-stu-id="77ef8-109">Prerequisites</span></span>

<span data-ttu-id="77ef8-110">Installez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="77ef8-110">Install the following:</span></span>

* <span data-ttu-id="77ef8-111">[Kit .NET Core 2.0.0 SDK](https://dot.net/core) ou ultérieur</span><span class="sxs-lookup"><span data-stu-id="77ef8-111">[.NET Core 2.0.0 SDK](https://dot.net/core) or later</span></span>
* [<span data-ttu-id="77ef8-112">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="77ef8-112">Visual Studio Code</span></span>](https://code.visualstudio.com)
* <span data-ttu-id="77ef8-113">[Extension C#](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) VS Code</span><span class="sxs-lookup"><span data-stu-id="77ef8-113">VS Code [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)</span></span> 

## <a name="create-a-razor-web-app"></a><span data-ttu-id="77ef8-114">Créer une application web Razor</span><span class="sxs-lookup"><span data-stu-id="77ef8-114">Create a Razor web app</span></span>

<span data-ttu-id="77ef8-115">À partir d’un terminal, exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="77ef8-115">From a terminal, run the following commands:</span></span>

```console
dotnet new razor -o RazorPagesMovie
cd RazorPagesMovie
dotnet run
```

<span data-ttu-id="77ef8-116">Les commandes précédentes utilisent le [CLI .NET Core](https://docs.microsoft.com/dotnet/core/tools/dotnet) pour créer et exécuter un projet de pages Razor.</span><span class="sxs-lookup"><span data-stu-id="77ef8-116">The preceding commands use the [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet) to create and run a Razor Pages project.</span></span> <span data-ttu-id="77ef8-117">Ouvrez un navigateur à l’adresse http://localhost:5000 pour afficher l’application.</span><span class="sxs-lookup"><span data-stu-id="77ef8-117">Open a browser to http://localhost:5000 to view the application.</span></span>

![Page d’accueil ou page d’index](../razor-pages/razor-pages-start/_static/home.png)

[!INCLUDE[razor-pages-start](../../includes/RP/razor-pages-start.md)]

## <a name="open-the-project"></a><span data-ttu-id="77ef8-119">Ouvrir le projet</span><span class="sxs-lookup"><span data-stu-id="77ef8-119">Open the project</span></span>

<span data-ttu-id="77ef8-120">Appuyez sur Ctrl+C pour arrêter l’application.</span><span class="sxs-lookup"><span data-stu-id="77ef8-120">Press Ctrl+C to shut down the application.</span></span>

<span data-ttu-id="77ef8-121">Dans Visual Studio Code (VS Code), sélectionnez **Fichier > Ouvrir le dossier**, puis sélectionnez le dossier *RazorPagesMovie*.</span><span class="sxs-lookup"><span data-stu-id="77ef8-121">From Visual Studio Code (VS Code), select **File > Open Folder**, and then select the *RazorPagesMovie* folder.</span></span>

- <span data-ttu-id="77ef8-122">Sélectionnez **Oui** quand une boîte de dialogue **Avertissement** s’affiche en indiquant le message suivant : « Les composants nécessaires à la build et au débogage sont manquants dans ‘RazorPagesMovie’.</span><span class="sxs-lookup"><span data-stu-id="77ef8-122">Select **Yes** to the **Warn** message "Required assets to build and debug are missing from 'RazorPagesMovie'.</span></span> <span data-ttu-id="77ef8-123">Faut-il les ajouter ? »</span><span class="sxs-lookup"><span data-stu-id="77ef8-123">Add them?"</span></span>
- <span data-ttu-id="77ef8-124">Sélectionnez **Restaurer** quand une boîte de dialogue **Informations** s’affiche en indiquant qu’il existe des dépendances non résolues.</span><span class="sxs-lookup"><span data-stu-id="77ef8-124">Select **Restore** to the **Info** message "There are unresolved dependencies".</span></span>

### <a name="launch-the-app"></a><span data-ttu-id="77ef8-125">Lancer l’application</span><span class="sxs-lookup"><span data-stu-id="77ef8-125">Launch the app</span></span>

<span data-ttu-id="77ef8-126">Appuyez sur Ctrl+F5 pour démarrer l’application sans débogage.</span><span class="sxs-lookup"><span data-stu-id="77ef8-126">Press Ctrl+F5 to start the app without debugging.</span></span> <span data-ttu-id="77ef8-127">Vous pouvez également aller dans le menu **Déboguer**, puis sélectionner **Exécuter sans débogage**.</span><span class="sxs-lookup"><span data-stu-id="77ef8-127">Alternatively, from the **Debug** menu, select **Start Without Debugging**.</span></span>

<span data-ttu-id="77ef8-128">Dans le prochain didacticiel, nous allons ajouter un modèle au projet.</span><span class="sxs-lookup"><span data-stu-id="77ef8-128">In the next tutorial, we add a model to the project.</span></span> 

>[!div class="step-by-step"]
[<span data-ttu-id="77ef8-129">Suivant : Ajout d’un modèle</span><span class="sxs-lookup"><span data-stu-id="77ef8-129">Next: Adding a model</span></span>](xref:tutorials/razor-pages-vsc/model)  