---
title: "Cœur de ASP.NET MVC avec EF Core - trier, filtrer, la pagination - 3 sur 10"
author: tdykstra
description: "Dans ce didacticiel, vous allez ajouter le tri, filtrage et d’échange vers la page à l’aide d’ASP.NET Core et Entity Framework Core."
keywords: ASP.NET Core, Entity Framework Core, trier, filtrer, la pagination, regroupement
ms.author: tdykstra
ms.date: 03/15/2017
ms.topic: get-started-article
ms.assetid: e6c1ff3c-5673-43bf-9c2d-077f6ada1f29
ms.technology: aspnet
ms.prod: asp.net-core
uid: data/ef-mvc/sort-filter-page
ms.openlocfilehash: bc2896d0eeda7e84cef06ee3f235e637bfe04318
ms.sourcegitcommit: 5355c96a1768e5a1d5698a98c190e7addcc4ded5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/05/2017
---
# <a name="sorting-filtering-paging-and-grouping---ef-core-with-aspnet-core-mvc-tutorial-3-of-10"></a><span data-ttu-id="a5f0d-104">Le tri, le filtrage, la pagination et le regroupement - Core EF avec le didacticiel ASP.NET Core MVC (partie 3 sur 10)</span><span class="sxs-lookup"><span data-stu-id="a5f0d-104">Sorting, filtering, paging, and grouping - EF Core with ASP.NET Core MVC tutorial (3 of 10)</span></span>

<span data-ttu-id="a5f0d-105">Par [Tom Dykstra](https://github.com/tdykstra) et [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="a5f0d-105">By [Tom Dykstra](https://github.com/tdykstra) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="a5f0d-106">L’exemple d’application web Contoso University montre comment créer des applications web ASP.NET MVC de base à l’aide d’Entity Framework Core et Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-106">The Contoso University sample web application demonstrates how to create ASP.NET Core MVC web applications using Entity Framework Core and Visual Studio.</span></span> <span data-ttu-id="a5f0d-107">Pour plus d’informations sur la série de didacticiels, consultez [le premier didacticiel de la série](intro.md).</span><span class="sxs-lookup"><span data-stu-id="a5f0d-107">For information about the tutorial series, see [the first tutorial in the series](intro.md).</span></span>

<span data-ttu-id="a5f0d-108">Dans le didacticiel précédent, vous implémenté un ensemble de pages web pour les opérations CRUD de base pour les entités de Student.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-108">In the previous tutorial, you implemented a set of web pages for basic CRUD operations for Student entities.</span></span> <span data-ttu-id="a5f0d-109">Dans ce didacticiel, vous allez ajouter le tri, filtrage et la fonctionnalité de pagination à la page d’Index d’étudiants.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-109">In this tutorial you'll add sorting, filtering, and paging functionality to the Students Index page.</span></span> <span data-ttu-id="a5f0d-110">Vous allez également créer une page qui effectue le regroupement simple.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-110">You'll also create a page that does simple grouping.</span></span>

<span data-ttu-id="a5f0d-111">L’illustration suivante montre à quoi ressemblera la page une lorsque vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-111">The following illustration shows what the page will look like when you're done.</span></span> <span data-ttu-id="a5f0d-112">Les en-têtes de colonne sont des liens que l’utilisateur peut cliquer pour trier par colonne.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-112">The column headings are links that the user can click to sort by that column.</span></span> <span data-ttu-id="a5f0d-113">En cliquant sur un en-tête à plusieurs reprises de colonne bascule entre croissant et décroissant d’ordre de tri.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-113">Clicking a column heading repeatedly toggles between ascending and descending sort order.</span></span>

![Page d’index les étudiants](sort-filter-page/_static/paging.png)

## <a name="add-column-sort-links-to-the-students-index-page"></a><span data-ttu-id="a5f0d-115">Ajouter des liens de tri de colonne à la Page d’Index les étudiants</span><span class="sxs-lookup"><span data-stu-id="a5f0d-115">Add Column Sort Links to the Students Index Page</span></span>

<span data-ttu-id="a5f0d-116">Pour ajouter le tri à la page d’Index de l’étudiant, vous allez modifier le `Index` méthode du contrôleur étudiants et ajouter du code à la vue de l’Index de l’étudiant.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-116">To add sorting to the Student Index page, you'll change the `Index` method of the Students controller and add code to the Student Index view.</span></span>

### <a name="add-sorting-functionality-to-the-index-method"></a><span data-ttu-id="a5f0d-117">Ajouter les fonctionnalités de tri pour l’Index (méthode)</span><span class="sxs-lookup"><span data-stu-id="a5f0d-117">Add sorting Functionality to the Index method</span></span>

<span data-ttu-id="a5f0d-118">Dans *StudentsController.cs*, remplacez le `Index` méthode avec le code suivant :</span><span class="sxs-lookup"><span data-stu-id="a5f0d-118">In *StudentsController.cs*, replace the `Index` method with the following code:</span></span>

<span data-ttu-id="a5f0d-119">[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_SortOnly)]</span><span class="sxs-lookup"><span data-stu-id="a5f0d-119">[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_SortOnly)]</span></span>

