---
uid: aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
title: Prise en main OWIN et Katana | Documents Microsoft
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/27/2013
ms.topic: article
ms.assetid: 6dae249f-5ac6-4f6e-bc49-13bcd5a54a70
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
msc.type: authoredcontent
ms.openlocfilehash: 8922aada723da9b149ec111902fcd883c8241dfb
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/10/2017
---
<a name="getting-started-with-owin-and-katana"></a><span data-ttu-id="4993e-102">Prise en main OWIN et Katana</span><span class="sxs-lookup"><span data-stu-id="4993e-102">Getting Started with OWIN and Katana</span></span>
====================
<span data-ttu-id="4993e-103">par [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="4993e-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="4993e-104">[Ouvrir l’Interface Web pour .NET (OWIN)](http://owin.org/) définit une abstraction entre les serveurs web .NET et des applications web.</span><span class="sxs-lookup"><span data-stu-id="4993e-104">[Open Web Interface for .NET (OWIN)](http://owin.org/) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="4993e-105">En séparant le serveur web à partir de l’application, OWIN rend plus facile de créer l’intergiciel (middleware) pour le développement web .NET.</span><span class="sxs-lookup"><span data-stu-id="4993e-105">By decoupling the web server from the application, OWIN makes it easier to create middleware for .NET web development.</span></span> <span data-ttu-id="4993e-106">OWIN facilite également les applications web à d’autres hôtes &#8212; par exemple, l’auto-hébergement dans un service Windows ou d’autres processus.</span><span class="sxs-lookup"><span data-stu-id="4993e-106">Also, OWIN makes it easier to port web applications to other hosts&#8212;for example, self-hosting in a Windows service or other process.</span></span>

<span data-ttu-id="4993e-107">OWIN est une spécification appartenant à la Communauté, pas une implémentation.</span><span class="sxs-lookup"><span data-stu-id="4993e-107">OWIN is a community-owned specification, not an implementation.</span></span> <span data-ttu-id="4993e-108">Le projet Katana est un ensemble de composants OWIN open source développé par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4993e-108">The Katana project is a set of open-source OWIN components developed by Microsoft.</span></span> <span data-ttu-id="4993e-109">Pour obtenir une vue d’ensemble de OWIN et Katana, consultez [une vue d’ensemble du projet Katana](an-overview-of-project-katana.md).</span><span class="sxs-lookup"><span data-stu-id="4993e-109">For a general overview of both OWIN and Katana, see [An Overview of Project Katana](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="4993e-110">Dans cet article, j’accédera à droite dans le code pour commencer.</span><span class="sxs-lookup"><span data-stu-id="4993e-110">In this article, I will jump right into code to get started.</span></span>

<span data-ttu-id="4993e-111">Ce didacticiel utilise [Visual Studio 2013 Release Candidate](https://go.microsoft.com/fwlink/?LinkId=306566), mais vous pouvez également utiliser Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="4993e-111">This tutorial uses [Visual Studio 2013 Release Candidate](https://go.microsoft.com/fwlink/?LinkId=306566), but you can also use Visual Studio 2012.</span></span> <span data-ttu-id="4993e-112">Certaines des étapes sont différents dans Visual Studio 2012, je remarque ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="4993e-112">A few of the steps are different in Visual Studio 2012, which I note below.</span></span>

## <a name="host-owin-in-iis"></a><span data-ttu-id="4993e-113">Hôte OWIN dans IIS</span><span class="sxs-lookup"><span data-stu-id="4993e-113">Host OWIN in IIS</span></span>

<span data-ttu-id="4993e-114">Dans cette section, nous allons héberger OWIN dans IIS.</span><span class="sxs-lookup"><span data-stu-id="4993e-114">In this section, we'll host OWIN in IIS.</span></span> <span data-ttu-id="4993e-115">Cette option vous donne la souplesse et la composabilité d’un pipeline OWIN ainsi que l’ensemble des fonctionnalités matures d’IIS.</span><span class="sxs-lookup"><span data-stu-id="4993e-115">This option gives you the flexibility and composability of an OWIN pipeline together with the mature feature set of IIS.</span></span> <span data-ttu-id="4993e-116">À l’aide de cette option, l’application OWIN s’exécute dans le pipeline de demande ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4993e-116">Using this option, the OWIN application runs in the ASP.NET request pipeline.</span></span>

<span data-ttu-id="4993e-117">Commencez par créer un nouveau projet d’Application Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4993e-117">First, create a new ASP.NET Web Application project.</span></span> <span data-ttu-id="4993e-118">(Dans Visual Studio 2012, utilisez le type de projet d’Application Web ASP.NET vide).</span><span class="sxs-lookup"><span data-stu-id="4993e-118">(In Visual Studio 2012, use the ASP.NET Empty Web Application project type.)</span></span>

![](getting-started-with-owin-and-katana/_static/image1.png)

<span data-ttu-id="4993e-119">Dans le **nouveau projet ASP.NET** boîte de dialogue, sélectionnez le **vide** modèle.</span><span class="sxs-lookup"><span data-stu-id="4993e-119">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span>

![](getting-started-with-owin-and-katana/_static/image2.png)

### <a name="add-nuget-packages"></a><span data-ttu-id="4993e-120">Ajouter des Packages NuGet</span><span class="sxs-lookup"><span data-stu-id="4993e-120">Add NuGet Packages</span></span>

<span data-ttu-id="4993e-121">Ensuite, ajoutez les packages NuGet nécessaires.</span><span class="sxs-lookup"><span data-stu-id="4993e-121">Next, add the required NuGet packages.</span></span> <span data-ttu-id="4993e-122">À partir de la **outils** menu, sélectionnez **Gestionnaire de Package de bibliothèque**, puis sélectionnez **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="4993e-122">From the **Tools** menu, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="4993e-123">Dans la fenêtre de Console du Gestionnaire de Package, tapez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4993e-123">In the Package Manager Console window, type the following command:</span></span>

`install-package Microsoft.Owin.Host.SystemWeb –Pre`

![](getting-started-with-owin-and-katana/_static/image3.png)

### <a name="add-a-startup-class"></a><span data-ttu-id="4993e-124">Ajoutez une classe de démarrage</span><span class="sxs-lookup"><span data-stu-id="4993e-124">Add a Startup Class</span></span>

<span data-ttu-id="4993e-125">Ensuite, ajoutez une classe de démarrage OWIN.</span><span class="sxs-lookup"><span data-stu-id="4993e-125">Next, add an OWIN startup class.</span></span> <span data-ttu-id="4993e-126">Dans l’Explorateur de solutions, cliquez sur le projet et sélectionnez **ajouter**, puis sélectionnez **un nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="4993e-126">In Solution Explorer, right-click the project and select **Add**, then select **New Item**.</span></span> <span data-ttu-id="4993e-127">Dans le **ajouter un nouvel élément** boîte de dialogue, sélectionnez **classe de démarrage Owin**.</span><span class="sxs-lookup"><span data-stu-id="4993e-127">In the **Add New Item** dialog, select **Owin Startup class**.</span></span> <span data-ttu-id="4993e-128">Pour plus d’informations sur la configuration de la classe de démarrage, consultez [détection de classe de démarrage OWIN](owin-startup-class-detection.md).</span><span class="sxs-lookup"><span data-stu-id="4993e-128">For more info on configuring the startup class, see [OWIN Startup Class Detection](owin-startup-class-detection.md).</span></span>

![](getting-started-with-owin-and-katana/_static/image4.png)

<span data-ttu-id="4993e-129">Ajoutez le code suivant à la méthode `Startup1.Configuration` :</span><span class="sxs-lookup"><span data-stu-id="4993e-129">Add the following code to the `Startup1.Configuration` method:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample1.cs?highlight=3)]

