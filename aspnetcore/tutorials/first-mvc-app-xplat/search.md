---
title: "Ajout d’une fonction de recherche"
author: rick-anderson
description: "Montre comment ajouter une fonction de recherche à une application ASP.NET MVC simple"
keywords: ASP.NET Core,
ms.author: riande
manager: wpickett
ms.date: 04/07/2017
ms.topic: get-started-article
ms.assetid: d69e5529-ffff-4628-855d-200206d96269
ms.technology: aspnet
ms.prod: asp.net-core
uid: tutorials/first-mvc-app-xplat/search
ms.openlocfilehash: 57419c697aea80a054e906c75002f5a39c512fc6
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/10/2017
---
[!INCLUDE[adding-model](../../includes/mvc-intro/search1.md)]

<span data-ttu-id="d9a49-104">Remarque : SQLite respecte la casse, vous devez donc rechercher « Ghost » et non pas « ghost ».</span><span class="sxs-lookup"><span data-stu-id="d9a49-104">Note: SQLlite is case sensitive, so you'll need to search for "Ghost" and not "ghost".</span></span>

[!INCLUDE[adding-model](../../includes/mvc-intro/search2.md)]

<span data-ttu-id="d9a49-105">Changez la balise `<form>` dans la vue Razor *Views\movie\Index.cshtml* pour spécifier `method="get"` :</span><span class="sxs-lookup"><span data-stu-id="d9a49-105">Change the `<form>` tag in the *Views\movie\Index.cshtml* Razor view to specify `method="get"`:</span></span>

```html
<form asp-controller="Movies" asp-action="Index" method="get">
```

[!INCLUDE[adding-model](../../includes/mvc-intro/search3.md)]

>[!div class="step-by-step"]
<span data-ttu-id="d9a49-106">[Précédent - Méthodes et vues du contrôleur](controller-methods-views.md)
[Suivant - Ajouter un champ](new-field.md)</span><span class="sxs-lookup"><span data-stu-id="d9a49-106">[Previous - Controller methods and views](controller-methods-views.md)
[Next - Add a field](new-field.md)</span></span>  