<span data-ttu-id="a5f0d-120">Ce code reçoit un `sortOrder` paramètre à partir de la chaîne de requête dans l’URL.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-120">This code receives a `sortOrder` parameter from the query string in the URL.</span></span> <span data-ttu-id="a5f0d-121">La valeur de chaîne de requête est fournie par ASP.NET MVC de base en tant que paramètre à la méthode d’action.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-121">The query string value is provided by ASP.NET Core MVC as a parameter to the action method.</span></span> <span data-ttu-id="a5f0d-122">Le paramètre sera une chaîne qui est « Name » ou « Date », éventuellement suivie d’un trait de soulignement et de la chaîne « desc » pour spécifier l’ordre décroissant.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-122">The parameter will be a string that's either "Name" or "Date", optionally followed by an underscore and the string "desc" to specify descending order.</span></span> <span data-ttu-id="a5f0d-123">L'ordre de tri par défaut est le tri croissant.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-123">The default sort order is ascending.</span></span>

<span data-ttu-id="a5f0d-124">La première fois que la page d’Index est demandée, il n’aucune chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-124">The first time the Index page is requested, there's no query string.</span></span> <span data-ttu-id="a5f0d-125">Les étudiants sont affichés dans l’ordre croissant par nom, qui est la valeur par défaut établies par le cas de passage dans le `switch` instruction.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-125">The students are displayed in ascending order by last name, which is the default as established by the fall-through case in the `switch` statement.</span></span> <span data-ttu-id="a5f0d-126">Lorsque l’utilisateur clique sur un colonne titre lien hypertexte, approprié `sortOrder` valeur est fournie dans la chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-126">When the user clicks a column heading hyperlink, the appropriate `sortOrder` value is provided in the query string.</span></span>

<span data-ttu-id="a5f0d-127">Les deux `ViewData` éléments (NameSortParm et DateSortParm) sont utilisés par la vue pour configurer des liens hypertexte du titre de colonne avec les valeurs de chaîne de requête appropriée.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-127">The two `ViewData` elements (NameSortParm and DateSortParm) are used by the view to configure the column heading hyperlinks with the appropriate query string values.</span></span>

<span data-ttu-id="a5f0d-128">[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_SortOnly&highlight=3-4)]</span><span class="sxs-lookup"><span data-stu-id="a5f0d-128">[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_SortOnly&highlight=3-4)]</span></span>

<span data-ttu-id="a5f0d-129">Il s’agit d’instructions ternaires.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-129">These are ternary statements.</span></span> <span data-ttu-id="a5f0d-130">La première condition spécifie que si le `sortOrder` paramètre est null ou vide, NameSortParm doit être défini sur « name_desc » ; sinon, il doit être défini sur une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-130">The first one specifies that if the `sortOrder` parameter is null or empty, NameSortParm should be set to "name_desc"; otherwise, it should be set to an empty string.</span></span> <span data-ttu-id="a5f0d-131">Ces deux instructions activer l’affichage définir la colonne des liens hypertexte du titre comme suit :</span><span class="sxs-lookup"><span data-stu-id="a5f0d-131">These two statements enable the view to set the column heading hyperlinks as follows:</span></span>

|  <span data-ttu-id="a5f0d-132">Ordre de tri en cours</span><span class="sxs-lookup"><span data-stu-id="a5f0d-132">Current sort order</span></span>  | <span data-ttu-id="a5f0d-133">Lien hypertexte du nom du dernier</span><span class="sxs-lookup"><span data-stu-id="a5f0d-133">Last Name Hyperlink</span></span> | <span data-ttu-id="a5f0d-134">Lien hypertexte de date</span><span class="sxs-lookup"><span data-stu-id="a5f0d-134">Date Hyperlink</span></span> |
|:--------------------:|:-------------------:|:--------------:|
| <span data-ttu-id="a5f0d-135">Dernier nom par ordre croissant</span><span class="sxs-lookup"><span data-stu-id="a5f0d-135">Last Name ascending</span></span>  | <span data-ttu-id="a5f0d-136">descending</span><span class="sxs-lookup"><span data-stu-id="a5f0d-136">descending</span></span>          | <span data-ttu-id="a5f0d-137">ascending</span><span class="sxs-lookup"><span data-stu-id="a5f0d-137">ascending</span></span>      |
| <span data-ttu-id="a5f0d-138">Dernier nom décroissant</span><span class="sxs-lookup"><span data-stu-id="a5f0d-138">Last Name descending</span></span> | <span data-ttu-id="a5f0d-139">ascending</span><span class="sxs-lookup"><span data-stu-id="a5f0d-139">ascending</span></span>           | <span data-ttu-id="a5f0d-140">ascending</span><span class="sxs-lookup"><span data-stu-id="a5f0d-140">ascending</span></span>      |
| <span data-ttu-id="a5f0d-141">Date de l’ordre croissant</span><span class="sxs-lookup"><span data-stu-id="a5f0d-141">Date ascending</span></span>       | <span data-ttu-id="a5f0d-142">ascending</span><span class="sxs-lookup"><span data-stu-id="a5f0d-142">ascending</span></span>           | <span data-ttu-id="a5f0d-143">descending</span><span class="sxs-lookup"><span data-stu-id="a5f0d-143">descending</span></span>     |
| <span data-ttu-id="a5f0d-144">Date décroissant</span><span class="sxs-lookup"><span data-stu-id="a5f0d-144">Date descending</span></span>      | <span data-ttu-id="a5f0d-145">ascending</span><span class="sxs-lookup"><span data-stu-id="a5f0d-145">ascending</span></span>           | <span data-ttu-id="a5f0d-146">ascending</span><span class="sxs-lookup"><span data-stu-id="a5f0d-146">ascending</span></span>      |

