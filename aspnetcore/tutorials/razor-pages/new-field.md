---
title: "Ajout d’un nouveau champ à une page Razor"
author: rick-anderson
description: "Montre comment ajouter un nouveau champ à une page Razor avec Entity Framework Core"
keywords: ASP.NET Core, Entity Framework Core, migrations
ms.author: riande
manager: wpickett
ms.date: 8/7/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: aspnet-core
uid: tutorials/razor-pages/new-field
ms.openlocfilehash: bda00f290043251ad308192c5b1a873ae7cd0d85
ms.sourcegitcommit: e832a9b9f41a8b26a8c88edfd8fc35b8bfd97d5d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="adding-a-new-field-to-a-razor-page"></a><span data-ttu-id="69bfa-104">Ajout d’un nouveau champ à une page Razor</span><span class="sxs-lookup"><span data-stu-id="69bfa-104">Adding a new field to a Razor Page</span></span>

<span data-ttu-id="69bfa-105">Par [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="69bfa-105">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="69bfa-106">Dans cette section, vous allez utiliser la fonctionnalité Migrations Code First [d’Entity Framework](http://docs.efproject.net/en/latest/platforms/aspnetcore/new-db.html) pour ajouter un nouveau champ au modèle et migrer ce changement dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="69bfa-106">In this section you'll use [Entity Framework](http://docs.efproject.net/en/latest/platforms/aspnetcore/new-db.html) Code First Migrations to add a new field to the model and migrate that change to the database.</span></span>

<span data-ttu-id="69bfa-107">Quand vous utilisez EF Code First pour créer automatiquement une base de données, Code First ajoute une table à la base de données pour déterminer si le schéma de la base de données est synchronisé avec les classes de modèle à partir desquelles il a été généré.</span><span class="sxs-lookup"><span data-stu-id="69bfa-107">When you use EF Code First to automatically create a database, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="69bfa-108">S’ils ne sont pas synchronisés, EF lève une exception.</span><span class="sxs-lookup"><span data-stu-id="69bfa-108">If they aren't in sync, EF throws an exception.</span></span> <span data-ttu-id="69bfa-109">Cela facilite la recherche de problèmes d’incohérence de code/de bases de données.</span><span class="sxs-lookup"><span data-stu-id="69bfa-109">This makes it easier to find inconsistent database/code issues.</span></span>

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="69bfa-110">Ajout d’une propriété Rating au modèle Movie</span><span class="sxs-lookup"><span data-stu-id="69bfa-110">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="69bfa-111">Ouvrez le fichier *Models/Movie.cs* et ajoutez une propriété `Rating` :</span><span class="sxs-lookup"><span data-stu-id="69bfa-111">Open the *Models/Movie.cs* file and add a `Rating` property:</span></span>

<span data-ttu-id="69bfa-112">[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Models/MovieDateRating.cs?highlight=11&range=7-18)]</span><span class="sxs-lookup"><span data-stu-id="69bfa-112">[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Models/MovieDateRating.cs?highlight=11&range=7-18)]</span></span>

<span data-ttu-id="69bfa-113">Générez l’application (Ctrl+Maj+B).</span><span class="sxs-lookup"><span data-stu-id="69bfa-113">Build the app (Ctrl+Shift+B).</span></span>

<span data-ttu-id="69bfa-114">Modifiez *Pages/Movies/Index.cshtml*et ajoutez un champ `Rating` :</span><span class="sxs-lookup"><span data-stu-id="69bfa-114">Edit *Pages/Movies/Index.cshtml*, and add a `Rating` field:</span></span>

<span data-ttu-id="69bfa-115">[!code-cshtml[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml?highlight=40-42,61-63)]</span><span class="sxs-lookup"><span data-stu-id="69bfa-115">[!code-cshtml[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml?highlight=40-42,61-63)]</span></span>

<span data-ttu-id="69bfa-116">Ajoutez le champ `Rating` aux pages Delete et Details.</span><span class="sxs-lookup"><span data-stu-id="69bfa-116">Add the `Rating` field to the Delete and Details pages.</span></span>

