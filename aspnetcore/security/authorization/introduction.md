---
title: Introduction
author: rick-anderson
description: 
keywords: ASP.NET Core,
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: a6a556ed-ba59-4107-9358-44cf20e5931b
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authorization/introduction
ms.openlocfilehash: 040525505a982fc1be1901effb9186a8fe1cdbdf
ms.sourcegitcommit: 0b6c8e6d81d2b3c161cd375036eecbace46a9707
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/11/2017
---
# <a name="introduction"></a><span data-ttu-id="7bae2-103">Introduction</span><span class="sxs-lookup"><span data-stu-id="7bae2-103">Introduction</span></span>

<a name=security-authorization-introduction></a>

<span data-ttu-id="7bae2-104">Autorisation désigne le processus qui détermine ce qu’un utilisateur est en mesure d’effectuer.</span><span class="sxs-lookup"><span data-stu-id="7bae2-104">Authorization refers to the process that determines what a user is able to do.</span></span> <span data-ttu-id="7bae2-105">Par exemple, un utilisateur administratif est autorisé à créer une bibliothèque de documents, ajoutez les documents, modifier des documents et les supprimer.</span><span class="sxs-lookup"><span data-stu-id="7bae2-105">For example, an administrative user is allowed to create a document library, add documents, edit documents, and delete them.</span></span> <span data-ttu-id="7bae2-106">Un utilisateur non-administrateur, utilisation de la bibliothèque est uniquement autorisé à lire les documents.</span><span class="sxs-lookup"><span data-stu-id="7bae2-106">A non-administrative user working with the library is only authorized to read the documents.</span></span>

<span data-ttu-id="7bae2-107">L’autorisation est orthogonales et indépendante de l’authentification, qui est le processus d’évaluation qui est un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7bae2-107">Authorization is orthogonal and independent from authentication, which is the process of ascertaining who a user is.</span></span> <span data-ttu-id="7bae2-108">L’authentification peut créer une ou plusieurs identités pour l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="7bae2-108">Authentication may create one or more identities for the current user.</span></span>

## <a name="authorization-types"></a><span data-ttu-id="7bae2-109">Types d’autorisation</span><span class="sxs-lookup"><span data-stu-id="7bae2-109">Authorization Types</span></span>

<span data-ttu-id="7bae2-110">Autorisation de ASP.NET Core fournit un simple déclaratif [rôle](roles.md#security-authorization-role-based) et un [enrichie basée sur la stratégie](policies.md#security-authorization-policies-based) modèle.</span><span class="sxs-lookup"><span data-stu-id="7bae2-110">ASP.NET Core authorization provides a simple declarative [role](roles.md#security-authorization-role-based) and a [rich policy based](policies.md#security-authorization-policies-based) model.</span></span> <span data-ttu-id="7bae2-111">L’autorisation est exprimée dans la configuration requise et gestionnaires d’évaluent les revendications d’un utilisateur par rapport aux exigences.</span><span class="sxs-lookup"><span data-stu-id="7bae2-111">Authorization is expressed in requirements, and handlers evaluate a user's claims against requirements.</span></span> <span data-ttu-id="7bae2-112">Vérifications impératives peuvent reposer sur des stratégies simples ou qui évaluent l’identité de l’utilisateur et les propriétés de la ressource à laquelle l’utilisateur tente d’accéder.</span><span class="sxs-lookup"><span data-stu-id="7bae2-112">Imperative checks can be based on simple policies or policies which evaluate both the user identity and properties of the resource that the user is attempting to access.</span></span>

## <a name="namespaces"></a><span data-ttu-id="7bae2-113">Espaces de noms</span><span class="sxs-lookup"><span data-stu-id="7bae2-113">Namespaces</span></span>

<span data-ttu-id="7bae2-114">Les composants d’autorisation, y compris le `AuthorizeAttribute` et `AllowAnonymousAttribute` attributs sont trouvent dans le `Microsoft.AspNetCore.Authorization` espace de noms.</span><span class="sxs-lookup"><span data-stu-id="7bae2-114">Authorization components, including the `AuthorizeAttribute` and `AllowAnonymousAttribute` attributes are found in the `Microsoft.AspNetCore.Authorization` namespace.</span></span>
