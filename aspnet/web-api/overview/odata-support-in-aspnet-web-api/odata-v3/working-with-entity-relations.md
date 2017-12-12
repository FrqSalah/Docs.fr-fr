---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
title: "Prise en charge des Relations d’entité dans OData v3 avec l’API Web 2 | Documents Microsoft"
author: MikeWasson
description: "La plupart des jeux de données définissent les relations entre des entités : les clients ont passé des commandes ; les livres peuvent avoir auteurs ; les produits ont des fournisseurs. L’utilisation d’OData, les clients peuvent naviguer sur..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/26/2014
ms.topic: article
ms.assetid: 1e4c2eb4-b6cf-42ff-8a65-4d71ddca0394
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
msc.type: authoredcontent
ms.openlocfilehash: dec7e10e59cc2441c967afe062df227b105106a1
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/10/2017
---
<a name="supporting-entity-relations-in-odata-v3-with-web-api-2"></a><span data-ttu-id="0fba4-104">Prise en charge des Relations d’entité dans OData v3 avec l’API Web 2</span><span class="sxs-lookup"><span data-stu-id="0fba4-104">Supporting Entity Relations in OData v3 with Web API 2</span></span>
====================
<span data-ttu-id="0fba4-105">par [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="0fba4-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="0fba4-106">Télécharger le projet terminé</span><span class="sxs-lookup"><span data-stu-id="0fba4-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="0fba4-107">La plupart des jeux de données définissent les relations entre des entités : les clients ont passé des commandes ; les livres peuvent avoir auteurs ; les produits ont des fournisseurs.</span><span class="sxs-lookup"><span data-stu-id="0fba4-107">Most data sets define relations between entities: Customers have orders; books have authors; products have suppliers.</span></span> <span data-ttu-id="0fba4-108">L’utilisation d’OData, les clients peuvent naviguer sur les relations d’entité.</span><span class="sxs-lookup"><span data-stu-id="0fba4-108">Using OData, clients can navigate over entity relations.</span></span> <span data-ttu-id="0fba4-109">Étant donné un produit, vous pouvez trouver le fournisseur.</span><span class="sxs-lookup"><span data-stu-id="0fba4-109">Given a product, you can find the supplier.</span></span> <span data-ttu-id="0fba4-110">Vous pouvez également créer ou supprimer des relations.</span><span class="sxs-lookup"><span data-stu-id="0fba4-110">You can also create or remove relationships.</span></span> <span data-ttu-id="0fba4-111">Par exemple, vous pouvez définir le fournisseur pour un produit.</span><span class="sxs-lookup"><span data-stu-id="0fba4-111">For example, you can set the supplier for a product.</span></span>
> 
> <span data-ttu-id="0fba4-112">Ce didacticiel montre comment prendre en charge ces opérations dans l’API Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="0fba4-112">This tutorial shows how to support these operations in ASP.NET Web API.</span></span> <span data-ttu-id="0fba4-113">Le didacticiel s’appuie sur le didacticiel [création d’un point de terminaison OData v3 avec l’API Web 2](creating-an-odata-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="0fba4-113">The tutorial builds on the tutorial [Creating an OData v3 Endpoint with Web API 2](creating-an-odata-endpoint.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="0fba4-114">Versions du logiciel utilisées dans le didacticiel</span><span class="sxs-lookup"><span data-stu-id="0fba4-114">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="0fba4-115">API Web 2</span><span class="sxs-lookup"><span data-stu-id="0fba4-115">Web API 2</span></span>
> - <span data-ttu-id="0fba4-116">OData Version 3</span><span class="sxs-lookup"><span data-stu-id="0fba4-116">OData Version 3</span></span>
> - <span data-ttu-id="0fba4-117">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="0fba4-117">Entity Framework 6</span></span>


## <a name="add-a-supplier-entity"></a><span data-ttu-id="0fba4-118">Ajouter une entité de fournisseur</span><span class="sxs-lookup"><span data-stu-id="0fba4-118">Add a Supplier Entity</span></span>

<span data-ttu-id="0fba4-119">Nous devons d’abord ajouter un nouveau type d’entité à notre flux OData.</span><span class="sxs-lookup"><span data-stu-id="0fba4-119">First we need to add a new entity type to our OData feed.</span></span> <span data-ttu-id="0fba4-120">Nous allons ajouter un `Supplier` classe.</span><span class="sxs-lookup"><span data-stu-id="0fba4-120">We'll add a `Supplier` class.</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample1.cs)]

<span data-ttu-id="0fba4-121">Cette classe utilise une chaîne pour la clé d’entité.</span><span class="sxs-lookup"><span data-stu-id="0fba4-121">This class uses a string for the entity key.</span></span> <span data-ttu-id="0fba4-122">Dans la pratique, qui peut être moins fréquentes qu’à l’aide d’une clé de type entier.</span><span class="sxs-lookup"><span data-stu-id="0fba4-122">In practice, that might be less common than using an integer key.</span></span> <span data-ttu-id="0fba4-123">Mais il est intéressant de voir comment OData gère les autres types de clés en plus des entiers.</span><span class="sxs-lookup"><span data-stu-id="0fba4-123">But it's worth seeing how OData handles other key types besides integers.</span></span>

<span data-ttu-id="0fba4-124">Ensuite, nous allons créer une relation en ajoutant un `Supplier` propriété le `Product` classe :</span><span class="sxs-lookup"><span data-stu-id="0fba4-124">Next, we'll create a relation by adding a `Supplier` property to the `Product` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample2.cs)]

<span data-ttu-id="0fba4-125">Ajouter un nouveau **DbSet** à la `ProductServiceContext` classe, afin qu’Entity Framework inclura le `Supplier` table dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="0fba4-125">Add a new **DbSet** to the `ProductServiceContext` class, so that Entity Framework will include the `Supplier` table in the database.</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample3.cs?highlight=9)]

<span data-ttu-id="0fba4-126">Dans WebApiConfig.cs, ajoutez une entité « Fournisseurs » pour le modèle EDM :</span><span class="sxs-lookup"><span data-stu-id="0fba4-126">In WebApiConfig.cs, add a "Suppliers" entity to the EDM model:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample4.cs?highlight=4)]