<span data-ttu-id="4993e-130">Ce code ajoute un élément simple d’intergiciel (middleware) au pipeline OWIN, implémenté comme une fonction qui reçoit un **Microsoft.Owin.IOwinContext** instance.</span><span class="sxs-lookup"><span data-stu-id="4993e-130">This code adds a simple piece of middleware to the OWIN pipeline, implemented as a function that receives a **Microsoft.Owin.IOwinContext** instance.</span></span> <span data-ttu-id="4993e-131">Lorsque le serveur reçoit une requête HTTP, le pipeline OWIN appelle l’intergiciel (middleware).</span><span class="sxs-lookup"><span data-stu-id="4993e-131">When the server receives an HTTP request, the OWIN pipeline invokes the middleware.</span></span> <span data-ttu-id="4993e-132">L’intergiciel (middleware) définit le type de contenu pour la réponse et écrit le corps de réponse.</span><span class="sxs-lookup"><span data-stu-id="4993e-132">The middleware sets the content type for the response and writes the response body.</span></span>

> [!NOTE]
> <span data-ttu-id="4993e-133">Le modèle de classe de démarrage OWIN est disponible dans Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="4993e-133">The OWIN Startup class template is available in Visual Studio 2013.</span></span> <span data-ttu-id="4993e-134">Si vous utilisez Visual Studio 2012, ajoutez simplement une classe vide nommée `Startup1`et collez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="4993e-134">If you are using Visual Studio 2012, just add a new empty class named `Startup1`, and paste in the following code:</span></span>