<span data-ttu-id="a5f0d-147">La méthode utilise LINQ to Entities pour spécifier la colonne à trier.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-147">The method uses LINQ to Entities to specify the column to sort by.</span></span> <span data-ttu-id="a5f0d-148">Le code crée un `IQueryable` variable avant l’instruction switch, il modifie dans l’instruction switch et appelle le `ToListAsync` méthode après le `switch` instruction.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-148">The code creates an `IQueryable` variable before the switch statement, modifies it in the switch statement, and calls the `ToListAsync` method after the `switch` statement.</span></span> <span data-ttu-id="a5f0d-149">Lorsque vous créez et modifiez `IQueryable` variables, aucune requête n’est envoyée à la base de données.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-149">When you create and modify `IQueryable` variables, no query is sent to the database.</span></span> <span data-ttu-id="a5f0d-150">La requête n’est pas exécutée jusqu'à ce que vous convertissez la `IQueryable` objet dans une collection en appelant une méthode comme `ToListAsync`.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-150">The query is not executed until you convert the `IQueryable` object into a collection by calling a method such as `ToListAsync`.</span></span> <span data-ttu-id="a5f0d-151">Par conséquent, ce code génère une requête unique qui n’est pas exécutée tant que la `return View` instruction.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-151">Therefore, this code results in a single query that is not executed until the `return View` statement.</span></span>

<span data-ttu-id="a5f0d-152">Ce code peut obtenir documentée avec un grand nombre de colonnes.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-152">This code could get verbose with a large number of columns.</span></span> <span data-ttu-id="a5f0d-153">[Le didacticiel dernière de cette série](advanced.md#dynamic-linq) montre comment écrire du code qui vous permet de passer le nom de la `OrderBy` colonne dans une variable de chaîne.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-153">[The last tutorial in this series](advanced.md#dynamic-linq) shows how to write code that lets you pass the name of the `OrderBy` column in a string variable.</span></span>

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a><span data-ttu-id="a5f0d-154">Ajouter des liens hypertexte du titre de colonne à la vue de l’Index de l’étudiant</span><span class="sxs-lookup"><span data-stu-id="a5f0d-154">Add column heading hyperlinks to the Student Index view</span></span>

<span data-ttu-id="a5f0d-155">Remplacez le code dans *Views/Students/Index.cshtml*, avec le code suivant pour ajouter des liens hypertexte du titre de colonne.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-155">Replace the code in *Views/Students/Index.cshtml*, with the following code to add column heading hyperlinks.</span></span> <span data-ttu-id="a5f0d-156">Les lignes modifiées sont mises en surbrillance.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-156">The changed lines are highlighted.</span></span>

[!code-html[](intro/samples/cu/Views/Students/Index2.cshtml?highlight=16,22)]

<span data-ttu-id="a5f0d-157">Ce code utilise les informations contenues dans `ViewData` les valeurs de chaîne de propriétés pour configurer des liens hypertexte avec la requête appropriée.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-157">This code uses the information in `ViewData` properties to set up hyperlinks with the appropriate query string values.</span></span>

<span data-ttu-id="a5f0d-158">Exécutez la page et cliquez sur le **nom** et **Date d’inscription** des en-têtes de colonne pour vérifier que le tri fonctionne.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-158">Run the page and click the **Last Name** and **Enrollment Date** column headings to verify that sorting works.</span></span>

![Page d’index étudiants dans l’ordre de nom](sort-filter-page/_static/name-order.png)

## <a name="add-a-search-box-to-the-students-index-page"></a><span data-ttu-id="a5f0d-160">Ajouter une zone de recherche à la page d’Index des étudiants</span><span class="sxs-lookup"><span data-stu-id="a5f0d-160">Add a Search Box to the Students Index page</span></span>

<span data-ttu-id="a5f0d-161">Pour ajouter le filtrage sur la page d’Index des étudiants, vous allez ajouter une zone de texte et un bouton d’envoi à la vue et apporter les modifications correspondantes dans le `Index` (méthode).</span><span class="sxs-lookup"><span data-stu-id="a5f0d-161">To add filtering to the Students Index page, you'll add a text box and a submit button to the view and make corresponding changes in the `Index` method.</span></span> <span data-ttu-id="a5f0d-162">La zone de texte vous permet d’entrer une chaîne à rechercher dans le prénom et le champ.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-162">The text box will let you enter a string to search for in the first name and last name fields.</span></span>

### <a name="add-filtering-functionality-to-the-index-method"></a><span data-ttu-id="a5f0d-163">Ajouter des fonctionnalités de filtrage à l’Index (méthode)</span><span class="sxs-lookup"><span data-stu-id="a5f0d-163">Add filtering functionality to the Index method</span></span>

<span data-ttu-id="a5f0d-164">Dans *StudentsController.cs*, remplacez le `Index` méthode avec le code suivant (les modifications sont mises en surbrillance).</span><span class="sxs-lookup"><span data-stu-id="a5f0d-164">In *StudentsController.cs*, replace the `Index` method with the following code (the changes are highlighted).</span></span>

<span data-ttu-id="a5f0d-165">[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_SortFilter&highlight=1,5,9-13)]</span><span class="sxs-lookup"><span data-stu-id="a5f0d-165">[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_SortFilter&highlight=1,5,9-13)]</span></span>

