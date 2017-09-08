# <a name="aspnet-core-response-caching-sample-aspnet-core-1x"></a><span data-ttu-id="eaaeb-101">Réponse ASP.NET Core exemple de mise en cache (ASP.NET Core 1.x)</span><span class="sxs-lookup"><span data-stu-id="eaaeb-101">ASP.NET Core Response Caching Sample (ASP.NET Core 1.x)</span></span>

<span data-ttu-id="eaaeb-102">Cet exemple illustre l’utilisation de ASP.NET Core [intergiciel (middleware) de réponse mise en cache](xref:performance/caching/middleware) avec ASP.NET Core 1.x.</span><span class="sxs-lookup"><span data-stu-id="eaaeb-102">This sample illustrates the usage of ASP.NET Core [Response Caching Middleware](xref:performance/caching/middleware) with ASP.NET Core 1.x.</span></span> <span data-ttu-id="eaaeb-103">Pour l’exemple 2.x ASP.NET Core, consultez [exemple de mise en cache de réponse ASP.NET Core (ASP.NET Core 2.x)](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/middleware/samples/2.x).</span><span class="sxs-lookup"><span data-stu-id="eaaeb-103">For the ASP.NET Core 2.x sample, see [ASP.NET Core Response Caching Sample (ASP.NET Core 2.x)](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/middleware/samples/2.x).</span></span>

<span data-ttu-id="eaaeb-104">L’application envoie un `Hello World!` message et l’heure actuelle avec un `Cache-Control` en-tête pour configurer le comportement de mise en cache.</span><span class="sxs-lookup"><span data-stu-id="eaaeb-104">The application sends a `Hello World!` message and the current time along with a `Cache-Control` header to configure caching behavior.</span></span> <span data-ttu-id="eaaeb-105">L’application envoie également un `Vary` en-tête pour configurer le cache pour prendre en charge la réponse uniquement si le `Accept-Encoding` en-tête des demandes ultérieures correspond à celle de la demande d’origine.</span><span class="sxs-lookup"><span data-stu-id="eaaeb-105">The application also sends a `Vary` header to configure the cache to serve the response only if the `Accept-Encoding` header of subsequent requests matches that from the original request.</span></span>

<span data-ttu-id="eaaeb-106">Lorsque vous exécutez l’exemple, une réponse est pris en charge à partir du cache si possible, stockées pendant 10 secondes.</span><span class="sxs-lookup"><span data-stu-id="eaaeb-106">When running the sample, a response is served from cache when possible and stored for up to 10 seconds.</span></span>