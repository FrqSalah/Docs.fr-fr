---
title: "Mettre en cache d’assistance de balise dans le cœur d’ASP.NET MVC"
author: pkellner
description: "Montre comment travailler avec l’application d’assistance de balise de Cache"
keywords: "ASP.NET Core, d’assistance de balise"
ms.author: riande
manager: wpickett
ms.date: 02/14/2017
ms.topic: article
ms.assetid: c045d485-d1dc-4cea-a675-46be83b7a012
ms.technology: aspnet
ms.prod: aspnet-core
uid: mvc/views/tag-helpers/builtin-th/CacheTagHelper
ms.openlocfilehash: 37f93816c75d83211a85c311395e2664d8a649b9
ms.sourcegitcommit: 0b6c8e6d81d2b3c161cd375036eecbace46a9707
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/11/2017
---
# <a name="cache-tag-helper-in-aspnet-core-mvc"></a><span data-ttu-id="c9913-104">Mettre en cache d’assistance de balise dans le cœur d’ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="c9913-104">Cache Tag Helper in ASP.NET Core MVC</span></span>

<span data-ttu-id="c9913-105">Par [Peter Kellner](http://peterkellner.net)</span><span class="sxs-lookup"><span data-stu-id="c9913-105">By [Peter Kellner](http://peterkellner.net)</span></span> 


<span data-ttu-id="c9913-106">L’application d’assistance de balise de Cache permet d’améliorer considérablement les performances de votre application ASP.NET Core par son contenu pour le fournisseur de cache ASP.NET Core interne de la mise en cache.</span><span class="sxs-lookup"><span data-stu-id="c9913-106">The  Cache Tag Helper provides the ability to dramatically improve the performance of your ASP.NET Core app by caching its content to the internal ASP.NET Core cache provider.</span></span>

<span data-ttu-id="c9913-107">Le moteur d’affichage Razor définit la valeur par défaut `expires-after` vingt minutes.</span><span class="sxs-lookup"><span data-stu-id="c9913-107">The Razor View Engine sets the default `expires-after` to twenty minutes.</span></span>

<span data-ttu-id="c9913-108">Le balisage de Razor suivant met en cache la date/heure :</span><span class="sxs-lookup"><span data-stu-id="c9913-108">The following Razor markup caches the date/time:</span></span>

```cshtml
<Cache>@DateTime.Now<Cache>
```

<span data-ttu-id="c9913-109">La première demande vers la page qui contient `CacheTagHelper` affiche la date/heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="c9913-109">The first request to the page that contains `CacheTagHelper` will display the current date/time.</span></span> <span data-ttu-id="c9913-110">Demandes supplémentaires affichera la valeur mise en cache jusqu'à ce que le cache expire (par défaut, 20 minutes) ou est supprimé par sollicitation de la mémoire.</span><span class="sxs-lookup"><span data-stu-id="c9913-110">Additional requests will show the cached value until the cache expires (default 20 minutes) or is evicted by memory pressure.</span></span>

<span data-ttu-id="c9913-111">Vous pouvez définir la durée du cache avec les attributs suivants :</span><span class="sxs-lookup"><span data-stu-id="c9913-111">You can set the cache duration with the following attributes:</span></span>

## <a name="cache-tag-helper-attributes"></a><span data-ttu-id="c9913-112">Mettre en cache les attributs d’assistance de balise</span><span class="sxs-lookup"><span data-stu-id="c9913-112">Cache Tag Helper Attributes</span></span>

- - -

### <a name="enabled"></a><span data-ttu-id="c9913-113">enabled</span><span class="sxs-lookup"><span data-stu-id="c9913-113">enabled</span></span>    


| <span data-ttu-id="c9913-114">Type d’attribut</span><span class="sxs-lookup"><span data-stu-id="c9913-114">Attribute Type</span></span>    | <span data-ttu-id="c9913-115">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="c9913-115">Valid Values</span></span>      |
|----------------   |----------------   |
| <span data-ttu-id="c9913-116">boolean</span><span class="sxs-lookup"><span data-stu-id="c9913-116">boolean</span></span>           | <span data-ttu-id="c9913-117">« true » (par défaut)</span><span class="sxs-lookup"><span data-stu-id="c9913-117">"true" (default)</span></span>  |
|                   | <span data-ttu-id="c9913-118">"false"</span><span class="sxs-lookup"><span data-stu-id="c9913-118">"false"</span></span>   |


<span data-ttu-id="c9913-119">Détermine si le contenu du programme d’assistance de balise de Cache est mis en cache.</span><span class="sxs-lookup"><span data-stu-id="c9913-119">Determines whether the content enclosed by the Cache Tag Helper is cached.</span></span> <span data-ttu-id="c9913-120">La valeur par défaut est `true`.</span><span class="sxs-lookup"><span data-stu-id="c9913-120">The default is `true`.</span></span>  <span data-ttu-id="c9913-121">Si la valeur `false` ce programme d’assistance de balise de Cache n’a aucun effet mise en cache sur la sortie rendue.</span><span class="sxs-lookup"><span data-stu-id="c9913-121">If set to `false` this Cache Tag Helper will have no caching effect on the rendered output.</span></span>

<span data-ttu-id="c9913-122">Exemple :</span><span class="sxs-lookup"><span data-stu-id="c9913-122">Example:</span></span>

```cshtml
<Cache enabled="true">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

- - -

### <a name="expires-on"></a><span data-ttu-id="c9913-123">expiration sur</span><span class="sxs-lookup"><span data-stu-id="c9913-123">expires-on</span></span> 

| <span data-ttu-id="c9913-124">Type d’attribut</span><span class="sxs-lookup"><span data-stu-id="c9913-124">Attribute Type</span></span>    | <span data-ttu-id="c9913-125">Exemple de valeur</span><span class="sxs-lookup"><span data-stu-id="c9913-125">Example Value</span></span>     |
|----------------   |----------------   |
| <span data-ttu-id="c9913-126">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="c9913-126">DateTimeOffset</span></span>    | <span data-ttu-id="c9913-127">«@new DateTime(2025,1,29,17,02,0) »</span><span class="sxs-lookup"><span data-stu-id="c9913-127">"@new DateTime(2025,1,29,17,02,0)"</span></span>    |


<span data-ttu-id="c9913-128">Définit une date d’expiration absolue.</span><span class="sxs-lookup"><span data-stu-id="c9913-128">Sets an absolute expiration date.</span></span> <span data-ttu-id="c9913-129">L’exemple suivant met en cache le contenu de l’application d’assistance de balise de Cache jusqu'à 5 h 02 le 29 janvier 2025.</span><span class="sxs-lookup"><span data-stu-id="c9913-129">The following example will cache the contents of the Cache Tag Helper until 5:02 PM on January 29, 2025.</span></span>

<span data-ttu-id="c9913-130">Exemple :</span><span class="sxs-lookup"><span data-stu-id="c9913-130">Example:</span></span>

```cshtml
<Cache expires-on="@new DateTime(2025,1,29,17,02,0)">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

- - -

### <a name="expires-after"></a><span data-ttu-id="c9913-131">expire après</span><span class="sxs-lookup"><span data-stu-id="c9913-131">expires-after</span></span>

| <span data-ttu-id="c9913-132">Type d’attribut</span><span class="sxs-lookup"><span data-stu-id="c9913-132">Attribute Type</span></span>    | <span data-ttu-id="c9913-133">Exemple de valeur</span><span class="sxs-lookup"><span data-stu-id="c9913-133">Example Value</span></span>     |
|----------------   |----------------   |
| <span data-ttu-id="c9913-134">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="c9913-134">TimeSpan</span></span>    | <span data-ttu-id="c9913-135">"@TimeSpan.FromSeconds(120)"</span><span class="sxs-lookup"><span data-stu-id="c9913-135">"@TimeSpan.FromSeconds(120)"</span></span>    |


<span data-ttu-id="c9913-136">Définit la durée à partir de la première demande pour mettre en cache le contenu.</span><span class="sxs-lookup"><span data-stu-id="c9913-136">Sets the length of time from the first request time to cache the contents.</span></span> 

<span data-ttu-id="c9913-137">Exemple :</span><span class="sxs-lookup"><span data-stu-id="c9913-137">Example:</span></span>

```cshtml
<Cache expires-on="@TimeSpan.FromSeconds(120)">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

- - -

### <a name="expires-sliding"></a><span data-ttu-id="c9913-138">expiration de retrait</span><span class="sxs-lookup"><span data-stu-id="c9913-138">expires-sliding</span></span>

| <span data-ttu-id="c9913-139">Type d’attribut</span><span class="sxs-lookup"><span data-stu-id="c9913-139">Attribute Type</span></span>    | <span data-ttu-id="c9913-140">Exemple de valeur</span><span class="sxs-lookup"><span data-stu-id="c9913-140">Example Value</span></span>     |
|----------------   |----------------   |
| <span data-ttu-id="c9913-141">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="c9913-141">TimeSpan</span></span>    | <span data-ttu-id="c9913-142">"@TimeSpan.FromSeconds(60)"</span><span class="sxs-lookup"><span data-stu-id="c9913-142">"@TimeSpan.FromSeconds(60)"</span></span>     |


<span data-ttu-id="c9913-143">Définit l’heure à laquelle une entrée de cache doit être supprimée si elle n’a pas été accédé.</span><span class="sxs-lookup"><span data-stu-id="c9913-143">Sets the time that a cache entry should be evicted if it has not been accessed.</span></span>

<span data-ttu-id="c9913-144">Exemple :</span><span class="sxs-lookup"><span data-stu-id="c9913-144">Example:</span></span>

```cshtml
<Cache expires-sliding="@TimeSpan.FromSeconds(60)">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

- - -

### <a name="vary-by-header"></a><span data-ttu-id="c9913-145">varient en fonction de l’en-tête</span><span class="sxs-lookup"><span data-stu-id="c9913-145">vary-by-header</span></span>

| <span data-ttu-id="c9913-146">Type d’attribut</span><span class="sxs-lookup"><span data-stu-id="c9913-146">Attribute Type</span></span>    | <span data-ttu-id="c9913-147">Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="c9913-147">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="c9913-148">Chaîne</span><span class="sxs-lookup"><span data-stu-id="c9913-148">String</span></span>            | <span data-ttu-id="c9913-149">« User-Agent »</span><span class="sxs-lookup"><span data-stu-id="c9913-149">"User-Agent"</span></span>                  |
|                   | <span data-ttu-id="c9913-150">« User-Agent, content-encoding »</span><span class="sxs-lookup"><span data-stu-id="c9913-150">"User-Agent,content-encoding"</span></span> |

<span data-ttu-id="c9913-151">Accepte une valeur d’en-tête unique ou une liste séparée par des virgules de valeurs d’en-tête qui déclenchent une actualisation du cache quand ils changent.</span><span class="sxs-lookup"><span data-stu-id="c9913-151">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when they change.</span></span> <span data-ttu-id="c9913-152">L’exemple suivant analyse la valeur d’en-tête `User-Agent`.</span><span class="sxs-lookup"><span data-stu-id="c9913-152">The following example monitors the header value `User-Agent`.</span></span> <span data-ttu-id="c9913-153">L’exemple mettra en cache le contenu de chaque autre `User-Agent` présenté au serveur web.</span><span class="sxs-lookup"><span data-stu-id="c9913-153">The example will cache the content for every different `User-Agent` presented to the web server.</span></span>

<span data-ttu-id="c9913-154">Exemple :</span><span class="sxs-lookup"><span data-stu-id="c9913-154">Example:</span></span>

```cshtml
<Cache vary-by-header="User-Agent">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

- - -

### <a name="vary-by-query"></a><span data-ttu-id="c9913-155">varient par requête</span><span class="sxs-lookup"><span data-stu-id="c9913-155">vary-by-query</span></span>

| <span data-ttu-id="c9913-156">Type d’attribut</span><span class="sxs-lookup"><span data-stu-id="c9913-156">Attribute Type</span></span>    | <span data-ttu-id="c9913-157">Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="c9913-157">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="c9913-158">Chaîne</span><span class="sxs-lookup"><span data-stu-id="c9913-158">String</span></span>            | <span data-ttu-id="c9913-159">« Vérifiez »</span><span class="sxs-lookup"><span data-stu-id="c9913-159">"Make"</span></span>                |
|                   | <span data-ttu-id="c9913-160">« Assurez-vous, modèle »</span><span class="sxs-lookup"><span data-stu-id="c9913-160">"Make,Model"</span></span> |

<span data-ttu-id="c9913-161">Accepte une valeur d’en-tête unique ou une liste séparée par des virgules de valeurs d’en-tête qui déclenchent une actualisation du cache lorsque la valeur d’en-tête.</span><span class="sxs-lookup"><span data-stu-id="c9913-161">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when the header value changes.</span></span> <span data-ttu-id="c9913-162">L’exemple suivant présente les valeurs de `Make` et `Model`.</span><span class="sxs-lookup"><span data-stu-id="c9913-162">The following example looks at the values of `Make` and `Model`.</span></span>

<span data-ttu-id="c9913-163">Exemple :</span><span class="sxs-lookup"><span data-stu-id="c9913-163">Example:</span></span>

```cshtml
<Cache vary-by-query="Make,Model">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

- - -

### <a name="vary-by-route"></a><span data-ttu-id="c9913-164">varient par itinéraire</span><span class="sxs-lookup"><span data-stu-id="c9913-164">vary-by-route</span></span>

| <span data-ttu-id="c9913-165">Type d’attribut</span><span class="sxs-lookup"><span data-stu-id="c9913-165">Attribute Type</span></span>    | <span data-ttu-id="c9913-166">Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="c9913-166">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="c9913-167">Chaîne</span><span class="sxs-lookup"><span data-stu-id="c9913-167">String</span></span>            | <span data-ttu-id="c9913-168">« Vérifiez »</span><span class="sxs-lookup"><span data-stu-id="c9913-168">"Make"</span></span>                |
|                   | <span data-ttu-id="c9913-169">« Assurez-vous, modèle »</span><span class="sxs-lookup"><span data-stu-id="c9913-169">"Make,Model"</span></span> |

<span data-ttu-id="c9913-170">Accepte une valeur d’en-tête unique ou une liste séparée par des virgules de valeurs d’en-tête qui déclenchent une actualisation du cache lorsque le paramètre de données d’itinéraire spécifiées à modifier.</span><span class="sxs-lookup"><span data-stu-id="c9913-170">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when the route data parameter value(s) change.</span></span> <span data-ttu-id="c9913-171">Exemple :</span><span class="sxs-lookup"><span data-stu-id="c9913-171">Example:</span></span>

<span data-ttu-id="c9913-172">*Startup.cs*</span><span class="sxs-lookup"><span data-stu-id="c9913-172">*Startup.cs*</span></span> 

```csharp
routes.MapRoute(
    name: "default",
    template: "{controller=Home}/{action=Index}/{Make?}/{Model?}");
```
  
<span data-ttu-id="c9913-173">*Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="c9913-173">*Index.cshtml*</span></span>

```cshtml
<Cache vary-by-route="Make,Model">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

- - -

### <a name="vary-by-cookie"></a><span data-ttu-id="c9913-174">varient par cookie</span><span class="sxs-lookup"><span data-stu-id="c9913-174">vary-by-cookie</span></span>

| <span data-ttu-id="c9913-175">Type d’attribut</span><span class="sxs-lookup"><span data-stu-id="c9913-175">Attribute Type</span></span>    | <span data-ttu-id="c9913-176">Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="c9913-176">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="c9913-177">Chaîne</span><span class="sxs-lookup"><span data-stu-id="c9913-177">String</span></span>            | <span data-ttu-id="c9913-178">". AspNetCore.Identity.Application »</span><span class="sxs-lookup"><span data-stu-id="c9913-178">".AspNetCore.Identity.Application"</span></span>                |
|                   | <span data-ttu-id="c9913-179">". AspNetCore.Identity.Application,HairColor »</span><span class="sxs-lookup"><span data-stu-id="c9913-179">".AspNetCore.Identity.Application,HairColor"</span></span> |

<span data-ttu-id="c9913-180">Accepte une valeur d’en-tête unique ou une liste séparée par des virgules de valeurs d’en-tête qui déclenchent une actualisation du cache lorsque les valeurs d’en-tête changement de (s).</span><span class="sxs-lookup"><span data-stu-id="c9913-180">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when the header values(s) change.</span></span> <span data-ttu-id="c9913-181">L’exemple suivant présente le cookie associé d’identité ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c9913-181">The following example looks at the cookie associated with ASP.NET Identity.</span></span> <span data-ttu-id="c9913-182">Lorsqu’un utilisateur est authentifié le cookie de la demande à définir qui déclenche une actualisation du cache.</span><span class="sxs-lookup"><span data-stu-id="c9913-182">When a user is authenticated the request cookie to be set which triggers a cache refresh.</span></span>

<span data-ttu-id="c9913-183">Exemple :</span><span class="sxs-lookup"><span data-stu-id="c9913-183">Example:</span></span>

```cshtml
<Cache vary-by-cookie=".AspNetCore.Identity.Application">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

- - -

### <a name="vary-by-user"></a><span data-ttu-id="c9913-184">varient par utilisateur</span><span class="sxs-lookup"><span data-stu-id="c9913-184">vary-by-user</span></span>

| <span data-ttu-id="c9913-185">Type d’attribut</span><span class="sxs-lookup"><span data-stu-id="c9913-185">Attribute Type</span></span>    | <span data-ttu-id="c9913-186">Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="c9913-186">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="c9913-187">Booléen</span><span class="sxs-lookup"><span data-stu-id="c9913-187">Boolean</span></span>             | <span data-ttu-id="c9913-188">"true"</span><span class="sxs-lookup"><span data-stu-id="c9913-188">"true"</span></span>                  |
|                     | <span data-ttu-id="c9913-189">« false » (valeur par défaut)</span><span class="sxs-lookup"><span data-stu-id="c9913-189">"false" (default)</span></span> |

<span data-ttu-id="c9913-190">Spécifie si le cache doit réinitialiser lorsque l’utilisateur connecté (ou Principal du contexte) change.</span><span class="sxs-lookup"><span data-stu-id="c9913-190">Specifies whether or not the cache should reset when the logged-in user (or Context Principal) changes.</span></span> <span data-ttu-id="c9913-191">L’utilisateur actuel est également connue sous le Principal demande du contexte et peuvent être affiché dans une vue Razor en référençant `@User.Identity.Name`.</span><span class="sxs-lookup"><span data-stu-id="c9913-191">The current user is also known as the Request Context Principal and can be viewed in a Razor view by referencing `@User.Identity.Name`.</span></span>

<span data-ttu-id="c9913-192">L’exemple suivant ressemble au niveau de l’utilisateur actuellement connecté.</span><span class="sxs-lookup"><span data-stu-id="c9913-192">The following example looks at the current logged in user.</span></span>  

<span data-ttu-id="c9913-193">Exemple :</span><span class="sxs-lookup"><span data-stu-id="c9913-193">Example:</span></span>

```cshtml
<Cache vary-by-user="true">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

<span data-ttu-id="c9913-194">À l’aide de cet attribut gère le contenu dans le cache via un cycle de connexion et déconnexion.</span><span class="sxs-lookup"><span data-stu-id="c9913-194">Using this attribute maintains the contents in cache through a log-in and log-out cycle.</span></span>  <span data-ttu-id="c9913-195">Lorsque vous utilisez `vary-by-user="true"`, une action de connexion et déconnexion invalide le cache pour l’utilisateur authentifié.</span><span class="sxs-lookup"><span data-stu-id="c9913-195">When using `vary-by-user="true"`, a log-in and log-out action invalidates the cache for the authenticated user.</span></span>  <span data-ttu-id="c9913-196">Le cache est invalidé, car une nouvelle valeur de cookie unique est générée sur la connexion.</span><span class="sxs-lookup"><span data-stu-id="c9913-196">The cache is invalidated because a new unique cookie value is generated on login.</span></span> <span data-ttu-id="c9913-197">Cache est conservé à l’état anonyme lorsque aucun cookie n’est présent ou a expiré.</span><span class="sxs-lookup"><span data-stu-id="c9913-197">Cache is maintained for the anonymous state when no cookie is present or has expired.</span></span> <span data-ttu-id="c9913-198">Cela signifie que si aucun utilisateur n’est connecté, le cache est conservé.</span><span class="sxs-lookup"><span data-stu-id="c9913-198">This means if no user is logged in, the cache will be maintained.</span></span>

- - -

### <a name="vary-by"></a><span data-ttu-id="c9913-199">variation de</span><span class="sxs-lookup"><span data-stu-id="c9913-199">vary-by</span></span>

| <span data-ttu-id="c9913-200">Type d’attribut</span><span class="sxs-lookup"><span data-stu-id="c9913-200">Attribute Type</span></span>    | <span data-ttu-id="c9913-201">Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="c9913-201">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="c9913-202">Chaîne</span><span class="sxs-lookup"><span data-stu-id="c9913-202">String</span></span>             | <span data-ttu-id="c9913-203">"@Model"</span><span class="sxs-lookup"><span data-stu-id="c9913-203">"@Model"</span></span>                 |


<span data-ttu-id="c9913-204">Permet la personnalisation de données obtient mis en cache.</span><span class="sxs-lookup"><span data-stu-id="c9913-204">Allows for customization of what data gets cached.</span></span> <span data-ttu-id="c9913-205">Lorsque l’objet référencé par les modifications apportées à la valeur de la chaîne de l’attribut, le contenu de l’application d’assistance de balise de Cache est mis à jour.</span><span class="sxs-lookup"><span data-stu-id="c9913-205">When the object referenced by the attribute's string value changes, the content of the Cache Tag Helper is updated.</span></span> <span data-ttu-id="c9913-206">Fréquence à laquelle une concaténation de chaînes de valeurs de modèle sont affectées à cet attribut.</span><span class="sxs-lookup"><span data-stu-id="c9913-206">Often a string-concatenation of model values are assigned to this attribute.</span></span>  <span data-ttu-id="c9913-207">En effet, cela signifie qu'une mise à jour à une des valeurs concaténées invalide le cache.</span><span class="sxs-lookup"><span data-stu-id="c9913-207">Effectively, that means an update to any of the concatenated values invalidates the cache.</span></span>

<span data-ttu-id="c9913-208">L’exemple suivant suppose la somme de la vue de rendu de la valeur entière des deux paramètres d’itinéraire, la méthode du contrôleur `myParam1` et `myParam2`et qui retourne en tant que la propriété de modèle unique.</span><span class="sxs-lookup"><span data-stu-id="c9913-208">The following example assumes the controller method rendering the view sums the integer value of the two route parameters, `myParam1` and `myParam2`, and returns that as the single model property.</span></span> <span data-ttu-id="c9913-209">Lorsque cette somme est modifié, le contenu de l’application d’assistance de balise de Cache est rendu et mis en cache à nouveau.</span><span class="sxs-lookup"><span data-stu-id="c9913-209">When this sum changes, the content of the Cache Tag Helper is rendered and cached again.</span></span>  

<span data-ttu-id="c9913-210">Exemple :</span><span class="sxs-lookup"><span data-stu-id="c9913-210">Example:</span></span>

<span data-ttu-id="c9913-211">Action :</span><span class="sxs-lookup"><span data-stu-id="c9913-211">Action:</span></span>

```csharp
public IActionResult Index(string myParam1,string myParam2,string myParam3)
{
    int num1;
    int num2;
    int.TryParse(myParam1, out num1);
    int.TryParse(myParam2, out num2);
    return View(viewName, num1 + num2);
}
```

<span data-ttu-id="c9913-212">*Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="c9913-212">*Index.cshtml*</span></span>

```cshtml
<Cache vary-by="@Model"">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

- - -

### <a name="priority"></a><span data-ttu-id="c9913-213">priority</span><span class="sxs-lookup"><span data-stu-id="c9913-213">priority</span></span>

| <span data-ttu-id="c9913-214">Type d’attribut</span><span class="sxs-lookup"><span data-stu-id="c9913-214">Attribute Type</span></span>    | <span data-ttu-id="c9913-215">Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="c9913-215">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="c9913-216">Énumération CacheItemPriority</span><span class="sxs-lookup"><span data-stu-id="c9913-216">CacheItemPriority</span></span>  | <span data-ttu-id="c9913-217">« High »</span><span class="sxs-lookup"><span data-stu-id="c9913-217">"High"</span></span>                   |
|                    | <span data-ttu-id="c9913-218">« Low »</span><span class="sxs-lookup"><span data-stu-id="c9913-218">"Low"</span></span> |
|                    | <span data-ttu-id="c9913-219">« NeverRemove »</span><span class="sxs-lookup"><span data-stu-id="c9913-219">"NeverRemove"</span></span> |
|                    | <span data-ttu-id="c9913-220">« Normal »</span><span class="sxs-lookup"><span data-stu-id="c9913-220">"Normal"</span></span> |

<span data-ttu-id="c9913-221">Fournit des instructions de suppression de cache au fournisseur de cache intégré.</span><span class="sxs-lookup"><span data-stu-id="c9913-221">Provides cache eviction guidance to the built-in cache provider.</span></span> <span data-ttu-id="c9913-222">Supprimez le serveur web `Low` mettre en cache les entrées tout d’abord une mémoire insuffisante.</span><span class="sxs-lookup"><span data-stu-id="c9913-222">The web server will evict `Low` cache entries first when it's under memory pressure.</span></span>

<span data-ttu-id="c9913-223">Exemple :</span><span class="sxs-lookup"><span data-stu-id="c9913-223">Example:</span></span>

```cshtml
<Cache priority="High">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

<span data-ttu-id="c9913-224">Le `priority` attribut ne garantit pas un niveau spécifique de la rétention du cache.</span><span class="sxs-lookup"><span data-stu-id="c9913-224">The `priority` attribute does not guarantee a specific level of cache retention.</span></span> <span data-ttu-id="c9913-225">`CacheItemPriority`est uniquement une suggestion.</span><span class="sxs-lookup"><span data-stu-id="c9913-225">`CacheItemPriority` is only a suggestion.</span></span> <span data-ttu-id="c9913-226">Cet attribut `NeverRemove` ne garantit pas que le cache est conservé.</span><span class="sxs-lookup"><span data-stu-id="c9913-226">Setting this attribute to `NeverRemove` does not guarantee that the cache will always be retained.</span></span> <span data-ttu-id="c9913-227">Consultez [des ressources supplémentaires](#additional-resources) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="c9913-227">See [Additional Resources](#additional-resources) for more information.</span></span>

<span data-ttu-id="c9913-228">L’application d’assistance de balise de Cache est dépendante de la [du service de cache mémoire](xref:performance/caching/memory).</span><span class="sxs-lookup"><span data-stu-id="c9913-228">The Cache Tag Helper is dependent on the [memory cache service](xref:performance/caching/memory).</span></span> <span data-ttu-id="c9913-229">L’application d’assistance de balise de Cache ajoute le service s’il n’a pas été ajouté.</span><span class="sxs-lookup"><span data-stu-id="c9913-229">The Cache Tag Helper adds the service if it has not been added.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c9913-230">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c9913-230">Additional resources</span></span>

* <xref:performance/caching/memory>
* <xref:security/authentication/identity>