## <a name="navigation-properties"></a><span data-ttu-id="0fba4-127">Propriétés de navigation</span><span class="sxs-lookup"><span data-stu-id="0fba4-127">Navigation Properties</span></span>

<span data-ttu-id="0fba4-128">Pour obtenir le fournisseur pour un produit, le client envoie une demande GET :</span><span class="sxs-lookup"><span data-stu-id="0fba4-128">To get the supplier for a product, the client sends a GET request:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample5.cmd)]

<span data-ttu-id="0fba4-129">« Fournisseur » est une propriété de navigation sur le `Product` type.</span><span class="sxs-lookup"><span data-stu-id="0fba4-129">Here "Supplier" is a navigation property on the `Product` type.</span></span> <span data-ttu-id="0fba4-130">Dans ce cas, `Supplier` fait référence à un élément unique, mais une navigation de propriété peut également retourner une collection (relation un-à-plusieurs ou plusieurs-à-plusieurs).</span><span class="sxs-lookup"><span data-stu-id="0fba4-130">In this case, `Supplier` refers to a single item, but a navigation property can also return a collection (one-to-many or many-to-many relation).</span></span>

<span data-ttu-id="0fba4-131">Pour prendre en charge de cette demande, ajoutez la méthode suivante à la `ProductsController` classe :</span><span class="sxs-lookup"><span data-stu-id="0fba4-131">To support this request, add the following method to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample6.cs)]

<span data-ttu-id="0fba4-132">Le *clé* paramètre est la clé du produit.</span><span class="sxs-lookup"><span data-stu-id="0fba4-132">The *key* parameter is the key of the product.</span></span> <span data-ttu-id="0fba4-133">La méthode retourne l’entité associée &#8212;dans ce cas, un `Supplier` instance.</span><span class="sxs-lookup"><span data-stu-id="0fba4-133">The method returns the related entity&#8212in this case, a `Supplier` instance.</span></span> <span data-ttu-id="0fba4-134">Le nom de la méthode et le nom de paramètre sont cruciales.</span><span class="sxs-lookup"><span data-stu-id="0fba4-134">The method name and parameter name are both important.</span></span> <span data-ttu-id="0fba4-135">En règle générale, si la propriété de navigation est nommée « X », vous devez ajouter une méthode nommée « GetX ».</span><span class="sxs-lookup"><span data-stu-id="0fba4-135">In general, if the navigation property is named "X", you need to add a method named "GetX".</span></span> <span data-ttu-id="0fba4-136">La méthode doit prendre un paramètre nommé «*clé*» qui correspond au type de données de clé du parent.</span><span class="sxs-lookup"><span data-stu-id="0fba4-136">The method must take a parameter named "*key*" that matches the data type of the parent's key.</span></span>

<span data-ttu-id="0fba4-137">Il est également important d’inclure le **[FromOdataUri]** d’attribut dans le *clé* paramètre.</span><span class="sxs-lookup"><span data-stu-id="0fba4-137">It is also important to include the **[FromOdataUri]** attribute in the *key* parameter.</span></span> <span data-ttu-id="0fba4-138">Cet attribut indique à l’API Web à utiliser les règles de syntaxe OData lorsqu’il analyse la clé à partir de l’URI de requête.</span><span class="sxs-lookup"><span data-stu-id="0fba4-138">This attribute tells Web API to use OData syntax rules when it parses the key from the request URI.</span></span>

