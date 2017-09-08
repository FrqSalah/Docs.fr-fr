---
title: "À l’aide de JavaScriptServices pour la création d’Applications à Page unique"
author: scottaddie
description: "En savoir plus sur les avantages de l’utilisation de JavaScriptServices pour créer une Application de Page unique (SPA) est soutenu par ASP.NET Core."
keywords: ASP.NET Core, angulaire, SPA, JavaScriptServices, SpaServices
ms.author: scaddie
manager: wpickett
ms.date: 08/02/2017
ms.topic: article
ms.assetid: 4b30576b-2718-4c39-9253-a59966747893
ms.technology: aspnet
ms.prod: asp.net-core
uid: client-side/spa-services
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 300e90912a03980d1dcde2edaf34677d80cab136
ms.sourcegitcommit: 0b6c8e6d81d2b3c161cd375036eecbace46a9707
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/11/2017
---
# <a name="using-javascriptservices-for-creating-single-page-applications-with-aspnet-core"></a><span data-ttu-id="0e380-104">À l’aide de JavaScriptServices pour la création d’Applications à Page unique avec ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="0e380-104">Using JavaScriptServices for Creating Single Page Applications with ASP.NET Core</span></span>

<span data-ttu-id="0e380-105">Par [Scott Addie](https://github.com/scottaddie) et [Fiyaz Hasan](http://fiyazhasan.me/)</span><span class="sxs-lookup"><span data-stu-id="0e380-105">By [Scott Addie](https://github.com/scottaddie) and [Fiyaz Hasan](http://fiyazhasan.me/)</span></span>

<span data-ttu-id="0e380-106">Une Application à Page unique (SPA) est un type d’application web en raison de son expérience utilisateur riche inhérente.</span><span class="sxs-lookup"><span data-stu-id="0e380-106">A Single Page Application (SPA) is a popular type of web application due to its inherent rich user experience.</span></span> <span data-ttu-id="0e380-107">Intégration des infrastructures SPA côté client ou les bibliothèques, telles que [angulaire](https://angular.io/) ou [réagir](https://facebook.github.io/react/), avec les infrastructures de côté serveur telles que ASP.NET Core peut être difficile.</span><span class="sxs-lookup"><span data-stu-id="0e380-107">Integrating client-side SPA frameworks or libraries, such as [Angular](https://angular.io/) or [React](https://facebook.github.io/react/), with server-side frameworks like ASP.NET Core can be difficult.</span></span> <span data-ttu-id="0e380-108">[JavaScriptServices](https://github.com/aspnet/JavaScriptServices) a été développé afin de réduire la friction dans le processus d’intégration.</span><span class="sxs-lookup"><span data-stu-id="0e380-108">[JavaScriptServices](https://github.com/aspnet/JavaScriptServices) was developed to reduce friction in the integration process.</span></span> <span data-ttu-id="0e380-109">Il permet à une opération transparente entre les piles de technologie de serveur et de client.</span><span class="sxs-lookup"><span data-stu-id="0e380-109">It enables seamless operation between the different client and server technology stacks.</span></span>

[<span data-ttu-id="0e380-110">Afficher ou télécharger l’exemple de code</span><span class="sxs-lookup"><span data-stu-id="0e380-110">View or download sample code</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/client-side/spa-services/sample)

<a name="what-is-js-services"></a>

## <a name="what-is-javascriptservices"></a><span data-ttu-id="0e380-111">Qu’est JavaScriptServices ?</span><span class="sxs-lookup"><span data-stu-id="0e380-111">What is JavaScriptServices?</span></span>

<span data-ttu-id="0e380-112">JavaScriptServices est une collection de technologies côté client pour ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="0e380-112">JavaScriptServices is a collection of client-side technologies for ASP.NET Core.</span></span> <span data-ttu-id="0e380-113">Son objectif est de positionner ASP.NET Core en tant que plateforme par défaut côté serveur développeurs de génération SPAs.</span><span class="sxs-lookup"><span data-stu-id="0e380-113">Its goal is to position ASP.NET Core as developers' preferred server-side platform for building SPAs.</span></span>

<span data-ttu-id="0e380-114">JavaScriptServices se compose de trois packages NuGet distinctes :</span><span class="sxs-lookup"><span data-stu-id="0e380-114">JavaScriptServices consists of three distinct NuGet packages:</span></span>
* <span data-ttu-id="0e380-115">[Microsoft.AspNetCore.NodeServices](http://www.nuget.org/packages/Microsoft.AspNetCore.NodeServices/) (NodeServices)</span><span class="sxs-lookup"><span data-stu-id="0e380-115">[Microsoft.AspNetCore.NodeServices](http://www.nuget.org/packages/Microsoft.AspNetCore.NodeServices/) (NodeServices)</span></span>
* <span data-ttu-id="0e380-116">[Microsoft.AspNetCore.SpaServices](http://www.nuget.org/packages/Microsoft.AspNetCore.SpaServices/) (SpaServices)</span><span class="sxs-lookup"><span data-stu-id="0e380-116">[Microsoft.AspNetCore.SpaServices](http://www.nuget.org/packages/Microsoft.AspNetCore.SpaServices/) (SpaServices)</span></span>
* <span data-ttu-id="0e380-117">[Microsoft.AspNetCore.SpaTemplates](http://www.nuget.org/packages/Microsoft.AspNetCore.SpaTemplates/) (SpaTemplates)</span><span class="sxs-lookup"><span data-stu-id="0e380-117">[Microsoft.AspNetCore.SpaTemplates](http://www.nuget.org/packages/Microsoft.AspNetCore.SpaTemplates/) (SpaTemplates)</span></span>

<span data-ttu-id="0e380-118">Ces packages sont utiles si vous :</span><span class="sxs-lookup"><span data-stu-id="0e380-118">These packages are useful if you:</span></span>
* <span data-ttu-id="0e380-119">Exécuter JavaScript sur le serveur</span><span class="sxs-lookup"><span data-stu-id="0e380-119">Run JavaScript on the server</span></span>
* <span data-ttu-id="0e380-120">Utiliser une infrastructure SPA ou la bibliothèque</span><span class="sxs-lookup"><span data-stu-id="0e380-120">Use a SPA framework or library</span></span>
* <span data-ttu-id="0e380-121">Générer des composants côté client avec Webpack</span><span class="sxs-lookup"><span data-stu-id="0e380-121">Build client-side assets with Webpack</span></span>

<span data-ttu-id="0e380-122">Une grande partie du focus dans cet article est placée sur l’utilisation du package SpaServices.</span><span class="sxs-lookup"><span data-stu-id="0e380-122">Much of the focus in this article is placed on using the SpaServices package.</span></span>

<a name="what-is-spa-services"></a>

## <a name="what-is-spaservices"></a><span data-ttu-id="0e380-123">Qu’est SpaServices ?</span><span class="sxs-lookup"><span data-stu-id="0e380-123">What is SpaServices?</span></span>

<span data-ttu-id="0e380-124">SpaServices a été créé pour positionner plateforme par défaut côté serveur les développeurs de génération SPAs ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="0e380-124">SpaServices was created to position ASP.NET Core as developers' preferred server-side platform for building SPAs.</span></span> <span data-ttu-id="0e380-125">SpaServices n’est pas requis pour développer des SPAs avec ASP.NET Core, et il ne vous dans une infrastructure client particulier.</span><span class="sxs-lookup"><span data-stu-id="0e380-125">SpaServices is not required to develop SPAs with ASP.NET Core, and it doesn't lock you into a particular client framework.</span></span>

<span data-ttu-id="0e380-126">SpaServices fournit une infrastructure utile telles que :</span><span class="sxs-lookup"><span data-stu-id="0e380-126">SpaServices provides useful infrastructure such as:</span></span>
* [<span data-ttu-id="0e380-127">Pré-rendu du côté serveur</span><span class="sxs-lookup"><span data-stu-id="0e380-127">Server-side prerendering</span></span>](#server-prerendering)
* [<span data-ttu-id="0e380-128">Intergiciel (middleware) de Webpack Dev</span><span class="sxs-lookup"><span data-stu-id="0e380-128">Webpack Dev Middleware</span></span>](#webpack-dev-middleware)
* [<span data-ttu-id="0e380-129">Remplacement d’un Module à chaud</span><span class="sxs-lookup"><span data-stu-id="0e380-129">Hot Module Replacement</span></span>](#hot-module-replacement)
* [<span data-ttu-id="0e380-130">Programmes d’assistance de routage</span><span class="sxs-lookup"><span data-stu-id="0e380-130">Routing helpers</span></span>](#routing-helpers)

<span data-ttu-id="0e380-131">Collectivement, ces composants d’infrastructure améliorent le flux de travail de développement et de l’expérience de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="0e380-131">Collectively, these infrastructure components enhance both the development workflow and the runtime experience.</span></span> <span data-ttu-id="0e380-132">Les composants peuvent être adoptées individuellement.</span><span class="sxs-lookup"><span data-stu-id="0e380-132">The components can be adopted individually.</span></span>

<a name="spa-services-prereqs"></a>

## <a name="prerequisites-for-using-spaservices"></a><span data-ttu-id="0e380-133">Conditions préalables pour l’utilisation de SpaServices</span><span class="sxs-lookup"><span data-stu-id="0e380-133">Prerequisites for using SpaServices</span></span>

<span data-ttu-id="0e380-134">Pour utiliser SpaServices, vous devez installer les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0e380-134">To work with SpaServices, install the following:</span></span>
* <span data-ttu-id="0e380-135">[Node.js](https://nodejs.org/) (version 6 ou version ultérieure) avec npm</span><span class="sxs-lookup"><span data-stu-id="0e380-135">[Node.js](https://nodejs.org/) (version 6 or later) with npm</span></span>
    * <span data-ttu-id="0e380-136">Pour vérifier que ces composants sont installés et sont accessibles, exécutez la commande suivante à partir de la ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="0e380-136">To verify these components are installed and can be found, run the following from the command line:</span></span>

    ```console
    node -v && npm -v
    ```

<span data-ttu-id="0e380-137">Remarque : Si vous effectuez un déploiement vers un site web Azure, vous n’avez à faire quoi que ce soit ici &mdash; Node.js est installé et disponible dans les environnements de serveur.</span><span class="sxs-lookup"><span data-stu-id="0e380-137">Note: If you're deploying to an Azure web site, you don't need to do anything here &mdash; Node.js is installed and available in the server environments.</span></span>

* <span data-ttu-id="0e380-138">[Kit de développement .NET core](https://www.microsoft.com/net/download/core) 1.0 (ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="0e380-138">[.NET Core SDK](https://www.microsoft.com/net/download/core) 1.0 (or later)</span></span>
    * <span data-ttu-id="0e380-139">Si vous êtes sous Windows, cela peut être installé en sélectionnant de 2017 Visual Studio **.NET Core le développement multiplateforme** la charge de travail.</span><span class="sxs-lookup"><span data-stu-id="0e380-139">If you're on Windows, this can be installed by selecting Visual Studio 2017's **.NET Core cross-platform development** workload.</span></span>

* <span data-ttu-id="0e380-140">[Microsoft.AspNetCore.SpaServices](http://www.nuget.org/packages/Microsoft.AspNetCore.SpaServices/) package NuGet</span><span class="sxs-lookup"><span data-stu-id="0e380-140">[Microsoft.AspNetCore.SpaServices](http://www.nuget.org/packages/Microsoft.AspNetCore.SpaServices/) NuGet package</span></span>

<a name="server-prerendering"></a>

## <a name="server-side-prerendering"></a><span data-ttu-id="0e380-141">Pré-rendu du côté serveur</span><span class="sxs-lookup"><span data-stu-id="0e380-141">Server-side prerendering</span></span>

<span data-ttu-id="0e380-142">Une application (également appelé isomorphes) universelle est une application JavaScript capable d’exécuter à la fois sur le serveur et le client.</span><span class="sxs-lookup"><span data-stu-id="0e380-142">A universal (also known as isomorphic) application is a JavaScript application capable of running both on the server and the client.</span></span> <span data-ttu-id="0e380-143">Angulaire, réagissent et autres infrastructures répandues ; fournit une plateforme universelle pour ce style de développement d’application.</span><span class="sxs-lookup"><span data-stu-id="0e380-143">Angular, React, and other popular frameworks provide a universal platform for this application development style.</span></span> <span data-ttu-id="0e380-144">L’idée est d’abord restituer les composants framework sur le serveur via Node.js, puis de déléguer davantage d’exécution pour le client.</span><span class="sxs-lookup"><span data-stu-id="0e380-144">The idea is to first render the framework components on the server via Node.js, and then delegate further execution to the client.</span></span>

<span data-ttu-id="0e380-145">ASP.NET Core [programmes d’assistance de balise](xref:mvc/views/tag-helpers/intro) fournie par SpaServices simplifier l’implémentation de pré-rendu du côté serveur en appelant les fonctions JavaScript sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="0e380-145">ASP.NET Core [Tag Helpers](xref:mvc/views/tag-helpers/intro) provided by SpaServices simplify the implementation of server-side prerendering by invoking the JavaScript functions on the server.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="0e380-146">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="0e380-146">Prerequisites</span></span>

<span data-ttu-id="0e380-147">Installer les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0e380-147">Install the following:</span></span>
* <span data-ttu-id="0e380-148">[ASPNET-pré-rendu](https://www.npmjs.com/package/aspnet-prerendering) package npm :</span><span class="sxs-lookup"><span data-stu-id="0e380-148">[aspnet-prerendering](https://www.npmjs.com/package/aspnet-prerendering) npm package:</span></span>

    ```console
    npm i -S aspnet-prerendering
    ```

### <a name="configuration"></a><span data-ttu-id="0e380-149">Configuration</span><span class="sxs-lookup"><span data-stu-id="0e380-149">Configuration</span></span>

<span data-ttu-id="0e380-150">Les programmes d’assistance de balise deviennent détectables via l’inscription de l’espace de noms du projet *_ViewImports.cshtml* fichier :</span><span class="sxs-lookup"><span data-stu-id="0e380-150">The Tag Helpers are made discoverable via namespace registration in the project's *_ViewImports.cshtml* file:</span></span>

<span data-ttu-id="0e380-151">[!code-csharp[Main](../client-side/spa-services/sample/SpaServicesSampleApp/Views/_ViewImports.cshtml?highlight=3)]</span><span class="sxs-lookup"><span data-stu-id="0e380-151">[!code-csharp[Main](../client-side/spa-services/sample/SpaServicesSampleApp/Views/_ViewImports.cshtml?highlight=3)]</span></span>

<span data-ttu-id="0e380-152">Ces programmes d’assistance de balise abstraire les complexités de communiquer directement avec les API de bas niveau en utilisant une syntaxe de type HTML à l’intérieur de la vue Razor :</span><span class="sxs-lookup"><span data-stu-id="0e380-152">These Tag Helpers abstract away the intricacies of communicating directly with low-level APIs by leveraging an HTML-like syntax inside the Razor view:</span></span>

<span data-ttu-id="0e380-153">[!code-html[Main](../client-side/spa-services/sample/SpaServicesSampleApp/Views/Home/Index.cshtml?range=5)]</span><span class="sxs-lookup"><span data-stu-id="0e380-153">[!code-html[Main](../client-side/spa-services/sample/SpaServicesSampleApp/Views/Home/Index.cshtml?range=5)]</span></span>

### <a name="the-asp-prerender-module-tag-helper"></a><span data-ttu-id="0e380-154">Le `asp-prerender-module` d’assistance de balise</span><span class="sxs-lookup"><span data-stu-id="0e380-154">The `asp-prerender-module` Tag Helper</span></span>

<span data-ttu-id="0e380-155">Le `asp-prerender-module` s’exécute le programme d’assistance de balise, utilisés dans l’exemple de code précédent, *ClientApp/dist/main-server.js* sur le serveur via Node.js.</span><span class="sxs-lookup"><span data-stu-id="0e380-155">The `asp-prerender-module` Tag Helper, used in the preceding code example, executes *ClientApp/dist/main-server.js* on the server via Node.js.</span></span> <span data-ttu-id="0e380-156">Pour de clarté, *principal-server.js* fichier est un artefact de la tâche de transpilation TypeScript et JavaScript dans les [Webpack](http://webpack.github.io/) processus de génération.</span><span class="sxs-lookup"><span data-stu-id="0e380-156">For clarity's sake, *main-server.js* file is an artifact of the TypeScript-to-JavaScript transpilation task in the [Webpack](http://webpack.github.io/) build process.</span></span> <span data-ttu-id="0e380-157">Webpack définit un alias de point d’entrée de `main-server`; et, le parcours du graphique de dépendance pour cet alias où commence la *démarrage/ClientApp-server.ts* fichier :</span><span class="sxs-lookup"><span data-stu-id="0e380-157">Webpack defines an entry point alias of `main-server`; and, traversal of the dependency graph for this alias begins at the *ClientApp/boot-server.ts* file:</span></span>

<span data-ttu-id="0e380-158">[!code-javascript[Main](../client-side/spa-services/sample/SpaServicesSampleApp/webpack.config.js?range=53)]</span><span class="sxs-lookup"><span data-stu-id="0e380-158">[!code-javascript[Main](../client-side/spa-services/sample/SpaServicesSampleApp/webpack.config.js?range=53)]</span></span>

<span data-ttu-id="0e380-159">Dans l’exemple suivant angulaire, le *démarrage/ClientApp-server.ts* fichier utilise le `createServerRenderer` (fonction) et `RenderResult` le type de la `aspnet-prerendering` package npm pour configurer le rendu du serveur via Node.js.</span><span class="sxs-lookup"><span data-stu-id="0e380-159">In the following Angular example, the *ClientApp/boot-server.ts* file utilizes the `createServerRenderer` function and `RenderResult` type of the `aspnet-prerendering` npm package to configure server rendering via Node.js.</span></span> <span data-ttu-id="0e380-160">Le balisage HTML destiné à rendu côté serveur est passé à un appel de fonction de résolution, qui est encapsulé dans un script JavaScript fortement typée `Promise` objet.</span><span class="sxs-lookup"><span data-stu-id="0e380-160">The HTML markup destined for server-side rendering is passed to a resolve function call, which is wrapped in a strongly-typed JavaScript `Promise` object.</span></span> <span data-ttu-id="0e380-161">Le `Promise` importance de l’objet est qu’elle fournit en mode asynchrone le balisage HTML pour la page pour l’injection dans l’élément d’espace réservé du DOM.</span><span class="sxs-lookup"><span data-stu-id="0e380-161">The `Promise` object's significance is that it asynchronously supplies the HTML markup to the page for injection in the DOM's placeholder element.</span></span>

<span data-ttu-id="0e380-162">[!code-typescript[Main](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/boot-server.ts?range=6,10-34,79-)]</span><span class="sxs-lookup"><span data-stu-id="0e380-162">[!code-typescript[Main](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/boot-server.ts?range=6,10-34,79-)]</span></span>

### <a name="the-asp-prerender-data-tag-helper"></a><span data-ttu-id="0e380-163">Le `asp-prerender-data` d’assistance de balise</span><span class="sxs-lookup"><span data-stu-id="0e380-163">The `asp-prerender-data` Tag Helper</span></span>

<span data-ttu-id="0e380-164">Associée à la `asp-prerender-module` assistance de balise, le `asp-prerender-data` application d’assistance de balise peut servir à transmettre des informations contextuelles à partir de la vue Razor pour le code JavaScript côté serveur.</span><span class="sxs-lookup"><span data-stu-id="0e380-164">When coupled with the `asp-prerender-module` Tag Helper, the `asp-prerender-data` Tag Helper can be used to pass contextual information from the Razor view to the server-side JavaScript.</span></span> <span data-ttu-id="0e380-165">Par exemple, le balisage suivant passe des données utilisateur à la `main-server` module :</span><span class="sxs-lookup"><span data-stu-id="0e380-165">For example, the following markup passes user data to the `main-server` module:</span></span>

<span data-ttu-id="0e380-166">[!code-html[Main](../client-side/spa-services/sample/SpaServicesSampleApp/Views/Home/Index.cshtml?range=9-12)]</span><span class="sxs-lookup"><span data-stu-id="0e380-166">[!code-html[Main](../client-side/spa-services/sample/SpaServicesSampleApp/Views/Home/Index.cshtml?range=9-12)]</span></span>

<span data-ttu-id="0e380-167">Les données reçues `UserName` argument est sérialisé en utilisant le sérialiseur JSON intégré et est stocké dans le `params.data` objet.</span><span class="sxs-lookup"><span data-stu-id="0e380-167">The received `UserName` argument is serialized using the built-in JSON serializer and is stored in the `params.data` object.</span></span> <span data-ttu-id="0e380-168">Dans l’exemple suivant angulaire, les données sont utilisées pour construire un message d’accueil personnalisé dans un `h1` élément :</span><span class="sxs-lookup"><span data-stu-id="0e380-168">In the following Angular example, the data is used to construct a personalized greeting within an `h1` element:</span></span>

<span data-ttu-id="0e380-169">[!code-typescript[Main](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/boot-server.ts?range=6,10-21,38-52,79-)]</span><span class="sxs-lookup"><span data-stu-id="0e380-169">[!code-typescript[Main](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/boot-server.ts?range=6,10-21,38-52,79-)]</span></span>

<span data-ttu-id="0e380-170">Remarque : Les noms de propriété passés dans les programmes d’assistance de balise sont représentés par **PascalCase** notation.</span><span class="sxs-lookup"><span data-stu-id="0e380-170">Note: Property names passed in Tag Helpers are represented with **PascalCase** notation.</span></span> <span data-ttu-id="0e380-171">Comparez cela à JavaScript, où les mêmes noms de propriété sont représentés par **camelCase**.</span><span class="sxs-lookup"><span data-stu-id="0e380-171">Contrast that to JavaScript, where the same property names are represented with **camelCase**.</span></span> <span data-ttu-id="0e380-172">La configuration de sérialisation JSON par défaut est responsable de cette différence.</span><span class="sxs-lookup"><span data-stu-id="0e380-172">The default JSON serialization configuration is responsible for this difference.</span></span>

<span data-ttu-id="0e380-173">Pour développer l’exemple de code précédent, données peuvent être passées à partir du serveur à la vue par HYDRATATION le `globals` cette propriété est fournie pour le `resolve` fonction :</span><span class="sxs-lookup"><span data-stu-id="0e380-173">To expand upon the preceding code example, data can be passed from the server to the view by hydrating the `globals` property provided to the `resolve` function:</span></span>

<span data-ttu-id="0e380-174">[!code-typescript[Main](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/boot-server.ts?range=6,10-21,57-77,79-)]</span><span class="sxs-lookup"><span data-stu-id="0e380-174">[!code-typescript[Main](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/boot-server.ts?range=6,10-21,57-77,79-)]</span></span>

<span data-ttu-id="0e380-175">Le `postList` tableau défini à l’intérieur de la `globals` objet est attaché au navigateur global `window` objet.</span><span class="sxs-lookup"><span data-stu-id="0e380-175">The `postList` array defined inside the `globals` object is attached to the browser's global `window` object.</span></span> <span data-ttu-id="0e380-176">Cette levée variable à portée globale d’élimine la duplication des efforts, notamment en ce qui concerne le chargement des données de mêmes qu’une seule fois sur le serveur et de nouveau sur le client.</span><span class="sxs-lookup"><span data-stu-id="0e380-176">This variable hoisting to global scope eliminates duplication of effort, particularly as it pertains to loading the same data once on the server and again on the client.</span></span>

![variable globale de postList attaché à un objet de fenêtre](spa-services/_static/global_variable.png)

<a name="webpack-dev-middleware"></a>

## <a name="webpack-dev-middleware"></a><span data-ttu-id="0e380-178">Intergiciel (middleware) de Webpack Dev</span><span class="sxs-lookup"><span data-stu-id="0e380-178">Webpack Dev Middleware</span></span>

<span data-ttu-id="0e380-179">[Intergiciel (middleware) de Webpack Dev](https://webpack.github.io/docs/webpack-dev-middleware.html) introduit un flux de travail de développement simplifié par laquelle Webpack génère les ressources à la demande.</span><span class="sxs-lookup"><span data-stu-id="0e380-179">[Webpack Dev Middleware](https://webpack.github.io/docs/webpack-dev-middleware.html) introduces a streamlined development workflow whereby Webpack builds resources on demand.</span></span> <span data-ttu-id="0e380-180">L’intergiciel (middleware) compile automatiquement et fournit des ressources de côté client lorsqu’une page est rechargée dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="0e380-180">The middleware automatically compiles and serves client-side resources when a page is reloaded in the browser.</span></span> <span data-ttu-id="0e380-181">L’autre approche consiste à appeler manuellement des Webpack via un script de génération du projet npm quand une dépendance tierce ou le code personnalisé change.</span><span class="sxs-lookup"><span data-stu-id="0e380-181">The alternate approach is to manually invoke Webpack via the project's npm build script when a third-party dependency or the custom code changes.</span></span> <span data-ttu-id="0e380-182">Un npm générer un script le *package.json* fichier est indiqué dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="0e380-182">An npm build script in the *package.json* file is shown in the following example:</span></span>

<span data-ttu-id="0e380-183">[!code-json[Main](../client-side/spa-services/sample/SpaServicesSampleApp/package.json?range=5)]</span><span class="sxs-lookup"><span data-stu-id="0e380-183">[!code-json[Main](../client-side/spa-services/sample/SpaServicesSampleApp/package.json?range=5)]</span></span>

### <a name="prerequisites"></a><span data-ttu-id="0e380-184">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="0e380-184">Prerequisites</span></span>

<span data-ttu-id="0e380-185">Installer les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0e380-185">Install the following:</span></span>
* <span data-ttu-id="0e380-186">[ASPNET-webpack](https://www.npmjs.com/package/aspnet-webpack) package npm :</span><span class="sxs-lookup"><span data-stu-id="0e380-186">[aspnet-webpack](https://www.npmjs.com/package/aspnet-webpack) npm package:</span></span>

    ```console
    npm i -D aspnet-webpack
    ```

### <a name="configuration"></a><span data-ttu-id="0e380-187">Configuration</span><span class="sxs-lookup"><span data-stu-id="0e380-187">Configuration</span></span>

<span data-ttu-id="0e380-188">Intergiciel (middleware) de Webpack Dev est inscrit dans le pipeline de demande HTTP via le code suivant dans le *Startup.cs* du fichier `Configure` méthode :</span><span class="sxs-lookup"><span data-stu-id="0e380-188">Webpack Dev Middleware is registered into the HTTP request pipeline via the following code in the *Startup.cs* file's `Configure` method:</span></span>

<span data-ttu-id="0e380-189">[!code-csharp[Main](../client-side/spa-services/sample/SpaServicesSampleApp/Startup.cs?name=webpack-middleware-registration&highlight=4)]</span><span class="sxs-lookup"><span data-stu-id="0e380-189">[!code-csharp[Main](../client-side/spa-services/sample/SpaServicesSampleApp/Startup.cs?name=webpack-middleware-registration&highlight=4)]</span></span>

<span data-ttu-id="0e380-190">Le `UseWebpackDevMiddleware` méthode d’extension doit être appelée avant [l’inscription d’hébergement de fichiers statiques](xref:fundamentals/static-files) via la `UseStaticFiles` méthode d’extension.</span><span class="sxs-lookup"><span data-stu-id="0e380-190">The `UseWebpackDevMiddleware` extension method must be called before [registering static file hosting](xref:fundamentals/static-files) via the `UseStaticFiles` extension method.</span></span> <span data-ttu-id="0e380-191">Pour des raisons de sécurité, inscrire l’intergiciel (middleware) uniquement lorsque l’application s’exécute en mode de développement.</span><span class="sxs-lookup"><span data-stu-id="0e380-191">For security reasons, register the middleware only when the app runs in development mode.</span></span>

<span data-ttu-id="0e380-192">Le *webpack.config.js* du fichier `output.publicPath` propriété indique à l’intergiciel (middleware) pour surveiller le `dist` dossier pour les modifications :</span><span class="sxs-lookup"><span data-stu-id="0e380-192">The *webpack.config.js* file's `output.publicPath` property tells the middleware to watch the `dist` folder for changes:</span></span>

<span data-ttu-id="0e380-193">[!code-javascript[Main](../client-side/spa-services/sample/SpaServicesSampleApp/webpack.config.js?range=6,13-16)]</span><span class="sxs-lookup"><span data-stu-id="0e380-193">[!code-javascript[Main](../client-side/spa-services/sample/SpaServicesSampleApp/webpack.config.js?range=6,13-16)]</span></span>

<a name="hot-module-replacement"></a>

## <a name="hot-module-replacement"></a><span data-ttu-id="0e380-194">Remplacement d’un Module à chaud</span><span class="sxs-lookup"><span data-stu-id="0e380-194">Hot Module Replacement</span></span>

<span data-ttu-id="0e380-195">Pensez à Webpack [remplacement d’un Module à chaud](https://webpack.github.io/docs/hot-module-replacement-with-webpack.html) fonctionnalité (HMR) comme une évolution du [Webpack Dev Middleware](#webpack-dev-middleware).</span><span class="sxs-lookup"><span data-stu-id="0e380-195">Think of Webpack's [Hot Module Replacement](https://webpack.github.io/docs/hot-module-replacement-with-webpack.html) (HMR) feature as an evolution of [Webpack Dev Middleware](#webpack-dev-middleware).</span></span> <span data-ttu-id="0e380-196">HMR présente les mêmes avantages, mais il simplifie davantage le flux de travail de développement en mettant à jour automatiquement de contenu de la page après la compilation des modifications.</span><span class="sxs-lookup"><span data-stu-id="0e380-196">HMR introduces all the same benefits, but it further streamlines the development workflow by automatically updating page content after compiling the changes.</span></span> <span data-ttu-id="0e380-197">Ne pas confondre avec une actualisation du navigateur, ce qui entraînerait une interférence avec l’état en mémoire actuel et la session de débogage de SPA.</span><span class="sxs-lookup"><span data-stu-id="0e380-197">Don't confuse this with a refresh of the browser, which would interfere with the current in-memory state and debugging session of the SPA.</span></span> <span data-ttu-id="0e380-198">Il existe un lien direct entre le service de l’intergiciel (middleware) de Webpack développement et le navigateur, ce qui signifie que les modifications sont ~ simplement un autre mot interdit ~ envoyée au navigateur.</span><span class="sxs-lookup"><span data-stu-id="0e380-198">There is a live link between the Webpack Dev Middleware service and the browser, which means changes are ~simply another banned word~ pushed to the browser.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="0e380-199">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="0e380-199">Prerequisites</span></span>

<span data-ttu-id="0e380-200">Installer les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0e380-200">Install the following:</span></span>
* <span data-ttu-id="0e380-201">[intergiciel Webpack à chaud](https://www.npmjs.com/package/webpack-hot-middleware) package npm :</span><span class="sxs-lookup"><span data-stu-id="0e380-201">[webpack-hot-middleware](https://www.npmjs.com/package/webpack-hot-middleware) npm package:</span></span>

    ```console
    npm i -D webpack-hot-middleware
    ```

### <a name="configuration"></a><span data-ttu-id="0e380-202">Configuration</span><span class="sxs-lookup"><span data-stu-id="0e380-202">Configuration</span></span>

<span data-ttu-id="0e380-203">Le composant HMR doit être inscrit dans le pipeline de demande HTTP de MVC dans le `Configure` méthode :</span><span class="sxs-lookup"><span data-stu-id="0e380-203">The HMR component must be registered into MVC's HTTP request pipeline in the `Configure` method:</span></span>

```csharp
app.UseWebpackDevMiddleware(new WebpackDevMiddlewareOptions {
    HotModuleReplacement = true
});
```

<span data-ttu-id="0e380-204">En tant qu’était le cas avec [Webpack Dev Middleware](#webpack-dev-middleware), le `UseWebpackDevMiddleware` méthode d’extension doit être appelée avant la `UseStaticFiles` méthode d’extension.</span><span class="sxs-lookup"><span data-stu-id="0e380-204">As was true with [Webpack Dev Middleware](#webpack-dev-middleware), the `UseWebpackDevMiddleware` extension method must be called before the `UseStaticFiles` extension method.</span></span> <span data-ttu-id="0e380-205">Pour des raisons de sécurité, inscrire l’intergiciel (middleware) uniquement lorsque l’application s’exécute en mode de développement.</span><span class="sxs-lookup"><span data-stu-id="0e380-205">For security reasons, register the middleware only when the app runs in development mode.</span></span>

<span data-ttu-id="0e380-206">Le *webpack.config.js* fichier doit définir un `plugins` de tableau, même si celui-ci est laissé vide :</span><span class="sxs-lookup"><span data-stu-id="0e380-206">The *webpack.config.js* file must define a `plugins` array, even if it's left empty:</span></span>

<span data-ttu-id="0e380-207">[!code-javascript[Main](../client-side/spa-services/sample/SpaServicesSampleApp/webpack.config.js?range=6,25)]</span><span class="sxs-lookup"><span data-stu-id="0e380-207">[!code-javascript[Main](../client-side/spa-services/sample/SpaServicesSampleApp/webpack.config.js?range=6,25)]</span></span>

<span data-ttu-id="0e380-208">Après le chargement de l’application dans le navigateur, onglet de la Console des outils de développement fournit la confirmation de l’activation de HMR :</span><span class="sxs-lookup"><span data-stu-id="0e380-208">After loading the app in the browser, the developer tools' Console tab provides confirmation of HMR activation:</span></span>

![Message de connexion de remplacement d’un Module à chaud](spa-services/_static/hmr_connected.png)

<a name="routing-helpers"></a>

## <a name="routing-helpers"></a><span data-ttu-id="0e380-210">Programmes d’assistance de routage</span><span class="sxs-lookup"><span data-stu-id="0e380-210">Routing helpers</span></span>

<span data-ttu-id="0e380-211">Dans la plupart des SPAs basée sur ASP.NET Core, vous souhaiterez routage côté client en plus du routage du côté serveur.</span><span class="sxs-lookup"><span data-stu-id="0e380-211">In most ASP.NET Core-based SPAs, you'll want client-side routing in addition to server-side routing.</span></span> <span data-ttu-id="0e380-212">Les systèmes de routage SPA et MVC peuvent travailler indépendamment sans interférence.</span><span class="sxs-lookup"><span data-stu-id="0e380-212">The SPA and MVC routing systems can work independently without interference.</span></span> <span data-ttu-id="0e380-213">Il existe, toutefois, un bord cas posant des défis : identification des réponses HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="0e380-213">There is, however, one edge case posing challenges: identifying 404 HTTP responses.</span></span>

<span data-ttu-id="0e380-214">Considérez le scénario dans lequel un itinéraire sans extension de `/some/page` est utilisé.</span><span class="sxs-lookup"><span data-stu-id="0e380-214">Consider the scenario in which an extensionless route of `/some/page` is used.</span></span> <span data-ttu-id="0e380-215">Supposons que la demande n’à la correspondance un itinéraire côté serveur, mais son modèle ne correspond pas à un itinéraire côté client.</span><span class="sxs-lookup"><span data-stu-id="0e380-215">Assume the request doesn't pattern-match a server-side route, but its pattern does match a client-side route.</span></span> <span data-ttu-id="0e380-216">Examinons à présent une demande entrante de `/images/user-512.png`, qui généralement s’attend à trouver un fichier image sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="0e380-216">Now consider an incoming request for `/images/user-512.png`, which generally expects to find an image file on the server.</span></span> <span data-ttu-id="0e380-217">Si ce chemin d’accès de la ressource demandée ne correspond pas à un itinéraire de côté serveur ou d’un fichier statique, il est peu probable que l’application côté client serait la gérer, il est souvent préférable de retourner un code d’état HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="0e380-217">If that requested resource path doesn't match any server-side route or static file, it's unlikely that the client-side application would handle it — you generally want to return a 404 HTTP status code.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="0e380-218">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="0e380-218">Prerequisites</span></span>

<span data-ttu-id="0e380-219">Installer les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0e380-219">Install the following:</span></span>
* <span data-ttu-id="0e380-220">Le package npm de routage côté client.</span><span class="sxs-lookup"><span data-stu-id="0e380-220">The client-side routing npm package.</span></span> <span data-ttu-id="0e380-221">À l’aide d’angulaire par exemple :</span><span class="sxs-lookup"><span data-stu-id="0e380-221">Using Angular as an example:</span></span>

    ```console
    npm i -S @angular/router
    ```

### <a name="configuration"></a><span data-ttu-id="0e380-222">Configuration</span><span class="sxs-lookup"><span data-stu-id="0e380-222">Configuration</span></span>

<span data-ttu-id="0e380-223">Une méthode d’extension nommée `MapSpaFallbackRoute` est utilisé dans le `Configure` méthode :</span><span class="sxs-lookup"><span data-stu-id="0e380-223">An extension method named `MapSpaFallbackRoute` is used in the `Configure` method:</span></span>

<span data-ttu-id="0e380-224">[!code-csharp[Main](../client-side/spa-services/sample/SpaServicesSampleApp/Startup.cs?name=mvc-routing-table&highlight=7-9)]</span><span class="sxs-lookup"><span data-stu-id="0e380-224">[!code-csharp[Main](../client-side/spa-services/sample/SpaServicesSampleApp/Startup.cs?name=mvc-routing-table&highlight=7-9)]</span></span>

<span data-ttu-id="0e380-225">Conseil : Les itinéraires sont évaluées dans l’ordre dans lequel ils sont configurés.</span><span class="sxs-lookup"><span data-stu-id="0e380-225">Tip: Routes are evaluated in the order in which they're configured.</span></span> <span data-ttu-id="0e380-226">Par conséquent, le `default` itinéraire dans l’exemple de code précédent est utilisé pour la recherche de correspondance.</span><span class="sxs-lookup"><span data-stu-id="0e380-226">Consequently, the `default` route in the preceding code example is used first for pattern matching.</span></span>

<a name="new-project-creation"></a>

## <a name="creating-a-new-project"></a><span data-ttu-id="0e380-227">Création d’un projet</span><span class="sxs-lookup"><span data-stu-id="0e380-227">Creating a new project</span></span>

<span data-ttu-id="0e380-228">JavaScriptServices fournit des modèles d’application préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="0e380-228">JavaScriptServices provides pre-configured application templates.</span></span> <span data-ttu-id="0e380-229">SpaServices est utilisé dans ces modèles, en association avec différentes infrastructures et bibliothèques, telles qu’angulaire, Aurelia, Knockout, réagissent et la Vue.</span><span class="sxs-lookup"><span data-stu-id="0e380-229">SpaServices is used in these templates, in conjunction with different frameworks and libraries such as Angular, Aurelia, Knockout, React, and Vue.</span></span>

<span data-ttu-id="0e380-230">Ces modèles peuvent être installés via l’interface de ligne de base .NET en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0e380-230">These templates can be installed via the .NET Core CLI by running the following command:</span></span>

```console
dotnet new --install Microsoft.AspNetCore.SpaTemplates::*
```

<span data-ttu-id="0e380-231">Une liste des modèles SPA disponibles s’affiche :</span><span class="sxs-lookup"><span data-stu-id="0e380-231">A list of available SPA templates is displayed:</span></span>

| <span data-ttu-id="0e380-232">Modèles</span><span class="sxs-lookup"><span data-stu-id="0e380-232">Templates</span></span>                                 | <span data-ttu-id="0e380-233">Nom court</span><span class="sxs-lookup"><span data-stu-id="0e380-233">Short Name</span></span> | <span data-ttu-id="0e380-234">Langue</span><span class="sxs-lookup"><span data-stu-id="0e380-234">Language</span></span> | <span data-ttu-id="0e380-235">Balises</span><span class="sxs-lookup"><span data-stu-id="0e380-235">Tags</span></span>        |
|:------------------------------------------|:-----------|:---------|:------------|
| <span data-ttu-id="0e380-236">MVC ASP.NET Core avec angulaire</span><span class="sxs-lookup"><span data-stu-id="0e380-236">MVC ASP.NET Core with Angular</span></span>             | <span data-ttu-id="0e380-237">angular</span><span class="sxs-lookup"><span data-stu-id="0e380-237">angular</span></span>    | <span data-ttu-id="0e380-238">[C#]</span><span class="sxs-lookup"><span data-stu-id="0e380-238">[C#]</span></span>     | <span data-ttu-id="0e380-239">MVC/Web/SPA</span><span class="sxs-lookup"><span data-stu-id="0e380-239">Web/MVC/SPA</span></span> |
| <span data-ttu-id="0e380-240">MVC ASP.NET Core avec Aurelia</span><span class="sxs-lookup"><span data-stu-id="0e380-240">MVC ASP.NET Core with Aurelia</span></span>             | <span data-ttu-id="0e380-241">aurelia</span><span class="sxs-lookup"><span data-stu-id="0e380-241">aurelia</span></span>    | <span data-ttu-id="0e380-242">[C#]</span><span class="sxs-lookup"><span data-stu-id="0e380-242">[C#]</span></span>     | <span data-ttu-id="0e380-243">MVC/Web/SPA</span><span class="sxs-lookup"><span data-stu-id="0e380-243">Web/MVC/SPA</span></span> |
| <span data-ttu-id="0e380-244">MVC ASP.NET Core avec Knockout.js</span><span class="sxs-lookup"><span data-stu-id="0e380-244">MVC ASP.NET Core with Knockout.js</span></span>         | <span data-ttu-id="0e380-245">Knockout</span><span class="sxs-lookup"><span data-stu-id="0e380-245">knockout</span></span>   | <span data-ttu-id="0e380-246">[C#]</span><span class="sxs-lookup"><span data-stu-id="0e380-246">[C#]</span></span>     | <span data-ttu-id="0e380-247">MVC/Web/SPA</span><span class="sxs-lookup"><span data-stu-id="0e380-247">Web/MVC/SPA</span></span> |
| <span data-ttu-id="0e380-248">MVC ASP.NET Core avec React.js</span><span class="sxs-lookup"><span data-stu-id="0e380-248">MVC ASP.NET Core with React.js</span></span>            | <span data-ttu-id="0e380-249">react</span><span class="sxs-lookup"><span data-stu-id="0e380-249">react</span></span>      | <span data-ttu-id="0e380-250">[C#]</span><span class="sxs-lookup"><span data-stu-id="0e380-250">[C#]</span></span>     | <span data-ttu-id="0e380-251">MVC/Web/SPA</span><span class="sxs-lookup"><span data-stu-id="0e380-251">Web/MVC/SPA</span></span> |
| <span data-ttu-id="0e380-252">MVC ASP.NET Core avec React.js et réédition</span><span class="sxs-lookup"><span data-stu-id="0e380-252">MVC ASP.NET Core with React.js and Redux</span></span>  | <span data-ttu-id="0e380-253">reactredux</span><span class="sxs-lookup"><span data-stu-id="0e380-253">reactredux</span></span> | <span data-ttu-id="0e380-254">[C#]</span><span class="sxs-lookup"><span data-stu-id="0e380-254">[C#]</span></span>     | <span data-ttu-id="0e380-255">MVC/Web/SPA</span><span class="sxs-lookup"><span data-stu-id="0e380-255">Web/MVC/SPA</span></span> |
| <span data-ttu-id="0e380-256">MVC ASP.NET Core avec Vue.js</span><span class="sxs-lookup"><span data-stu-id="0e380-256">MVC ASP.NET Core with Vue.js</span></span>              | <span data-ttu-id="0e380-257">vue</span><span class="sxs-lookup"><span data-stu-id="0e380-257">vue</span></span>        | <span data-ttu-id="0e380-258">[C#]</span><span class="sxs-lookup"><span data-stu-id="0e380-258">[C#]</span></span>     | <span data-ttu-id="0e380-259">MVC/Web/SPA</span><span class="sxs-lookup"><span data-stu-id="0e380-259">Web/MVC/SPA</span></span> | 

<span data-ttu-id="0e380-260">Pour créer un nouveau projet à l’aide d’un des modèles de SPA, incluez le **nom court** du modèle dans le `dotnet new` commande.</span><span class="sxs-lookup"><span data-stu-id="0e380-260">To create a new project using one of the SPA templates, include the **Short Name** of the template in the `dotnet new` command.</span></span> <span data-ttu-id="0e380-261">La commande suivante crée une application angulaire avec ASP.NET MVC de base configuré pour le côté serveur :</span><span class="sxs-lookup"><span data-stu-id="0e380-261">The following command creates an Angular application with ASP.NET Core MVC configured for the server side:</span></span>

```console
dotnet new angular
```

<a name="runtime-config-mode"></a>

### <a name="set-the-runtime-configuration-mode"></a><span data-ttu-id="0e380-262">Définir le mode de configuration du runtime</span><span class="sxs-lookup"><span data-stu-id="0e380-262">Set the runtime configuration mode</span></span>

<span data-ttu-id="0e380-263">Il existe deux modes de configuration principal d’exécution :</span><span class="sxs-lookup"><span data-stu-id="0e380-263">Two primary runtime configuration modes exist:</span></span>
* <span data-ttu-id="0e380-264">**Développement**:</span><span class="sxs-lookup"><span data-stu-id="0e380-264">**Development**:</span></span>
    * <span data-ttu-id="0e380-265">Inclut des mappages de sources pour faciliter le débogage.</span><span class="sxs-lookup"><span data-stu-id="0e380-265">Includes source maps to ease debugging.</span></span>
    * <span data-ttu-id="0e380-266">N’Optimisez le code côté client pour les performances.</span><span class="sxs-lookup"><span data-stu-id="0e380-266">Doesn't optimize the client-side code for performance.</span></span>
* <span data-ttu-id="0e380-267">**Production**:</span><span class="sxs-lookup"><span data-stu-id="0e380-267">**Production**:</span></span>
    * <span data-ttu-id="0e380-268">Exclut les mappages de sources.</span><span class="sxs-lookup"><span data-stu-id="0e380-268">Excludes source maps.</span></span>
    * <span data-ttu-id="0e380-269">Optimise le code côté client via une minimisation & de regroupement.</span><span class="sxs-lookup"><span data-stu-id="0e380-269">Optimizes the client-side code via bundling & minification.</span></span>

<span data-ttu-id="0e380-270">ASP.NET Core utilise une variable d’environnement nommée `ASPNETCORE_ENVIRONMENT` pour stocker le mode de configuration.</span><span class="sxs-lookup"><span data-stu-id="0e380-270">ASP.NET Core uses an environment variable named `ASPNETCORE_ENVIRONMENT` to store the configuration mode.</span></span> <span data-ttu-id="0e380-271">Consultez  **[définition de l’environnement](xref:fundamentals/environments#setting-the-environment)**  pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="0e380-271">See **[Setting the environment](xref:fundamentals/environments#setting-the-environment)** for more information.</span></span>

### <a name="running-with-net-core-cli"></a><span data-ttu-id="0e380-272">En cours d’exécution avec le .NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="0e380-272">Running with .NET Core CLI</span></span>

<span data-ttu-id="0e380-273">Restaurer les packages npm NuGet requis en exécutant la commande suivante à la racine du projet :</span><span class="sxs-lookup"><span data-stu-id="0e380-273">Restore the required NuGet and npm packages by running the following command at the project root:</span></span>

```console
dotnet restore && npm i
```

<span data-ttu-id="0e380-274">Générer et exécuter l’application :</span><span class="sxs-lookup"><span data-stu-id="0e380-274">Build and run the application:</span></span>

```console
dotnet run
```

<span data-ttu-id="0e380-275">Démarrage de l’application sur localhost conformément à la [mode de configuration d’exécution](#runtime-config-mode).</span><span class="sxs-lookup"><span data-stu-id="0e380-275">The application starts on localhost according to the [runtime configuration mode](#runtime-config-mode).</span></span> <span data-ttu-id="0e380-276">Navigation vers `http://localhost:5000` dans le navigateur affiche la page d’accueil.</span><span class="sxs-lookup"><span data-stu-id="0e380-276">Navigating to `http://localhost:5000` in the browser displays the landing page.</span></span>

### <a name="running-with-visual-studio-2017"></a><span data-ttu-id="0e380-277">En cours d’exécution avec Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="0e380-277">Running with Visual Studio 2017</span></span>

<span data-ttu-id="0e380-278">Ouvrez le *.csproj* fichier généré par le `dotnet new` commande.</span><span class="sxs-lookup"><span data-stu-id="0e380-278">Open the *.csproj* file generated by the `dotnet new` command.</span></span> <span data-ttu-id="0e380-279">Les packages NuGet et npm nécessaires soient restaurés automatiquement sur le projet ouvert.</span><span class="sxs-lookup"><span data-stu-id="0e380-279">The required NuGet and npm packages are restored automatically upon project open.</span></span> <span data-ttu-id="0e380-280">Ce processus de restauration peut prendre quelques minutes, et l’application est prête à s’exécuter quand elle se termine.</span><span class="sxs-lookup"><span data-stu-id="0e380-280">This restoration process may take up to a few minutes, and the application is ready to run when it completes.</span></span> <span data-ttu-id="0e380-281">Cliquez sur le bouton vert d’exécution ou appuyez sur `Ctrl + F5`, et le navigateur s’ouvre à la page d’accueil de l’application.</span><span class="sxs-lookup"><span data-stu-id="0e380-281">Click the green run button or press `Ctrl + F5`, and the browser opens to the application's landing page.</span></span> <span data-ttu-id="0e380-282">L’application s’exécute sur localhost conformément à la [mode de configuration d’exécution](#runtime-config-mode).</span><span class="sxs-lookup"><span data-stu-id="0e380-282">The application runs on localhost according to the [runtime configuration mode](#runtime-config-mode).</span></span> 

<a name="app-testing"></a>

## <a name="testing-the-app"></a><span data-ttu-id="0e380-283">Test de l’application</span><span class="sxs-lookup"><span data-stu-id="0e380-283">Testing the app</span></span>

<span data-ttu-id="0e380-284">Modèles de SpaServices sont préconfigurés pour exécuter des tests côté client à l’aide de [Karma](https://karma-runner.github.io/1.0/index.html) et [Jasmine](https://jasmine.github.io/).</span><span class="sxs-lookup"><span data-stu-id="0e380-284">SpaServices templates are pre-configured to run client-side tests using [Karma](https://karma-runner.github.io/1.0/index.html) and [Jasmine](https://jasmine.github.io/).</span></span> <span data-ttu-id="0e380-285">Jasmine est une unité de populaires infrastructure de test pour JavaScript, alors que Karma est un test runner pour ces tests.</span><span class="sxs-lookup"><span data-stu-id="0e380-285">Jasmine is a popular unit testing framework for JavaScript, whereas Karma is a test runner for those tests.</span></span> <span data-ttu-id="0e380-286">KARMA est configuré pour fonctionner avec le [Webpack Dev Middleware](#webpack-dev-middleware) telles que vous n’êtes pas obligé d’arrêter et d’exécuter le test chaque fois que des modifications.</span><span class="sxs-lookup"><span data-stu-id="0e380-286">Karma is configured to work with the [Webpack Dev Middleware](#webpack-dev-middleware) such that you don’t have to stop and run the test every time changes are made.</span></span> <span data-ttu-id="0e380-287">S’il s’agit du code en cours d’exécution sur le cas de test ou le cas de test lui-même, le test s’exécute automatiquement.</span><span class="sxs-lookup"><span data-stu-id="0e380-287">Whether it's the code running against the test case or the test case itself, the test runs automatically.</span></span>

<span data-ttu-id="0e380-288">À l’aide de l’application angulaire par exemple, deux cas de test au jasmin sont déjà fournies pour le `CounterComponent` dans les *counter.component.spec.ts* fichier :</span><span class="sxs-lookup"><span data-stu-id="0e380-288">Using the Angular application as an example, two Jasmine test cases are already provided for the `CounterComponent` in the *counter.component.spec.ts* file:</span></span>

<span data-ttu-id="0e380-289">[!code-typescript[Main](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/app/components/counter/counter.component.spec.ts?range=15-28)]</span><span class="sxs-lookup"><span data-stu-id="0e380-289">[!code-typescript[Main](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/app/components/counter/counter.component.spec.ts?range=15-28)]</span></span>

<span data-ttu-id="0e380-290">Ouvrez l’invite de commandes à la racine du projet et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0e380-290">Open the command prompt at the project root, and run the following command:</span></span>

```console
npm test
```

<span data-ttu-id="0e380-291">Le script lance Karma test runner, qui lit les paramètres définis dans le *karma.conf.js* fichier.</span><span class="sxs-lookup"><span data-stu-id="0e380-291">The script launches the Karma test runner, which reads the settings defined in the *karma.conf.js* file.</span></span> <span data-ttu-id="0e380-292">Parmi d’autres paramètres, le *karma.conf.js* identifie les fichiers de test à exécuter son `files` tableau :</span><span class="sxs-lookup"><span data-stu-id="0e380-292">Among other settings, the *karma.conf.js* identifies the test files to be executed via its `files` array:</span></span>

<span data-ttu-id="0e380-293">[!code-javascript[Main](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/test/karma.conf.js?range=4-5,8-11)]</span><span class="sxs-lookup"><span data-stu-id="0e380-293">[!code-javascript[Main](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/test/karma.conf.js?range=4-5,8-11)]</span></span>

<a name="app-publishing"></a>

## <a name="publishing-the-application"></a><span data-ttu-id="0e380-294">Publication de l’application</span><span class="sxs-lookup"><span data-stu-id="0e380-294">Publishing the application</span></span>

<span data-ttu-id="0e380-295">Combinant les composants côté client générés et les artefacts ASP.NET Core publiées dans un package prêt à déployer peut s’avérer lourde.</span><span class="sxs-lookup"><span data-stu-id="0e380-295">Combining the generated client-side assets and the published ASP.NET Core artifacts into a ready-to-deploy package can be cumbersome.</span></span> <span data-ttu-id="0e380-296">Heureusement, SpaServices orchestre ce processus d’ensemble de la publication avec une cible MSBuild personnalisée nommée `RunWebpack`:</span><span class="sxs-lookup"><span data-stu-id="0e380-296">Thankfully, SpaServices orchestrates that entire publication process with a custom MSBuild target named `RunWebpack`:</span></span>

<span data-ttu-id="0e380-297">[!code-xml[Main](../client-side/spa-services/sample/SpaServicesSampleApp/SpaServicesSampleApp.csproj?range=31-45)]</span><span class="sxs-lookup"><span data-stu-id="0e380-297">[!code-xml[Main](../client-side/spa-services/sample/SpaServicesSampleApp/SpaServicesSampleApp.csproj?range=31-45)]</span></span>

<span data-ttu-id="0e380-298">La cible MSBuild a les responsabilités suivantes :</span><span class="sxs-lookup"><span data-stu-id="0e380-298">The MSBuild target has the following responsibilities:</span></span>
1. <span data-ttu-id="0e380-299">Restaurez les packages npm</span><span class="sxs-lookup"><span data-stu-id="0e380-299">Restore the npm packages</span></span>
1. <span data-ttu-id="0e380-300">Créer une build de production à l’échelle des ressources tierces, côté client</span><span class="sxs-lookup"><span data-stu-id="0e380-300">Create a production-grade build of the third-party, client-side assets</span></span>
1. <span data-ttu-id="0e380-301">Créer une build de production à l’échelle des ressources côté client personnalisées</span><span class="sxs-lookup"><span data-stu-id="0e380-301">Create a production-grade build of the custom client-side assets</span></span>
1. <span data-ttu-id="0e380-302">Copier les actifs Webpack généré dans le dossier de publication</span><span class="sxs-lookup"><span data-stu-id="0e380-302">Copy the Webpack-generated assets to the publish folder</span></span>

<span data-ttu-id="0e380-303">La cible MSBuild est appelée lors de l’exécution :</span><span class="sxs-lookup"><span data-stu-id="0e380-303">The MSBuild target is invoked when running:</span></span>

```console
dotnet publish -c Release
```

## <a name="additional-resources"></a><span data-ttu-id="0e380-304">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="0e380-304">Additional resources</span></span>

* [<span data-ttu-id="0e380-305">Docs angulaires</span><span class="sxs-lookup"><span data-stu-id="0e380-305">Angular Docs</span></span>](https://angular.io/docs)