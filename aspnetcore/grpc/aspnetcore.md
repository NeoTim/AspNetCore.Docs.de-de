---
title: gRPC-Dienste mit ASP.NET Core
author: juntaoluo
description: Erfahren Sie, die grundlegenden Konzepten gRPC-Dienste mit ASP.NET Core zu schreiben.
monikerRange: '>= aspnetcore-3.0'
ms.author: johluo
ms.date: 03/08/2019
uid: grpc/aspnetcore
ms.openlocfilehash: c99a499fad824c3ac026f6f390c826c0418fc069
ms.sourcegitcommit: 57a974556acd09363a58f38c26f74dc21e0d4339
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59515474"
---
# <a name="grpc-services-with-aspnet-core"></a><span data-ttu-id="24f2c-103">gRPC-Dienste mit ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="24f2c-103">gRPC services with ASP.NET Core</span></span>

<span data-ttu-id="24f2c-104">Diesem Dokument wird erläutert, wie Sie die ersten Schritte mit gRPC-Services mithilfe von ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="24f2c-104">This document shows how to get started with gRPC services using ASP.NET Core.</span></span>

[!INCLUDE[](~/includes/net-core-prereqs-all-3.0.md)]

## <a name="get-started-with-grpc-service-in-aspnet-core"></a><span data-ttu-id="24f2c-105">Erste Schritte mit dem gRPC-Dienst in ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="24f2c-105">Get started with gRPC service in ASP.NET Core</span></span>

[!INCLUDE[View or download sample code](~/includes/grpc/download.md)]

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="24f2c-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="24f2c-106">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="24f2c-107">Finden Sie unter [erste Schritte mit gRPC Services](xref:tutorials/grpc/grpc-start) ausführliche Anleitungen zum Erstellen eines Projekts gRPC.</span><span class="sxs-lookup"><span data-stu-id="24f2c-107">See [Get started with gRPC services](xref:tutorials/grpc/grpc-start) for detailed instructions on how to create a gRPC project.</span></span>

# <a name="visual-studio-code--visual-studio-for-mactabvisual-studio-codevisual-studio-mac"></a>[<span data-ttu-id="24f2c-108">Visual Studio Code / Visual Studio für Mac</span><span class="sxs-lookup"><span data-stu-id="24f2c-108">Visual Studio Code / Visual Studio for Mac</span></span>](#tab/visual-studio-code+visual-studio-mac)

<span data-ttu-id="24f2c-109">Führen Sie `dotnet new grpc -o GrpcGreeter` über die Befehlszeile aus.</span><span class="sxs-lookup"><span data-stu-id="24f2c-109">Run `dotnet new grpc -o GrpcGreeter` from the command line.</span></span>

---

## <a name="add-grpc-services-to-an-aspnet-core-app"></a><span data-ttu-id="24f2c-110">Hinzufügen von gRPC-Services zu einer ASP.NET Core-app</span><span class="sxs-lookup"><span data-stu-id="24f2c-110">Add gRPC services to an ASP.NET Core app</span></span>

<span data-ttu-id="24f2c-111">gRPC erfordert die folgenden Pakete:</span><span class="sxs-lookup"><span data-stu-id="24f2c-111">gRPC requires the following packages:</span></span>