## <a name="creating-and-deleting-links"></a><span data-ttu-id="0fba4-139">Création et suppression de liens</span><span class="sxs-lookup"><span data-stu-id="0fba4-139">Creating and Deleting Links</span></span>

<span data-ttu-id="0fba4-140">OData prend en charge la création ou la suppression des relations entre deux entités.</span><span class="sxs-lookup"><span data-stu-id="0fba4-140">OData supports creating or removing relationships between two entities.</span></span> <span data-ttu-id="0fba4-141">Dans la terminologie d’OData, la relation est un lien «. »</span><span class="sxs-lookup"><span data-stu-id="0fba4-141">In OData terminology, the relationship is a "link."</span></span> <span data-ttu-id="0fba4-142">Chaque lien a un URI avec le formulaire *entité*/$links /*entité*.</span><span class="sxs-lookup"><span data-stu-id="0fba4-142">Each link has a URI with the form *entity*/$links/*entity*.</span></span> <span data-ttu-id="0fba4-143">Par exemple, le lien à partir du produit fournisseur ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="0fba4-143">For example, the link from product to supplier looks like this:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample7.cmd)]

<span data-ttu-id="0fba4-144">Pour créer un nouveau lien, le client envoie une demande POST à l’URI de lien.</span><span class="sxs-lookup"><span data-stu-id="0fba4-144">To create a new link, the client sends a POST request to the link URI.</span></span> <span data-ttu-id="0fba4-145">Le corps de la demande est l’URI de l’entité cible.</span><span class="sxs-lookup"><span data-stu-id="0fba4-145">The body of the request is the URI of the target entity.</span></span> <span data-ttu-id="0fba4-146">Par exemple, qu'un fournisseur avec la clé « CTSO ».</span><span class="sxs-lookup"><span data-stu-id="0fba4-146">For example, suppose there is a supplier with the key "CTSO".</span></span> <span data-ttu-id="0fba4-147">Pour créer un lien entre « Product(1) » et « Supplier('CTSO') », le client envoie une requête comme suit :</span><span class="sxs-lookup"><span data-stu-id="0fba4-147">To create a link from "Product(1)" to "Supplier('CTSO')", the client sends a request like the following:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample8.cmd)]

<span data-ttu-id="0fba4-148">Pour supprimer un lien, le client envoie une demande de suppression pour l’URI de lien.</span><span class="sxs-lookup"><span data-stu-id="0fba4-148">To delete a link, the client sends a DELETE request to the link URI.</span></span>

<span data-ttu-id="0fba4-149">**Création de liens**</span><span class="sxs-lookup"><span data-stu-id="0fba4-149">**Creating Links**</span></span>

<span data-ttu-id="0fba4-150">Pour permettre à un client créer des liens du fournisseur du produit, ajoutez le code suivant à la `ProductsController` classe :</span><span class="sxs-lookup"><span data-stu-id="0fba4-150">To enable a client to create product-supplier links, add the following code to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample9.cs)]

<span data-ttu-id="0fba4-151">Cette méthode accepte trois paramètres :</span><span class="sxs-lookup"><span data-stu-id="0fba4-151">This method takes three parameters:</span></span>

- <span data-ttu-id="0fba4-152">*clé*: la clé à l’entité parente (le produit)</span><span class="sxs-lookup"><span data-stu-id="0fba4-152">*key*: The key to the parent entity (the product)</span></span>
- <span data-ttu-id="0fba4-153">*navigationProperty*: le nom de la propriété de navigation.</span><span class="sxs-lookup"><span data-stu-id="0fba4-153">*navigationProperty*: The name of the navigation property.</span></span> <span data-ttu-id="0fba4-154">Dans cet exemple, la propriété de navigation uniquement valide est « Fournisseur ».</span><span class="sxs-lookup"><span data-stu-id="0fba4-154">In this example, the only valid navigation property is "Supplier".</span></span>
- <span data-ttu-id="0fba4-155">*lien*: OData URI de l’entité associée.</span><span class="sxs-lookup"><span data-stu-id="0fba4-155">*link*: The OData URI of the related entity.</span></span> <span data-ttu-id="0fba4-156">Cette valeur provient de corps de la demande.</span><span class="sxs-lookup"><span data-stu-id="0fba4-156">This value is taken from the request body.</span></span> <span data-ttu-id="0fba4-157">Par exemple, le lien URI peut être «`http://localhost/odata/Suppliers('CTSO')`, ce qui signifie que le fournisseur avec l’ID = 'CTSO'.</span><span class="sxs-lookup"><span data-stu-id="0fba4-157">For example, the link URI might be "`http://localhost/odata/Suppliers('CTSO')`, meaning the supplier with ID = ‘CTSO'.</span></span>

<span data-ttu-id="0fba4-158">La méthode utilise le lien pour rechercher le fournisseur.</span><span class="sxs-lookup"><span data-stu-id="0fba4-158">The method uses the link to look up the supplier.</span></span> <span data-ttu-id="0fba4-159">Si le fournisseur correspondant est trouvé, la méthode définit le `Product.Supplier` propriété et enregistre le résultat dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="0fba4-159">If the matching supplier is found, the method sets the `Product.Supplier` property and saves the result to the database.</span></span>

<span data-ttu-id="0fba4-160">La partie la plus difficile est l’analyse de l’URI de lien.</span><span class="sxs-lookup"><span data-stu-id="0fba4-160">The hardest part is parsing the link URI.</span></span> <span data-ttu-id="0fba4-161">En fait, vous devez simuler le résultat de l’envoi d’une requête GET à cet URI.</span><span class="sxs-lookup"><span data-stu-id="0fba4-161">Basically, you need to simulate the result of sending a GET request to that URI.</span></span> <span data-ttu-id="0fba4-162">La méthode d’assistance suivante montre comment effectuer cette opération.</span><span class="sxs-lookup"><span data-stu-id="0fba4-162">The following helper method shows how to do this.</span></span> <span data-ttu-id="0fba4-163">La méthode appelle le processus de routage d’API Web et récupère un **ODataPath** instance qui représente le chemin d’accès OData analysé.</span><span class="sxs-lookup"><span data-stu-id="0fba4-163">The method invokes the Web API routing process and gets back an **ODataPath** instance that represents the parsed OData path.</span></span> <span data-ttu-id="0fba4-164">Pour un URI de lien, un des segments doit être la clé d’entité.</span><span class="sxs-lookup"><span data-stu-id="0fba4-164">For a link URI, one of the segments should be the entity key.</span></span> <span data-ttu-id="0fba4-165">(Dans le cas contraire, le client a envoyé un URI incorrect.)</span><span class="sxs-lookup"><span data-stu-id="0fba4-165">(If not, the client sent a bad URI.)</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample10.cs)]

<span data-ttu-id="0fba4-166">**Suppression de liens**</span><span class="sxs-lookup"><span data-stu-id="0fba4-166">**Deleting Links**</span></span>

<span data-ttu-id="0fba4-167">Pour supprimer un lien, ajoutez le code suivant à la `ProductsController` classe :</span><span class="sxs-lookup"><span data-stu-id="0fba4-167">To delete a link, add the following code to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample11.cs)]

<span data-ttu-id="0fba4-168">Dans cet exemple, la propriété de navigation est un seul `Supplier` entité.</span><span class="sxs-lookup"><span data-stu-id="0fba4-168">In this example, the navigation property is a single `Supplier` entity.</span></span> <span data-ttu-id="0fba4-169">Si la propriété de navigation est une collection, l’URI pour supprimer un lien doit inclure une clé pour l’entité associée.</span><span class="sxs-lookup"><span data-stu-id="0fba4-169">If the navigation property is a collection, the URI to delete a link must include a key for the related entity.</span></span> <span data-ttu-id="0fba4-170">Exemple :</span><span class="sxs-lookup"><span data-stu-id="0fba4-170">For example:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample12.cmd)]

<span data-ttu-id="0fba4-171">Cette requête supprime l’ordre 1 client 1.</span><span class="sxs-lookup"><span data-stu-id="0fba4-171">This request removes order 1 from customer 1.</span></span> <span data-ttu-id="0fba4-172">Dans ce cas, la méthode DeleteLink aura la signature suivante :</span><span class="sxs-lookup"><span data-stu-id="0fba4-172">In this case, the DeleteLink method will have the following signature:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample13.cs)]

<span data-ttu-id="0fba4-173">Le *relatedKey* paramètre indique la clé pour l’entité associée.</span><span class="sxs-lookup"><span data-stu-id="0fba4-173">The *relatedKey* parameter gives the key for the related entity.</span></span> <span data-ttu-id="0fba4-174">C’est le cas dans votre `DeleteLink` méthode, rechercher l’entité principale par le *clé* paramètre, rechercher l’entité associée par le *relatedKey* paramètre, puis supprimez l’association.</span><span class="sxs-lookup"><span data-stu-id="0fba4-174">So in your `DeleteLink` method, look up the primary entity by the *key* parameter, find the related entity by the *relatedKey* parameter, and then remove the association.</span></span> <span data-ttu-id="0fba4-175">Selon votre modèle de données, vous devrez peut-être implémenter les deux versions de `DeleteLink`.</span><span class="sxs-lookup"><span data-stu-id="0fba4-175">Depending on your data model, you might need to implement both versions of `DeleteLink`.</span></span> <span data-ttu-id="0fba4-176">API Web appellera la version correcte en fonction de l’URI de requête.</span><span class="sxs-lookup"><span data-stu-id="0fba4-176">Web API will call the correct version based on the request URI.</span></span>