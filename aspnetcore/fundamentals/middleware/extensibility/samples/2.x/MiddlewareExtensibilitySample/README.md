---
ms.openlocfilehash: 41021e30ae85dd0ae42cbe6f1606727e21bd7707
ms.sourcegitcommit: 78339e9891c8676db01a6e81e9cb0cdaa280162f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59705522"
---
# <a name="aspnet-core-middleware-extensibility-sample"></a><span data-ttu-id="90a02-101">Beispiel: ASP.NET Core-Middleware-Erweiterbarkeit</span><span class="sxs-lookup"><span data-stu-id="90a02-101">ASP.NET Core Middleware Extensibility Sample</span></span>

<span data-ttu-id="90a02-102">Dieses Beispiel veranschaulicht die unter [Factorybezogene Middlewareaktivierung in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/middleware/middleware-extensibility) beschriebenen Szenarios.</span><span class="sxs-lookup"><span data-stu-id="90a02-102">This sample demonstrates the scenarios described in [Factory-based middleware activation in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/middleware/middleware-extensibility).</span></span>

<span data-ttu-id="90a02-103">Die Beispiel-App stellt Middleware dar, die wie folgt aktiviert wurde:</span><span class="sxs-lookup"><span data-stu-id="90a02-103">The sample app demonstrates middleware activated by:</span></span>

* <span data-ttu-id="90a02-104">Per Konvention</span><span class="sxs-lookup"><span data-stu-id="90a02-104">Convention.</span></span> <span data-ttu-id="90a02-105">Weitere Informationen zur konventionellen Middlewareaktivierung finden Sie im Artikel [Middleware](https://docs.microsoft.com/aspnet/core/fundamentals/middleware/).</span><span class="sxs-lookup"><span data-stu-id="90a02-105">For more information on conventional middleware activation, see the [Middleware](https://docs.microsoft.com/aspnet/core/fundamentals/middleware/) topic.</span></span>
* <span data-ttu-id="90a02-106">Durch die Implementierung von [IMiddleware](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.http.imiddleware)</span><span class="sxs-lookup"><span data-stu-id="90a02-106">An [IMiddleware](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.http.imiddleware) implementation.</span></span> <span data-ttu-id="90a02-107">Die Standard-[IMiddlewareFactory-Klasse](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.http.imiddlewarefactory) aktiviert die Middleware.</span><span class="sxs-lookup"><span data-stu-id="90a02-107">The default [IMiddlewareFactory](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.http.imiddlewarefactory) class activates the middleware.</span></span>

<span data-ttu-id="90a02-108">Die Middlewareimplementierungen funktionieren auf identische Weise und erfassen den Wert, der von einem Abfragezeichenfolgenparameter (`key`) bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="90a02-108">The middleware implementations function identically and record the value provided by a query string parameter (`key`).</span></span> <span data-ttu-id="90a02-109">Die Middlewares verwenden einen eingefügten Datenbankkontext (einen bereichsbezogenen Dienst), um den Abfragezeichenwert in einer In-Memory Database zu erfassen.</span><span class="sxs-lookup"><span data-stu-id="90a02-109">The middlewares use an injected database context (a scoped service) to record the query string value in an in-memory database.</span></span>