<span data-ttu-id="69bfa-117">Mettez à jour *Create.cshtml* avec un champ `Rating`.</span><span class="sxs-lookup"><span data-stu-id="69bfa-117">Update *Create.cshtml* with a `Rating` field.</span></span> <span data-ttu-id="69bfa-118">Vous pouvez copier/coller l’élément `<div>` précédent et laisser IntelliSense vous aider à mettre à jour les champs.</span><span class="sxs-lookup"><span data-stu-id="69bfa-118">You can copy/paste the previous `<div>` element and let intelliSense help you update the fields.</span></span> <span data-ttu-id="69bfa-119">IntelliSense fonctionne avec des [Tag Helpers](xref:mvc/views/tag-helpers/intro).</span><span class="sxs-lookup"><span data-stu-id="69bfa-119">IntelliSense works with [Tag Helpers](xref:mvc/views/tag-helpers/intro).</span></span>

![Le développeur a tapé la lettre R comme valeur d’attribut asp-for dans le deuxième élément étiquette de la vue.](new-field/_static/cr.png)

<span data-ttu-id="69bfa-123">Le code suivant montre *Create.cshtml* avec un champ `Rating` :</span><span class="sxs-lookup"><span data-stu-id="69bfa-123">The following code shows *Create.cshtml* with a `Rating` field:</span></span>

<span data-ttu-id="69bfa-124">[!code-cshtml[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Create.cshtml?highlight=31-35)]</span><span class="sxs-lookup"><span data-stu-id="69bfa-124">[!code-cshtml[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Create.cshtml?highlight=31-35)]</span></span>

<span data-ttu-id="69bfa-125">Ajoutez le champ `Rating` à la Page Edit.</span><span class="sxs-lookup"><span data-stu-id="69bfa-125">Add the `Rating` field to the Edit Page.</span></span>

<span data-ttu-id="69bfa-126">L’application ne fonctionne pas tant que la base de données n’est pas mise à jour pour inclure le nouveau champ.</span><span class="sxs-lookup"><span data-stu-id="69bfa-126">The app won't work until the DB is updated to include the new field.</span></span> <span data-ttu-id="69bfa-127">Si vous l’exécutez à présent, l’application lève une `SqlException` :</span><span class="sxs-lookup"><span data-stu-id="69bfa-127">If run now, the app throws a `SqlException`:</span></span>

`SqlException: Invalid column name 'Rating'.`

<span data-ttu-id="69bfa-128">Cette erreur est due au fait que la classe du modèle Movie mise à jour est différente du schéma de la table Movie de la base de données.</span><span class="sxs-lookup"><span data-stu-id="69bfa-128">This error is caused by the updated Movie model class being different than the schema of the Movie table of the database.</span></span> <span data-ttu-id="69bfa-129">(Il n’existe pas de colonne `Rating` dans la table de base de données.)</span><span class="sxs-lookup"><span data-stu-id="69bfa-129">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="69bfa-130">Plusieurs approches sont possibles pour résoudre l’erreur :</span><span class="sxs-lookup"><span data-stu-id="69bfa-130">There are a few approaches to resolving the error:</span></span>

1. <span data-ttu-id="69bfa-131">Laisser Entity Framework supprimer et recréer automatiquement la base de données à l’aide du nouveau schéma de classe de modèle.</span><span class="sxs-lookup"><span data-stu-id="69bfa-131">Have the Entity Framework automatically drop and re-create the database using  the new model class schema.</span></span> <span data-ttu-id="69bfa-132">Cette approche est très utile au début du cycle de développement. Elle permet de faire évoluer rapidement le modèle et le schéma de base de données ensemble.</span><span class="sxs-lookup"><span data-stu-id="69bfa-132">This approach is convenient early in the development cycle; it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="69bfa-133">L’inconvénient est que vous perdez les données existantes dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="69bfa-133">The downside is that you lose existing data in the database.</span></span> <span data-ttu-id="69bfa-134">Il ne faut pas adopter cette approche sur une base de données de production.</span><span class="sxs-lookup"><span data-stu-id="69bfa-134">You don't want to use this approach on a production database!</span></span> <span data-ttu-id="69bfa-135">La suppression de la base de données lors des changements de schéma et l’utilisation d’un initialiseur pour amorcer automatiquement la base de données avec des données de test est souvent un moyen efficace pour développer une application.</span><span class="sxs-lookup"><span data-stu-id="69bfa-135">Dropping the DB on schema changes and using an initializer to automatically seed the database with test data is often a productive way to develop an app.</span></span>

