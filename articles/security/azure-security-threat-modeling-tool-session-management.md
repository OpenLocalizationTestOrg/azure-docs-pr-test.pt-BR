---
title: "Gerenciamento de sessão - Ferramenta de Modelagem de Ameaças da Microsoft - Azure | Microsoft Docs"
description: "atenuações de ameaças expostas na Ferramenta de Modelagem de Ameaças"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 56471d8ef68eacacb3ecebad5056d7e7a9f3ca40
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="security-frame-session-management--articles"></a><span data-ttu-id="99fc5-103">Quadro de segurança: Gerenciamento de sessão | Artigos</span><span class="sxs-lookup"><span data-stu-id="99fc5-103">Security Frame: Session Management | Articles</span></span> 
| <span data-ttu-id="99fc5-104">Produto/Serviço</span><span class="sxs-lookup"><span data-stu-id="99fc5-104">Product/Service</span></span> | <span data-ttu-id="99fc5-105">Artigo</span><span class="sxs-lookup"><span data-stu-id="99fc5-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="99fc5-106">**Azure AD**</span><span class="sxs-lookup"><span data-stu-id="99fc5-106">**Azure AD**</span></span>    | <ul><li>[<span data-ttu-id="99fc5-107">Implementar o logoff apropriado usando métodos ADAL ao usar o Azure AD</span><span class="sxs-lookup"><span data-stu-id="99fc5-107">Implement proper logout using ADAL methods when using Azure AD</span></span>](#logout-adal)</li></ul> |
| <span data-ttu-id="99fc5-108">Dispositivo IoT</span><span class="sxs-lookup"><span data-stu-id="99fc5-108">IoT Device</span></span> | <ul><li>[<span data-ttu-id="99fc5-109">Usar tempos de vida finitos para tokens SaS gerados</span><span class="sxs-lookup"><span data-stu-id="99fc5-109">Use finite lifetimes for generated SaS tokens</span></span>](#finite-tokens)</li></ul> |
| <span data-ttu-id="99fc5-110">**Azure DocumentDB**</span><span class="sxs-lookup"><span data-stu-id="99fc5-110">**Azure Document DB**</span></span> | <ul><li>[<span data-ttu-id="99fc5-111">Usar tempos de vida mínimos de tokens para tokens de Recurso gerados</span><span class="sxs-lookup"><span data-stu-id="99fc5-111">Use minimum token lifetimes for generated Resource tokens</span></span>](#resource-tokens)</li></ul> |
| <span data-ttu-id="99fc5-112">**ADFS**</span><span class="sxs-lookup"><span data-stu-id="99fc5-112">**ADFS**</span></span> | <ul><li>[<span data-ttu-id="99fc5-113">Implementar o logoff apropriado usando métodos WsFederation ao usar o ADFS</span><span class="sxs-lookup"><span data-stu-id="99fc5-113">Implement proper logout using WsFederation methods when using ADFS</span></span>](#wsfederation-logout)</li></ul> |
| <span data-ttu-id="99fc5-114">**Identity Server**</span><span class="sxs-lookup"><span data-stu-id="99fc5-114">**Identity Server**</span></span> | <ul><li>[<span data-ttu-id="99fc5-115">Implementar o logoff adequado ao usar o Servidor de identidade</span><span class="sxs-lookup"><span data-stu-id="99fc5-115">Implement proper logout when using Identity Server</span></span>](#proper-logout)</li></ul> |
| <span data-ttu-id="99fc5-116">**Aplicativo Web**</span><span class="sxs-lookup"><span data-stu-id="99fc5-116">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="99fc5-117">Os aplicativos disponíveis via HTTPS devem usar cookies seguros</span><span class="sxs-lookup"><span data-stu-id="99fc5-117">Applications available over HTTPS must use secure cookies</span></span>](#https-secure-cookies)</li><li>[<span data-ttu-id="99fc5-118">Todo aplicativo baseado em http deve especificar http somente para definição de cookie</span><span class="sxs-lookup"><span data-stu-id="99fc5-118">All http based application should specify http only for cookie definition</span></span>](#cookie-definition)</li><li>[<span data-ttu-id="99fc5-119">Atenuar ataques CSRF (solicitação intersite forjada) em páginas Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="99fc5-119">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>](#csrf-asp)</li><li>[<span data-ttu-id="99fc5-120">Configurar sessão para tempo de vida de inatividade</span><span class="sxs-lookup"><span data-stu-id="99fc5-120">Set up session for inactivity lifetime</span></span>](#inactivity-lifetime)</li><li>[<span data-ttu-id="99fc5-121">Implementar o logoff apropriado do aplicativo</span><span class="sxs-lookup"><span data-stu-id="99fc5-121">Implement proper logout from the application</span></span>](#proper-app-logout)</li></ul> |
| <span data-ttu-id="99fc5-122">**API da Web**</span><span class="sxs-lookup"><span data-stu-id="99fc5-122">**Web API**</span></span> | <ul><li>[<span data-ttu-id="99fc5-123">Atenuar ataques CSRF (solicitação intersite forjada) em APIs da Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="99fc5-123">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>](#csrf-api)</li></ul> |

## <span data-ttu-id="99fc5-124"><a id="logout-adal"></a>Implementar o logoff apropriado usando métodos ADAL ao usar o Azure AD</span><span class="sxs-lookup"><span data-stu-id="99fc5-124"><a id="logout-adal"></a>Implement proper logout using ADAL methods when using Azure AD</span></span>

| <span data-ttu-id="99fc5-125">Title</span><span class="sxs-lookup"><span data-stu-id="99fc5-125">Title</span></span>                   | <span data-ttu-id="99fc5-126">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99fc5-126">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99fc5-127">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99fc5-127">**Component**</span></span>               | <span data-ttu-id="99fc5-128">AD do Azure</span><span class="sxs-lookup"><span data-stu-id="99fc5-128">Azure AD</span></span> | 
| <span data-ttu-id="99fc5-129">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99fc5-129">**SDL Phase**</span></span>               | <span data-ttu-id="99fc5-130">Compilação</span><span class="sxs-lookup"><span data-stu-id="99fc5-130">Build</span></span> |  
| <span data-ttu-id="99fc5-131">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99fc5-131">**Applicable Technologies**</span></span> | <span data-ttu-id="99fc5-132">Genérico</span><span class="sxs-lookup"><span data-stu-id="99fc5-132">Generic</span></span> |
| <span data-ttu-id="99fc5-133">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99fc5-133">**Attributes**</span></span>              | <span data-ttu-id="99fc5-134">N/D</span><span class="sxs-lookup"><span data-stu-id="99fc5-134">N/A</span></span>  |
| <span data-ttu-id="99fc5-135">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99fc5-135">**References**</span></span>              | <span data-ttu-id="99fc5-136">N/D</span><span class="sxs-lookup"><span data-stu-id="99fc5-136">N/A</span></span>  |
| <span data-ttu-id="99fc5-137">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99fc5-137">**Steps**</span></span> | <span data-ttu-id="99fc5-138">Se o aplicativo depende do token de acesso emitido pelo Azure AD, o manipulador de evento de logoff deverá chamar</span><span class="sxs-lookup"><span data-stu-id="99fc5-138">If the application relies on access token issued by Azure AD, the logout event handler should call</span></span> |

### <a name="example"></a><span data-ttu-id="99fc5-139">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99fc5-139">Example</span></span>
```C#
HttpContext.GetOwinContext().Authentication.SignOut(OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType)
```

### <a name="example"></a><span data-ttu-id="99fc5-140">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99fc5-140">Example</span></span>
<span data-ttu-id="99fc5-141">Também deve destruir a sessão do usuário chamando o método Session.Abandon().</span><span class="sxs-lookup"><span data-stu-id="99fc5-141">It should also destroy user's session by calling Session.Abandon() method.</span></span> <span data-ttu-id="99fc5-142">O método a seguir mostra a implementação segura do logoff do usuário:</span><span class="sxs-lookup"><span data-stu-id="99fc5-142">Following method shows secure implementation of user logout:</span></span>
```C#
    [HttpPost]
        [ValidateAntiForgeryToken]
        public void LogOff()
        {
            string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            AuthenticationContext authContext = new AuthenticationContext(Authority + TenantId, new NaiveSessionCache(userObjectID));
            authContext.TokenCache.Clear();
            Session.Clear();
            Session.Abandon();
            Response.SetCookie(new HttpCookie("ASP.NET_SessionId", string.Empty));
            HttpContext.GetOwinContext().Authentication.SignOut(
                OpenIdConnectAuthenticationDefaults.AuthenticationType,
                CookieAuthenticationDefaults.AuthenticationType);
        } 
```

## <span data-ttu-id="99fc5-143"><a id="finite-tokens"></a>Usar tempos de vida finitos para tokens SaS gerados</span><span class="sxs-lookup"><span data-stu-id="99fc5-143"><a id="finite-tokens"></a>Use finite lifetimes for generated SaS tokens</span></span>

| <span data-ttu-id="99fc5-144">Title</span><span class="sxs-lookup"><span data-stu-id="99fc5-144">Title</span></span>                   | <span data-ttu-id="99fc5-145">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99fc5-145">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99fc5-146">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99fc5-146">**Component**</span></span>               | <span data-ttu-id="99fc5-147">Dispositivo IoT</span><span class="sxs-lookup"><span data-stu-id="99fc5-147">IoT Device</span></span> | 
| <span data-ttu-id="99fc5-148">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99fc5-148">**SDL Phase**</span></span>               | <span data-ttu-id="99fc5-149">Compilação</span><span class="sxs-lookup"><span data-stu-id="99fc5-149">Build</span></span> |  
| <span data-ttu-id="99fc5-150">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99fc5-150">**Applicable Technologies**</span></span> | <span data-ttu-id="99fc5-151">Genérico</span><span class="sxs-lookup"><span data-stu-id="99fc5-151">Generic</span></span> |
| <span data-ttu-id="99fc5-152">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99fc5-152">**Attributes**</span></span>              | <span data-ttu-id="99fc5-153">N/D</span><span class="sxs-lookup"><span data-stu-id="99fc5-153">N/A</span></span>  |
| <span data-ttu-id="99fc5-154">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99fc5-154">**References**</span></span>              | <span data-ttu-id="99fc5-155">N/D</span><span class="sxs-lookup"><span data-stu-id="99fc5-155">N/A</span></span>  |
| <span data-ttu-id="99fc5-156">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99fc5-156">**Steps**</span></span> | <span data-ttu-id="99fc5-157">Tokens SaS gerados para autenticar no Hub IoT do Azure devem ter um período de expiração finito.</span><span class="sxs-lookup"><span data-stu-id="99fc5-157">SaS tokens generated for authenticating to Azure IoT Hub should have a finite expiry period.</span></span> <span data-ttu-id="99fc5-158">Mantenha o tempo de vida do token SaS com um valor mínimo a fim de limitar o tempo que ele pode ser reproduzido em caso de comprometimento do token.</span><span class="sxs-lookup"><span data-stu-id="99fc5-158">Keep the SaS token lifetimes to a minimum to limit the amount of time they can be replayed in case the tokens are compromised.</span></span>|

## <span data-ttu-id="99fc5-159"><a id="resource-tokens"></a>Usar tempos de vida mínimos de tokens para tokens de Recurso gerados</span><span class="sxs-lookup"><span data-stu-id="99fc5-159"><a id="resource-tokens"></a>Use minimum token lifetimes for generated Resource tokens</span></span>

| <span data-ttu-id="99fc5-160">Title</span><span class="sxs-lookup"><span data-stu-id="99fc5-160">Title</span></span>                   | <span data-ttu-id="99fc5-161">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99fc5-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99fc5-162">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99fc5-162">**Component**</span></span>               | <span data-ttu-id="99fc5-163">Azure Document DB</span><span class="sxs-lookup"><span data-stu-id="99fc5-163">Azure Document DB</span></span> | 
| <span data-ttu-id="99fc5-164">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99fc5-164">**SDL Phase**</span></span>               | <span data-ttu-id="99fc5-165">Compilação</span><span class="sxs-lookup"><span data-stu-id="99fc5-165">Build</span></span> |  
| <span data-ttu-id="99fc5-166">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99fc5-166">**Applicable Technologies**</span></span> | <span data-ttu-id="99fc5-167">Genérico</span><span class="sxs-lookup"><span data-stu-id="99fc5-167">Generic</span></span> |
| <span data-ttu-id="99fc5-168">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99fc5-168">**Attributes**</span></span>              | <span data-ttu-id="99fc5-169">N/D</span><span class="sxs-lookup"><span data-stu-id="99fc5-169">N/A</span></span>  |
| <span data-ttu-id="99fc5-170">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99fc5-170">**References**</span></span>              | <span data-ttu-id="99fc5-171">N/D</span><span class="sxs-lookup"><span data-stu-id="99fc5-171">N/A</span></span>  |
| <span data-ttu-id="99fc5-172">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99fc5-172">**Steps**</span></span> | <span data-ttu-id="99fc5-173">Reduza o intervalo de tempo do token de recurso para um valor mínimo necessário.</span><span class="sxs-lookup"><span data-stu-id="99fc5-173">Reduce the timespan of resource token to a minimum value required.</span></span> <span data-ttu-id="99fc5-174">Tokens de recurso têm um intervalo de tempo válido padrão de uma hora.</span><span class="sxs-lookup"><span data-stu-id="99fc5-174">Resource tokens have a default valid timespan of 1 hour.</span></span>|

## <span data-ttu-id="99fc5-175"><a id="wsfederation-logout"></a>Implementar o logoff apropriado usando métodos WsFederation ao usar o ADFS</span><span class="sxs-lookup"><span data-stu-id="99fc5-175"><a id="wsfederation-logout"></a>Implement proper logout using WsFederation methods when using ADFS</span></span>

| <span data-ttu-id="99fc5-176">Title</span><span class="sxs-lookup"><span data-stu-id="99fc5-176">Title</span></span>                   | <span data-ttu-id="99fc5-177">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99fc5-177">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99fc5-178">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99fc5-178">**Component**</span></span>               | <span data-ttu-id="99fc5-179">ADFS</span><span class="sxs-lookup"><span data-stu-id="99fc5-179">ADFS</span></span> | 
| <span data-ttu-id="99fc5-180">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99fc5-180">**SDL Phase**</span></span>               | <span data-ttu-id="99fc5-181">Compilação</span><span class="sxs-lookup"><span data-stu-id="99fc5-181">Build</span></span> |  
| <span data-ttu-id="99fc5-182">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99fc5-182">**Applicable Technologies**</span></span> | <span data-ttu-id="99fc5-183">Genérico</span><span class="sxs-lookup"><span data-stu-id="99fc5-183">Generic</span></span> |
| <span data-ttu-id="99fc5-184">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99fc5-184">**Attributes**</span></span>              | <span data-ttu-id="99fc5-185">N/D</span><span class="sxs-lookup"><span data-stu-id="99fc5-185">N/A</span></span>  |
| <span data-ttu-id="99fc5-186">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99fc5-186">**References**</span></span>              | <span data-ttu-id="99fc5-187">N/D</span><span class="sxs-lookup"><span data-stu-id="99fc5-187">N/A</span></span>  |
| <span data-ttu-id="99fc5-188">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99fc5-188">**Steps**</span></span> | <span data-ttu-id="99fc5-189">Se o aplicativo depender do token de STS emitido pelo ADFS, o manipulador de eventos de logoff deverá chamar o método WSFederationAuthenticationModule.FederatedSignOut() para fazer logoff do usuário.</span><span class="sxs-lookup"><span data-stu-id="99fc5-189">If the application relies on STS token issued by ADFS, the logout event handler should call WSFederationAuthenticationModule.FederatedSignOut() method to log out the user.</span></span> <span data-ttu-id="99fc5-190">Além disso, a sessão atual deve ser destruída, e o valor do token da sessão deve ser redefinido e tornado nulo.</span><span class="sxs-lookup"><span data-stu-id="99fc5-190">Also the current session should be destroyed, and the session token value should be reset and nullified.</span></span>|

### <a name="example"></a><span data-ttu-id="99fc5-191">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99fc5-191">Example</span></span>
```C#
        [HttpPost, ValidateAntiForgeryToken]
        [Authorization]
        public ActionResult SignOut(string redirectUrl)
        {
            if (!this.User.Identity.IsAuthenticated)
            {
                return this.View("LogOff", null);
            }

            // Removes the user profile.
            this.Session.Clear();
            this.Session.Abandon();
            HttpContext.Current.Response.Cookies.Add(new System.Web.HttpCookie("ASP.NET_SessionId", string.Empty)
                {
                    Expires = DateTime.Now.AddDays(-1D),
                    Secure = true,
                    HttpOnly = true
                });

            // Signs out at the specified security token service (STS) by using the WS-Federation protocol.
            Uri signOutUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Issuer);
            Uri replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm);
            if (!string.IsNullOrEmpty(redirectUrl))
            {
                replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm + redirectUrl);
            }
           //     Signs out of the current session and raises the appropriate events.
            var authModule = FederatedAuthentication.WSFederationAuthenticationModule;
            authModule.SignOut(false);
        //     Signs out at the specified security token service (STS) by using the WS-Federation
        //     protocol.            
            WSFederationAuthenticationModule.FederatedSignOut(signOutUrl, replyUrl);
            return new RedirectResult(redirectUrl);
        }
```

## <span data-ttu-id="99fc5-192"><a id="proper-logout"></a>Implementar o logoff adequado ao usar o Servidor de identidade</span><span class="sxs-lookup"><span data-stu-id="99fc5-192"><a id="proper-logout"></a>Implement proper logout when using Identity Server</span></span>

| <span data-ttu-id="99fc5-193">Title</span><span class="sxs-lookup"><span data-stu-id="99fc5-193">Title</span></span>                   | <span data-ttu-id="99fc5-194">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99fc5-194">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99fc5-195">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99fc5-195">**Component**</span></span>               | <span data-ttu-id="99fc5-196">Servidor de Identidade</span><span class="sxs-lookup"><span data-stu-id="99fc5-196">Identity Server</span></span> | 
| <span data-ttu-id="99fc5-197">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99fc5-197">**SDL Phase**</span></span>               | <span data-ttu-id="99fc5-198">Compilação</span><span class="sxs-lookup"><span data-stu-id="99fc5-198">Build</span></span> |  
| <span data-ttu-id="99fc5-199">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99fc5-199">**Applicable Technologies**</span></span> | <span data-ttu-id="99fc5-200">Genérico</span><span class="sxs-lookup"><span data-stu-id="99fc5-200">Generic</span></span> |
| <span data-ttu-id="99fc5-201">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99fc5-201">**Attributes**</span></span>              | <span data-ttu-id="99fc5-202">N/D</span><span class="sxs-lookup"><span data-stu-id="99fc5-202">N/A</span></span>  |
| <span data-ttu-id="99fc5-203">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99fc5-203">**References**</span></span>              | [<span data-ttu-id="99fc5-204">Saída do IdentityServer3-Federated</span><span class="sxs-lookup"><span data-stu-id="99fc5-204">IdentityServer3-Federated sign out</span></span>](https://identityserver.github.io/Documentation/docsv2/advanced/federated-signout.html) |
| <span data-ttu-id="99fc5-205">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99fc5-205">**Steps**</span></span> | <span data-ttu-id="99fc5-206">O IdentityServer oferece suporte à federação com provedores de identidade externos.</span><span class="sxs-lookup"><span data-stu-id="99fc5-206">IdentityServer supports the ability to federate with external identity providers.</span></span> <span data-ttu-id="99fc5-207">Quando um usuário sai de um provedor de identidade upstream, dependendo do protocolo usado, talvez seja possível receber uma notificação quando o usuário se desconectar. Isso permite que o IdentityServer notifique seus clientes para que eles também possam desconectar o usuário. Consulte a documentação na seção de referências para obter detalhes sobre a implementação.</span><span class="sxs-lookup"><span data-stu-id="99fc5-207">When a user signs out of an upstream identity provider, depending upon the protocol used, it might be possible to receive a notification when the user signs out. It allows IdentityServer to notify its clients so they can also sign the user out. Check the documentation in the references section for the implementation details.</span></span>|

## <span data-ttu-id="99fc5-208"><a id="https-secure-cookies"></a>Os aplicativos disponíveis via HTTPS devem usar cookies seguros</span><span class="sxs-lookup"><span data-stu-id="99fc5-208"><a id="https-secure-cookies"></a>Applications available over HTTPS must use secure cookies</span></span>

| <span data-ttu-id="99fc5-209">Title</span><span class="sxs-lookup"><span data-stu-id="99fc5-209">Title</span></span>                   | <span data-ttu-id="99fc5-210">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99fc5-210">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99fc5-211">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99fc5-211">**Component**</span></span>               | <span data-ttu-id="99fc5-212">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="99fc5-212">Web Application</span></span> | 
| <span data-ttu-id="99fc5-213">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99fc5-213">**SDL Phase**</span></span>               | <span data-ttu-id="99fc5-214">Compilação</span><span class="sxs-lookup"><span data-stu-id="99fc5-214">Build</span></span> |  
| <span data-ttu-id="99fc5-215">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99fc5-215">**Applicable Technologies**</span></span> | <span data-ttu-id="99fc5-216">Genérico</span><span class="sxs-lookup"><span data-stu-id="99fc5-216">Generic</span></span> |
| <span data-ttu-id="99fc5-217">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99fc5-217">**Attributes**</span></span>              | <span data-ttu-id="99fc5-218">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="99fc5-218">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="99fc5-219">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99fc5-219">**References**</span></span>              | <span data-ttu-id="99fc5-220">[httpCookies Element (Esquema de configurações ASP.NET)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [Propriedade HttpCookie.Secure](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span><span class="sxs-lookup"><span data-stu-id="99fc5-220">[httpCookies Element (ASP.NET Settings Schema)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure Property](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span></span> |
| <span data-ttu-id="99fc5-221">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99fc5-221">**Steps**</span></span> | <span data-ttu-id="99fc5-222">Normalmente, os cookies só são acessíveis ao domínio para o qual foram definidos.</span><span class="sxs-lookup"><span data-stu-id="99fc5-222">Cookies are normally only accessible to the domain for which they were scoped.</span></span> <span data-ttu-id="99fc5-223">Infelizmente, a definição de "domínio" não inclui o protocolo para que cookies criados por HTTPS sejam acessíveis via HTTP.</span><span class="sxs-lookup"><span data-stu-id="99fc5-223">Unfortunately, the definition of "domain" does not include the protocol so cookies that are created over HTTPS are accessible over HTTP.</span></span> <span data-ttu-id="99fc5-224">O atributo "secure" indica para o navegador que o cookie deve ser disponibilizado apenas por HTTPS.</span><span class="sxs-lookup"><span data-stu-id="99fc5-224">The "secure" attribute indicates to the browser that the cookie should only be made available over HTTPS.</span></span> <span data-ttu-id="99fc5-225">Certifique-se de que todos os cookies definidos por HTTPS usem o atributo **secure**.</span><span class="sxs-lookup"><span data-stu-id="99fc5-225">Ensure that all cookies set over HTTPS use the **secure** attribute.</span></span> <span data-ttu-id="99fc5-226">Esse requisito pode ser imposto no arquivo web.config pela configuração do atributo requireSSL como true.</span><span class="sxs-lookup"><span data-stu-id="99fc5-226">The requirement can be enforced in the web.config file by setting the requireSSL attribute to true.</span></span> <span data-ttu-id="99fc5-227">Essa é a abordagem preferencial, pois vai impor o atributo **secure** a todos os cookies atuais e futuros, sem a necessidade de fazer qualquer alteração adicional no código.</span><span class="sxs-lookup"><span data-stu-id="99fc5-227">It is the preferred approach because it will enforce the **secure** attribute for all current and future cookies without the need to make any additional code changes.</span></span>|

### <a name="example"></a><span data-ttu-id="99fc5-228">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99fc5-228">Example</span></span>
```C#
<configuration>
  <system.web>
    <httpCookies requireSSL="true"/>
  </system.web>
</configuration>
```
<span data-ttu-id="99fc5-229">A configuração é aplicada mesmo que HTTP seja usado para acessar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="99fc5-229">The setting is enforced even if HTTP is used to access the application.</span></span> <span data-ttu-id="99fc5-230">Se HTTP é usado para acessar o aplicativo, a configuração interrompe o aplicativo, pois os cookies estão definidos com o atributo secure e o navegador não os enviará de volta ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="99fc5-230">If HTTP is used to access the application, the setting breaks the application because the cookies are set with the secure attribute and the browser will not send them back to the application.</span></span>

| <span data-ttu-id="99fc5-231">Title</span><span class="sxs-lookup"><span data-stu-id="99fc5-231">Title</span></span>                   | <span data-ttu-id="99fc5-232">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99fc5-232">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99fc5-233">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99fc5-233">**Component**</span></span>               | <span data-ttu-id="99fc5-234">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="99fc5-234">Web Application</span></span> | 
| <span data-ttu-id="99fc5-235">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99fc5-235">**SDL Phase**</span></span>               | <span data-ttu-id="99fc5-236">Compilação</span><span class="sxs-lookup"><span data-stu-id="99fc5-236">Build</span></span> |  
| <span data-ttu-id="99fc5-237">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99fc5-237">**Applicable Technologies**</span></span> | <span data-ttu-id="99fc5-238">Web Forms, MVC5</span><span class="sxs-lookup"><span data-stu-id="99fc5-238">Web Forms, MVC5</span></span> |
| <span data-ttu-id="99fc5-239">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99fc5-239">**Attributes**</span></span>              | <span data-ttu-id="99fc5-240">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="99fc5-240">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="99fc5-241">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99fc5-241">**References**</span></span>              | <span data-ttu-id="99fc5-242">N/D</span><span class="sxs-lookup"><span data-stu-id="99fc5-242">N/A</span></span>  |
| <span data-ttu-id="99fc5-243">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99fc5-243">**Steps**</span></span> | <span data-ttu-id="99fc5-244">Quando o aplicativo Web for a terceira parte confiável, e o IdP for o servidor ADFS, o atributo secure do token FedAuth poderá ser configurado definindo requireSSL como True na seção `system.identityModel.services` de web.config:</span><span class="sxs-lookup"><span data-stu-id="99fc5-244">When the web application is the Relying Party, and the IdP is ADFS server, the FedAuth token's secure attribute can be configured by setting requireSSL to True in `system.identityModel.services` section of web.config:</span></span>|

### <a name="example"></a><span data-ttu-id="99fc5-245">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99fc5-245">Example</span></span>
```C#
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:20:0" />
    ....  
    </federationConfiguration>
  </system.identityModel.services>
```

## <span data-ttu-id="99fc5-246"><a id="cookie-definition"></a>Todo aplicativo baseado em http deve especificar http somente para definição de cookie</span><span class="sxs-lookup"><span data-stu-id="99fc5-246"><a id="cookie-definition"></a>All http based application should specify http only for cookie definition</span></span>

| <span data-ttu-id="99fc5-247">Title</span><span class="sxs-lookup"><span data-stu-id="99fc5-247">Title</span></span>                   | <span data-ttu-id="99fc5-248">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99fc5-248">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99fc5-249">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99fc5-249">**Component**</span></span>               | <span data-ttu-id="99fc5-250">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="99fc5-250">Web Application</span></span> | 
| <span data-ttu-id="99fc5-251">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99fc5-251">**SDL Phase**</span></span>               | <span data-ttu-id="99fc5-252">Compilação</span><span class="sxs-lookup"><span data-stu-id="99fc5-252">Build</span></span> |  
| <span data-ttu-id="99fc5-253">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99fc5-253">**Applicable Technologies**</span></span> | <span data-ttu-id="99fc5-254">Genérico</span><span class="sxs-lookup"><span data-stu-id="99fc5-254">Generic</span></span> |
| <span data-ttu-id="99fc5-255">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99fc5-255">**Attributes**</span></span>              | <span data-ttu-id="99fc5-256">N/D</span><span class="sxs-lookup"><span data-stu-id="99fc5-256">N/A</span></span>  |
| <span data-ttu-id="99fc5-257">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99fc5-257">**References**</span></span>              | [<span data-ttu-id="99fc5-258">Atributo Secure Cookie</span><span class="sxs-lookup"><span data-stu-id="99fc5-258">Secure Cookie Attribute</span></span>](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie) |
| <span data-ttu-id="99fc5-259">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99fc5-259">**Steps**</span></span> | <span data-ttu-id="99fc5-260">Para atenuar o risco de divulgação de informações com um ataque XSS (script entre sites), um novo atributo - httpOnly - foi introduzido aos cookies e é suportado por todos os principais navegadores.</span><span class="sxs-lookup"><span data-stu-id="99fc5-260">To mitigate the risk of information disclosure with a cross-site scripting (XSS) attack, a new attribute - httpOnly - was introduced to cookies and is supported by all major browsers.</span></span> <span data-ttu-id="99fc5-261">O atributo especifica que um cookie não pode ser acessado por script.</span><span class="sxs-lookup"><span data-stu-id="99fc5-261">The attribute specifies that a cookie is not accessible through script.</span></span> <span data-ttu-id="99fc5-262">Usando cookies HttpOnly, um aplicativo Web reduz a possibilidade de roubo de informações confidenciais contidas no cookie por meio de script e o envio dessas informações ao site de um invasor.</span><span class="sxs-lookup"><span data-stu-id="99fc5-262">By using HttpOnly cookies, a web application reduces the possibility that sensitive information contained in the cookie can be stolen via script and sent to an attacker's website.</span></span> |

### <a name="example"></a><span data-ttu-id="99fc5-263">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99fc5-263">Example</span></span>
<span data-ttu-id="99fc5-264">Todos os aplicativos baseados em HTTP que usam cookies devem especificar HttpOnly na definição de cookie implementando a seguinte configuração em web.config:</span><span class="sxs-lookup"><span data-stu-id="99fc5-264">All HTTP-based applications that use cookies should specify HttpOnly in the cookie definition, by implementing following configuration in web.config:</span></span>
```XML
<system.web>
.
.
   <httpCookies requireSSL="false" httpOnlyCookies="true"/>
.
.
</system.web>
```

| <span data-ttu-id="99fc5-265">Title</span><span class="sxs-lookup"><span data-stu-id="99fc5-265">Title</span></span>                   | <span data-ttu-id="99fc5-266">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99fc5-266">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99fc5-267">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99fc5-267">**Component**</span></span>               | <span data-ttu-id="99fc5-268">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="99fc5-268">Web Application</span></span> | 
| <span data-ttu-id="99fc5-269">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99fc5-269">**SDL Phase**</span></span>               | <span data-ttu-id="99fc5-270">Compilação</span><span class="sxs-lookup"><span data-stu-id="99fc5-270">Build</span></span> |  
| <span data-ttu-id="99fc5-271">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99fc5-271">**Applicable Technologies**</span></span> | <span data-ttu-id="99fc5-272">Formulários da Web</span><span class="sxs-lookup"><span data-stu-id="99fc5-272">Web Forms</span></span> |
| <span data-ttu-id="99fc5-273">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99fc5-273">**Attributes**</span></span>              | <span data-ttu-id="99fc5-274">N/D</span><span class="sxs-lookup"><span data-stu-id="99fc5-274">N/A</span></span>  |
| <span data-ttu-id="99fc5-275">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99fc5-275">**References**</span></span>              | [<span data-ttu-id="99fc5-276">Propriedade FormsAuthentication.RequireSSL</span><span class="sxs-lookup"><span data-stu-id="99fc5-276">FormsAuthentication.RequireSSL Property</span></span>](https://msdn.microsoft.com/library/system.web.security.formsauthentication.requiressl.aspx) |
| <span data-ttu-id="99fc5-277">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99fc5-277">**Steps**</span></span> | <span data-ttu-id="99fc5-278">O valor da propriedade RequireSSL é definido no arquivo de configuração para um aplicativo ASP.NET usando o atributo requireSSL do elemento de configuração.</span><span class="sxs-lookup"><span data-stu-id="99fc5-278">The RequireSSL property value is set in the configuration file for an ASP.NET application by using the requireSSL attribute of the configuration element.</span></span> <span data-ttu-id="99fc5-279">Especifique no arquivo web.config para seu aplicativo ASP.NET se o protocolo SSL (Secure Sockets Layer) é necessário para retornar o cookie de autenticação de formulários para o servidor configurando o atributo requireSSL.</span><span class="sxs-lookup"><span data-stu-id="99fc5-279">You can specify in the Web.config file for your ASP.NET application whether SSL (Secure Sockets Layer) is required to return the forms-authentication cookie to the server by setting the requireSSL attribute.</span></span>|

### <a name="example"></a><span data-ttu-id="99fc5-280">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99fc5-280">Example</span></span> 
<span data-ttu-id="99fc5-281">O exemplo de código a seguir define o atributo requireSSL no arquivo Web.config.</span><span class="sxs-lookup"><span data-stu-id="99fc5-281">The following code example sets the requireSSL attribute in the Web.config file.</span></span>
```XML
<authentication mode="Forms">
  <forms loginUrl="member_login.aspx" cookieless="UseCookies" requireSSL="true"/>
</authentication>
```

| <span data-ttu-id="99fc5-282">Title</span><span class="sxs-lookup"><span data-stu-id="99fc5-282">Title</span></span>                   | <span data-ttu-id="99fc5-283">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99fc5-283">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99fc5-284">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99fc5-284">**Component**</span></span>               | <span data-ttu-id="99fc5-285">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="99fc5-285">Web Application</span></span> | 
| <span data-ttu-id="99fc5-286">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99fc5-286">**SDL Phase**</span></span>               | <span data-ttu-id="99fc5-287">Compilação</span><span class="sxs-lookup"><span data-stu-id="99fc5-287">Build</span></span> |  
| <span data-ttu-id="99fc5-288">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99fc5-288">**Applicable Technologies**</span></span> | <span data-ttu-id="99fc5-289">MVC5</span><span class="sxs-lookup"><span data-stu-id="99fc5-289">MVC5</span></span> |
| <span data-ttu-id="99fc5-290">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99fc5-290">**Attributes**</span></span>              | <span data-ttu-id="99fc5-291">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="99fc5-291">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="99fc5-292">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99fc5-292">**References**</span></span>              | [<span data-ttu-id="99fc5-293">Configuração do Windows Identity Foundation (WIF) – Part II</span><span class="sxs-lookup"><span data-stu-id="99fc5-293">Windows Identity Foundation (WIF) Configuration – Part II</span></span>](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/) |
| <span data-ttu-id="99fc5-294">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99fc5-294">**Steps**</span></span> | <span data-ttu-id="99fc5-295">Para definir o atributo httpOnly para cookies FedAuth, o valor do atributo hideFromCsript deve ser definido como True.</span><span class="sxs-lookup"><span data-stu-id="99fc5-295">To set httpOnly attribute for FedAuth cookies, hideFromCsript attribute value should be set to True.</span></span> |

### <a name="example"></a><span data-ttu-id="99fc5-296">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99fc5-296">Example</span></span>
<span data-ttu-id="99fc5-297">A configuração a seguir mostra a configuração correta:</span><span class="sxs-lookup"><span data-stu-id="99fc5-297">Following configuration shows the correct configuration:</span></span>
```XML
<federatedAuthentication>
<cookieHandler mode="Custom"
                       hideFromScript="true"
                       name="FedAuth"
                       path="/"
                       requireSsl="true"
                       persistentSessionLifetime="25">
</cookieHandler>
</federatedAuthentication>
```

## <span data-ttu-id="99fc5-298"><a id="csrf-asp"></a>Atenuar ataques CSRF (solicitação intersite forjada) em páginas Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="99fc5-298"><a id="csrf-asp"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>

| <span data-ttu-id="99fc5-299">Title</span><span class="sxs-lookup"><span data-stu-id="99fc5-299">Title</span></span>                   | <span data-ttu-id="99fc5-300">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99fc5-300">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99fc5-301">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99fc5-301">**Component**</span></span>               | <span data-ttu-id="99fc5-302">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="99fc5-302">Web Application</span></span> | 
| <span data-ttu-id="99fc5-303">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99fc5-303">**SDL Phase**</span></span>               | <span data-ttu-id="99fc5-304">Compilação</span><span class="sxs-lookup"><span data-stu-id="99fc5-304">Build</span></span> |  
| <span data-ttu-id="99fc5-305">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99fc5-305">**Applicable Technologies**</span></span> | <span data-ttu-id="99fc5-306">Genérico</span><span class="sxs-lookup"><span data-stu-id="99fc5-306">Generic</span></span> |
| <span data-ttu-id="99fc5-307">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99fc5-307">**Attributes**</span></span>              | <span data-ttu-id="99fc5-308">N/D</span><span class="sxs-lookup"><span data-stu-id="99fc5-308">N/A</span></span>  |
| <span data-ttu-id="99fc5-309">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99fc5-309">**References**</span></span>              | <span data-ttu-id="99fc5-310">N/D</span><span class="sxs-lookup"><span data-stu-id="99fc5-310">N/A</span></span>  |
| <span data-ttu-id="99fc5-311">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99fc5-311">**Steps**</span></span> | <span data-ttu-id="99fc5-312">A CSRF ou XSRF (solicitação intersite forjada) é um tipo de ataque em que um invasor pode realizar ações no contexto de segurança da sessão estabelecida de um usuário diferente em um site da Web.</span><span class="sxs-lookup"><span data-stu-id="99fc5-312">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in the security context of a different user's established session on a web site.</span></span> <span data-ttu-id="99fc5-313">A meta é modificar ou excluir o conteúdo, caso o site de destino dependa exclusivamente de cookies de sessão para autenticar a solicitação recebida.</span><span class="sxs-lookup"><span data-stu-id="99fc5-313">The goal is to modify or delete content, if the targeted web site relies exclusively on session cookies to authenticate received request.</span></span> <span data-ttu-id="99fc5-314">Um invasor pode explorar essa vulnerabilidade fazendo com que um navegador diferente de um usuário carregue uma URL com um comando de um site vulnerável no qual o usuário já esteja conectado.</span><span class="sxs-lookup"><span data-stu-id="99fc5-314">An attacker could exploit this vulnerability by getting a different user's browser to load a URL with a command from a vulnerable site on which the user is already logged in.</span></span> <span data-ttu-id="99fc5-315">Há muitas maneiras de um invasor fazer isso, como hospedando um site diferente que carrega um recurso do servidor vulnerável ou fazendo o usuário clicar em um link.</span><span class="sxs-lookup"><span data-stu-id="99fc5-315">There are many ways for an attacker to do that, such as by hosting a different web site that loads a resource from the vulnerable server, or getting the user to click a link.</span></span> <span data-ttu-id="99fc5-316">Esse ataque pode ser evitado se o servidor enviar um token adicional ao cliente, exigir que o cliente inclua esse token em todas as solicitações futuras e verificar se todas as solicitações futuras incluem um token que pertence à sessão atual, por exemplo, usando o ASP.NET AntiForgeryToken ou ViewState.</span><span class="sxs-lookup"><span data-stu-id="99fc5-316">The attack can be prevented if the server sends an additional token to the client, requires the client to include that token in all future requests, and verifies that all future requests include a token that pertains to the current session, such as by using the ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="99fc5-317">Title</span><span class="sxs-lookup"><span data-stu-id="99fc5-317">Title</span></span>                   | <span data-ttu-id="99fc5-318">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99fc5-318">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99fc5-319">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99fc5-319">**Component**</span></span>               | <span data-ttu-id="99fc5-320">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="99fc5-320">Web Application</span></span> | 
| <span data-ttu-id="99fc5-321">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99fc5-321">**SDL Phase**</span></span>               | <span data-ttu-id="99fc5-322">Compilação</span><span class="sxs-lookup"><span data-stu-id="99fc5-322">Build</span></span> |  
| <span data-ttu-id="99fc5-323">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99fc5-323">**Applicable Technologies**</span></span> | <span data-ttu-id="99fc5-324">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="99fc5-324">MVC5, MVC6</span></span> |
| <span data-ttu-id="99fc5-325">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99fc5-325">**Attributes**</span></span>              | <span data-ttu-id="99fc5-326">N/D</span><span class="sxs-lookup"><span data-stu-id="99fc5-326">N/A</span></span>  |
| <span data-ttu-id="99fc5-327">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99fc5-327">**References**</span></span>              | [<span data-ttu-id="99fc5-328">Prevenção de XSRF/CSRF no ASP.NET MVC e páginas Web</span><span class="sxs-lookup"><span data-stu-id="99fc5-328">XSRF/CSRF Prevention in ASP.NET MVC and Web Pages</span></span>](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) |
| <span data-ttu-id="99fc5-329">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99fc5-329">**Steps**</span></span> | <span data-ttu-id="99fc5-330">Formulários MVC Anti-CSRF e do ASP.NET – Use o método auxiliar `AntiForgeryToken` em Exibições; coloque um `Html.AntiForgeryToken()` no formulário, por exemplo,</span><span class="sxs-lookup"><span data-stu-id="99fc5-330">Anti-CSRF and ASP.NET MVC forms - Use the `AntiForgeryToken` helper method on Views; put an `Html.AntiForgeryToken()` into the form, for example,</span></span>|

### <a name="example"></a><span data-ttu-id="99fc5-331">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99fc5-331">Example</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
```

### <a name="example"></a><span data-ttu-id="99fc5-332">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99fc5-332">Example</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="99fc5-333">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99fc5-333">Example</span></span>
<span data-ttu-id="99fc5-334">Ao mesmo tempo, Html.AntiForgeryToken() fornece ao visitante um cookie chamado __RequestVerificationToken, com o mesmo valor que o valor oculto aleatório mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="99fc5-334">At the same time, Html.AntiForgeryToken() gives the visitor a cookie called __RequestVerificationToken, with the same value as the random hidden value shown above.</span></span> <span data-ttu-id="99fc5-335">Em seguida, para validar uma postagem de formulário de entrada, adicione o filtro [ValidateAntiForgeryToken] ao método de ação de destino.</span><span class="sxs-lookup"><span data-stu-id="99fc5-335">Next, to validate an incoming form post, add the [ValidateAntiForgeryToken] filter to the target action method.</span></span> <span data-ttu-id="99fc5-336">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="99fc5-336">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="99fc5-337">Filtro de autorização que verifica se:</span><span class="sxs-lookup"><span data-stu-id="99fc5-337">Authorization filter that checks that:</span></span>
* <span data-ttu-id="99fc5-338">A solicitação de entrada tem um cookie chamado __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="99fc5-338">The incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="99fc5-339">A solicitação de entrada tem um `Request.Form` chamado __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="99fc5-339">The incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="99fc5-340">O cookie e o valor `Request.Form` são correspondentes. Supondo que tudo esteja certo, a solicitação passará normalmente.</span><span class="sxs-lookup"><span data-stu-id="99fc5-340">These cookie and `Request.Form` values match Assuming all is well, the request goes through as normal.</span></span> <span data-ttu-id="99fc5-341">Mas, se não estiver, uma falha de autorização com a mensagem "Um token antifalsificação necessário não foi fornecido ou era inválido".</span><span class="sxs-lookup"><span data-stu-id="99fc5-341">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span> 

### <a name="example"></a><span data-ttu-id="99fc5-342">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99fc5-342">Example</span></span>
<span data-ttu-id="99fc5-343">Anti-CSRF e AJAX: O token do formulário pode ser um problema para solicitações AJAX, pois uma solicitação AJAX pode enviar dados JSON, não dados de formulário HTML.</span><span class="sxs-lookup"><span data-stu-id="99fc5-343">Anti-CSRF and AJAX: The form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="99fc5-344">Uma solução é enviar os tokens em um cabeçalho HTTP personalizado.</span><span class="sxs-lookup"><span data-stu-id="99fc5-344">One solution is to send the tokens in a custom HTTP header.</span></span> <span data-ttu-id="99fc5-345">O código a seguir usa a sintaxe Razor para gerar os tokens e adiciona os tokens a uma solicitação AJAX.</span><span class="sxs-lookup"><span data-stu-id="99fc5-345">The following code uses Razor syntax to generate the tokens, and then adds the tokens to an AJAX request.</span></span> 
```C#
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }

    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a><span data-ttu-id="99fc5-346">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99fc5-346">Example</span></span>
<span data-ttu-id="99fc5-347">Ao processar a solicitação, extraia os tokens do cabeçalho da solicitação.</span><span class="sxs-lookup"><span data-stu-id="99fc5-347">When you process the request, extract the tokens from the request header.</span></span> <span data-ttu-id="99fc5-348">Em seguida, chame o método AntiForgery.Validate para validar os tokens.</span><span class="sxs-lookup"><span data-stu-id="99fc5-348">Then call the AntiForgery.Validate method to validate the tokens.</span></span> <span data-ttu-id="99fc5-349">O método Validate lança uma exceção se os tokens não forem válidos.</span><span class="sxs-lookup"><span data-stu-id="99fc5-349">The Validate method throws an exception if the tokens are not valid.</span></span>
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

| <span data-ttu-id="99fc5-350">Title</span><span class="sxs-lookup"><span data-stu-id="99fc5-350">Title</span></span>                   | <span data-ttu-id="99fc5-351">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99fc5-351">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99fc5-352">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99fc5-352">**Component**</span></span>               | <span data-ttu-id="99fc5-353">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="99fc5-353">Web Application</span></span> | 
| <span data-ttu-id="99fc5-354">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99fc5-354">**SDL Phase**</span></span>               | <span data-ttu-id="99fc5-355">Compilação</span><span class="sxs-lookup"><span data-stu-id="99fc5-355">Build</span></span> |  
| <span data-ttu-id="99fc5-356">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99fc5-356">**Applicable Technologies**</span></span> | <span data-ttu-id="99fc5-357">Formulários da Web</span><span class="sxs-lookup"><span data-stu-id="99fc5-357">Web Forms</span></span> |
| <span data-ttu-id="99fc5-358">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99fc5-358">**Attributes**</span></span>              | <span data-ttu-id="99fc5-359">N/D</span><span class="sxs-lookup"><span data-stu-id="99fc5-359">N/A</span></span>  |
| <span data-ttu-id="99fc5-360">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99fc5-360">**References**</span></span>              | [<span data-ttu-id="99fc5-361">Tirar proveito dos recursos internos do ASP.NET para afastar os ataques na Web</span><span class="sxs-lookup"><span data-stu-id="99fc5-361">Take Advantage of ASP.NET Built-in Features to Fend Off Web Attacks</span></span>](https://msdn.microsoft.com/library/ms972969.aspx#securitybarriers_topic2) |
| <span data-ttu-id="99fc5-362">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99fc5-362">**Steps**</span></span> | <span data-ttu-id="99fc5-363">Os ataques CSRF em aplicativos baseados em WebForm podem ser minimizados definindo ViewStateUserKey para uma cadeia de caracteres aleatória que varia para cada usuário - ID de usuário ou, melhor ainda, ID de sessão.</span><span class="sxs-lookup"><span data-stu-id="99fc5-363">CSRF attacks in WebForm based applications can be mitigated by setting ViewStateUserKey to a random string that varies for each user - user ID or, better yet, session ID.</span></span> <span data-ttu-id="99fc5-364">Por diversos motivos técnicos e sociais, ID de sessão é uma opção bem melhor, pois é imprevisível, atinge um tempo limite e varia de acordo com o usuário.</span><span class="sxs-lookup"><span data-stu-id="99fc5-364">For a number of technical and social reasons, session ID is a much better fit because a session ID is unpredictable, times out, and varies on a per-user basis.</span></span>|

### <a name="example"></a><span data-ttu-id="99fc5-365">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99fc5-365">Example</span></span>
<span data-ttu-id="99fc5-366">Aqui está o código necessário em todas as suas páginas:</span><span class="sxs-lookup"><span data-stu-id="99fc5-366">Here's the code you need to have in all of your pages:</span></span>
```C#
void Page_Init (object sender, EventArgs e) {
   ViewStateUserKey = Session.SessionID;
   :
}
```

## <span data-ttu-id="99fc5-367"><a id="inactivity-lifetime"></a>Configurar sessão para tempo de vida de inatividade</span><span class="sxs-lookup"><span data-stu-id="99fc5-367"><a id="inactivity-lifetime"></a>Set up session for inactivity lifetime</span></span>

| <span data-ttu-id="99fc5-368">Title</span><span class="sxs-lookup"><span data-stu-id="99fc5-368">Title</span></span>                   | <span data-ttu-id="99fc5-369">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99fc5-369">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99fc5-370">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99fc5-370">**Component**</span></span>               | <span data-ttu-id="99fc5-371">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="99fc5-371">Web Application</span></span> | 
| <span data-ttu-id="99fc5-372">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99fc5-372">**SDL Phase**</span></span>               | <span data-ttu-id="99fc5-373">Compilação</span><span class="sxs-lookup"><span data-stu-id="99fc5-373">Build</span></span> |  
| <span data-ttu-id="99fc5-374">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99fc5-374">**Applicable Technologies**</span></span> | <span data-ttu-id="99fc5-375">Genérico</span><span class="sxs-lookup"><span data-stu-id="99fc5-375">Generic</span></span> |
| <span data-ttu-id="99fc5-376">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99fc5-376">**Attributes**</span></span>              | <span data-ttu-id="99fc5-377">N/D</span><span class="sxs-lookup"><span data-stu-id="99fc5-377">N/A</span></span>  |
| <span data-ttu-id="99fc5-378">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99fc5-378">**References**</span></span>              | <span data-ttu-id="99fc5-379">[Propriedade HttpSessionState.Timeout](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="99fc5-379">[HttpSessionState.Timeout Property](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span></span> |
| <span data-ttu-id="99fc5-380">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99fc5-380">**Steps**</span></span> | <span data-ttu-id="99fc5-381">O tempo limite de sessão representa o evento que ocorre quando um usuário não realiza qualquer ação em um site durante um intervalo (definido pelo servidor Web).</span><span class="sxs-lookup"><span data-stu-id="99fc5-381">Session timeout represents the event occurring when a user does not perform any action on a web site during a interval (defined by web server).</span></span> <span data-ttu-id="99fc5-382">O evento, no lado do servidor, altera o status da sessão do usuário para "inválida" (por exemplo, "não mais utilizada") e instrui o servidor Web a destruí-la (excluindo todos os dados contidos nela).</span><span class="sxs-lookup"><span data-stu-id="99fc5-382">The event, on server side, change the status of the user session to 'invalid' (for example  "not used anymore") and instruct the web server to destroy it (deleting all data contained into it).</span></span> <span data-ttu-id="99fc5-383">O exemplo de código a seguir define o atributo de tempo limite de sessão como 15 minutos no arquivo Web.config.</span><span class="sxs-lookup"><span data-stu-id="99fc5-383">The following code example sets the timeout session attribute to 15 minutes in the Web.config file.</span></span>|

### <a name="example"></a><span data-ttu-id="99fc5-384">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99fc5-384">Example</span></span>
<span data-ttu-id="99fc5-385">``\`código XML <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration></span><span class="sxs-lookup"><span data-stu-id="99fc5-385">``\`XML code <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration></span></span>
```

## <a id="threat-detection"></a>Enable Threat detection on Azure SQL
```

| <span data-ttu-id="99fc5-386">Title</span><span class="sxs-lookup"><span data-stu-id="99fc5-386">Title</span></span>                   | <span data-ttu-id="99fc5-387">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99fc5-387">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99fc5-388">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99fc5-388">**Component**</span></span>               | <span data-ttu-id="99fc5-389">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="99fc5-389">Web Application</span></span> | 
| <span data-ttu-id="99fc5-390">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99fc5-390">**SDL Phase**</span></span>               | <span data-ttu-id="99fc5-391">Compilação</span><span class="sxs-lookup"><span data-stu-id="99fc5-391">Build</span></span> |  
| <span data-ttu-id="99fc5-392">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99fc5-392">**Applicable Technologies**</span></span> | <span data-ttu-id="99fc5-393">Formulários da Web</span><span class="sxs-lookup"><span data-stu-id="99fc5-393">Web Forms</span></span> |
| <span data-ttu-id="99fc5-394">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99fc5-394">**Attributes**</span></span>              | <span data-ttu-id="99fc5-395">N/D</span><span class="sxs-lookup"><span data-stu-id="99fc5-395">N/A</span></span>  |
| <span data-ttu-id="99fc5-396">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99fc5-396">**References**</span></span>              | <span data-ttu-id="99fc5-397">[Elemento forms para autenticação (Esquema de configuração ASP.NET)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="99fc5-397">[forms Element for authentication (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span></span> |
| <span data-ttu-id="99fc5-398">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99fc5-398">**Steps**</span></span> | <span data-ttu-id="99fc5-399">Defina o tempo limite de cookie do tíquete de autenticação de formulários como 15 minutos</span><span class="sxs-lookup"><span data-stu-id="99fc5-399">Set the Forms Authentication Ticket cookie timeout to 15 minutes</span></span>|

### <a name="example"></a><span data-ttu-id="99fc5-400">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99fc5-400">Example</span></span>
<span data-ttu-id="99fc5-401">``\`código XML <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span><span class="sxs-lookup"><span data-stu-id="99fc5-401">``\`XML code <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span></span>
```

| Title                   | Details      |
| ----------------------- | ------------ |
| **Component**               | Web Application | 
| **SDL Phase**               | Build |  
| **Applicable Technologies** | Web Forms, MVC5 |
| **Attributes**              | EnvironmentType - OnPrem |
| **References**              | [asdeqa](https://skf.azurewebsites.net/Mitigations/Details/wefr) |
| **Steps** | When the web application is Relying Party and ADFS is the STS, the lifetime of the authentication cookies - FedAuth tokens - can be set by the following configuration in web.config:|

### Example
```XML
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:15:0" />
      <!-- Set requireHttps=true; -->
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:39529/" realm="https://localhost:44302/" reply="https://localhost:44302/" requireHttps="true"/>
      <!--
      Use the code below to enable encryption-decryption of claims received from ADFS. Thumbprint value varies based on the certificate being used.
      <serviceCertificate>
        <certificateReference findValue="4FBBBA33A1D11A9022A5BF3492FF83320007686A" storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" />
      </serviceCertificate>
      -->
    </federationConfiguration>
  </system.identityModel.services>
```

### <a name="example"></a><span data-ttu-id="99fc5-402">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99fc5-402">Example</span></span>
<span data-ttu-id="99fc5-403">Além disso, o tempo de vida do token da declaração SAML emitida pelo ADFS deve ser definido como 15 minutos, executando o seguinte comando powershell no servidor ADFS:</span><span class="sxs-lookup"><span data-stu-id="99fc5-403">Also the ADFS issued SAML claim token's lifetime should be set to 15 minutes, by executing the following powershell command on the ADFS server:</span></span>
```C#
Set-ADFSRelyingPartyTrust -TargetName “<RelyingPartyWebApp>” -ClaimsProviderName @(“Active Directory”) -TokenLifetime 15 -AlwaysRequireAuthentication $true
```

## <span data-ttu-id="99fc5-404"><a id="proper-app-logout"></a>Implementar o logoff apropriado do aplicativo</span><span class="sxs-lookup"><span data-stu-id="99fc5-404"><a id="proper-app-logout"></a>Implement proper logout from the application</span></span>

| <span data-ttu-id="99fc5-405">Title</span><span class="sxs-lookup"><span data-stu-id="99fc5-405">Title</span></span>                   | <span data-ttu-id="99fc5-406">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99fc5-406">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99fc5-407">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99fc5-407">**Component**</span></span>               | <span data-ttu-id="99fc5-408">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="99fc5-408">Web Application</span></span> | 
| <span data-ttu-id="99fc5-409">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99fc5-409">**SDL Phase**</span></span>               | <span data-ttu-id="99fc5-410">Compilação</span><span class="sxs-lookup"><span data-stu-id="99fc5-410">Build</span></span> |  
| <span data-ttu-id="99fc5-411">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99fc5-411">**Applicable Technologies**</span></span> | <span data-ttu-id="99fc5-412">Genérico</span><span class="sxs-lookup"><span data-stu-id="99fc5-412">Generic</span></span> |
| <span data-ttu-id="99fc5-413">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99fc5-413">**Attributes**</span></span>              | <span data-ttu-id="99fc5-414">N/D</span><span class="sxs-lookup"><span data-stu-id="99fc5-414">N/A</span></span>  |
| <span data-ttu-id="99fc5-415">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99fc5-415">**References**</span></span>              | <span data-ttu-id="99fc5-416">N/D</span><span class="sxs-lookup"><span data-stu-id="99fc5-416">N/A</span></span>  |
| <span data-ttu-id="99fc5-417">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99fc5-417">**Steps**</span></span> | <span data-ttu-id="99fc5-418">Execute uma Saída adequada do aplicativo, quando o usuário pressionar o botão logoff.</span><span class="sxs-lookup"><span data-stu-id="99fc5-418">Perform proper Sign Out from the application, when user presses log out button.</span></span> <span data-ttu-id="99fc5-419">Após o logoff, o aplicativo deve destruir a sessão do usuário e também redefinir e anular o valor do cookie de sessão, juntamente com a redefinição e anulação do valor do cookie de autenticação.</span><span class="sxs-lookup"><span data-stu-id="99fc5-419">Upon logout, application should destroy user's session, and also reset and nullify session cookie value, along with resetting and nullifying authentication cookie value.</span></span> <span data-ttu-id="99fc5-420">Além disso, quando várias sessões estiverem vinculadas a uma única identidade de usuário, elas deverão ser coletivamente encerradas no lado do servidor no momento do tempo limite ou no logoff.</span><span class="sxs-lookup"><span data-stu-id="99fc5-420">Also, when multiple sessions are tied to a single user identity, they must be collectively terminated on the server side at timeout or logout.</span></span> <span data-ttu-id="99fc5-421">Por fim, certifique-se de que a funcionalidade de Logoff esteja disponível em cada página.</span><span class="sxs-lookup"><span data-stu-id="99fc5-421">Lastly, ensure that Logout functionality is available on every page.</span></span> |

## <span data-ttu-id="99fc5-422"><a id="csrf-api"></a>Atenuar ataques CSRF (solicitação intersite forjada) em APIs da Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="99fc5-422"><a id="csrf-api"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>

| <span data-ttu-id="99fc5-423">Title</span><span class="sxs-lookup"><span data-stu-id="99fc5-423">Title</span></span>                   | <span data-ttu-id="99fc5-424">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99fc5-424">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99fc5-425">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99fc5-425">**Component**</span></span>               | <span data-ttu-id="99fc5-426">API Web</span><span class="sxs-lookup"><span data-stu-id="99fc5-426">Web API</span></span> | 
| <span data-ttu-id="99fc5-427">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99fc5-427">**SDL Phase**</span></span>               | <span data-ttu-id="99fc5-428">Compilação</span><span class="sxs-lookup"><span data-stu-id="99fc5-428">Build</span></span> |  
| <span data-ttu-id="99fc5-429">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99fc5-429">**Applicable Technologies**</span></span> | <span data-ttu-id="99fc5-430">Genérico</span><span class="sxs-lookup"><span data-stu-id="99fc5-430">Generic</span></span> |
| <span data-ttu-id="99fc5-431">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99fc5-431">**Attributes**</span></span>              | <span data-ttu-id="99fc5-432">N/D</span><span class="sxs-lookup"><span data-stu-id="99fc5-432">N/A</span></span>  |
| <span data-ttu-id="99fc5-433">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99fc5-433">**References**</span></span>              | <span data-ttu-id="99fc5-434">N/D</span><span class="sxs-lookup"><span data-stu-id="99fc5-434">N/A</span></span>  |
| <span data-ttu-id="99fc5-435">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99fc5-435">**Steps**</span></span> | <span data-ttu-id="99fc5-436">A CSRF ou XSRF (solicitação intersite forjada) é um tipo de ataque em que um invasor pode realizar ações no contexto de segurança da sessão estabelecida de um usuário diferente em um site da Web.</span><span class="sxs-lookup"><span data-stu-id="99fc5-436">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in the security context of a different user's established session on a web site.</span></span> <span data-ttu-id="99fc5-437">A meta é modificar ou excluir o conteúdo, caso o site de destino dependa exclusivamente de cookies de sessão para autenticar a solicitação recebida.</span><span class="sxs-lookup"><span data-stu-id="99fc5-437">The goal is to modify or delete content, if the targeted web site relies exclusively on session cookies to authenticate received request.</span></span> <span data-ttu-id="99fc5-438">Um invasor pode explorar essa vulnerabilidade fazendo com que um navegador diferente de um usuário carregue uma URL com um comando de um site vulnerável no qual o usuário já esteja conectado.</span><span class="sxs-lookup"><span data-stu-id="99fc5-438">An attacker could exploit this vulnerability by getting a different user's browser to load a URL with a command from a vulnerable site on which the user is already logged in.</span></span> <span data-ttu-id="99fc5-439">Há muitas maneiras de um invasor fazer isso, como hospedando um site diferente que carrega um recurso do servidor vulnerável ou fazendo o usuário clicar em um link.</span><span class="sxs-lookup"><span data-stu-id="99fc5-439">There are many ways for an attacker to do that, such as by hosting a different web site that loads a resource from the vulnerable server, or getting the user to click a link.</span></span> <span data-ttu-id="99fc5-440">Esse ataque pode ser evitado se o servidor enviar um token adicional ao cliente, exigir que o cliente inclua esse token em todas as solicitações futuras e verificar se todas as solicitações futuras incluem um token que pertence à sessão atual, por exemplo, usando o ASP.NET AntiForgeryToken ou ViewState.</span><span class="sxs-lookup"><span data-stu-id="99fc5-440">The attack can be prevented if the server sends an additional token to the client, requires the client to include that token in all future requests, and verifies that all future requests include a token that pertains to the current session, such as by using the ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="99fc5-441">Title</span><span class="sxs-lookup"><span data-stu-id="99fc5-441">Title</span></span>                   | <span data-ttu-id="99fc5-442">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99fc5-442">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99fc5-443">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99fc5-443">**Component**</span></span>               | <span data-ttu-id="99fc5-444">API Web</span><span class="sxs-lookup"><span data-stu-id="99fc5-444">Web API</span></span> | 
| <span data-ttu-id="99fc5-445">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99fc5-445">**SDL Phase**</span></span>               | <span data-ttu-id="99fc5-446">Compilação</span><span class="sxs-lookup"><span data-stu-id="99fc5-446">Build</span></span> |  
| <span data-ttu-id="99fc5-447">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99fc5-447">**Applicable Technologies**</span></span> | <span data-ttu-id="99fc5-448">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="99fc5-448">MVC5, MVC6</span></span> |
| <span data-ttu-id="99fc5-449">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99fc5-449">**Attributes**</span></span>              | <span data-ttu-id="99fc5-450">N/D</span><span class="sxs-lookup"><span data-stu-id="99fc5-450">N/A</span></span>  |
| <span data-ttu-id="99fc5-451">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99fc5-451">**References**</span></span>              | [<span data-ttu-id="99fc5-452">Impedir ataques CSRF (solicitação intersite forjada) em APIs da Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="99fc5-452">Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks) |
| <span data-ttu-id="99fc5-453">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99fc5-453">**Steps**</span></span> | <span data-ttu-id="99fc5-454">Anti-CSRF e AJAX: O token do formulário pode ser um problema para solicitações AJAX, pois uma solicitação AJAX pode enviar dados JSON, não dados de formulário HTML.</span><span class="sxs-lookup"><span data-stu-id="99fc5-454">Anti-CSRF and AJAX: The form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="99fc5-455">Uma solução é enviar os tokens em um cabeçalho HTTP personalizado.</span><span class="sxs-lookup"><span data-stu-id="99fc5-455">One solution is to send the tokens in a custom HTTP header.</span></span> <span data-ttu-id="99fc5-456">O código a seguir usa a sintaxe Razor para gerar os tokens e adiciona os tokens a uma solicitação AJAX.</span><span class="sxs-lookup"><span data-stu-id="99fc5-456">The following code uses Razor syntax to generate the tokens, and then adds the tokens to an AJAX request.</span></span> |

### <a name="example"></a><span data-ttu-id="99fc5-457">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99fc5-457">Example</span></span>
```Javascript
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }
    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a><span data-ttu-id="99fc5-458">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99fc5-458">Example</span></span>
<span data-ttu-id="99fc5-459">Ao processar a solicitação, extraia os tokens do cabeçalho da solicitação.</span><span class="sxs-lookup"><span data-stu-id="99fc5-459">When you process the request, extract the tokens from the request header.</span></span> <span data-ttu-id="99fc5-460">Em seguida, chame o método AntiForgery.Validate para validar os tokens.</span><span class="sxs-lookup"><span data-stu-id="99fc5-460">Then call the AntiForgery.Validate method to validate the tokens.</span></span> <span data-ttu-id="99fc5-461">O método Validate lança uma exceção se os tokens não forem válidos.</span><span class="sxs-lookup"><span data-stu-id="99fc5-461">The Validate method throws an exception if the tokens are not valid.</span></span>
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

### <a name="example"></a><span data-ttu-id="99fc5-462">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99fc5-462">Example</span></span>
<span data-ttu-id="99fc5-463">Formulários MVC Anti-CSRF e do ASP.NET – Use o método auxiliar AntiForgeryToken em Exibições; coloque um Html.AntiForgeryToken() no formulário, por exemplo,</span><span class="sxs-lookup"><span data-stu-id="99fc5-463">Anti-CSRF and ASP.NET MVC forms - Use the AntiForgeryToken helper method on Views; put an Html.AntiForgeryToken() into the form, for example,</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
}
```

### <a name="example"></a><span data-ttu-id="99fc5-464">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99fc5-464">Example</span></span>
<span data-ttu-id="99fc5-465">O exemplo acima produzirá algo como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="99fc5-465">The example above will output something like the following:</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="99fc5-466">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99fc5-466">Example</span></span>
<span data-ttu-id="99fc5-467">Ao mesmo tempo, Html.AntiForgeryToken() fornece ao visitante um cookie chamado __RequestVerificationToken, com o mesmo valor que o valor oculto aleatório mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="99fc5-467">At the same time, Html.AntiForgeryToken() gives the visitor a cookie called __RequestVerificationToken, with the same value as the random hidden value shown above.</span></span> <span data-ttu-id="99fc5-468">Em seguida, para validar uma postagem de formulário de entrada, adicione o filtro [ValidateAntiForgeryToken] ao método de ação de destino.</span><span class="sxs-lookup"><span data-stu-id="99fc5-468">Next, to validate an incoming form post, add the [ValidateAntiForgeryToken] filter to the target action method.</span></span> <span data-ttu-id="99fc5-469">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="99fc5-469">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="99fc5-470">Filtro de autorização que verifica se:</span><span class="sxs-lookup"><span data-stu-id="99fc5-470">Authorization filter that checks that:</span></span>
* <span data-ttu-id="99fc5-471">A solicitação de entrada tem um cookie chamado __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="99fc5-471">The incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="99fc5-472">A solicitação de entrada tem um `Request.Form` chamado __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="99fc5-472">The incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="99fc5-473">O cookie e o valor `Request.Form` são correspondentes. Supondo que tudo esteja certo, a solicitação passará normalmente.</span><span class="sxs-lookup"><span data-stu-id="99fc5-473">These cookie and `Request.Form` values match Assuming all is well, the request goes through as normal.</span></span> <span data-ttu-id="99fc5-474">Mas, se não estiver, uma falha de autorização com a mensagem "Um token antifalsificação necessário não foi fornecido ou era inválido".</span><span class="sxs-lookup"><span data-stu-id="99fc5-474">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span>

| <span data-ttu-id="99fc5-475">Title</span><span class="sxs-lookup"><span data-stu-id="99fc5-475">Title</span></span>                   | <span data-ttu-id="99fc5-476">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99fc5-476">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99fc5-477">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99fc5-477">**Component**</span></span>               | <span data-ttu-id="99fc5-478">API Web</span><span class="sxs-lookup"><span data-stu-id="99fc5-478">Web API</span></span> | 
| <span data-ttu-id="99fc5-479">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99fc5-479">**SDL Phase**</span></span>               | <span data-ttu-id="99fc5-480">Compilação</span><span class="sxs-lookup"><span data-stu-id="99fc5-480">Build</span></span> |  
| <span data-ttu-id="99fc5-481">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99fc5-481">**Applicable Technologies**</span></span> | <span data-ttu-id="99fc5-482">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="99fc5-482">MVC5, MVC6</span></span> |
| <span data-ttu-id="99fc5-483">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99fc5-483">**Attributes**</span></span>              | <span data-ttu-id="99fc5-484">Provedor de Identidade - ADFS, Provedor de Identidade - Azure AD</span><span class="sxs-lookup"><span data-stu-id="99fc5-484">Identity Provider - ADFS, Identity Provider - Azure AD</span></span> |
| <span data-ttu-id="99fc5-485">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99fc5-485">**References**</span></span>              | [<span data-ttu-id="99fc5-486">Proteger uma API Web com contas individuais e logon local na API Web ASP.NET 2.2</span><span class="sxs-lookup"><span data-stu-id="99fc5-486">Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2</span></span>](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api) |
| <span data-ttu-id="99fc5-487">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99fc5-487">**Steps**</span></span> | <span data-ttu-id="99fc5-488">Se a API Web for protegida usando OAuth 2.0, ela esperará um token de portador no cabeçalho de solicitação de Autorização e a concederá o acesso à solicitação somente se o token for válido.</span><span class="sxs-lookup"><span data-stu-id="99fc5-488">If the Web API is secured using OAuth 2.0, then it expects a bearer token in Authorization request header and grants access to the request only if the token is valid.</span></span> <span data-ttu-id="99fc5-489">Diferentemente da autenticação baseada em cookie, os navegadores não anexam os tokens de portador às solicitações.</span><span class="sxs-lookup"><span data-stu-id="99fc5-489">Unlike cookie based authentication, browsers do not attach the bearer tokens to requests.</span></span> <span data-ttu-id="99fc5-490">O cliente solicitante deve anexar explicitamente o token de portador no cabeçalho da solicitação.</span><span class="sxs-lookup"><span data-stu-id="99fc5-490">The requesting client needs to explicitly attach the bearer token in the request header.</span></span> <span data-ttu-id="99fc5-491">Portanto, para APIs Web ASP.NET protegidas usando o OAuth 2.0, os tokens de portador são considerados uma defesa contra ataques de CSRF.</span><span class="sxs-lookup"><span data-stu-id="99fc5-491">Therefore, for ASP.NET Web APIs protected using OAuth 2.0, bearer tokens are considered as a defense against CSRF attacks.</span></span> <span data-ttu-id="99fc5-492">Observe que, se a parte MVC do aplicativo usar a autenticação de formulários (ou seja, cookies), será necessário usar tokens antifalsificação pelo aplicativo Web do MVC.</span><span class="sxs-lookup"><span data-stu-id="99fc5-492">Please note that if the MVC portion of the application uses forms authentication (i.e., uses cookies), anti-forgery tokens have to be used by the MVC web app.</span></span> |

### <a name="example"></a><span data-ttu-id="99fc5-493">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99fc5-493">Example</span></span>
<span data-ttu-id="99fc5-494">A API Web precisa ser informada para confiar SOMENTE em tokens de portador e não em cookies.</span><span class="sxs-lookup"><span data-stu-id="99fc5-494">The Web API has to be informed to rely ONLY on bearer tokens and not on cookies.</span></span> <span data-ttu-id="99fc5-495">Isso pode ser feito pela configuração a seguir no método `WebApiConfig.Register`: ``\`Código C-Sharp config.SuppressDefaultHostAuthentication(); config.Filters.Add(new HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span><span class="sxs-lookup"><span data-stu-id="99fc5-495">It can be done by the following configuration in `WebApiConfig.Register` method: ``\`C-Sharp code config.SuppressDefaultHostAuthentication(); config.Filters.Add(new HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span></span>
```
The SuppressDefaultHostAuthentication method tells Web API to ignore any authentication that happens before the request reaches the Web API pipeline, either by IIS or by OWIN middleware. That way, we can restrict Web API to authenticate only using bearer tokens.