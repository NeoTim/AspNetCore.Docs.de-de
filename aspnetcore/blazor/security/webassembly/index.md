---
title: Sichern von Blazor-WebAssembly für ASP.NET Core
author: guardrex
description: Erfahren Sie, wie Sie Blazor-WebAssembly-Apps als Single-Page-Anwendungen (SPAs) sichern.
monikerRange: '>= aspnetcore-3.1'
ms.author: riande
ms.custom: mvc
ms.date: 06/01/2020
no-loc:
- Blazor
- Identity
- Let's Encrypt
- Razor
- SignalR
uid: blazor/security/webassembly/index
ms.openlocfilehash: 5b20ab96f5419a86ab162fdcf7a57020f6aa7227
ms.sourcegitcommit: 490434a700ba8c5ed24d849bd99d8489858538e3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85103137"
---
# <a name="secure-aspnet-core-blazor-webassembly"></a><span data-ttu-id="82981-103">Sichern von Blazor-WebAssembly für ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="82981-103">Secure ASP.NET Core Blazor WebAssembly</span></span>

<span data-ttu-id="82981-104">Von [Javier Calvarro Nelson](https://github.com/javiercn)</span><span class="sxs-lookup"><span data-stu-id="82981-104">By [Javier Calvarro Nelson](https://github.com/javiercn)</span></span>

Blazor<span data-ttu-id="82981-105">-WebAssembly-Apps werden auf die gleiche Weise gesichert wie Single-Page-Anwendungen (SPAs).</span><span class="sxs-lookup"><span data-stu-id="82981-105"> WebAssembly apps are secured in the same manner as Single Page Applications (SPAs).</span></span> <span data-ttu-id="82981-106">Es gibt mehrere Ansätze für die Authentifizierung von Benutzern bei SPAs, der gängigste und umfassendste Ansatz besteht jedoch darin, eine auf dem [OAuth 2.0-Protokoll](https://oauth.net/) basierende Implementierung wie [Open ID Connect (OIDC)](https://openid.net/connect/) zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="82981-106">There are several approaches for authenticating users to SPAs, but the most common and comprehensive approach is to use an implementation based on the [OAuth 2.0 protocol](https://oauth.net/), such as [Open ID Connect (OIDC)](https://openid.net/connect/).</span></span>

## <a name="authentication-library"></a><span data-ttu-id="82981-107">Authentifizierungsbibliothek</span><span class="sxs-lookup"><span data-stu-id="82981-107">Authentication library</span></span>

Blazor<span data-ttu-id="82981-108"> WebAssembly unterstützt die Authentifizierung und Autorisierung von Apps mithilfe von OIDC über die [Microsoft.AspNetCore.Components.WebAssembly.Authentication](https://www.nuget.org/packages/Microsoft.AspNetCore.Components.WebAssembly.Authentication/)-Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="82981-108"> WebAssembly supports authenticating and authorizing apps using OIDC via the [Microsoft.AspNetCore.Components.WebAssembly.Authentication](https://www.nuget.org/packages/Microsoft.AspNetCore.Components.WebAssembly.Authentication/) library.</span></span> <span data-ttu-id="82981-109">Die Bibliothek stellt mehrere Primitive für die nahtlose Authentifizierung für ASP.NET Core-Back-Ends bereit.</span><span class="sxs-lookup"><span data-stu-id="82981-109">The library provides a set of primitives for seamlessly authenticating against ASP.NET Core backends.</span></span> <span data-ttu-id="82981-110">Die Bibliothek integriert ASP.NET Core Identity mit der API-Authentifizierungsunterstützung, die auf [Identity Server](https://identityserver.io/) basiert.</span><span class="sxs-lookup"><span data-stu-id="82981-110">The library integrates ASP.NET Core Identity with API authorization support built on top of [Identity Server](https://identityserver.io/).</span></span> <span data-ttu-id="82981-111">Die Bibliothek kann bei einem Drittanbieter-Identitätsanbieter authentifiziert werden, der OIDC unterstützt (die OpenID-Anbieter).</span><span class="sxs-lookup"><span data-stu-id="82981-111">The library can authenticate against any third-party Identity Provider (IP) that supports OIDC, which are called OpenID Providers (OP).</span></span>

<span data-ttu-id="82981-112">Die Authentifizierungsunterstützung in Blazor-WebAssembly basiert auf der *oidc-client.js*-Bibliothek, die für die Verarbeitung der zugrunde liegenden Details des Authentifizierungsprotokolls verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="82981-112">The authentication support in Blazor WebAssembly is built on top of the *oidc-client.js* library, which is used to handle the underlying authentication protocol details.</span></span>

<span data-ttu-id="82981-113">Eine weitere Option zum Authentifizieren von SPAs ist die Verwendung von SameSite-Cookies.</span><span class="sxs-lookup"><span data-stu-id="82981-113">Other options for authenticating SPAs exist, such as the use of SameSite cookies.</span></span> <span data-ttu-id="82981-114">Das Entwurfsdesign von Blazor WebAssembly verwendet jedoch OAuth und OIDC als bewährte Option für die Authentifizierung bei Blazor WebAssembly-Apps.</span><span class="sxs-lookup"><span data-stu-id="82981-114">However, the engineering design of Blazor WebAssembly is settled on OAuth and OIDC as the best option for authentication in Blazor WebAssembly apps.</span></span> <span data-ttu-id="82981-115">Die auf [JSON Web Token](https://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) gestützte [tokenbasierte Authentifizierung](xref:security/anti-request-forgery#token-based-authentication) wurde aus Funktions- und Sicherheitsgründen der [cookiebasierten Authentifizierung](xref:security/anti-request-forgery#cookie-based-authentication) vorgezogen.</span><span class="sxs-lookup"><span data-stu-id="82981-115">[Token-based authentication](xref:security/anti-request-forgery#token-based-authentication) based on [JSON Web Tokens (JWTs)](https://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) was chosen over [cookie-based authentication](xref:security/anti-request-forgery#cookie-based-authentication) for functional and security reasons:</span></span>

* <span data-ttu-id="82981-116">Ein tokenbasiertes Protokoll bietet eine kleinere Angriffsfläche, da die Token nicht in allen Anforderungen gesendet werden.</span><span class="sxs-lookup"><span data-stu-id="82981-116">Using a token-based protocol offers a smaller attack surface area, as the tokens aren't sent in all requests.</span></span>
* <span data-ttu-id="82981-117">Serverendpunkte erfordern keinen Schutz gegenüber [websiteübergreifender Anforderungsfälschung (CSRF, Cross-Site Request Forgery)](xref:security/anti-request-forgery), da die Token explizit gesendet werden.</span><span class="sxs-lookup"><span data-stu-id="82981-117">Server endpoints don't require protection against [Cross-Site Request Forgery (CSRF)](xref:security/anti-request-forgery) because the tokens are sent explicitly.</span></span> <span data-ttu-id="82981-118">Dadurch können Sie Blazor-WebAssembly-Apps zusammen mit MVC- oder Razor Pages-Apps hosten.</span><span class="sxs-lookup"><span data-stu-id="82981-118">This allows you to host Blazor WebAssembly apps alongside MVC or Razor pages apps.</span></span>
* <span data-ttu-id="82981-119">Token haben eingeschränktere Berechtigungen als Cookies.</span><span class="sxs-lookup"><span data-stu-id="82981-119">Tokens have narrower permissions than cookies.</span></span> <span data-ttu-id="82981-120">Beispielsweise können Token nicht zum Verwalten des Benutzerkontos oder zur Änderung eines Benutzerkennworts verwendet werden, es sei denn, diese Funktionalität wird explizit implementiert.</span><span class="sxs-lookup"><span data-stu-id="82981-120">For example, tokens can't be used to manage the user account or change a user's password unless such functionality is explicitly implemented.</span></span>
* <span data-ttu-id="82981-121">Token haben eine kürzere Lebensdauer, standardmäßig eine Stunde, wodurch sich das Angriffsfenster verkleinert.</span><span class="sxs-lookup"><span data-stu-id="82981-121">Tokens have a short lifetime, one hour by default, which limits the attack window.</span></span> <span data-ttu-id="82981-122">Token können auch zu jeder Zeit widerrufen werden.</span><span class="sxs-lookup"><span data-stu-id="82981-122">Tokens can also be revoked at any time.</span></span>
* <span data-ttu-id="82981-123">Eigenständige JWTs bieten dem Client und dem Server Garantien zum Authentifizierungsprozess.</span><span class="sxs-lookup"><span data-stu-id="82981-123">Self-contained JWTs offer guarantees to the client and server about the authentication process.</span></span> <span data-ttu-id="82981-124">Ein Client verfügt zum Beispiel über die Mittel, um zu erkennen und zu überprüfen, dass die von ihm empfangenen Token legitim sind und im Rahmen eines bestimmten Authentifizierungsprozesses ausgegeben wurden.</span><span class="sxs-lookup"><span data-stu-id="82981-124">For example, a client has the means to detect and validate that the tokens it receives are legitimate and were emitted as part of a given authentication process.</span></span> <span data-ttu-id="82981-125">Wenn Dritte versuchen, ein Token inmitten des Authentifizierungsprozesses zu tauschen, kann der Client das ausgetauschte Token erkennen und so die Nutzung vermeiden.</span><span class="sxs-lookup"><span data-stu-id="82981-125">If a third party attempts to switch a token in the middle of the authentication process, the client can detect the switched token and avoid using it.</span></span>
* <span data-ttu-id="82981-126">Token mit OAuth und OIDC sind nicht vom ordnungsgemäßen Verhalten des Benutzer-Agents und davon abhängig, dass dieser gewährleistet, dass die App sicher ist.</span><span class="sxs-lookup"><span data-stu-id="82981-126">Tokens with OAuth and OIDC don't rely on the user agent behaving correctly to ensure that the app is secure.</span></span>
* <span data-ttu-id="82981-127">Tokenbasierte Protokolle wie OAuth und OIDC lassen die Authentifizierung und Autorisierung gehosteter und eigenständiger Apps mit denselben Sicherheitsmerkmalen zu.</span><span class="sxs-lookup"><span data-stu-id="82981-127">Token-based protocols, such as OAuth and OIDC, allow for authenticating and authorizing hosted and standalone apps with the same set of security characteristics.</span></span>

## <a name="authentication-process-with-oidc"></a><span data-ttu-id="82981-128">Authentifizierungsprozess mit OIDC</span><span class="sxs-lookup"><span data-stu-id="82981-128">Authentication process with OIDC</span></span>

<span data-ttu-id="82981-129">Die [Microsoft.AspNetCore.Components.WebAssembly.Authentication](https://www.nuget.org/packages/Microsoft.AspNetCore.Components.WebAssembly.Authentication/)-Bibliothek bietet verschiedene Primitive zum Implementieren der Authentifizierung und Autorisierung mithilfe von OIDC.</span><span class="sxs-lookup"><span data-stu-id="82981-129">The [Microsoft.AspNetCore.Components.WebAssembly.Authentication](https://www.nuget.org/packages/Microsoft.AspNetCore.Components.WebAssembly.Authentication/) library offers several primitives to implement authentication and authorization using OIDC.</span></span> <span data-ttu-id="82981-130">Im Allgemeinen funktioniert die Authentifizierung wie folgt:</span><span class="sxs-lookup"><span data-stu-id="82981-130">In broad terms, authentication works as follows:</span></span>

* <span data-ttu-id="82981-131">Wenn ein anonymer Benutzer auf die Anmeldeschaltfläche klickt oder eine Seite mit angewendetem [`[Authorize]`](xref:Microsoft.AspNetCore.Authorization.AuthorizeAttribute)-Attribut anfordert, wird der Benutzer zur Anmeldeseite (`/authentication/login`) der App weitergeleitet.</span><span class="sxs-lookup"><span data-stu-id="82981-131">When an anonymous user selects the login button or requests a page with the [`[Authorize]`](xref:Microsoft.AspNetCore.Authorization.AuthorizeAttribute) attribute applied, the user is redirected to the app's login page (`/authentication/login`).</span></span>
* <span data-ttu-id="82981-132">Auf der Anmeldeseite bereitet die Authentifizierungsbibliothek eine Umleitung zum Autorisierungsendpunkt vor.</span><span class="sxs-lookup"><span data-stu-id="82981-132">In the login page, the authentication library prepares for a redirect to the authorization endpoint.</span></span> <span data-ttu-id="82981-133">Der Autorisierungsendpunkt befindet sich außerhalb der Blazor-WebAssembly-App und kann als separater Ursprung gehostet werden.</span><span class="sxs-lookup"><span data-stu-id="82981-133">The authorization endpoint is outside of the Blazor WebAssembly app and can be hosted at a separate origin.</span></span> <span data-ttu-id="82981-134">Der Endpunkt ist dafür verantwortlich, zu bestimmen, ob der Benutzer authentifiziert ist, und dass ein oder mehrere Token als Antwort ausgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="82981-134">The endpoint is responsible for determining whether the user is authenticated and for issuing one or more tokens in response.</span></span> <span data-ttu-id="82981-135">Die Authentifizierungsbibliothek stellt einen Anmelderückruf zum Empfangen der Authentifizierungsantwort bereit.</span><span class="sxs-lookup"><span data-stu-id="82981-135">The authentication library provides a login callback to receive the authentication response.</span></span>
  * <span data-ttu-id="82981-136">Wenn der Benutzer nicht authentifiziert ist, wird er an das zugrunde liegende Authentifizierungssystem umgeleitet (normalerweise ASP.NET Core Identity).</span><span class="sxs-lookup"><span data-stu-id="82981-136">If the user isn't authenticated, the user is redirected to the underlying authentication system, which is usually ASP.NET Core Identity.</span></span>
  * <span data-ttu-id="82981-137">Wenn der Benutzer bereits authentifiziert wurde, generiert der Authentifizierungsendpunkt die entsprechenden Token und leitet den Browser zurück an den Anmelderückrufendpunkt (`/authentication/login-callback`).</span><span class="sxs-lookup"><span data-stu-id="82981-137">If the user was already authenticated, the authorization endpoint generates the appropriate tokens and redirects the browser back to the login callback endpoint (`/authentication/login-callback`).</span></span>
* <span data-ttu-id="82981-138">Wenn die Blazor-WebAssembly-App den Anmelderückrufendpunkt (`/authentication/login-callback`) lädt, wird die Authentifizierungsantwort verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="82981-138">When the Blazor WebAssembly app loads the login callback endpoint (`/authentication/login-callback`), the authentication response is processed.</span></span>
  * <span data-ttu-id="82981-139">Sobald der Authentifizierungsprozess erfolgreich abgeschlossen wird, wird der Benutzer authentifiziert und optional an die ursprüngliche geschützte URL weitergeleitet, die vom Benutzer angefordert wurde.</span><span class="sxs-lookup"><span data-stu-id="82981-139">If the authentication process completes successfully, the user is authenticated and optionally sent back to the original protected URL that the user requested.</span></span>
  * <span data-ttu-id="82981-140">Sollte der Authentifizierungsprozess aus irgend einem Grund fehlschlagen, wird der Benutzer auf die Seite „Fehler bei der Anmeldung“ (`/authentication/login-failed`) weitergeleitet, und ein Fehler wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="82981-140">If the authentication process fails for any reason, the user is sent to the login failed page (`/authentication/login-failed`), and an error is displayed.</span></span>

## <a name="authorization"></a><span data-ttu-id="82981-141">Autorisierung</span><span class="sxs-lookup"><span data-stu-id="82981-141">Authorization</span></span>

<span data-ttu-id="82981-142">In Blazor WebAssembly-Apps können Autorisierungsprüfungen umgangen werden, da der gesamte clientseitige Code von Benutzern geändert werden kann.</span><span class="sxs-lookup"><span data-stu-id="82981-142">In Blazor WebAssembly apps, authorization checks can be bypassed because all client-side code can be modified by users.</span></span> <span data-ttu-id="82981-143">Dasselbe gilt für alle clientseitigen App-Technologien, einschließlich JavaScript SPA-Frameworks oder native Apps für jedes Betriebssystem.</span><span class="sxs-lookup"><span data-stu-id="82981-143">The same is true for all client-side app technologies, including JavaScript SPA frameworks or native apps for any operating system.</span></span>

<span data-ttu-id="82981-144">**Führen Sie Autorisierungsprüfungen auf dem Server immer innerhalb aller API-Endpunkte durch, auf die Ihre clientseitige App zugreift.**</span><span class="sxs-lookup"><span data-stu-id="82981-144">**Always perform authorization checks on the server within any API endpoints accessed by your client-side app.**</span></span>

## <a name="refresh-tokens"></a><span data-ttu-id="82981-145">Aktualisierungstoken</span><span class="sxs-lookup"><span data-stu-id="82981-145">Refresh tokens</span></span>

<span data-ttu-id="82981-146">Aktualisierungstoken können nicht auf Clientseite in Blazor-WebAssembly-Apps gesichert werden.</span><span class="sxs-lookup"><span data-stu-id="82981-146">Refresh tokens can't be secured client-side in Blazor WebAssembly apps.</span></span> <span data-ttu-id="82981-147">Daher sollten Aktualisierungstoken nicht zur direkten Verwendung an die App gesendet werden.</span><span class="sxs-lookup"><span data-stu-id="82981-147">Therefore, refresh tokens shouldn't be sent to the app for direct use.</span></span>

<span data-ttu-id="82981-148">Aktualisierungstoken können von der serverseitigen App in einer gehosteten Blazor-WebAssembly-Lösung verwaltet und verwendet werden, um auf APIs von Drittanbietern zuzugreifen.</span><span class="sxs-lookup"><span data-stu-id="82981-148">Refresh tokens can be maintained and used by the server-side app in a Hosted Blazor WebAssembly solution to access third-party APIs.</span></span> <span data-ttu-id="82981-149">Weitere Informationen finden Sie unter <xref:blazor/security/webassembly/additional-scenarios#authenticate-users-with-a-third-party-provider-and-call-protected-apis-on-the-host-server-and-the-third-party>.</span><span class="sxs-lookup"><span data-stu-id="82981-149">For more information, see <xref:blazor/security/webassembly/additional-scenarios#authenticate-users-with-a-third-party-provider-and-call-protected-apis-on-the-host-server-and-the-third-party>.</span></span>

## <a name="implementation-guidance"></a><span data-ttu-id="82981-150">Implementierungsleitfaden</span><span class="sxs-lookup"><span data-stu-id="82981-150">Implementation guidance</span></span>

<span data-ttu-id="82981-151">Artikel unter dieser *Übersicht* bieten Informationen zum Authentifizieren von Benutzern in Blazor WebAssembly-Apps für bestimmte Anbieter.</span><span class="sxs-lookup"><span data-stu-id="82981-151">Articles under this *Overview* provide information on authenticating users in Blazor WebAssembly apps against specific providers.</span></span>

<span data-ttu-id="82981-152">Eigenständige Blazor-WebAssembly-Apps</span><span class="sxs-lookup"><span data-stu-id="82981-152">Standalone Blazor WebAssembly apps:</span></span>

* [<span data-ttu-id="82981-153">Allgemeiner Leitfaden für OIDC-Anbieter und die WebAssembly-Authentifizierungsbibliothek</span><span class="sxs-lookup"><span data-stu-id="82981-153">General guidance for OIDC providers and the WebAssembly Authentication Library</span></span>](xref:blazor/security/webassembly/standalone-with-authentication-library)
* [<span data-ttu-id="82981-154">Microsoft-Konten</span><span class="sxs-lookup"><span data-stu-id="82981-154">Microsoft Accounts</span></span>](xref:blazor/security/webassembly/standalone-with-microsoft-accounts)
* [<span data-ttu-id="82981-155">Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="82981-155">Azure Active Directory (AAD)</span></span>](xref:blazor/security/webassembly/standalone-with-azure-active-directory)
* [<span data-ttu-id="82981-156">Azure Active Directory (AAD) B2C</span><span class="sxs-lookup"><span data-stu-id="82981-156">Azure Active Directory (AAD) B2C</span></span>](xref:blazor/security/webassembly/standalone-with-azure-active-directory-b2c)

<span data-ttu-id="82981-157">Gehostete Blazor-WebAssembly-Apps:</span><span class="sxs-lookup"><span data-stu-id="82981-157">Hosted Blazor WebAssembly apps:</span></span>

* [<span data-ttu-id="82981-158">Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="82981-158">Azure Active Directory (AAD)</span></span>](xref:blazor/security/webassembly/hosted-with-azure-active-directory)
* [<span data-ttu-id="82981-159">Azure Active Directory (AAD) B2C</span><span class="sxs-lookup"><span data-stu-id="82981-159">Azure Active Directory (AAD) B2C</span></span>](xref:blazor/security/webassembly/hosted-with-azure-active-directory-b2c)
* <span data-ttu-id="82981-160">[Identity Server](xref:blazor/security/webassembly/hosted-with-identity-server)</span><span class="sxs-lookup"><span data-stu-id="82981-160">[Identity Server](xref:blazor/security/webassembly/hosted-with-identity-server)</span></span>

<span data-ttu-id="82981-161">Weitere Anleitungen zur Konfiguration finden Sie unter <xref:blazor/security/webassembly/additional-scenarios>.</span><span class="sxs-lookup"><span data-stu-id="82981-161">For further guidance on configuration, see <xref:blazor/security/webassembly/additional-scenarios>.</span></span>