2. <span data-ttu-id="69bfa-136">Modifier explicitement le schéma de la base de données existante pour le faire correspondre aux classes du modèle.</span><span class="sxs-lookup"><span data-stu-id="69bfa-136">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="69bfa-137">L’avantage de cette approche est que vous conservez vos données.</span><span class="sxs-lookup"><span data-stu-id="69bfa-137">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="69bfa-138">Vous pouvez apporter cette modification manuellement ou en créant un script de modification de la base de données.</span><span class="sxs-lookup"><span data-stu-id="69bfa-138">You can make this change either manually or by creating a database change script.</span></span>

3. <span data-ttu-id="69bfa-139">Utilisez les migrations Code First pour mettre à jour le schéma de base de données.</span><span class="sxs-lookup"><span data-stu-id="69bfa-139">Use Code First Migrations to update the database schema.</span></span>

<span data-ttu-id="69bfa-140">Pour ce didacticiel, nous allons utiliser les migrations Code First.</span><span class="sxs-lookup"><span data-stu-id="69bfa-140">For this tutorial, use Code First Migrations.</span></span>

<span data-ttu-id="69bfa-141">Mettez à jour la classe `SeedData` pour qu’elle fournisse une valeur pour la nouvelle colonne.</span><span class="sxs-lookup"><span data-stu-id="69bfa-141">Update the `SeedData` class so that it provides a value for the new column.</span></span> <span data-ttu-id="69bfa-142">Vous pouvez voir un exemple de modification ci-dessous, mais elle doit être appliquée à chaque bloc `new Movie`.</span><span class="sxs-lookup"><span data-stu-id="69bfa-142">A sample change is shown below, but you'll want to make this change for each `new Movie` block.</span></span>

<span data-ttu-id="69bfa-143">[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Models/SeedDataRating.cs?name=snippet1&highlight=6)]</span><span class="sxs-lookup"><span data-stu-id="69bfa-143">[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Models/SeedDataRating.cs?name=snippet1&highlight=6)]</span></span>