<span data-ttu-id="a5f0d-166">Vous avez ajouté un `searchString` paramètre à la `Index` (méthode).</span><span class="sxs-lookup"><span data-stu-id="a5f0d-166">You've added a `searchString` parameter to the `Index` method.</span></span> <span data-ttu-id="a5f0d-167">La valeur de chaîne de recherche est reçue à partir d’une zone de texte que vous ajouterez à la vue Index.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-167">The search string value is received from a text box that you'll add to the Index view.</span></span> <span data-ttu-id="a5f0d-168">Vous avez également ajouté à l’instruction LINQ where clause qui sélectionne uniquement les étudiants dont prénom ou le nom contient la chaîne de recherche.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-168">You've also added to the LINQ statement a where clause that selects only students whose first name or last name contains the search string.</span></span> <span data-ttu-id="a5f0d-169">L’instruction qui ajoute where clause est exécutée uniquement s’il existe une valeur à rechercher.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-169">The statement that adds the where clause is executed only if there's a value to search for.</span></span>

> [!NOTE]
> <span data-ttu-id="a5f0d-170">Ici vous appelez le `Where` méthode sur une `IQueryable` objet et le filtre seront traités sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-170">Here you are calling the `Where` method on an `IQueryable` object, and the filter will be processed on the server.</span></span> <span data-ttu-id="a5f0d-171">Dans certains scénarios vous pouvez appeler la `Where` méthode comme méthode d’extension sur une collection en mémoire.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-171">In some scenarios you might be calling the `Where` method as an extension method on an in-memory collection.</span></span> <span data-ttu-id="a5f0d-172">(Par exemple, supposons que vous modifiez la référence à `_context.Students` ainsi qu’au lieu d’un FE `DbSet` il fait référence à une méthode de référentiel qui retourne un `IEnumerable` collection.) Le résultat serait normalement le même, mais dans certains cas, peut être différent.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-172">(For example, suppose you change the reference to `_context.Students` so that instead of an EF `DbSet` it references a repository method that returns an `IEnumerable` collection.) The result would normally be the same but in some cases may be different.</span></span>
>
><span data-ttu-id="a5f0d-173">Par exemple, l’implémentation du .NET Framework de la `Contains` méthode effectue une comparaison respectant la casse par défaut, mais dans SQL Server, cela est déterminé par le paramètre de classement de l’instance de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-173">For example, the .NET Framework implementation of the `Contains` method performs a case-sensitive comparison by default, but in SQL Server this is determined by the collation setting of the SQL Server instance.</span></span> <span data-ttu-id="a5f0d-174">Ce paramètre par défaut à la casse.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-174">That setting defaults to case-insensitive.</span></span> <span data-ttu-id="a5f0d-175">Vous pouvez appeler la `ToUpper` méthode le test doit être explicitement pas la casse : *où (s = > s.LastName.ToUpper(). Contains(searchString.ToUpper())*.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-175">You could call the `ToUpper` method to make the test explicitly case-insensitive:  *Where(s => s.LastName.ToUpper().Contains(searchString.ToUpper())*.</span></span> <span data-ttu-id="a5f0d-176">Qui s’assurent que que résultats restent le même si vous modifiez le code ultérieurement pour utiliser un référentiel qui retourne un `IEnumerable` collection au lieu d’un `IQueryable` objet.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-176">That would ensure that results stay the same if you change the code later to use a repository which returns   an `IEnumerable` collection instead of an `IQueryable` object.</span></span> <span data-ttu-id="a5f0d-177">(Lorsque vous appelez le `Contains` méthode sur une `IEnumerable` collection, vous obtenez l’implémentation du .NET Framework ; lorsque vous appelez sur un `IQueryable` de l’objet, vous obtenez l’implémentation du fournisseur de base de données.) Toutefois, il est d’une baisse des performances de cette solution.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-177">(When you call the `Contains` method on an `IEnumerable` collection, you get the .NET Framework implementation; when you call it on an `IQueryable` object, you get the database provider implementation.) However, there is a performance penalty for this solution.</span></span> <span data-ttu-id="a5f0d-178">Le `ToUpper` code place une fonction dans la clause WHERE de l’instruction SELECT de TSQL.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-178">The `ToUpper` code would put a function in the WHERE clause of the TSQL SELECT statement.</span></span> <span data-ttu-id="a5f0d-179">Qui empêche l’optimiseur d’à l’aide d’un index.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-179">That would prevent the optimizer from using an index.</span></span> <span data-ttu-id="a5f0d-180">Étant donné que SQL est installé principalement sans respecter la casse, il est préférable d’éviter le `ToUpper` code jusqu'à ce que vous migrez vers un magasin de données qui respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-180">Given that SQL is mostly installed as case-insensitive, it's best to avoid the `ToUpper` code until you migrate to a case-sensitive data store.</span></span>

### <a name="add-a-search-box-to-the-student-index-view"></a><span data-ttu-id="a5f0d-181">Ajouter une zone de recherche à la vue d’Index étudiant</span><span class="sxs-lookup"><span data-stu-id="a5f0d-181">Add a Search Box to the Student Index View</span></span>

<span data-ttu-id="a5f0d-182">Dans *Views/Student/Index.cshtml*, ajoutez le code en surbrillance immédiatement avant l’ouverture de balise table afin de créer une légende, une zone de texte et un **recherche** bouton.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-182">In *Views/Student/Index.cshtml*, add the highlighted code immediately before the opening table tag in order to create a caption, a text box, and a **Search** button.</span></span>

[!code-html[](intro/samples/cu/Views/Students/Index3.cshtml?range=9-23&highlight=5-13)]

<span data-ttu-id="a5f0d-183">Ce code utilise le `<form>` [d’assistance de balise](https://docs.asp.net/en/latest/mvc/views/tag-helpers/intro.html) pour ajouter la zone de texte de recherche et le bouton.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-183">This code uses the `<form>` [tag helper](https://docs.asp.net/en/latest/mvc/views/tag-helpers/intro.html) to add the search text box and button.</span></span> <span data-ttu-id="a5f0d-184">Par défaut, le `<form>` application d’assistance de balise envoie des données de formulaire avec une publication, ce qui signifie que les paramètres sont passés dans le corps du message HTTP et non dans l’URL sous forme de chaînes de requête.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-184">By default, the `<form>` tag helper submits form data with a POST, which means that parameters are passed in the HTTP message body and not in the URL as query strings.</span></span> <span data-ttu-id="a5f0d-185">Lorsque vous spécifiez HTTP GET, les données du formulaire sont passées dans l’URL sous forme de chaînes de requête, ce qui permet aux utilisateurs de l’URL de signet.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-185">When you specify HTTP GET, the form data is passed in the URL as query strings, which enables users to bookmark the URL.</span></span> <span data-ttu-id="a5f0d-186">W3C instructions il est conseillé que vous devez utiliser obtenir lors de l’action n’entraîne pas une mise à jour.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-186">The W3C guidelines recommend that you should use GET when the action does not result in an update.</span></span>

<span data-ttu-id="a5f0d-187">Exécutez la page, entrez une chaîne de recherche et cliquez sur Rechercher pour vérifier que le filtrage fonctionne.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-187">Run the page, enter a search string, and click Search to verify that filtering is working.</span></span>

![Page d’index de stagiaires de filtrage](sort-filter-page/_static/filtering.png)

<span data-ttu-id="a5f0d-189">Notez que l’URL contient la chaîne de recherche.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-189">Notice that the URL contains the search string.</span></span>

```html
http://localhost:5813/Students?SearchString=an
```

<span data-ttu-id="a5f0d-190">Si vous créez un signet cette page, vous obtenez la liste filtrée lorsque vous utilisez le signet.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-190">If you bookmark this page, you'll get the filtered list when you use the bookmark.</span></span> <span data-ttu-id="a5f0d-191">Ajout de `method="get"` à la `form` balise est ce qui a provoqué la chaîne de requête à générer.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-191">Adding `method="get"` to the `form` tag is what caused the query string to be generated.</span></span>

<span data-ttu-id="a5f0d-192">À ce stade, si vous cliquez sur un lien de tri de titre de colonne vous perdez la valeur de filtre que vous avez entré dans le **recherche** boîte.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-192">At this stage, if you click a column heading sort link you'll lose the filter value that you entered in the **Search** box.</span></span> <span data-ttu-id="a5f0d-193">Vous allez résoudre cela dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-193">You'll fix that in the next section.</span></span>

## <a name="add-paging-functionality-to-the-students-index-page"></a><span data-ttu-id="a5f0d-194">Ajouter la fonctionnalité de pagination à la page d’Index des étudiants</span><span class="sxs-lookup"><span data-stu-id="a5f0d-194">Add paging functionality to the Students Index page</span></span>

<span data-ttu-id="a5f0d-195">Pour ajouter la pagination à la page d’Index des étudiants, vous allez créer un `PaginatedList` classe utilise `Skip` et `Take` instructions pour filtrer les données sur le serveur au lieu de toujours récupérer toutes les lignes de la table.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-195">To add paging to the Students Index page, you'll create a `PaginatedList` class that uses `Skip` and `Take` statements to filter data on the server instead of always retrieving all rows of the table.</span></span> <span data-ttu-id="a5f0d-196">Ensuite, vous allez apporter des modifications supplémentaires dans le `Index` (méthode) et ajouter des boutons de la pagination à la `Index` vue.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-196">Then you'll make additional changes in the `Index` method and add paging buttons to the `Index` view.</span></span> <span data-ttu-id="a5f0d-197">L’illustration suivante montre les boutons de la pagination.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-197">The following illustration shows the paging buttons.</span></span>

![Page avec des liens de pagination d’index les étudiants](sort-filter-page/_static/paging.png)

<span data-ttu-id="a5f0d-199">Dans le dossier du projet, créez `PaginatedList.cs`, puis remplacez le code du modèle par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-199">In the project folder, create `PaginatedList.cs`, and then replace the template code with the following code.</span></span>

<span data-ttu-id="a5f0d-200">[!code-csharp[Main](intro/samples/cu/PaginatedList.cs)]</span><span class="sxs-lookup"><span data-stu-id="a5f0d-200">[!code-csharp[Main](intro/samples/cu/PaginatedList.cs)]</span></span>

<span data-ttu-id="a5f0d-201">Le `CreateAsync` méthode dans ce code prend la taille de la page et le numéro de page et applique `Skip` et `Take` instructions pour le `IQueryable`.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-201">The `CreateAsync` method in this code takes page size and page number and applies the appropriate `Skip` and `Take` statements to the `IQueryable`.</span></span> <span data-ttu-id="a5f0d-202">Lorsque `ToListAsync` est appelée sur le `IQueryable`, il retourne une liste contenant uniquement la page demandée.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-202">When `ToListAsync` is called on the `IQueryable`, it will return a List containing only the requested page.</span></span> <span data-ttu-id="a5f0d-203">Les propriétés `HasPreviousPage` et `HasNextPage` peut être utilisé pour activer ou désactiver **précédent** et **suivant** boutons de pagination.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-203">The properties `HasPreviousPage` and `HasNextPage` can be used to enable or disable **Previous** and **Next** paging buttons.</span></span>

<span data-ttu-id="a5f0d-204">A `CreateAsync` méthode est utilisée au lieu d’un constructeur pour créer le `PaginatedList<T>` de l’objet, car les constructeurs ne peuvent pas exécuter du code asynchrone.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-204">A `CreateAsync` method is used instead of a constructor to create the `PaginatedList<T>` object because constructors can't run asynchronous code.</span></span>

## <a name="add-paging-functionality-to-the-index-method"></a><span data-ttu-id="a5f0d-205">Ajouter la fonctionnalité de pagination pour le Index (méthode)</span><span class="sxs-lookup"><span data-stu-id="a5f0d-205">Add paging functionality to the Index method</span></span>

<span data-ttu-id="a5f0d-206">Dans *StudentsController.cs*, remplacez le `Index` méthode avec le code suivant.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-206">In *StudentsController.cs*, replace the `Index` method with the following code.</span></span>

<span data-ttu-id="a5f0d-207">[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_SortFilterPage&highlight=1-5,7,11-18,45-46)]</span><span class="sxs-lookup"><span data-stu-id="a5f0d-207">[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_SortFilterPage&highlight=1-5,7,11-18,45-46)]</span></span>

