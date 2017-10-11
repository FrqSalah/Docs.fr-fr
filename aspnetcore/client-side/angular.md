---
title: "À l’aide d’AngularJS pour des Applications à Page unique (ZPS)"
author: rick-anderson
description: "Découvrez comment créer une application de style SPA ASP.NET à l’aide d’AngularJS"
keywords: ASP.NET Core, AngularJS, SPA
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: 4b30576b-2718-4c39-9253-a59966747893
ms.technology: aspnet
ms.prod: asp.net-core
uid: client-side/angular
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4aecf9e9bd11cc7e2b36b40955178d9e9368c185
ms.sourcegitcommit: 732cd2684246e49e796836596643a8d37e20c46d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/01/2017
---
# <a name="using-angularjs-for-single-page-applications-spas-with-aspnet-core"></a><span data-ttu-id="189ff-104">À l’aide d’AngularJS pour des Applications à Page unique (ZPS) avec ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="189ff-104">Using AngularJS for Single Page Applications (SPAs) with ASP.NET Core</span></span>


<span data-ttu-id="189ff-105">Par [Venkata Koppaka](https://blog.falafel.com/falafel-software-recognized-sitefinity-website-year/) et [Scott Addie](https://scottaddie.com)</span><span class="sxs-lookup"><span data-stu-id="189ff-105">By [Venkata Koppaka](https://blog.falafel.com/falafel-software-recognized-sitefinity-website-year/) and [Scott Addie](https://scottaddie.com)</span></span>

<span data-ttu-id="189ff-106">Dans cet article, vous allez apprendre à créer une application de style SPA ASP.NET à l’aide d’AngularJS.</span><span class="sxs-lookup"><span data-stu-id="189ff-106">In this article, you will learn how to build a SPA-style ASP.NET application using AngularJS.</span></span>

<span data-ttu-id="189ff-107">[Afficher ou télécharger l’exemple de code](https://github.com/aspnet/Docs/tree/master/aspnetcore/client-side/angular/sample) ([comment télécharger](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="189ff-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/client-side/angular/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="what-is-angularjs"></a><span data-ttu-id="189ff-108">Nouveautés AngularJS</span><span class="sxs-lookup"><span data-stu-id="189ff-108">What is AngularJS?</span></span>

<span data-ttu-id="189ff-109">[AngularJS](https://angularjs.org/) est une infrastructure JavaScript moderne à partir de Google couramment utilisé pour travailler avec des Applications à Page unique (ZPS).</span><span class="sxs-lookup"><span data-stu-id="189ff-109">[AngularJS](https://angularjs.org/) is a modern JavaScript framework from Google commonly used to work with Single Page Applications (SPAs).</span></span> <span data-ttu-id="189ff-110">AngularJS est open source sous licence du MIT, et la progression du développement d’AngularJS peut être suivie [son référentiel GitHub](https://github.com/angular/angular.js).</span><span class="sxs-lookup"><span data-stu-id="189ff-110">AngularJS is open sourced under MIT license, and the development progress of AngularJS can be followed on [its GitHub repository](https://github.com/angular/angular.js).</span></span> <span data-ttu-id="189ff-111">La bibliothèque est appelée angulaire car HTML utilise des crochets de forme angulaire.</span><span class="sxs-lookup"><span data-stu-id="189ff-111">The library is called Angular because HTML uses angular-shaped brackets.</span></span>

<span data-ttu-id="189ff-112">AngularJS n’est pas une bibliothèque de manipulation de DOM comme jQuery, mais il utilise un sous-ensemble de jQuery, appelé jQLite.</span><span class="sxs-lookup"><span data-stu-id="189ff-112">AngularJS is not a DOM manipulation library like jQuery, but it uses a subset of jQuery called jQLite.</span></span> <span data-ttu-id="189ff-113">AngularJS est principalement basée sur des attributs déclaratifs HTML que vous pouvez ajouter à vos balises HTML.</span><span class="sxs-lookup"><span data-stu-id="189ff-113">AngularJS is primarily based on declarative HTML attributes that you can add to your HTML tags.</span></span> <span data-ttu-id="189ff-114">Vous pouvez essayer de AngularJS dans votre navigateur à l’aide de la [site Web de l’école de Code](https://www.codeschool.com/courses/shaping-up-with-angularjs) ou [site Web de W3Schools](https://www.w3schools.com/angular/).</span><span class="sxs-lookup"><span data-stu-id="189ff-114">You can try AngularJS in your browser using the [Code School website](https://www.codeschool.com/courses/shaping-up-with-angularjs) or  [W3Schools website](https://www.w3schools.com/angular/).</span></span>

<span data-ttu-id="189ff-115">Cet article se concentre sur AngularJS avec quelques remarques sur où angulaire est un en-tête.</span><span class="sxs-lookup"><span data-stu-id="189ff-115">This article focuses on AngularJS with some notes on where Angular is heading.</span></span>

## <a name="getting-started"></a><span data-ttu-id="189ff-116">Bien démarrer</span><span class="sxs-lookup"><span data-stu-id="189ff-116">Getting started</span></span>

<span data-ttu-id="189ff-117">Pour démarrer à l’aide d’AngularJS dans votre application ASP.NET, vous devez l’installer en tant que partie de votre projet, ou référencer à partir d’un réseau de diffusion de contenu (CDN).</span><span class="sxs-lookup"><span data-stu-id="189ff-117">To start using AngularJS in your ASP.NET application, you must either install it as part of your project, or reference it from a content delivery network (CDN).</span></span>

### <a name="installation"></a><span data-ttu-id="189ff-118">Installation</span><span class="sxs-lookup"><span data-stu-id="189ff-118">Installation</span></span>

<span data-ttu-id="189ff-119">Il existe plusieurs façons d’ajouter AngularJS à votre application.</span><span class="sxs-lookup"><span data-stu-id="189ff-119">There are several ways to add AngularJS to your application.</span></span> <span data-ttu-id="189ff-120">Si vous démarrez une application web ASP.NET Core dans Visual Studio, vous pouvez ajouter AngularJS à l’aide de la fonction intégrée [Bower](bower.md) prennent en charge.</span><span class="sxs-lookup"><span data-stu-id="189ff-120">If you’re starting a new ASP.NET Core web application in Visual Studio, you can add AngularJS using the built-in [Bower](bower.md) support.</span></span> <span data-ttu-id="189ff-121">Ouvrez *bower.json*et ajouter une entrée à la `dependencies` propriété :</span><span class="sxs-lookup"><span data-stu-id="189ff-121">Open *bower.json*, and add an entry to the `dependencies` property:</span></span>

<a name=angular-bower-json></a>

[!code-json[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/bower.json?highlight=9)]

<span data-ttu-id="189ff-122">Lors de l’enregistrement du *bower.json* fichier angulaire est installé dans votre projet *wwwroot/lib* dossier.</span><span class="sxs-lookup"><span data-stu-id="189ff-122">Upon saving the *bower.json* file, Angular will be installed in your project's *wwwroot/lib* folder.</span></span> <span data-ttu-id="189ff-123">En outre, il sera répertorié dans le `Dependencies/Bower` dossier.</span><span class="sxs-lookup"><span data-stu-id="189ff-123">Additionally, it will be listed within the `Dependencies/Bower` folder.</span></span> <span data-ttu-id="189ff-124">Consultez la capture d’écran ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="189ff-124">See the screenshot below.</span></span>

![Explorateur de solutions avec AngularJS projet](angular/_static/angular-solution-explorer.png)

<span data-ttu-id="189ff-126">Ensuite, ajoutez un `<script>` référence vers le bas de la `<body>` section de votre page HTML ou *_Layout.cshtml* de fichiers, comme indiqué ici :</span><span class="sxs-lookup"><span data-stu-id="189ff-126">Next, add a `<script>` reference to the bottom of the `<body>` section of your HTML page or *_Layout.cshtml* file, as shown here:</span></span>

[!code-html[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/Views/Shared/_Layout.cshtml?highlight=4&range=48-52)]

<span data-ttu-id="189ff-127">Il est recommandé que les applications de production utilisent CDN pour les bibliothèques communes comme AngularJS.</span><span class="sxs-lookup"><span data-stu-id="189ff-127">It's recommended that production applications utilize CDNs for common libraries like AngularJS.</span></span> <span data-ttu-id="189ff-128">Vous pouvez référencer AngularJS parmi plusieurs CDN, telles que celle-ci :</span><span class="sxs-lookup"><span data-stu-id="189ff-128">You can reference AngularJS from one of several CDNs, such as this one:</span></span>

[!code-html[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/Views/Shared/_Layout.cshtml?highlight=10&range=53-67)]

<span data-ttu-id="189ff-129">Une fois que vous avez une référence à la *angular.js* fichier de script, vous êtes prêt à commencer à l’aide d’AngularJS dans vos pages web.</span><span class="sxs-lookup"><span data-stu-id="189ff-129">Once you have a reference to the *angular.js* script file, you're ready to begin using AngularJS in your web pages.</span></span>

## <a name="key-components"></a><span data-ttu-id="189ff-130">Composants clés</span><span class="sxs-lookup"><span data-stu-id="189ff-130">Key components</span></span>

<span data-ttu-id="189ff-131">AngularJS inclut un nombre de composants principaux, tels que *directives*, *modèles*, *répéteurs*, *modules*,  *contrôleurs*, *composants*, *routeur de composant* et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="189ff-131">AngularJS includes a number of major components, such as *directives*, *templates*, *repeaters*, *modules*, *controllers*, *components*, *component router* and more.</span></span> <span data-ttu-id="189ff-132">Nous allons examiner comment ces composants fonctionnent ensemble pour ajouter un comportement à vos pages web.</span><span class="sxs-lookup"><span data-stu-id="189ff-132">Let's examine how these components work together to add behavior to your web pages.</span></span>

### <a name="directives"></a><span data-ttu-id="189ff-133">Directives</span><span class="sxs-lookup"><span data-stu-id="189ff-133">Directives</span></span>

<span data-ttu-id="189ff-134">AngularJS utilise [directives](https://docs.angularjs.org/guide/directive) pour étendre le HTML avec des éléments et attributs personnalisés.</span><span class="sxs-lookup"><span data-stu-id="189ff-134">AngularJS uses [directives](https://docs.angularjs.org/guide/directive) to extend HTML with custom attributes and elements.</span></span> <span data-ttu-id="189ff-135">Les directives AngularJS sont définis `data-ng-*` ou `ng-*` préfixes (`ng` est l’abréviation d’angulaire).</span><span class="sxs-lookup"><span data-stu-id="189ff-135">AngularJS directives are defined via `data-ng-*` or `ng-*` prefixes (`ng` is short for angular).</span></span> <span data-ttu-id="189ff-136">Il existe deux types de directives AngularJS :</span><span class="sxs-lookup"><span data-stu-id="189ff-136">There are two types of AngularJS directives:</span></span>

   1. <span data-ttu-id="189ff-137">**Directives primitifs**: ceux-ci sont prédéfinis par l’équipe angulaire et font partie de l’infrastructure AngularJS.</span><span class="sxs-lookup"><span data-stu-id="189ff-137">**Primitive Directives**: These are predefined by the Angular team and are part of the AngularJS framework.</span></span>

   2. <span data-ttu-id="189ff-138">**Directives personnalisées**: il s’agit des directives personnalisées que vous pouvez définir.</span><span class="sxs-lookup"><span data-stu-id="189ff-138">**Custom Directives**: These are custom directives that you can define.</span></span>

<span data-ttu-id="189ff-139">Une des directives primitifs utilisés dans toutes les applications AngularJS est la `ng-app` directive amorce l’application AngularJS.</span><span class="sxs-lookup"><span data-stu-id="189ff-139">One of the primitive directives used in all AngularJS applications is the `ng-app` directive, which bootstraps the AngularJS application.</span></span> <span data-ttu-id="189ff-140">Cette directive peut être appliquée à la `<body>` balise ou à un élément enfant du corps.</span><span class="sxs-lookup"><span data-stu-id="189ff-140">This directive can be applied to the `<body>` tag or to a child element of the body.</span></span> <span data-ttu-id="189ff-141">Examinons un exemple en action.</span><span class="sxs-lookup"><span data-stu-id="189ff-141">Let's see an example in action.</span></span> <span data-ttu-id="189ff-142">En supposant que vous êtes dans un projet ASP.NET, vous pouvez ajouter un fichier HTML pour le `wwwroot` dossier, ou ajoutez une nouvelle action de contrôleur et une vue associée.</span><span class="sxs-lookup"><span data-stu-id="189ff-142">Assuming you're in an ASP.NET project, you can either add an HTML file to the `wwwroot` folder, or add a new controller action and an associated view.</span></span> <span data-ttu-id="189ff-143">Dans ce cas, j’ai ajouté une nouvelle `Directives` méthode d’action à `HomeController.cs`.</span><span class="sxs-lookup"><span data-stu-id="189ff-143">In this case, I've added a new `Directives` action method to `HomeController.cs`.</span></span> <span data-ttu-id="189ff-144">La vue associée est illustrée ici :</span><span class="sxs-lookup"><span data-stu-id="189ff-144">The associated view is shown here:</span></span>

[!code-html[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/Views/Home/Directives.cshtml?highlight=5,7)]

<span data-ttu-id="189ff-145">Pour conserver ces exemples indépendants, je n’utilise le fichier de disposition partagé.</span><span class="sxs-lookup"><span data-stu-id="189ff-145">To keep these samples independent of one another, I'm not using the shared layout file.</span></span> <span data-ttu-id="189ff-146">Vous pouvez voir que nous décorées la balise body avec la `ng-app` directive pour indiquer cette page est une application AngularJS.</span><span class="sxs-lookup"><span data-stu-id="189ff-146">You can see that we decorated the body tag with the `ng-app` directive to indicate this page is an AngularJS application.</span></span> <span data-ttu-id="189ff-147">Le `{{2+2}}` est une expression de liaison de données angulaire vous découvrirez plus tard.</span><span class="sxs-lookup"><span data-stu-id="189ff-147">The `{{2+2}}` is an Angular data binding expression that you will learn more about in a moment.</span></span> <span data-ttu-id="189ff-148">Voici le résultat si vous exécutez cette application :</span><span class="sxs-lookup"><span data-stu-id="189ff-148">Here is the result if you run this application:</span></span>

![Directive angulaire simple](angular/_static/simple-directive.png)

<span data-ttu-id="189ff-150">Autres directives AngularJS primitifs sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="189ff-150">Other primitive directives in AngularJS include:</span></span>

<span data-ttu-id="189ff-151">`ng-controller`Détermine quel contrôleur JavaScript est lié à la vue.</span><span class="sxs-lookup"><span data-stu-id="189ff-151">`ng-controller` Determines which JavaScript controller is bound to which view.</span></span>

<span data-ttu-id="189ff-152">`ng-model`Détermine le modèle auquel les valeurs des propriétés d’un élément HTML sont liées.</span><span class="sxs-lookup"><span data-stu-id="189ff-152">`ng-model` Determines the model to which the values of an HTML element's properties are bound.</span></span>

<span data-ttu-id="189ff-153">`ng-init`Utilisé pour initialiser les données d’application sous la forme d’une expression de l’étendue actuelle.</span><span class="sxs-lookup"><span data-stu-id="189ff-153">`ng-init` Used to initialize the application data in the form of an expression for the current scope.</span></span>

<span data-ttu-id="189ff-154">`ng-if`Supprime ou recrée l’élément HTML donné dans le DOM en fonction de la truthiness de l’expression fournie.</span><span class="sxs-lookup"><span data-stu-id="189ff-154">`ng-if` Removes or recreates the given HTML element in the DOM based on the truthiness of the expression provided.</span></span>

<span data-ttu-id="189ff-155">`ng-repeat`Répète un bloc de code HTML donné sur un jeu de données.</span><span class="sxs-lookup"><span data-stu-id="189ff-155">`ng-repeat` Repeats a given block of HTML over a set of data.</span></span>

<span data-ttu-id="189ff-156">`ng-show`Affiche ou masque l’élément HTML donné en fonction de l’expression fournie.</span><span class="sxs-lookup"><span data-stu-id="189ff-156">`ng-show` Shows or hides the given HTML element based on the expression provided.</span></span>

<span data-ttu-id="189ff-157">Pour obtenir une liste complète de toutes les directives primitifs pris en charge dans AngularJS, reportez-vous à la [section documentation directive sur le site Web de documentation AngularJS](https://docs.angularjs.org/api/ng/directive).</span><span class="sxs-lookup"><span data-stu-id="189ff-157">For a full list of all primitive directives supported in AngularJS, please refer to the [directive documentation section on the AngularJS documentation website](https://docs.angularjs.org/api/ng/directive).</span></span>

### <a name="data-binding"></a><span data-ttu-id="189ff-158">Liaison de données</span><span class="sxs-lookup"><span data-stu-id="189ff-158">Data binding</span></span>

<span data-ttu-id="189ff-159">Fournit des AngularJS [liaison de données](https://docs.angularjs.org/guide/databinding) out-of-the-box à l’aide de prendre en charge la `ng-bind` directive ou une syntaxe d’expression de liaison comme des données `{{expression}}`.</span><span class="sxs-lookup"><span data-stu-id="189ff-159">AngularJS provides [data binding](https://docs.angularjs.org/guide/databinding) support out-of-the-box using either the `ng-bind` directive or a data binding expression syntax such as `{{expression}}`.</span></span> <span data-ttu-id="189ff-160">AngularJS prend en charge la liaison de données bidirectionnelle où les données à partir d’un modèle sont conservées dans la synchronisation avec un modèle d’affichage à tout moment.</span><span class="sxs-lookup"><span data-stu-id="189ff-160">AngularJS supports two-way data binding where data from a model is kept in synchronization with a view template at all times.</span></span> <span data-ttu-id="189ff-161">Toute modification apportée à la vue est automatiquement répercutées dans le modèle.</span><span class="sxs-lookup"><span data-stu-id="189ff-161">Any changes to the view are automatically reflected in the model.</span></span> <span data-ttu-id="189ff-162">De même, toutes les modifications dans le modèle sont répercutées dans la vue.</span><span class="sxs-lookup"><span data-stu-id="189ff-162">Likewise, any changes in the model are reflected in the view.</span></span>

<span data-ttu-id="189ff-163">Créer un fichier HTML ou une action du contrôleur avec une vue qui l’accompagne nommée `Databinding`.</span><span class="sxs-lookup"><span data-stu-id="189ff-163">Create either an HTML file or a controller action with an accompanying view named `Databinding`.</span></span> <span data-ttu-id="189ff-164">Dans la vue, sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="189ff-164">Include the following in the view:</span></span>

[!code-html[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/Views/Home/Databinding.cshtml?highlight=8,9,10)]

<span data-ttu-id="189ff-165">Notez que vous pouvez afficher les valeurs du modèle à l’aide de la liaison de directives ou de données (`ng-bind`).</span><span class="sxs-lookup"><span data-stu-id="189ff-165">Notice that you can display model values using either directives or data binding (`ng-bind`).</span></span> <span data-ttu-id="189ff-166">La page résultante doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="189ff-166">The resulting page should look like this:</span></span>

![Liaison de données simple](angular/_static/simple-databinding.png)

### <a name="templates"></a><span data-ttu-id="189ff-168">Modèles</span><span class="sxs-lookup"><span data-stu-id="189ff-168">Templates</span></span>

<span data-ttu-id="189ff-169">[Modèles](https://docs.angularjs.org/guide/templates) dans AngularJS sont des pages HTML simples décorées avec les directives AngularJS et d’artefacts.</span><span class="sxs-lookup"><span data-stu-id="189ff-169">[Templates](https://docs.angularjs.org/guide/templates) in AngularJS are just plain HTML pages decorated with AngularJS directives and artifacts.</span></span> <span data-ttu-id="189ff-170">Un modèle dans AngularJS est une combinaison de directives, les expressions, les filtres et les contrôles qui combinent avec du code HTML pour le mode formulaire.</span><span class="sxs-lookup"><span data-stu-id="189ff-170">A template in AngularJS is a mixture of directives, expressions, filters, and controls that combine with HTML to form the view.</span></span>

<span data-ttu-id="189ff-171">Ajouter une autre vue pour illustrer les modèles et ajouter les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="189ff-171">Add another view to demonstrate templates, and add the following to it:</span></span>

[!code-html[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/Views/Home/Templates.cshtml?highlight=8,9,10)]

<span data-ttu-id="189ff-172">Le modèle a des directives AngularJS comme `ng-app`, `ng-init`, `ng-model` et la syntaxe d’expression de liaison de données pour lier le `personName` propriété.</span><span class="sxs-lookup"><span data-stu-id="189ff-172">The template has AngularJS directives like `ng-app`, `ng-init`, `ng-model` and data binding expression syntax to bind the `personName` property.</span></span> <span data-ttu-id="189ff-173">En cours d’exécution dans le navigateur, l’affichage ressemble à la capture d’écran ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="189ff-173">Running in the browser, the view looks like the screenshot below:</span></span>

![Exemple simple de modèles 1](angular/_static/simple-templates-1.png)

<span data-ttu-id="189ff-175">Si vous modifiez le nom en le tapant dans le champ d’entrée, vous verrez le texte en regard du champ d’entrée dynamiquement mise à jour, montrant une liaison de données bidirectionnelle angulaire en action.</span><span class="sxs-lookup"><span data-stu-id="189ff-175">If you change the name by typing in the input field, you will see the text next to the input field dynamically update, showing Angular two-way data binding in action.</span></span>

![Exemple simple de modèles 2](angular/_static/simple-templates-2.png)

### <a name="expressions"></a><span data-ttu-id="189ff-177">Expressions</span><span class="sxs-lookup"><span data-stu-id="189ff-177">Expressions</span></span>

<span data-ttu-id="189ff-178">[Expressions](https://docs.angularjs.org/guide/expression) dans AngularJS sont extraits de code de type JavaScript qui sont écrits à l’intérieur de la `{{ expression }}` syntaxe.</span><span class="sxs-lookup"><span data-stu-id="189ff-178">[Expressions](https://docs.angularjs.org/guide/expression) in AngularJS are JavaScript-like code snippets that are written inside the `{{ expression }}` syntax.</span></span> <span data-ttu-id="189ff-179">Les données à partir de ces expressions sont liées au format HTML de la même façon que `ng-bind` directives.</span><span class="sxs-lookup"><span data-stu-id="189ff-179">The data from these expressions is bound to HTML the same way as `ng-bind` directives.</span></span> <span data-ttu-id="189ff-180">La principale différence entre les expressions d’AngularJS et d’expressions régulières que JavaScript est que AngularJS les expressions sont évaluées par rapport à la `$scope` objet dans AngularJS.</span><span class="sxs-lookup"><span data-stu-id="189ff-180">The main difference between AngularJS expressions and regular JavaScript expressions is that AngularJS expressions are evaluated against the `$scope` object in AngularJS.</span></span>

<span data-ttu-id="189ff-181">Les expressions d’AngularJS dans l’exemple ci-dessous liaison `personName` et un code JavaScript simple calculée expression :</span><span class="sxs-lookup"><span data-stu-id="189ff-181">The AngularJS expressions in the sample below bind `personName` and a simple JavaScript calculated expression:</span></span>

[!code-html[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/Views/Home/Expressions.cshtml?highlight=8,9,10)]

<span data-ttu-id="189ff-182">L’exemple en cours d’exécution dans le navigateur affiche le `personName` données et les résultats du calcul :</span><span class="sxs-lookup"><span data-stu-id="189ff-182">The example running in the browser displays the `personName` data and the results of the calculation:</span></span>

![Expressions simples](angular/_static/simple-expressions.png)

### <a name="repeaters"></a><span data-ttu-id="189ff-184">Répéteurs</span><span class="sxs-lookup"><span data-stu-id="189ff-184">Repeaters</span></span>

<span data-ttu-id="189ff-185">Extensible de AngularJS est effectuée via une directive primitifs appelée `ng-repeat`.</span><span class="sxs-lookup"><span data-stu-id="189ff-185">Repeating in AngularJS is done via a primitive directive called `ng-repeat`.</span></span> <span data-ttu-id="189ff-186">Le `ng-repeat` directive répète un élément HTML donné dans une vue sur la longueur d’un tableau de données extensible.</span><span class="sxs-lookup"><span data-stu-id="189ff-186">The `ng-repeat` directive repeats a given HTML element in a view over the length of a repeating data array.</span></span> <span data-ttu-id="189ff-187">Répétez répéteurs dans AngularJS sur un tableau de chaînes ou objets.</span><span class="sxs-lookup"><span data-stu-id="189ff-187">Repeaters in AngularJS can repeat over an array of strings or objects.</span></span> <span data-ttu-id="189ff-188">Voici un exemple d’utilisation de répétition sur un tableau de chaînes :</span><span class="sxs-lookup"><span data-stu-id="189ff-188">Here is a sample usage of repeating over an array of strings:</span></span>

[!code-html[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/Views/Home/Repeaters.cshtml?highlight=8,10,11)]

<span data-ttu-id="189ff-189">Le [repeat (directive)](https://docs.angularjs.org/api/ng/directive/ngRepeat) génère une série d’éléments de liste dans une liste non triée, comme vous pouvez le voir dans les outils de développement indiqués dans cette capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="189ff-189">The [repeat directive](https://docs.angularjs.org/api/ng/directive/ngRepeat) outputs a series of list items in an unordered list, as you can see in the developer tools shown in this screenshot:</span></span>

![Exemple de répéteur](angular/_static/repeater.png)

<span data-ttu-id="189ff-191">Voici un exemple qui se répète sur un tableau d’objets.</span><span class="sxs-lookup"><span data-stu-id="189ff-191">Here is an example that repeats over an array of objects.</span></span> <span data-ttu-id="189ff-192">Le `ng-init` directive établit un `names` tableau, où chaque élément est un objet contenant le premier et le nom.</span><span class="sxs-lookup"><span data-stu-id="189ff-192">The `ng-init` directive establishes a `names` array, where each element is an object containing first and last names.</span></span> <span data-ttu-id="189ff-193">Le `ng-repeat` l’attribution, `name in names`, génère un élément de liste pour chaque élément du tableau.</span><span class="sxs-lookup"><span data-stu-id="189ff-193">The `ng-repeat` assignment, `name in names`, outputs a list item for every array element.</span></span>

[!code-html[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/Views/Home/Repeaters2.cshtml?highlight=8,9,10,11,13,14)]

<span data-ttu-id="189ff-194">La sortie dans ce cas est le même que dans l’exemple précédent.</span><span class="sxs-lookup"><span data-stu-id="189ff-194">The output in this case is the same as in the previous example.</span></span>

<span data-ttu-id="189ff-195">Angulaire fournit certaines directives supplémentaires qui peuvent aider à fournir un comportement en fonction de la boucle dans son exécution.</span><span class="sxs-lookup"><span data-stu-id="189ff-195">Angular provides some additional directives that can help provide behavior based on where the loop is in its execution.</span></span>

`$index`

<span data-ttu-id="189ff-196">Utilisez `$index` dans le `ng-repeat` se trouve sur la boucle pour déterminer quelle position d’index à votre boucle actuellement.</span><span class="sxs-lookup"><span data-stu-id="189ff-196">Use `$index` in the `ng-repeat` loop to determine which index position your loop currently is on.</span></span>

<span data-ttu-id="189ff-197">`$even` et `$odd`</span><span class="sxs-lookup"><span data-stu-id="189ff-197">`$even` and `$odd`</span></span>

<span data-ttu-id="189ff-198">Utilisez `$even` dans le `ng-repeat` boucle pour déterminer si l’index actuel dans la boucle est une ligne même indexée.</span><span class="sxs-lookup"><span data-stu-id="189ff-198">Use `$even` in the `ng-repeat` loop to determine whether the current index in your loop is an even indexed row.</span></span> <span data-ttu-id="189ff-199">De même, utilisez `$odd` pour déterminer si l’index actuel est une ligne indexée impaire.</span><span class="sxs-lookup"><span data-stu-id="189ff-199">Similarly, use `$odd` to determine if the current index is an odd indexed row.</span></span>

<span data-ttu-id="189ff-200">`$first` et `$last`</span><span class="sxs-lookup"><span data-stu-id="189ff-200">`$first` and `$last`</span></span>

<span data-ttu-id="189ff-201">Utilisez `$first` dans le `ng-repeat` boucle pour déterminer si l’index actuel dans la boucle est la première ligne.</span><span class="sxs-lookup"><span data-stu-id="189ff-201">Use `$first` in the `ng-repeat` loop to determine whether the current index in your loop is the first row.</span></span> <span data-ttu-id="189ff-202">De même, utilisez `$last` pour déterminer si l’index actuel est la dernière ligne.</span><span class="sxs-lookup"><span data-stu-id="189ff-202">Similarly, use `$last` to determine if the current index is the last row.</span></span>

<span data-ttu-id="189ff-203">Voici un exemple qui montre `$index`, `$even`, `$odd`, `$first`, et `$last` en action :</span><span class="sxs-lookup"><span data-stu-id="189ff-203">Below is a sample that shows `$index`, `$even`, `$odd`, `$first`, and `$last` in action:</span></span>

[!code-html[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/Views/Home/Repeaters3.cshtml?highlight=14,15,16,17,18)]

<span data-ttu-id="189ff-204">Voici le résultat obtenu :</span><span class="sxs-lookup"><span data-stu-id="189ff-204">Here is the resulting output:</span></span>

![Exemple de répéteur 2](angular/_static/repeaters2.png)

### <a name="scope"></a><span data-ttu-id="189ff-206">$scope</span><span class="sxs-lookup"><span data-stu-id="189ff-206">$scope</span></span>

<span data-ttu-id="189ff-207">`$scope`est un objet JavaScript qui agit comme un collage entre la vue (modèle) et le contrôleur (voir ci-après).</span><span class="sxs-lookup"><span data-stu-id="189ff-207">`$scope` is a JavaScript object that acts as glue between the view (template) and the controller (explained below).</span></span> <span data-ttu-id="189ff-208">Un modèle d’affichage dans AngularJS connaît uniquement les valeurs liées à la `$scope` objet dans le contrôleur.</span><span class="sxs-lookup"><span data-stu-id="189ff-208">A view template in AngularJS only knows about the values attached to the `$scope` object in the controller.</span></span>

> [!NOTE]
> <span data-ttu-id="189ff-209">Dans le monde MVVM, le `$scope` objet dans AngularJS est souvent définie comme le ViewModel.</span><span class="sxs-lookup"><span data-stu-id="189ff-209">In the MVVM world, the `$scope` object in AngularJS is often defined as the ViewModel.</span></span> <span data-ttu-id="189ff-210">L’équipe AngularJS fait référence à la `$scope` objet en tant que le modèle de données.</span><span class="sxs-lookup"><span data-stu-id="189ff-210">The AngularJS team refers to the `$scope` object as the Data-Model.</span></span> <span data-ttu-id="189ff-211">[En savoir plus sur les étendues dans AngularJS](https://docs.angularjs.org/guide/scope).</span><span class="sxs-lookup"><span data-stu-id="189ff-211">[Learn more about Scopes in AngularJS](https://docs.angularjs.org/guide/scope).</span></span>

<span data-ttu-id="189ff-212">Voici un exemple simple illustrant comment définir des propriétés sur `$scope` dans un fichier JavaScript distinct, *scope.js*:</span><span class="sxs-lookup"><span data-stu-id="189ff-212">Below is a simple example showing how to set properties on `$scope` within a separate JavaScript file, *scope.js*:</span></span>

[!code-html[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/wwwroot/app/scope.js?highlight=2,3)]

<span data-ttu-id="189ff-213">Observez le `$scope` paramètre passé au contrôleur sur la ligne 2.</span><span class="sxs-lookup"><span data-stu-id="189ff-213">Observe the `$scope` parameter passed to the controller on line 2.</span></span> <span data-ttu-id="189ff-214">Cet objet est ce que connaît la vue.</span><span class="sxs-lookup"><span data-stu-id="189ff-214">This object is what the view knows about.</span></span> <span data-ttu-id="189ff-215">Sur la ligne 3, nous définissons une propriété appelée « name » à « Mary Jane ».</span><span class="sxs-lookup"><span data-stu-id="189ff-215">On line 3, we are setting a property called "name" to "Mary Jane".</span></span>

<span data-ttu-id="189ff-216">Que se passe-t-il quand une propriété particulière n’est pas trouvée par la vue ?</span><span class="sxs-lookup"><span data-stu-id="189ff-216">What happens when a particular property is not found by the view?</span></span> <span data-ttu-id="189ff-217">La vue définie ci-dessous fait référence aux propriétés de « nom » et « age » :</span><span class="sxs-lookup"><span data-stu-id="189ff-217">The view defined below refers to "name" and "age" properties:</span></span>

[!code-html[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/Views/Home/Scope.cshtml?highlight=9,10,14)]

<span data-ttu-id="189ff-218">Notez à la ligne 9 que nous demandons angulaire pour afficher la propriété « name » à l’aide de la syntaxe d’expression.</span><span class="sxs-lookup"><span data-stu-id="189ff-218">Notice on line 9 that we are asking Angular to show the "name" property using expression syntax.</span></span> <span data-ttu-id="189ff-219">Ligne 10 alors fait référence à « age », une propriété qui n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="189ff-219">Line 10 then refers to "age", a property that does not exist.</span></span> <span data-ttu-id="189ff-220">L’exemple en cours affiche le nom de la valeur « Mary Jane » et rien d’âge.</span><span class="sxs-lookup"><span data-stu-id="189ff-220">The running example shows the name set to "Mary Jane" and nothing for age.</span></span> <span data-ttu-id="189ff-221">Propriétés manquantes sont ignorées.</span><span class="sxs-lookup"><span data-stu-id="189ff-221">Missing properties are ignored.</span></span>

![Exemple d’étendue](angular/_static/scope.png)

### <a name="modules"></a><span data-ttu-id="189ff-223">Modules</span><span class="sxs-lookup"><span data-stu-id="189ff-223">Modules</span></span>

<span data-ttu-id="189ff-224">A [module](https://docs.angularjs.org/guide/module) dans AngularJS est une collection de contrôleurs, les services, les directives, etc. Le `angular.module()` appel de fonction est utilisé pour créer, enregistrer et de récupérer les modules dans AngularJS.</span><span class="sxs-lookup"><span data-stu-id="189ff-224">A [module](https://docs.angularjs.org/guide/module) in AngularJS is a collection of controllers, services, directives, etc. The `angular.module()` function call is used to create, register, and retrieve modules in AngularJS.</span></span> <span data-ttu-id="189ff-225">Tous les modules, y compris ceux fournis par l’équipe de AngularJS et les bibliothèques de tierce partie, doivent être inscrites à l’aide de la `angular.module()` (fonction).</span><span class="sxs-lookup"><span data-stu-id="189ff-225">All modules, including those shipped by the AngularJS team and third party libraries, should be registered using the `angular.module()` function.</span></span>

<span data-ttu-id="189ff-226">Voici un extrait de code qui montre comment créer un nouveau module dans AngularJS.</span><span class="sxs-lookup"><span data-stu-id="189ff-226">Below is a snippet of code that shows how to create a new module in AngularJS.</span></span> <span data-ttu-id="189ff-227">Le premier paramètre est le nom du module.</span><span class="sxs-lookup"><span data-stu-id="189ff-227">The first parameter is the name of the module.</span></span> <span data-ttu-id="189ff-228">Le deuxième paramètre définit des dépendances sur d’autres modules.</span><span class="sxs-lookup"><span data-stu-id="189ff-228">The second parameter defines dependencies on other modules.</span></span> <span data-ttu-id="189ff-229">Plus loin dans cet article, nous montrant comment transmettre ces dépendances pour un `angular.module()` appel de méthode.</span><span class="sxs-lookup"><span data-stu-id="189ff-229">Later in this article, we will be showing how to pass these dependencies to an `angular.module()` method call.</span></span>

```javascript
var personApp = angular.module('personApp', []);
```

<span data-ttu-id="189ff-230">Utilisez la `ng-app` directive pour représenter un module AngularJS sur la page.</span><span class="sxs-lookup"><span data-stu-id="189ff-230">Use the `ng-app` directive to represent an AngularJS module on the page.</span></span> <span data-ttu-id="189ff-231">Pour utiliser un module, d’affecter le nom du module, `personApp` dans cet exemple, pour le `ng-app` directive dans notre modèle.</span><span class="sxs-lookup"><span data-stu-id="189ff-231">To use a module, assign the name of the module, `personApp` in this example, to the `ng-app` directive in our template.</span></span>

```html
<body ng-app="personApp">
```

### <a name="controllers"></a><span data-ttu-id="189ff-232">Contrôleurs</span><span class="sxs-lookup"><span data-stu-id="189ff-232">Controllers</span></span>

<span data-ttu-id="189ff-233">[Contrôleurs](https://docs.angularjs.org/guide/controller) dans AngularJS sont le premier point d’entrée pour votre code.</span><span class="sxs-lookup"><span data-stu-id="189ff-233">[Controllers](https://docs.angularjs.org/guide/controller) in AngularJS are the first point of entry for your code.</span></span> <span data-ttu-id="189ff-234">Le `<module name>.controller()` appel de fonction est utilisé pour créer et inscrire les contrôleurs dans AngularJS.</span><span class="sxs-lookup"><span data-stu-id="189ff-234">The `<module name>.controller()` function call is used to create and register controllers in AngularJS.</span></span> <span data-ttu-id="189ff-235">Le `ng-controller` directive est utilisée pour représenter un contrôleur AngularJS sur la page HTML.</span><span class="sxs-lookup"><span data-stu-id="189ff-235">The `ng-controller` directive is used to represent an AngularJS controller on the HTML page.</span></span> <span data-ttu-id="189ff-236">Le rôle du contrôleur dans angulaire consiste à définir l’état et le comportement du modèle de données (`$scope`).</span><span class="sxs-lookup"><span data-stu-id="189ff-236">The role of the controller in Angular is to set state and behavior of the data model (`$scope`).</span></span> <span data-ttu-id="189ff-237">Contrôleurs de ne doivent pas être utilisés pour manipuler le DOM directement.</span><span class="sxs-lookup"><span data-stu-id="189ff-237">Controllers should not be used to manipulate the DOM directly.</span></span>

<span data-ttu-id="189ff-238">Voici un extrait de code qui inscrit un nouveau contrôleur.</span><span class="sxs-lookup"><span data-stu-id="189ff-238">Below is a snippet of code that registers a new controller.</span></span> <span data-ttu-id="189ff-239">Le `personApp` variable dans l’extrait de code fait référence à un module angulaire, qui est défini sur la ligne 2.</span><span class="sxs-lookup"><span data-stu-id="189ff-239">The `personApp` variable in the snippet references an Angular module, which is defined on line 2.</span></span>

[!code-javascript[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/wwwroot/app/controllers.js?highlight=2,5)]

<span data-ttu-id="189ff-240">La vue à l’aide de la `ng-controller` directive attribue le nom du contrôleur :</span><span class="sxs-lookup"><span data-stu-id="189ff-240">The view using the `ng-controller` directive assigns the controller name:</span></span>

[!code-html[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/Views/Home/Controllers.cshtml?highlight=8,14)]

<span data-ttu-id="189ff-241">La page affiche « Mary » et « Jane » qui correspondent à la `firstName` et `lastName` propriétés attaché à la `$scope` objet :</span><span class="sxs-lookup"><span data-stu-id="189ff-241">The page shows "Mary" and "Jane" that correspond to the `firstName` and `lastName` properties attached to the `$scope` object:</span></span>

![Exemple de contrôleur](angular/_static/controllers.png)

### <a name="components"></a><span data-ttu-id="189ff-243">Composants</span><span class="sxs-lookup"><span data-stu-id="189ff-243">Components</span></span>

<span data-ttu-id="189ff-244">[Composants](https://docs.angularjs.org/guide/component) dans angulaire 1.5.x autoriser pour l’encapsulation et la capacité de créer des éléments HTML individuels.</span><span class="sxs-lookup"><span data-stu-id="189ff-244">[Components](https://docs.angularjs.org/guide/component) in Angular 1.5.x allow for the encapsulation and capability of creating individual HTML elements.</span></span> <span data-ttu-id="189ff-245">Vous pouvez d’obtenir la même fonctionnalité à l’aide de la méthode .directive() dans 1.4.x angulaire.</span><span class="sxs-lookup"><span data-stu-id="189ff-245">In Angular 1.4.x you could achieve the same feature using the .directive() method.</span></span>

<span data-ttu-id="189ff-246">À l’aide de la méthode .component(), développement est simplifié gagner de la fonctionnalité de la directive et le contrôleur.</span><span class="sxs-lookup"><span data-stu-id="189ff-246">By using the .component() method, development is simplified gaining the functionality of the directive and the controller.</span></span> <span data-ttu-id="189ff-247">Autres avantages ; isolement de la portée, les meilleures pratiques sont inhérentes et migration 2 angulaire devient une tâche plus facile.</span><span class="sxs-lookup"><span data-stu-id="189ff-247">Other benefits include; scope isolation, best practices are inherent, and migration to Angular 2 becomes an easier task.</span></span> <span data-ttu-id="189ff-248">Le `<module name>.component()` appel de fonction est utilisé pour créer et inscrire des composants dans AngularJS.</span><span class="sxs-lookup"><span data-stu-id="189ff-248">The `<module name>.component()` function call is used to create and register components in AngularJS.</span></span>

<span data-ttu-id="189ff-249">Voici un extrait de code qui inscrit un nouveau composant.</span><span class="sxs-lookup"><span data-stu-id="189ff-249">Below is a snippet of code that registers a new component.</span></span> <span data-ttu-id="189ff-250">Le `personApp` variable dans l’extrait de code fait référence à un module angulaire, qui est défini sur la ligne 2.</span><span class="sxs-lookup"><span data-stu-id="189ff-250">The `personApp` variable in the snippet references an Angular module, which is defined on line 2.</span></span>

[!code-javascript[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/wwwroot/app/components.js?highlight=2,5,13)]

<span data-ttu-id="189ff-251">La vue dans laquelle nous affichons l’élément HTML personnalisé.</span><span class="sxs-lookup"><span data-stu-id="189ff-251">The view where we are displaying the custom HTML element.</span></span>

[!code-html[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/Views/Home/Components.cshtml?highlight=8)]

<span data-ttu-id="189ff-252">Le modèle associé par composant :</span><span class="sxs-lookup"><span data-stu-id="189ff-252">The associated template used by component:</span></span>

[!code-html[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/wwwroot/app/partials/personcomponent.html?highlight=2,3)]

<span data-ttu-id="189ff-253">La page affiche « Aftab » et « Ansari » qui correspondent à la `firstName` et `lastName` propriétés attaché à la `vm` objet :</span><span class="sxs-lookup"><span data-stu-id="189ff-253">The page shows "Aftab" and "Ansari" that correspond to the `firstName` and `lastName` properties attached to the `vm` object:</span></span>

![Exemple de composants](angular/_static/components.png)

### <a name="services"></a><span data-ttu-id="189ff-255">Services</span><span class="sxs-lookup"><span data-stu-id="189ff-255">Services</span></span>

<span data-ttu-id="189ff-256">[Services](https://docs.angularjs.org/guide/services) dans AngularJS sont couramment utilisées pour le code partagé qui est abstrait dans un fichier qui peut être utilisé dans l’ensemble de la durée de vie d’une application angulaire.</span><span class="sxs-lookup"><span data-stu-id="189ff-256">[Services](https://docs.angularjs.org/guide/services) in AngularJS are commonly used for shared code that is abstracted away into a file which can be used throughout the lifetime of an Angular application.</span></span> <span data-ttu-id="189ff-257">Les services sont instanciés tardivement, ce qui signifie qu’il pas sera une instance d’un service, sauf si un composant dont dépend le service obtient utilisé.</span><span class="sxs-lookup"><span data-stu-id="189ff-257">Services are lazily instantiated, meaning that there will not be an instance of a service unless a component that depends on the service gets used.</span></span> <span data-ttu-id="189ff-258">Fabriques sont un exemple de service utilisé dans les applications d’AngularJS.</span><span class="sxs-lookup"><span data-stu-id="189ff-258">Factories are an example of a service used in AngularJS applications.</span></span> <span data-ttu-id="189ff-259">Fabriques sont créés à l’aide de la `myApp.factory()` , l’appel de fonction où `myApp` est le module.</span><span class="sxs-lookup"><span data-stu-id="189ff-259">Factories are created using the `myApp.factory()` function call, where `myApp` is the module.</span></span>

<span data-ttu-id="189ff-260">Voici un exemple qui montre comment utiliser des fabriques dans AngularJS :</span><span class="sxs-lookup"><span data-stu-id="189ff-260">Below is an example that shows how to use factories in AngularJS:</span></span>

[!code-javascript[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/wwwroot/app/simpleFactory.js?highlight=1)]

<span data-ttu-id="189ff-261">Pour appeler cette fabrique à partir du contrôleur, passez `personFactory` en tant que paramètre à la `controller` (fonction) :</span><span class="sxs-lookup"><span data-stu-id="189ff-261">To call this factory from the controller, pass `personFactory` as a parameter to the `controller` function:</span></span>

```javascript
personApp.controller('personController', function($scope,personFactory) {
  $scope.name = personFactory.getName();
});
```

### <a name="using-services-to-talk-to-a-rest-endpoint"></a><span data-ttu-id="189ff-262">À l’aide des services pour communiquer avec un point de terminaison REST</span><span class="sxs-lookup"><span data-stu-id="189ff-262">Using services to talk to a REST endpoint</span></span>

<span data-ttu-id="189ff-263">Ci-dessous est un exemple de bout en bout à l’aide de services dans AngularJS pour interagir avec un point de terminaison de l’API Web ASP.NET principale.</span><span class="sxs-lookup"><span data-stu-id="189ff-263">Below is an end-to-end example using services in AngularJS to interact with an ASP.NET Core Web API endpoint.</span></span> <span data-ttu-id="189ff-264">L’exemple obtienne les données de l’API Web et affiche les données dans un modèle d’affichage.</span><span class="sxs-lookup"><span data-stu-id="189ff-264">The example gets data from the Web API and displays the data in a view template.</span></span> <span data-ttu-id="189ff-265">Nous allons commencer par la vue :</span><span class="sxs-lookup"><span data-stu-id="189ff-265">Let's start with the view first:</span></span>

[!code-html[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/Views/People/Index.cshtml?highlight=5,8,10,17,18,19)]

<span data-ttu-id="189ff-266">Dans cette vue, nous avons un module angulaire appelé `PersonsApp` et un contrôleur appelé `personController`.</span><span class="sxs-lookup"><span data-stu-id="189ff-266">In this view, we have an Angular module called `PersonsApp` and a controller called `personController`.</span></span> <span data-ttu-id="189ff-267">Nous utilisons `ng-repeat` d’itérer sur la liste des personnes.</span><span class="sxs-lookup"><span data-stu-id="189ff-267">We are using `ng-repeat` to iterate over the list of persons.</span></span> <span data-ttu-id="189ff-268">Nous référençons trois fichiers JavaScript personnalisés sur les lignes 17-19.</span><span class="sxs-lookup"><span data-stu-id="189ff-268">We are referencing three custom JavaScript files on lines 17-19.</span></span>

<span data-ttu-id="189ff-269">Le *personApp.js* fichier est utilisé pour inscrire le `PersonsApp` module ; et la syntaxe est semblable aux exemples précédents.</span><span class="sxs-lookup"><span data-stu-id="189ff-269">The *personApp.js* file is used to register the `PersonsApp` module; and, the syntax is similar to previous examples.</span></span> <span data-ttu-id="189ff-270">Nous utilisons le `angular.module` fonction permettant de créer une nouvelle instance du module qui nous travaillerons avec.</span><span class="sxs-lookup"><span data-stu-id="189ff-270">We are using the `angular.module` function to create a new instance of the module that we will be working with.</span></span>

[!code-javascript[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/wwwroot/app/personApp.js?highlight=3)]

<span data-ttu-id="189ff-271">Examinons un *personFactory.js*, ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="189ff-271">Let's take a look at *personFactory.js*, below.</span></span> <span data-ttu-id="189ff-272">Nous appelons du module `factory` méthode pour créer une fabrique.</span><span class="sxs-lookup"><span data-stu-id="189ff-272">We are calling the module’s `factory` method to create a factory.</span></span> <span data-ttu-id="189ff-273">La ligne 12 montre l’angulaire intégré `$http` la récupération des informations sur les personnes à partir d’un service web de service.</span><span class="sxs-lookup"><span data-stu-id="189ff-273">Line 12 shows the built-in Angular `$http` service retrieving people information from a web service.</span></span>

[!code-javascript[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/wwwroot/app/personFactory.js?highlight=6,7,12)]

<span data-ttu-id="189ff-274">Dans *personController.js*, nous appelons du module `controller` pour créer le contrôleur.</span><span class="sxs-lookup"><span data-stu-id="189ff-274">In *personController.js*, we are calling the module’s `controller` method to create the controller.</span></span> <span data-ttu-id="189ff-275">Le `$scope` l’objet `people` les données retournées à partir de la personFactory (ligne 13) est assignée à la propriété.</span><span class="sxs-lookup"><span data-stu-id="189ff-275">The `$scope` object's `people` property is assigned the data returned from the personFactory (line 13).</span></span>

[!code-javascript[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/wwwroot/app/personController.js?highlight=6,7,13)]

<span data-ttu-id="189ff-276">Jetons un œil rapide à l’API Web et le modèle derrière lui.</span><span class="sxs-lookup"><span data-stu-id="189ff-276">Let's take a quick look at the Web API and the model behind it.</span></span> <span data-ttu-id="189ff-277">Le `Person` modèle est un POCO (objet CLR simple) avec `Id`, `FirstName`, et `LastName` propriétés :</span><span class="sxs-lookup"><span data-stu-id="189ff-277">The `Person` model is a POCO (Plain Old CLR Object) with `Id`, `FirstName`, and `LastName` properties:</span></span>

[!code-csharp[Main](angular/sample/AngularJSSample/src/AngularJSSample/Models/Person.cs)]

<span data-ttu-id="189ff-278">Le `Person` contrôleur retourne une liste au format JSON de `Person` objets :</span><span class="sxs-lookup"><span data-stu-id="189ff-278">The `Person` controller returns a JSON-formatted list of `Person` objects:</span></span>

[!code-csharp[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/Controllers/Api/PersonController.cs?highlight=9,10,19)]

<span data-ttu-id="189ff-279">Nous allons voir l’application en action :</span><span class="sxs-lookup"><span data-stu-id="189ff-279">Let's see the application in action:</span></span>

![Contrôleur affichant autres résultats](angular/_static/rest-bound.png)

<span data-ttu-id="189ff-281">Vous pouvez [permet d’afficher la structure de l’application sur GitHub](https://github.com/aspnet/Docs/tree/master/aspnetcore/client-side/angular/sample).</span><span class="sxs-lookup"><span data-stu-id="189ff-281">You can [view the application's structure on GitHub](https://github.com/aspnet/Docs/tree/master/aspnetcore/client-side/angular/sample).</span></span>

> [!NOTE]
> <span data-ttu-id="189ff-282">Pour plus d’informations sur l’organisation des applications d’AngularJS, consultez [Guide de Style de John Papa angulaire](https://github.com/johnpapa/angular-styleguide)</span><span class="sxs-lookup"><span data-stu-id="189ff-282">For more on structuring AngularJS applications, see [John Papa's Angular Style Guide](https://github.com/johnpapa/angular-styleguide)</span></span>

&nbsp;

> [!NOTE]
> <span data-ttu-id="189ff-283">Pour créer le module AngularJS, contrôleur, la fabrique, directive et afficher les fichiers facilement, veillez à consulter du Sayed Hashimi [pack de modèle SideWaffle pour Visual Studio](http://sidewaffle.com/).</span><span class="sxs-lookup"><span data-stu-id="189ff-283">To create AngularJS module, controller, factory, directive and view files easily, be sure to check out Sayed Hashimi's [SideWaffle template pack for Visual Studio](http://sidewaffle.com/).</span></span> <span data-ttu-id="189ff-284">Sayed Hashimi est un type de programme senior de l’équipe Visual Studio Web Microsoft et SideWaffle modèles sont considérées comme la norme or.</span><span class="sxs-lookup"><span data-stu-id="189ff-284">Sayed Hashimi is a Senior Program Manager on the Visual Studio Web Team at Microsoft and SideWaffle templates are considered the gold standard.</span></span> <span data-ttu-id="189ff-285">Au moment de la rédaction, SideWaffle est disponible pour Visual Studio 2012, 2013 et 2015.</span><span class="sxs-lookup"><span data-stu-id="189ff-285">At the time of this writing, SideWaffle is available for Visual Studio 2012, 2013, and 2015.</span></span>

### <a name="routing-and-multiple-views"></a><span data-ttu-id="189ff-286">Routage et vues multiples</span><span class="sxs-lookup"><span data-stu-id="189ff-286">Routing and multiple views</span></span>

<span data-ttu-id="189ff-287">AngularJS dispose d’un fournisseur de routage intégrée pour gérer la navigation de SPA (Application à Page unique) en fonction.</span><span class="sxs-lookup"><span data-stu-id="189ff-287">AngularJS has a built-in route provider to handle SPA (Single Page Application) based navigation.</span></span> <span data-ttu-id="189ff-288">Pour utiliser le routage AngularJS, vous devez ajouter le `angular-route` bibliothèque à l’aide de Bower.</span><span class="sxs-lookup"><span data-stu-id="189ff-288">To work with routing in AngularJS, you must add the `angular-route` library using Bower.</span></span> <span data-ttu-id="189ff-289">Vous pouvez voir dans le [bower.json](#angular-bower-json) fichier référencé au début de cet article que nous sommes déjà y faire référence dans notre projet.</span><span class="sxs-lookup"><span data-stu-id="189ff-289">You can see in the [bower.json](#angular-bower-json) file referenced at the start of this article that we are already referencing it in our project.</span></span>

<span data-ttu-id="189ff-290">Après avoir installé le package, ajoutez la référence de script (*angular-route.js*) à votre affichage.</span><span class="sxs-lookup"><span data-stu-id="189ff-290">After you install the package, add the script reference (*angular-route.js*) to your view.</span></span>

<span data-ttu-id="189ff-291">Maintenant examinons l’application de la personne nous ont été génération et ajouter la navigation à celui-ci.</span><span class="sxs-lookup"><span data-stu-id="189ff-291">Now let's take the Person App we have been building and add navigation to it.</span></span> <span data-ttu-id="189ff-292">Tout d’abord, nous effectuer une copie de l’application en créant un `PeopleController` action appelée `Spa` et `Spa.cshtml` vue en copiant la vue Index.cshtml dans le `People` dossier.</span><span class="sxs-lookup"><span data-stu-id="189ff-292">First, we will make a copy of the app by creating a new `PeopleController` action called `Spa` and a corresponding `Spa.cshtml` view by copying the Index.cshtml view in the `People` folder.</span></span> <span data-ttu-id="189ff-293">Ajouter une référence de script à `angular-route` (voir la ligne 11).</span><span class="sxs-lookup"><span data-stu-id="189ff-293">Add a script reference to `angular-route` (see line 11).</span></span> <span data-ttu-id="189ff-294">Également ajouter un `div` marquée avec la `ng-view` directive (voir la ligne 6) comme espace réservé de placer des vues dans.</span><span class="sxs-lookup"><span data-stu-id="189ff-294">Also add a `div` marked with the `ng-view` directive (see line 6) as a placeholder to place views in.</span></span> <span data-ttu-id="189ff-295">Nous allons utiliser plusieurs supplémentaires *.js* les fichiers qui sont référencés dans les lignes 13 à 16.</span><span class="sxs-lookup"><span data-stu-id="189ff-295">We are going to be using several additional *.js* files which are referenced on lines 13-16.</span></span>

[!code-html[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/Views/People/Spa.cshtml?highlight=6,11,12,13,14,15,16)]

<span data-ttu-id="189ff-296">Examinons un *personModule.js* fichier pour voir comment nous examinons l’instanciation du module avec le routage.</span><span class="sxs-lookup"><span data-stu-id="189ff-296">Let's take a look at *personModule.js* file to see how we are instantiating the module with routing.</span></span> <span data-ttu-id="189ff-297">Nous passons `ngRoute` en tant que bibliothèque dans le module.</span><span class="sxs-lookup"><span data-stu-id="189ff-297">We are passing `ngRoute` as a library into the module.</span></span> <span data-ttu-id="189ff-298">Ce module gère le routage dans notre application.</span><span class="sxs-lookup"><span data-stu-id="189ff-298">This module handles routing in our application.</span></span>

[!code-javascript[Main](angular/sample/AngularJSSample/src/AngularJSSample/wwwroot/app/personModule.js)]

<span data-ttu-id="189ff-299">Le *personRoutes.js* fichier ci-dessous, définit les itinéraires basés sur le fournisseur de l’itinéraire.</span><span class="sxs-lookup"><span data-stu-id="189ff-299">The *personRoutes.js* file, below, defines routes based on the route provider.</span></span> <span data-ttu-id="189ff-300">Définissent la navigation en disant efficacement lorsqu’une URL avec lignes 4-7 `/persons` est demandé, utilisez un modèle appelé `partials/personlist` en passant par `personListController`.</span><span class="sxs-lookup"><span data-stu-id="189ff-300">Lines 4-7 define navigation by effectively saying, when a URL with `/persons` is requested, use a template called `partials/personlist` by working through `personListController`.</span></span> <span data-ttu-id="189ff-301">Les lignes 8 à 11 indiquent une page de détails avec un paramètre d’itinéraire de `personId`.</span><span class="sxs-lookup"><span data-stu-id="189ff-301">Lines 8-11 indicate a detail page with a route parameter of `personId`.</span></span> <span data-ttu-id="189ff-302">Si l’URL ne correspond pas à un des modèles, angulaire par défaut est le `/persons` vue.</span><span class="sxs-lookup"><span data-stu-id="189ff-302">If the URL doesn't match one of the patterns, Angular defaults to the `/persons` view.</span></span>

[!code-javascript[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/wwwroot/app/personRoutes.js?highlight=4,5,6,7,8,9,10,11,13)]

<span data-ttu-id="189ff-303">Le `personlist.html` fichier est une vue partielle contenant uniquement le code HTML que nécessaire pour afficher la liste de personnes.</span><span class="sxs-lookup"><span data-stu-id="189ff-303">The `personlist.html` file is a partial view containing only the HTML needed to display person list.</span></span>

[!code-html[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/wwwroot/app/partials/personlist.html?highlight=3)]

<span data-ttu-id="189ff-304">Le contrôleur est défini à l’aide du module `controller` fonctionner dans *personListController.js*.</span><span class="sxs-lookup"><span data-stu-id="189ff-304">The controller is defined by using the module's `controller` function in *personListController.js*.</span></span>

[!code-javascript[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/wwwroot/app/personListController.js?highlight=1)]

<span data-ttu-id="189ff-305">Si nous exécuter cette application et accédez à la `people/spa#/persons` URL, nous allons voir :</span><span class="sxs-lookup"><span data-stu-id="189ff-305">If we run this application and navigate to the `people/spa#/persons` URL, we will see:</span></span>

![Mode liste de personnes](angular/_static/spa-persons.png)

<span data-ttu-id="189ff-307">Si nous, accédez à une page de détails, par exemple `people/spa#/persons/2`, nous allons voir la vue partielle en détail :</span><span class="sxs-lookup"><span data-stu-id="189ff-307">If we navigate to a detail page, for example `people/spa#/persons/2`, we will see the detail partial view:</span></span>

![Vue Détails](angular/_static/spa-persons-2.png)

<span data-ttu-id="189ff-309">Vous pouvez afficher la source complète et ne pas illustrés dans cet article sur tous les fichiers [GitHub](https://github.com/aspnet/Docs/tree/master/aspnetcore/client-side/angular/sample).</span><span class="sxs-lookup"><span data-stu-id="189ff-309">You can view the full source and any files not shown in this article on [GitHub](https://github.com/aspnet/Docs/tree/master/aspnetcore/client-side/angular/sample).</span></span>

### <a name="event-handlers"></a><span data-ttu-id="189ff-310">Gestionnaires d'événements</span><span class="sxs-lookup"><span data-stu-id="189ff-310">Event Handlers</span></span>

<span data-ttu-id="189ff-311">Il existe un certain nombre de directives dans AngularJS qui ajoutent des fonctionnalités de gestion des événements pour les éléments d’entrée dans votre DOM. HTML</span><span class="sxs-lookup"><span data-stu-id="189ff-311">There are a number of directives in AngularJS that add event-handling capabilities to the input elements in your HTML DOM.</span></span> <span data-ttu-id="189ff-312">Vous trouverez ci-dessous la liste des événements qui sont intégrées à AngularJS.</span><span class="sxs-lookup"><span data-stu-id="189ff-312">Below is a list of the events that are built into AngularJS.</span></span>

   * `ng-click`

   * `ng-dbl-click`

   * `ng-mousedown`

   * `ng-mouseup`

   * `ng-mouseenter`

   * `ng-mouseleave`

   * `ng-mousemove`

   * `ng-keydown`

   * `ng-keyup`

   * `ng-keypress`

   * `ng-change`

> [!NOTE]
> <span data-ttu-id="189ff-313">Vous pouvez ajouter vos propres gestionnaires d’événements à l’aide de la [directives personnalisées de fonctionnalité dans AngularJS](https://docs.angularjs.org/guide/directive).</span><span class="sxs-lookup"><span data-stu-id="189ff-313">You can add your own event handlers using the [custom directives feature in AngularJS](https://docs.angularjs.org/guide/directive).</span></span>

<span data-ttu-id="189ff-314">Voyons comment la `ng-click` événements sont associés.</span><span class="sxs-lookup"><span data-stu-id="189ff-314">Let's look at how the `ng-click` event is wired up.</span></span> <span data-ttu-id="189ff-315">Créer un fichier JavaScript nommé *eventHandlerController.js*et lui ajouter les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="189ff-315">Create a new JavaScript file named *eventHandlerController.js*, and add the following to it:</span></span>

[!code-javascript[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/wwwroot/app/eventHandlerController.js?highlight=5,6,7)]

<span data-ttu-id="189ff-316">Remarquez le nouveau `sayName` fonctionner dans `eventHandlerController` à la ligne 5 ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="189ff-316">Notice the new `sayName` function in `eventHandlerController` on line 5 above.</span></span> <span data-ttu-id="189ff-317">Effectue un ensemble de la méthode pour maintenant affiche une alerte de JavaScript à l’utilisateur avec un message d’accueil.</span><span class="sxs-lookup"><span data-stu-id="189ff-317">All the method is doing for now is showing a JavaScript alert to the user with a welcome message.</span></span>

<span data-ttu-id="189ff-318">La vue ci-dessous lie une fonction de contrôleur à un événement AngularJS.</span><span class="sxs-lookup"><span data-stu-id="189ff-318">The view below binds a controller function to an AngularJS event.</span></span> <span data-ttu-id="189ff-319">La ligne 9 comporte un bouton sur lequel le `ng-click` directive angulaire a été appliquée.</span><span class="sxs-lookup"><span data-stu-id="189ff-319">Line 9 has a button on which the `ng-click` Angular directive has been applied.</span></span> <span data-ttu-id="189ff-320">Il appelle notre `sayName` fonction, qui est attachée à la `$scope` objet passé à cette vue.</span><span class="sxs-lookup"><span data-stu-id="189ff-320">It calls our `sayName` function, which is attached to the `$scope` object passed to this view.</span></span>

[!code-html[Main](../client-side/angular/sample/AngularJSSample/src/AngularJSSample/Views/People/Events.cshtml?highlight=9)]

<span data-ttu-id="189ff-321">L’exemple en cours d’exécution montre que le contrôleur de `sayName` fonction est appelée automatiquement lorsque le bouton est activé.</span><span class="sxs-lookup"><span data-stu-id="189ff-321">The running example demonstrates that the controller's `sayName` function is called automatically when the button is clicked.</span></span>

![Événements Click](angular/_static/events.png)

<span data-ttu-id="189ff-323">Pour plus d’informations sur les directives de gestionnaire d’événements AngularJS, veillez à tête pour la [site Web de documentation](https://docs.angularjs.org/api/ng/directive/ngClick) d’AngularJS.</span><span class="sxs-lookup"><span data-stu-id="189ff-323">For more detail on AngularJS built-in event handler directives, be sure to head to the [documentation website](https://docs.angularjs.org/api/ng/directive/ngClick) of AngularJS.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="189ff-324">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="189ff-324">Additional resources</span></span>

* [<span data-ttu-id="189ff-325">Docs angulaires</span><span class="sxs-lookup"><span data-stu-id="189ff-325">Angular Docs</span></span>](https://docs.angularjs.org)

* [<span data-ttu-id="189ff-326">Info 2 angulaire</span><span class="sxs-lookup"><span data-stu-id="189ff-326">Angular 2 Info</span></span>](https://angular.io/)