<span data-ttu-id="69bfa-144">Consultez le [fichier SeedData.cs complet](https://github.com/aspnet/Docs/blob/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Models/SeedDataRating.cs).</span><span class="sxs-lookup"><span data-stu-id="69bfa-144">See the [completed SeedData.cs file](https://github.com/aspnet/Docs/blob/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Models/SeedDataRating.cs).</span></span>

<span data-ttu-id="69bfa-145">Générez la solution.</span><span class="sxs-lookup"><span data-stu-id="69bfa-145">Build the solution.</span></span>

<a name="pmc"></a>

<span data-ttu-id="69bfa-146">Dans le menu **Outils**, sélectionnez **Gestionnaire de package NuGet > Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="69bfa-146">From the **Tools** menu, select **NuGet Package Manager > Package Manager Console**.</span></span>
<span data-ttu-id="69bfa-147">Dans la console du Gestionnaire de package, entrez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="69bfa-147">In the PMC, enter the following commands:</span></span>

```PMC
Add-Migration Rating
Update-Database
```

<span data-ttu-id="69bfa-148">La commande `Add-Migration` indique au framework qu’il doit :</span><span class="sxs-lookup"><span data-stu-id="69bfa-148">The `Add-Migration` command tells the framework to:</span></span>

* <span data-ttu-id="69bfa-149">Comparer le modèle `Movie` au schéma de base de données `Movie`</span><span class="sxs-lookup"><span data-stu-id="69bfa-149">Compare the `Movie` model with the `Movie` DB schema.</span></span>
* <span data-ttu-id="69bfa-150">Créer du code pour migrer le schéma de base de données vers le nouveau modèle</span><span class="sxs-lookup"><span data-stu-id="69bfa-150">Create code to migrate the DB schema to the new model.</span></span>

<span data-ttu-id="69bfa-151">Le nom « Rating » est arbitraire et utilisé pour nommer le fichier de migration.</span><span class="sxs-lookup"><span data-stu-id="69bfa-151">The name "Rating" is arbitrary and is used to name the migration file.</span></span> <span data-ttu-id="69bfa-152">Il est utile d’utiliser un nom explicite pour le fichier de migration.</span><span class="sxs-lookup"><span data-stu-id="69bfa-152">It's helpful to use a meaningful name for the migration file.</span></span>

<span data-ttu-id="69bfa-153"><a name="ssox"></a> Si vous supprimez tous les enregistrements de la base de données, l’initialiseur amorce la base de données et inclut le champ `Rating`.</span><span class="sxs-lookup"><span data-stu-id="69bfa-153"><a name="ssox"></a> If you delete all the records in the DB, the initializer will seed the DB and include the `Rating` field.</span></span> <span data-ttu-id="69bfa-154">Pour ce faire, utilisez les liens de suppression disponibles dans le navigateur ou à partir de [Sql Server Object Explorer](xref:tutorials/razor-pages/sql#ssox).</span><span class="sxs-lookup"><span data-stu-id="69bfa-154">You can do this with the delete links in the browser or from [Sql Server Object Explorer](xref:tutorials/razor-pages/sql#ssox) (SSOX).</span></span> <span data-ttu-id="69bfa-155">Pour supprimer la base de données à partir de SSOX</span><span class="sxs-lookup"><span data-stu-id="69bfa-155">To delete the database from SSOX:</span></span>

* <span data-ttu-id="69bfa-156">Sélectionnez la base de données dans SSOX.</span><span class="sxs-lookup"><span data-stu-id="69bfa-156">Select the database in SSOX.</span></span>
* <span data-ttu-id="69bfa-157">Cliquez avec le bouton droit sur la base de données, puis sélectionnez *Supprimer*.</span><span class="sxs-lookup"><span data-stu-id="69bfa-157">Right click on the database, and select *Delete*.</span></span>
* <span data-ttu-id="69bfa-158">Cochez **Fermer les connexions existantes*.</span><span class="sxs-lookup"><span data-stu-id="69bfa-158">Check **Close existing connections*</span></span>
* <span data-ttu-id="69bfa-159">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="69bfa-159">Select **OK**</span></span>
* <span data-ttu-id="69bfa-160">Dans le [PMC](xref:tutorials/razor-pages/new-field#pmc), mettez à jour la base de données.</span><span class="sxs-lookup"><span data-stu-id="69bfa-160">In the [PMC](xref:tutorials/razor-pages/new-field#pmc), update the database</span></span> 

    ```PMC
    Update-Database
    ```

<span data-ttu-id="69bfa-161">Exécutez l’application et vérifiez que vous pouvez créer/modifier/afficher des films avec un champ `Rating`.</span><span class="sxs-lookup"><span data-stu-id="69bfa-161">Run the app and verify you can create/edit/display movies with a `Rating` field.</span></span> <span data-ttu-id="69bfa-162">Si la base de données n’est pas amorcée, arrêtez IIS Express puis exécutez l’application.</span><span class="sxs-lookup"><span data-stu-id="69bfa-162">If the database is not seeded, stop IIS Express, and then run the app.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="69bfa-163">[Précédent : Ajout de la recherche](xref:tutorials/razor-pages/search)
[Suivant : Ajout d’un nouveau champ](xref:tutorials/razor-pages/new-field)</span><span class="sxs-lookup"><span data-stu-id="69bfa-163">[Previous: Adding Search](xref:tutorials/razor-pages/search)
[Next: Adding a new field](xref:tutorials/razor-pages/new-field)</span></span>