<span data-ttu-id="a5f0d-208">Ce code ajoute un paramètre de numéro de page, un paramètre de commande de tri actuelle et un paramètre de filtre actuel pour la signature de méthode.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-208">This code adds a page number parameter, a current sort order parameter, and a current filter parameter to the method signature.</span></span>

```csharp
public async Task<IActionResult> Index(
    string sortOrder,
    string currentFilter,
    string searchString,
    int? page)
```

<span data-ttu-id="a5f0d-209">La première fois que la page s’affiche, ou si l’utilisateur n’a pas cliqué sur un échange ou le lien de tri, tous les paramètres sont null.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-209">The first time the page is displayed, or if the user hasn't clicked a paging or sorting link, all the parameters will be null.</span></span>  <span data-ttu-id="a5f0d-210">Si un lien de la pagination est activé, la variable de page contient le numéro de page à afficher.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-210">If a paging link is clicked, the page variable will contain the page number to display.</span></span>

<span data-ttu-id="a5f0d-211">Le `ViewData` élément nommé CurrentSort fournit la vue de l’ordre de tri actuel, car il doit être incluse dans les liens de la pagination afin de conserver l’ordre de tri lors de la pagination.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-211">The `ViewData` element named CurrentSort provides the view with the current sort order, because this must be included in the paging links in order to keep the sort order the same while paging.</span></span>

