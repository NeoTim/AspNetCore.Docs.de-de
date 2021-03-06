---
title: Authentifizierungs Beispiele für ASP.net Core
author: rick-anderson
description: Enthält Links zu den Authentifizierungs Beispielen im ASP.net Core Repository.
ms.author: riande
ms.date: 01/31/2019
no-loc:
- ASP.NET Core Identity
- cookie
- Cookie
- Blazor
- Blazor Server
- Blazor WebAssembly
- Identity
- Let's Encrypt
- Razor
- SignalR
uid: security/authentication/samples
ms.openlocfilehash: 290c956b2035e47e5b34dba15fbec665461dd94a
ms.sourcegitcommit: 65add17f74a29a647d812b04517e46cbc78258f9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88630743"
---
# <a name="authentication-samples-for-aspnet-core"></a>Authentifizierungs Beispiele für ASP.net Core

Von [Rick Anderson](https://twitter.com/RickAndMSFT)

::: moniker range=">= aspnetcore-3.0"

Das [ASP.net Core-Repository](https://github.com/dotnet/AspNetCore) enthält die folgenden Authentifizierungs Beispiele im Ordner " *aspnetcore/src/Security/Samples* ":

* [Transformation von Ansprüchen](https://github.com/dotnet/AspNetCore/tree/release/3.1/src/Security/samples/ClaimsTransformation)
* [Cookie Genehmigung](https://github.com/dotnet/AspNetCore/tree/release/3.1/src/Security/samples/Cookies)
* [Benutzerdefinierter Richtlinien Anbieter-iauthorizationpolicyprovider](https://github.com/dotnet/AspNetCore/tree/release/3.1/src/Security/samples/CustomPolicyProvider)
* [Dynamische Authentifizierungs Schemas und-Optionen](https://github.com/dotnet/AspNetCore/tree/release/3.1/src/Security/samples/DynamicSchemes)
* [Externe Ansprüche](https://github.com/dotnet/AspNetCore/tree/release/3.1/src/Security/samples/Identity.ExternalClaims)
* [Auswählen zwischen cookie und einem anderen Authentifizierungsschema basierend auf der Anforderung](https://github.com/dotnet/AspNetCore/tree/release/3.1/src/Security/samples/PathSchemeSelection)
* [Schränkt den Zugriff auf statische Dateien ein.](https://github.com/dotnet/AspNetCore/tree/release/3.1/src/Security/samples/StaticFilesAuth)

## <a name="run-the-samples"></a>Ausführen der Beispiele

* Wählen Sie eine [Verzweigung](https://github.com/dotnet/AspNetCore)aus. Zum Beispiel, `release/3.1`
* Klonen Sie das [ASP.net Core Repository](https://github.com/dotnet/AspNetCore), oder laden Sie es herunter.
* Vergewissern Sie sich, dass Sie die [.net Core SDK](https://dotnet.microsoft.com/download/dotnet-core) Version installiert haben, die mit dem Klon des ASP.net Core Repository übereinstimmt.
* Navigieren Sie in *aspnetcore/src/Security/Samples* zu einem Beispiel, und führen Sie das Beispiel mit aus `dotnet run` .

::: moniker-end

::: moniker range="< aspnetcore-3.0"

Das [ASP.net Core-Repository](https://github.com/dotnet/AspNetCore) enthält die folgenden Authentifizierungs Beispiele im Ordner " *aspnetcore/src/Security/Samples* ":

* [Transformation von Ansprüchen](https://github.com/dotnet/AspNetCore/tree/release/2.1/src/Security/samples/ClaimsTransformation)
* [Cookie Genehmigung](https://github.com/dotnet/AspNetCore/tree/release/2.1/src/Security/samples/Cookies)
* [Benutzerdefinierter Richtlinien Anbieter-iauthorizationpolicyprovider](https://github.com/dotnet/AspNetCore/tree/2.1.3/src/Security/samples/CustomPolicyProvider)
* [Dynamische Authentifizierungs Schemas und-Optionen](https://github.com/dotnet/AspNetCore/tree/release/2.1/src/Security/samples/DynamicSchemes)
* [Externe Ansprüche](https://github.com/dotnet/AspNetCore/tree/release/2.1/src/Security/samples/Identity.ExternalClaims)
* [Auswählen zwischen cookie und einem anderen Authentifizierungsschema basierend auf der Anforderung](https://github.com/dotnet/AspNetCore/tree/release/2.1/src/Security/samples/PathSchemeSelection)
* [Schränkt den Zugriff auf statische Dateien ein.](https://github.com/dotnet/AspNetCore/tree/2.1.3/src/Security/samples/StaticFilesAuth)

## <a name="run-the-samples"></a>Ausführen der Beispiele

* Wählen Sie eine [Verzweigung](https://github.com/dotnet/AspNetCore)aus. Zum Beispiel, `release/2.1`
* Klonen Sie das [ASP.net Core Repository](https://github.com/dotnet/AspNetCore), oder laden Sie es herunter.
* Vergewissern Sie sich, dass Sie die [.net Core SDK](https://dotnet.microsoft.com/download/dotnet-core) Version installiert haben, die mit dem Klon des ASP.net Core Repository übereinstimmt.
* Navigieren Sie in *aspnetcore/src/Security/Samples* zu einem Beispiel, und führen Sie das Beispiel mit aus `dotnet run` .

::: moniker-end