[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample2.cs)]

### <a name="run-the-application"></a><span data-ttu-id="4993e-135">Exécution de l'application</span><span class="sxs-lookup"><span data-stu-id="4993e-135">Run the Application</span></span>

<span data-ttu-id="4993e-136">Appuyez sur F5 pour commencer le débogage.</span><span class="sxs-lookup"><span data-stu-id="4993e-136">Press F5 to begin debugging.</span></span> <span data-ttu-id="4993e-137">Visual Studio ouvre une fenêtre de navigateur pour `http://localhost:*port*/`.</span><span class="sxs-lookup"><span data-stu-id="4993e-137">Visual Studio will open a browser window to `http://localhost:*port*/`.</span></span> <span data-ttu-id="4993e-138">La page doit ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="4993e-138">The page should look like the following:</span></span>

![](getting-started-with-owin-and-katana/_static/image5.png)

## <a name="self-host-owin-in-a-console-application"></a><span data-ttu-id="4993e-139">Auto-hébergement OWIN dans une Application Console</span><span class="sxs-lookup"><span data-stu-id="4993e-139">Self-Host OWIN in a Console Application</span></span>

<span data-ttu-id="4993e-140">Il est facile de convertir cette application à partir de l’hébergement IIS pour l’auto-hébergement d’un processus personnalisé.</span><span class="sxs-lookup"><span data-stu-id="4993e-140">It's easy to convert this application from IIS hosting to self-hosting in a custom process.</span></span> <span data-ttu-id="4993e-141">Avec l’hébergement IIS, IIS sert à la fois le serveur HTTP et que le processus qui hébergent le serveur.</span><span class="sxs-lookup"><span data-stu-id="4993e-141">With IIS hosting, IIS acts as both the HTTP server and as the process that host the sever.</span></span> <span data-ttu-id="4993e-142">Hébergement d’un serveur, votre application crée le processus et utilise le **HttpListener** classe en tant que le serveur HTTP.</span><span class="sxs-lookup"><span data-stu-id="4993e-142">With self-hosting, your application creates the process and uses the **HttpListener** class as the HTTP server.</span></span>

<span data-ttu-id="4993e-143">Dans Visual Studio, créez une nouvelle application console.</span><span class="sxs-lookup"><span data-stu-id="4993e-143">In Visual Studio, create a new console application.</span></span> <span data-ttu-id="4993e-144">Dans la fenêtre de Console du Gestionnaire de Package, tapez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4993e-144">In the Package Manager Console window, type the following command:</span></span>

`Install-Package Microsoft.Owin.SelfHost -Pre`

<span data-ttu-id="4993e-145">Ajouter un `Startup1` classe à partir de la partie 1 de ce didacticiel au projet.</span><span class="sxs-lookup"><span data-stu-id="4993e-145">Add a `Startup1` class from part 1 of this tutorial to the project.</span></span> <span data-ttu-id="4993e-146">Vous n’avez pas besoin de modifier cette classe.</span><span class="sxs-lookup"><span data-stu-id="4993e-146">You don't need to modify this class.</span></span>

<span data-ttu-id="4993e-147">Implémenter l’application `Main` méthode comme suit.</span><span class="sxs-lookup"><span data-stu-id="4993e-147">Implement the application's `Main` method as follows.</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample3.cs)]

<span data-ttu-id="4993e-148">Lorsque vous exécutez l’application console, le serveur commence à écouter pour `http://localhost:9000`.</span><span class="sxs-lookup"><span data-stu-id="4993e-148">When you run the console application, the server starts listening to `http://localhost:9000`.</span></span> <span data-ttu-id="4993e-149">Si vous accédez à cette adresse dans un navigateur web, vous verrez la page « Hello world ».</span><span class="sxs-lookup"><span data-stu-id="4993e-149">If you navigate to this address in a web browser, you will see the "Hello world" page.</span></span>