<span data-ttu-id="a5f0d-212">Le `ViewData` élément nommé FiltreActif fournit la vue avec la chaîne de filtre actuel.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-212">The `ViewData` element named CurrentFilter provides the view with the current filter string.</span></span> <span data-ttu-id="a5f0d-213">Cette valeur doit être incluse dans les liens de la pagination afin de conserver les paramètres de filtre lors de la pagination, et elle doit être restaurée à la zone de texte lorsque la page s’affiche de nouveau.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-213">This value must be included in the paging links in order to maintain the filter settings during paging, and it must be restored to the text box when the page is redisplayed.</span></span>

<span data-ttu-id="a5f0d-214">Si la chaîne de recherche est modifiée au cours de la pagination, la page doit être réinitialisé à 1, parce que le nouveau filtre pour afficher des données différentes.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-214">If the search string is changed during paging, the page has to be reset to 1, because the new filter can result in different data to display.</span></span> <span data-ttu-id="a5f0d-215">La chaîne de recherche est modifiée quand une valeur est entrée dans la zone de texte et le bouton d’envoi est enfoncé.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-215">The search string is changed when a value is entered in the text box and the Submit button is pressed.</span></span> <span data-ttu-id="a5f0d-216">Dans ce cas, le `searchString` paramètre n’est pas null.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-216">In that case, the `searchString` parameter is not null.</span></span>

```csharp
if (searchString != null)
{
    page = 1;
}
else
{
    searchString = currentFilter;
}
```

<span data-ttu-id="a5f0d-217">À la fin de la `Index` (méthode), la `PaginatedList.CreateAsync` méthode convertit la requête de student à une seule page d’étudiants dans un type de collection qui prend en charge la pagination.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-217">At the end of the `Index` method, the `PaginatedList.CreateAsync` method converts the student query to a single page of students in a collection type that supports paging.</span></span> <span data-ttu-id="a5f0d-218">Cette page unique des étudiants est ensuite passée à la vue.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-218">That single page of students is then passed to the view.</span></span>

```csharp
return View(await PaginatedList<Student>.CreateAsync(students.AsNoTracking(), page ?? 1, pageSize));
```

<span data-ttu-id="a5f0d-219">Le `PaginatedList.CreateAsync` méthode prend un numéro de page.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-219">The `PaginatedList.CreateAsync` method takes a page number.</span></span> <span data-ttu-id="a5f0d-220">Les deux points d’interrogation représenter l’opérateur de fusion null.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-220">The two question marks represent the null-coalescing operator.</span></span> <span data-ttu-id="a5f0d-221">L’opérateur de fusion null définit une valeur par défaut pour un type nullable ; l’expression `(page ?? 1)` signifie retourne la valeur de `page` si elle a une valeur, ou retourne 1 si `page` a la valeur null.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-221">The null-coalescing operator defines a default value for a nullable type; the expression `(page ?? 1)` means return the value of `page` if it has a value, or return 1 if `page` is null.</span></span>

## <a name="add-paging-links-to-the-student-index-view"></a><span data-ttu-id="a5f0d-222">Ajouter des liens de pagination à la vue de l’Index de l’étudiant</span><span class="sxs-lookup"><span data-stu-id="a5f0d-222">Add paging links to the Student Index view</span></span>

