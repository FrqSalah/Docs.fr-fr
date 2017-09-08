---
title: "Prise en main de l’API de Protection des données"
author: rick-anderson
description: 
keywords: ASP.NET Core,
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: 39b7a73c-29d4-4137-b311-49529adcf3cb
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/using-data-protection
ms.openlocfilehash: 2a381acf5faa7071fe4a22641037fcee11f6d362
ms.sourcegitcommit: 0b6c8e6d81d2b3c161cd375036eecbace46a9707
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/11/2017
---
# <a name="getting-started-with-the-data-protection-apis"></a>Prise en main de l’API de Protection des données

<a name=security-data-protection-getting-started></a>

Aux protection des données la plus simple se compose des étapes suivantes :

1. Créer un données protecteur à partir d’un fournisseur de protection des données.

2. Appelez la méthode de protection avec les données que vous souhaitez protéger.

3. Appelez la méthode de suppression de la protection avec les données que vous souhaitez reconvertir en texte brut.

La plupart des infrastructures telles que ASP.NET ou SignalR déjà configurer le système de protection des données et l’ajouter à un conteneur de service que vous pouvez accéder via l’injection de dépendances. L’exemple suivant montre comment configurer un conteneur de service pour l’injection de dépendance et l’inscription de la pile de protection des données, recevoir le fournisseur de protection des données via DI, création d’un protecteur et la protection puis ôter la protection des données

[!code-csharp[Main](../../security/data-protection/using-data-protection/samples/protectunprotect.cs?highlight=26,34,35,36,37,38,39,40)]

Lorsque vous créez un logiciel de protection, vous devez fournir un ou plusieurs [objectif chaînes](consumer-apis/purpose-strings.md). Une chaîne de l’objet fournit une isolation entre les consommateurs, par exemple un protecteur créé avec une chaîne de l’objectif de « vert » ne serait pas en mesure de déprotéger les données fournies par un protecteur dans un but de « violet ».

>[!TIP]
> Instances de IDataProtectionProvider et IDataProtector sont thread-safe pour les appelants plusieurs. Il est prévu qu’une fois qu’un composant obtient une référence à un IDataProtector via un appel à CreateProtector, il utilisera cette référence pour plusieurs appels à protéger et de suppression de la protection.
>
>Un appel à Unprotect lève CryptographicException si la charge utile protégée ne peut pas être vérifiée ou déchiffrée. Certains composants peuvent souhaiter ignorer les erreurs pendant les opérations ; ôter la protection un composant qui lit les cookies d’authentification peut gérer cette erreur et traiter la demande comme s’il n’avait aucun cookie tout plutôt qu’échouer la requête ferme. Les composants dont vous souhaitez que ce comportement doivent spécifiquement intercepter CryptographicException au lieu d’absorber toutes les exceptions.