![](getting-started-with-owin-and-katana/_static/image6.png)

## <a name="add-owin-diagnostics"></a><span data-ttu-id="4993e-150">Ajouter OWIN Diagnostics</span><span class="sxs-lookup"><span data-stu-id="4993e-150">Add OWIN Diagnostics</span></span>

<span data-ttu-id="4993e-151">Le package Microsoft.Owin.Diagnostics contient un intergiciel (middleware) qui intercepte les exceptions non gérées et affiche une page HTML avec les détails de l’erreur.</span><span class="sxs-lookup"><span data-stu-id="4993e-151">The Microsoft.Owin.Diagnostics package contains middleware that catches unhandled exceptions and displays an HTML page with error details.</span></span> <span data-ttu-id="4993e-152">Cette page même manière que la page d’erreurs ASP.NET qui est parfois appelée le «[jaune écran de décès](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)» (YSOD).</span><span class="sxs-lookup"><span data-stu-id="4993e-152">This page functions much like the ASP.NET error page that is sometimes called the "[yellow screen of death](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)" (YSOD).</span></span> <span data-ttu-id="4993e-153">Comme le YSOD, la page d’erreur Katana est utile lors du développement, mais il est conseillé de désactiver le mode de production.</span><span class="sxs-lookup"><span data-stu-id="4993e-153">Like the YSOD, the Katana error page is useful during development, but it's a good practice to disable it in production mode.</span></span>

<span data-ttu-id="4993e-154">Pour installer le package de Diagnostics dans votre projet, tapez la commande suivante dans la fenêtre de Console du Gestionnaire de Package :</span><span class="sxs-lookup"><span data-stu-id="4993e-154">To install the Diagnostics package in your project, type the following command in the Package Manager Console window:</span></span>

`install-package Microsoft.Owin.Diagnostics –Pre`

<span data-ttu-id="4993e-155">Modifier le code dans votre `Startup1.Configuration` méthode comme suit :</span><span class="sxs-lookup"><span data-stu-id="4993e-155">Change the code in your `Startup1.Configuration` method as follows:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample4.cs?highlight=4,9-12)]

<span data-ttu-id="4993e-156">Maintenant utiliser CTRL + F5 pour exécuter l’application sans débogage, afin que Visual Studio n’interrompra pas sur l’exception.</span><span class="sxs-lookup"><span data-stu-id="4993e-156">Now use CTRL+F5 to run the application without debugging, so that Visual Studio will not break on the exception.</span></span> <span data-ttu-id="4993e-157">L’application comporte comme avant, jusqu'à ce que vous accédez à `http://localhost/fail`, à partir de laquelle l’application lève l’exception.</span><span class="sxs-lookup"><span data-stu-id="4993e-157">The application behaves the same as before, until you navigate to `http://localhost/fail`, at which point the application throws the exception.</span></span> <span data-ttu-id="4993e-158">L’intergiciel (middleware) la page d’erreur sera intercepter l’exception et afficher une page HTML avec des informations sur l’erreur.</span><span class="sxs-lookup"><span data-stu-id="4993e-158">The error page middleware will catch the exception and display an HTML page with information about the error.</span></span> <span data-ttu-id="4993e-159">Vous pouvez cliquer sur les onglets pour afficher la pile de chaîne de requête, les cookies, en-tête de demande et les variables d’environnement OWIN.</span><span class="sxs-lookup"><span data-stu-id="4993e-159">You can click the tabs to see the stack, query string, cookies, request header, and OWIN environment variables.</span></span>

![](getting-started-with-owin-and-katana/_static/image7.png)

## <a name="next-steps"></a><span data-ttu-id="4993e-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4993e-160">Next Steps</span></span>

- [<span data-ttu-id="4993e-161">Détection de classe de démarrage OWIN</span><span class="sxs-lookup"><span data-stu-id="4993e-161">OWIN Startup Class Detection</span></span>](owin-startup-class-detection.md)
- [<span data-ttu-id="4993e-162">Permet l’auto-hébergement ASP.NET Web API OWIN</span><span class="sxs-lookup"><span data-stu-id="4993e-162">Use OWIN to Self-Host ASP.NET Web API</span></span>](../../../web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)
- [<span data-ttu-id="4993e-163">Utilisez OWIN pour l’auto-hébergement SignalR</span><span class="sxs-lookup"><span data-stu-id="4993e-163">Use OWIN to Self-Host SignalR</span></span>](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)