<span data-ttu-id="a5f0d-223">Dans *Views/Students/Index.cshtml*, remplacez le code existant par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-223">In *Views/Students/Index.cshtml*, replace the existing code with the following code.</span></span> <span data-ttu-id="a5f0d-224">Les modifications sont mises en surbrillance.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-224">The changes are highlighted.</span></span>

[!code-html[](intro/samples/cu/Views/Students/Index.cshtml?highlight=1,27,30,33,61-79)]

<span data-ttu-id="a5f0d-225">Le `@model` instruction en haut de la page spécifie que la vue obtient désormais une `PaginatedList<T>` de l’objet au lieu d’un `List<T>` objet.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-225">The `@model` statement at the top of the page specifies that the view now gets a `PaginatedList<T>` object instead of a `List<T>` object.</span></span>

<span data-ttu-id="a5f0d-226">Les liens d’en-tête de colonne permet de passer la chaîne de recherche en cours au contrôleur afin que l’utilisateur peut trier les résultats de filtre de la chaîne de requête :</span><span class="sxs-lookup"><span data-stu-id="a5f0d-226">The column header links use the query string to pass the current search string to the controller so that the user can sort within filter results:</span></span>

```html
<a asp-action="Index" asp-route-sortOrder="@ViewData["DateSortParm"]" asp-route-currentFilter ="@ViewData["CurrentFilter"]">Enrollment Date</a>
```

<span data-ttu-id="a5f0d-227">Les boutons de pagination sont affichés par les programmes d’assistance de balise :</span><span class="sxs-lookup"><span data-stu-id="a5f0d-227">The paging buttons are displayed by tag helpers:</span></span>

```html
<a asp-action="Index"
   asp-route-sortOrder="@ViewData["CurrentSort"]"
   asp-route-page="@(Model.PageIndex - 1)"
   asp-route-currentFilter="@ViewData["CurrentFilter"]"
   class="btn btn-default @prevDisabled">
   Previous
</a>
```

<span data-ttu-id="a5f0d-228">Exécutez la page.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-228">Run the page.</span></span>

![Page avec des liens de pagination d’index les étudiants](sort-filter-page/_static/paging.png)

<span data-ttu-id="a5f0d-230">Cliquez sur les liens de la pagination dans différents ordres de tri s’assurer que la pagination fonctionne.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-230">Click the paging links in different sort orders to make sure paging works.</span></span> <span data-ttu-id="a5f0d-231">Entrez une chaîne de recherche, puis recommencez la pagination pour vérifier que la pagination également fonctionne correctement avec le tri et de filtrage.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-231">Then enter a search string and try paging again to verify that paging also works correctly with sorting and filtering.</span></span>

## <a name="create-an-about-page-that-shows-student-statistics"></a><span data-ttu-id="a5f0d-232">Créer une page à propos qui affiche les statistiques de l’étudiant</span><span class="sxs-lookup"><span data-stu-id="a5f0d-232">Create an About page that shows Student statistics</span></span>

<span data-ttu-id="a5f0d-233">Pour le site de Web Contoso University **sur** page, vous afficherez le nombre d’étudiants inscrits pour chaque date d’inscription.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-233">For the Contoso University website's **About** page, you'll display how many students have enrolled for each enrollment date.</span></span> <span data-ttu-id="a5f0d-234">Cela nécessite de regroupement et simples des calculs sur les groupes.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-234">This requires grouping and simple calculations on the groups.</span></span> <span data-ttu-id="a5f0d-235">Pour ce faire, vous devez procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a5f0d-235">To accomplish this, you'll do the following:</span></span>

* <span data-ttu-id="a5f0d-236">Créer une classe de modèle d’affichage pour les données dont vous avez besoin pour passer à la vue.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-236">Create a view model class for the data that you need to pass to the view.</span></span>

* <span data-ttu-id="a5f0d-237">Modifiez la méthode à propos du contrôleur Home.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-237">Modify the About method in the Home controller.</span></span>

* <span data-ttu-id="a5f0d-238">Modifier la vue à propos de.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-238">Modify the About view.</span></span>

### <a name="create-the-view-model"></a><span data-ttu-id="a5f0d-239">Créer le modèle d’affichage</span><span class="sxs-lookup"><span data-stu-id="a5f0d-239">Create the view model</span></span>

<span data-ttu-id="a5f0d-240">Créer un *SchoolViewModels* dossier dans le *modèles* dossier.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-240">Create a *SchoolViewModels* folder in the *Models* folder.</span></span>

<span data-ttu-id="a5f0d-241">Dans le nouveau dossier, ajoutez un fichier de classe *EnrollmentDateGroup.cs* et remplacez le code de modèle par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="a5f0d-241">In the new folder, add a class file *EnrollmentDateGroup.cs* and replace the template code with the following code:</span></span>

<span data-ttu-id="a5f0d-242">[!code-csharp[Main](intro/samples/cu/Models/SchoolViewModels/EnrollmentDateGroup.cs)]</span><span class="sxs-lookup"><span data-stu-id="a5f0d-242">[!code-csharp[Main](intro/samples/cu/Models/SchoolViewModels/EnrollmentDateGroup.cs)]</span></span>

### <a name="modify-the-home-controller"></a><span data-ttu-id="a5f0d-243">Modifier le contrôleur Home</span><span class="sxs-lookup"><span data-stu-id="a5f0d-243">Modify the Home Controller</span></span>