* [<span data-ttu-id="24f2c-112">Grpc.AspNetCore.Server</span><span class="sxs-lookup"><span data-stu-id="24f2c-112">Grpc.AspNetCore.Server</span></span>](https://www.nuget.org/packages/Grpc.AspNetCore.Server)
* <span data-ttu-id="24f2c-113">[Google.Protobuf](https://www.nuget.org/packages/Google.Protobuf/) Protobuf-Nachricht APIs.</span><span class="sxs-lookup"><span data-stu-id="24f2c-113">[Google.Protobuf](https://www.nuget.org/packages/Google.Protobuf/) for protobuf message APIs.</span></span>
* [<span data-ttu-id="24f2c-114">Grpc.Tools</span><span class="sxs-lookup"><span data-stu-id="24f2c-114">Grpc.Tools</span></span>](https://www.nuget.org/packages/Grpc.Tools/)

### <a name="configure-grpc"></a><span data-ttu-id="24f2c-115">GRPC konfigurieren</span><span class="sxs-lookup"><span data-stu-id="24f2c-115">Configure gRPC</span></span>

<span data-ttu-id="24f2c-116">gRPC aktiviert ist, mit der `AddGrpc` Methode:</span><span class="sxs-lookup"><span data-stu-id="24f2c-116">gRPC is enabled with the `AddGrpc` method:</span></span>

[!code-cs[](~/tutorials/grpc/grpc-start/samples/GrpcGreeter/Startup.cs?name=snippet&highlight=5)]

<span data-ttu-id="24f2c-117">Jeder gRPC-Dienst wird hinzugefügt, die routing-Pipeline über die `MapGrpcService` Methode:</span><span class="sxs-lookup"><span data-stu-id="24f2c-117">Each gRPC service is added to the routing pipeline through the `MapGrpcService` method:</span></span>

[!code-cs[](~/tutorials/grpc/grpc-start/samples/GrpcGreeter/Startup.cs?name=snippet&highlight=21)]

<span data-ttu-id="24f2c-118">Freigeben von ASP.NET Core-Middleware und Funktionen der routing-Pipeline, die aus diesem Grund kann eine app konfiguriert werden, um zusätzliche Anforderungshandler zu verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="24f2c-118">ASP.NET Core middlewares and features share the routing pipeline, therefore an app can be configured to serve additional request handlers.</span></span> <span data-ttu-id="24f2c-119">Die zusätzliche Anforderung-Handler, z. B. MVC-Controller, arbeiten parallel mit den konfigurierten gRPC-Diensten.</span><span class="sxs-lookup"><span data-stu-id="24f2c-119">The additional request handlers, such as MVC controllers, work in parallel with the configured gRPC services.</span></span>

## <a name="integration-with-aspnet-core-apis"></a><span data-ttu-id="24f2c-120">Integration in ASP.NET Core-APIs</span><span class="sxs-lookup"><span data-stu-id="24f2c-120">Integration with ASP.NET Core APIs</span></span>

<span data-ttu-id="24f2c-121">gRPC-Dienste verfügen über Vollzugriff auf die ASP.NET Core-Features wie z. B. [Dependency Injection](xref:fundamentals/dependency-injection) (DI) und [Protokollierung](xref:fundamentals/logging/index).</span><span class="sxs-lookup"><span data-stu-id="24f2c-121">gRPC services have full access to the ASP.NET Core features such as [Dependency Injection](xref:fundamentals/dependency-injection) (DI) and [Logging](xref:fundamentals/logging/index).</span></span> <span data-ttu-id="24f2c-122">Die Implementierung des Diensts kann beispielsweise einen Dienst Protokollierung von DI-Container über den Konstruktor beheben:</span><span class="sxs-lookup"><span data-stu-id="24f2c-122">For example, the service implementation can resolve a logger service from the DI container via the constructor:</span></span>

```csharp
public class GreeterService : Greeter.GreeterBase
{
    public GreeterService(ILogger<GreeterService> logger)
    {
    }
}
```

<span data-ttu-id="24f2c-123">Standardmäßig kann die dienstimplementierung gRPC andere DI-Dienste mit jedem Lebensdauer (Singleton, Scoped oder vorübergehend) beheben.</span><span class="sxs-lookup"><span data-stu-id="24f2c-123">By default, the gRPC service implementation can resolve other DI services with any lifetime (Singleton, Scoped, or Transient).</span></span>

### <a name="resolve-httpcontext-in-grpc-methods"></a><span data-ttu-id="24f2c-124">Beheben von "HttpContext" gRPC-Methoden</span><span class="sxs-lookup"><span data-stu-id="24f2c-124">Resolve HttpContext in gRPC methods</span></span>

<span data-ttu-id="24f2c-125">Die gRPC-API ermöglicht den Zugriff auf einige Daten für das HTTP/2-Nachricht, z. B. die Methode, Host, Header und Nachspänne.</span><span class="sxs-lookup"><span data-stu-id="24f2c-125">The gRPC API provides access to some HTTP/2 message data, such as the method, host, header, and trailers.</span></span> <span data-ttu-id="24f2c-126">Der Zugriff erfolgt über die `ServerCallContext` Argument an jede gRPC-Methode übergeben:</span><span class="sxs-lookup"><span data-stu-id="24f2c-126">Access is through the `ServerCallContext` argument passed to each gRPC method:</span></span>

[!code-cs[](~/tutorials/grpc/grpc-start/samples/GrpcGreeter/Services/GreeterService.cs?highlight=3-4&name=snippet)]

<span data-ttu-id="24f2c-127">`ServerCallContext` bietet keine vollen Zugriff auf `HttpContext` in allen ASP.NET-APIs.</span><span class="sxs-lookup"><span data-stu-id="24f2c-127">`ServerCallContext` does not provide full access to `HttpContext` in all ASP.NET APIs.</span></span> <span data-ttu-id="24f2c-128">Die `GetHttpContext` Erweiterungsmethode bietet umfassenden Zugriff auf die `HttpContext` , die die zugrunde liegende HTTP/2-Nachricht in ASP.NET-APIs darstellt:</span><span class="sxs-lookup"><span data-stu-id="24f2c-128">The `GetHttpContext` extension method provides full access to the `HttpContext` representing the underlying HTTP/2 message in ASP.NET APIs:</span></span>

[!code-cs[](~/tutorials/grpc/grpc-start/samples/GrpcGreeter/Services/GreeterService.cs?name=snippet1)]

### <a name="request-body-data-rate-limit"></a><span data-ttu-id="24f2c-129">Für die Anforderung Text Datenrate</span><span class="sxs-lookup"><span data-stu-id="24f2c-129">Request body data rate limit</span></span>

<span data-ttu-id="24f2c-130">Standardmäßig legt der Kestrel-Server eine [minimale Datenrate des Anforderungstexts](
<xref:Microsoft.AspNetCore.Server.Kestrel.Core.KestrelServerLimits.MinRequestBodyDataRate>).</span><span class="sxs-lookup"><span data-stu-id="24f2c-130">By default, the Kestrel server imposes a [minimum request body data rate](
<xref:Microsoft.AspNetCore.Server.Kestrel.Core.KestrelServerLimits.MinRequestBodyDataRate>).</span></span> <span data-ttu-id="24f2c-131">Für streaming-Client und Duplex-streaming-Aufrufe diese Rate kann nicht erfüllt werden, und möglicherweise werden Verbindungstimeout. Die minimale-Anforderungstext für die Datenrate muss deaktiviert werden, wenn der Dienst gRPC-streaming-Client und Duplex-streaming-Aufrufe enthält:</span><span class="sxs-lookup"><span data-stu-id="24f2c-131">For client streaming and duplex streaming calls, this rate may not be satisfied and the connection may be timed out. The minimum request body data rate limit must be disabled when the gRPC service includes client streaming and duplex streaming calls:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateHostBuilder(args).Build().Run();
    }

    public static IHostBuilder CreateHostBuilder(string[] args) =>
         Host.CreateDefaultBuilder(args)
    .ConfigureWebHostDefaults(webBuilder =>
    {
        webBuilder.UseStartup<Startup>();
        webBuilder.ConfigureKestrel((context, options) =>
        {
            options.Limits.MinRequestBodyDataRate = null;
        });
    });
}
```

## <a name="additional-resources"></a><span data-ttu-id="24f2c-132">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="24f2c-132">Additional resources</span></span>

* <xref:tutorials/grpc/grpc-start>
* <xref:grpc/index>
* <xref:grpc/basics>
* <xref:grpc/migration>