<span data-ttu-id="a5f0d-244">Dans *HomeController.cs*, ajoutez le code suivant à l’aide d’instructions en haut du fichier :</span><span class="sxs-lookup"><span data-stu-id="a5f0d-244">In *HomeController.cs*, add the following using statements at the top of the file:</span></span>

<span data-ttu-id="a5f0d-245">[!code-csharp[Main](intro/samples/cu/Controllers/HomeController.cs?name=snippet_Usings1)]</span><span class="sxs-lookup"><span data-stu-id="a5f0d-245">[!code-csharp[Main](intro/samples/cu/Controllers/HomeController.cs?name=snippet_Usings1)]</span></span>

<span data-ttu-id="a5f0d-246">Ajouter une variable de classe pour le contexte de base de données immédiatement après l’accolade ouvrante de la classe et en obtenir une instance du contexte ASP.NET Core DI :</span><span class="sxs-lookup"><span data-stu-id="a5f0d-246">Add a class variable for the database context immediately after the opening curly brace for the class, and get an instance of the context from ASP.NET Core DI:</span></span>

<span data-ttu-id="a5f0d-247">[!code-csharp[Main](intro/samples/cu/Controllers/HomeController.cs?name=snippet_AddContext&highlight=3,5,7)]</span><span class="sxs-lookup"><span data-stu-id="a5f0d-247">[!code-csharp[Main](intro/samples/cu/Controllers/HomeController.cs?name=snippet_AddContext&highlight=3,5,7)]</span></span>

<span data-ttu-id="a5f0d-248">Remplacez la méthode `About` par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="a5f0d-248">Replace the `About` method with the following code:</span></span>

<span data-ttu-id="a5f0d-249">[!code-csharp[Main](intro/samples/cu/Controllers/HomeController.cs?name=snippet_UseDbSet)]</span><span class="sxs-lookup"><span data-stu-id="a5f0d-249">[!code-csharp[Main](intro/samples/cu/Controllers/HomeController.cs?name=snippet_UseDbSet)]</span></span>

<span data-ttu-id="a5f0d-250">L’instruction LINQ regroupe les entités étudiant par date d’inscription, calcule le nombre d’entités dans chaque groupe et stocke les résultats dans une collection de `EnrollmentDateGroup` afficher les objets de modèle.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-250">The LINQ statement groups the student entities by enrollment date, calculates the number of entities in each group, and stores the results in a collection of `EnrollmentDateGroup` view model objects.</span></span>
> [!NOTE] 
> <span data-ttu-id="a5f0d-251">Dans la 1.0 version de Entity Framework Core, le jeu de résultats entier est retourné au client, et de regroupement est effectué sur le client.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-251">In the 1.0 version of Entity Framework Core, the entire result set is returned to the client, and grouping is done on the client.</span></span> <span data-ttu-id="a5f0d-252">Dans certains scénarios, cela pourrait créer des problèmes de performances.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-252">In some scenarios this could create performance problems.</span></span> <span data-ttu-id="a5f0d-253">Veillez à tester les performances avec les volumes de données de production et si nécessaire utilisez brute SQL pour effectuer le regroupement sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-253">Be sure to test performance with production volumes of data, and if necessary use raw SQL to do the grouping on the server.</span></span> <span data-ttu-id="a5f0d-254">Pour plus d’informations sur l’utilisation de SQL brute, consultez [le dernier didacticiel de cette série](advanced.md).</span><span class="sxs-lookup"><span data-stu-id="a5f0d-254">For information about how to use raw SQL, see [the last tutorial in this series](advanced.md).</span></span>

### <a name="modify-the-about-view"></a><span data-ttu-id="a5f0d-255">Modifier le sur la vue</span><span class="sxs-lookup"><span data-stu-id="a5f0d-255">Modify the About View</span></span>

<span data-ttu-id="a5f0d-256">Remplacez le code dans le *Views/Home/About.cshtml* fichier avec le code suivant :</span><span class="sxs-lookup"><span data-stu-id="a5f0d-256">Replace the code in the *Views/Home/About.cshtml* file with the following code:</span></span>

[!code-html[](intro/samples/cu/Views/Home/About.cshtml)]

<span data-ttu-id="a5f0d-257">Exécutez l’application et cliquez sur le **sur** lien.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-257">Run the app and click the **About** link.</span></span> <span data-ttu-id="a5f0d-258">Le nombre d’étudiants pour chaque date d’inscription s’affiche dans une table.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-258">The count of students for each enrollment date is displayed in a table.</span></span>

![Sur la page](sort-filter-page/_static/about.png)

## <a name="summary"></a><span data-ttu-id="a5f0d-260">Résumé</span><span class="sxs-lookup"><span data-stu-id="a5f0d-260">Summary</span></span>

<span data-ttu-id="a5f0d-261">Dans ce didacticiel, vous avez vu comment effectuer le tri, le filtrage, la pagination et regroupement.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-261">In this tutorial, you've seen how to perform sorting, filtering, paging, and grouping.</span></span> <span data-ttu-id="a5f0d-262">Dans l’étape suivante du didacticiel, vous allez apprendre à gérer les modifications du modèle de données à l’aide des migrations.</span><span class="sxs-lookup"><span data-stu-id="a5f0d-262">In the next tutorial, you'll learn how to handle data model changes by using migrations.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="a5f0d-263">[Précédent](crud.md)
[Suivant](migrations.md)</span><span class="sxs-lookup"><span data-stu-id="a5f0d-263">[Previous](crud.md)
[Next](migrations.md)</span></span>  
