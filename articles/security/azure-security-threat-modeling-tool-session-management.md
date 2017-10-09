---
title: "aaaSession de gerenciamento - ferramenta de modelagem de ameaça Microsoft - Azure | Microsoft Docs"
description: "reduções de ameaças expostas em Olá, ferramenta de modelagem de ameaça"
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
ms.openlocfilehash: 915ffae3f775ca6902fcfb93e7e1952ce85612f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-session-management--articles"></a><span data-ttu-id="99df0-103">Quadro de segurança: Gerenciamento de sessão | Artigos</span><span class="sxs-lookup"><span data-stu-id="99df0-103">Security Frame: Session Management | Articles</span></span> 
| <span data-ttu-id="99df0-104">Produto/Serviço</span><span class="sxs-lookup"><span data-stu-id="99df0-104">Product/Service</span></span> | <span data-ttu-id="99df0-105">Artigo</span><span class="sxs-lookup"><span data-stu-id="99df0-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="99df0-106">**Azure AD**</span><span class="sxs-lookup"><span data-stu-id="99df0-106">**Azure AD**</span></span>    | <ul><li>[<span data-ttu-id="99df0-107">Implementar o logoff apropriado usando métodos ADAL ao usar o Azure AD</span><span class="sxs-lookup"><span data-stu-id="99df0-107">Implement proper logout using ADAL methods when using Azure AD</span></span>](#logout-adal)</li></ul> |
| <span data-ttu-id="99df0-108">Dispositivo IoT</span><span class="sxs-lookup"><span data-stu-id="99df0-108">IoT Device</span></span> | <ul><li>[<span data-ttu-id="99df0-109">Usar tempos de vida finitos para tokens SaS gerados</span><span class="sxs-lookup"><span data-stu-id="99df0-109">Use finite lifetimes for generated SaS tokens</span></span>](#finite-tokens)</li></ul> |
| <span data-ttu-id="99df0-110">**Azure DocumentDB**</span><span class="sxs-lookup"><span data-stu-id="99df0-110">**Azure Document DB**</span></span> | <ul><li>[<span data-ttu-id="99df0-111">Usar tempos de vida mínimos de tokens para tokens de Recurso gerados</span><span class="sxs-lookup"><span data-stu-id="99df0-111">Use minimum token lifetimes for generated Resource tokens</span></span>](#resource-tokens)</li></ul> |
| <span data-ttu-id="99df0-112">**ADFS**</span><span class="sxs-lookup"><span data-stu-id="99df0-112">**ADFS**</span></span> | <ul><li>[<span data-ttu-id="99df0-113">Implementar o logoff apropriado usando métodos WsFederation ao usar o ADFS</span><span class="sxs-lookup"><span data-stu-id="99df0-113">Implement proper logout using WsFederation methods when using ADFS</span></span>](#wsfederation-logout)</li></ul> |
| <span data-ttu-id="99df0-114">**Identity Server**</span><span class="sxs-lookup"><span data-stu-id="99df0-114">**Identity Server**</span></span> | <ul><li>[<span data-ttu-id="99df0-115">Implementar o logoff adequado ao usar o Servidor de identidade</span><span class="sxs-lookup"><span data-stu-id="99df0-115">Implement proper logout when using Identity Server</span></span>](#proper-logout)</li></ul> |
| <span data-ttu-id="99df0-116">**Aplicativo Web**</span><span class="sxs-lookup"><span data-stu-id="99df0-116">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="99df0-117">Os aplicativos disponíveis via HTTPS devem usar cookies seguros</span><span class="sxs-lookup"><span data-stu-id="99df0-117">Applications available over HTTPS must use secure cookies</span></span>](#https-secure-cookies)</li><li>[<span data-ttu-id="99df0-118">Todo aplicativo baseado em http deve especificar http somente para definição de cookie</span><span class="sxs-lookup"><span data-stu-id="99df0-118">All http based application should specify http only for cookie definition</span></span>](#cookie-definition)</li><li>[<span data-ttu-id="99df0-119">Atenuar ataques CSRF (solicitação intersite forjada) em páginas Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="99df0-119">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>](#csrf-asp)</li><li>[<span data-ttu-id="99df0-120">Configurar sessão para tempo de vida de inatividade</span><span class="sxs-lookup"><span data-stu-id="99df0-120">Set up session for inactivity lifetime</span></span>](#inactivity-lifetime)</li><li>[<span data-ttu-id="99df0-121">Implementar o logout adequado do aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="99df0-121">Implement proper logout from hello application</span></span>](#proper-app-logout)</li></ul> |
| <span data-ttu-id="99df0-122">**API da Web**</span><span class="sxs-lookup"><span data-stu-id="99df0-122">**Web API**</span></span> | <ul><li>[<span data-ttu-id="99df0-123">Atenuar ataques CSRF (solicitação intersite forjada) em APIs da Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="99df0-123">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>](#csrf-api)</li></ul> |

## <span data-ttu-id="99df0-124"><a id="logout-adal"></a>Implementar o logoff apropriado usando métodos ADAL ao usar o Azure AD</span><span class="sxs-lookup"><span data-stu-id="99df0-124"><a id="logout-adal"></a>Implement proper logout using ADAL methods when using Azure AD</span></span>

| <span data-ttu-id="99df0-125">Title</span><span class="sxs-lookup"><span data-stu-id="99df0-125">Title</span></span>                   | <span data-ttu-id="99df0-126">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99df0-126">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99df0-127">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99df0-127">**Component**</span></span>               | <span data-ttu-id="99df0-128">AD do Azure</span><span class="sxs-lookup"><span data-stu-id="99df0-128">Azure AD</span></span> | 
| <span data-ttu-id="99df0-129">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99df0-129">**SDL Phase**</span></span>               | <span data-ttu-id="99df0-130">Compilação</span><span class="sxs-lookup"><span data-stu-id="99df0-130">Build</span></span> |  
| <span data-ttu-id="99df0-131">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99df0-131">**Applicable Technologies**</span></span> | <span data-ttu-id="99df0-132">Genérico</span><span class="sxs-lookup"><span data-stu-id="99df0-132">Generic</span></span> |
| <span data-ttu-id="99df0-133">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99df0-133">**Attributes**</span></span>              | <span data-ttu-id="99df0-134">N/D</span><span class="sxs-lookup"><span data-stu-id="99df0-134">N/A</span></span>  |
| <span data-ttu-id="99df0-135">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99df0-135">**References**</span></span>              | <span data-ttu-id="99df0-136">N/D</span><span class="sxs-lookup"><span data-stu-id="99df0-136">N/A</span></span>  |
| <span data-ttu-id="99df0-137">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99df0-137">**Steps**</span></span> | <span data-ttu-id="99df0-138">Se o aplicativo hello depende de token de acesso emitido pelo AD do Azure, o manipulador de eventos de logoff de saudação deve chamar</span><span class="sxs-lookup"><span data-stu-id="99df0-138">If hello application relies on access token issued by Azure AD, hello logout event handler should call</span></span> |

### <a name="example"></a><span data-ttu-id="99df0-139">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99df0-139">Example</span></span>
```C#
HttpContext.GetOwinContext().Authentication.SignOut(OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType)
```

### <a name="example"></a><span data-ttu-id="99df0-140">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99df0-140">Example</span></span>
<span data-ttu-id="99df0-141">Também deve destruir a sessão do usuário chamando o método Session.Abandon().</span><span class="sxs-lookup"><span data-stu-id="99df0-141">It should also destroy user's session by calling Session.Abandon() method.</span></span> <span data-ttu-id="99df0-142">O método a seguir mostra a implementação segura do logoff do usuário:</span><span class="sxs-lookup"><span data-stu-id="99df0-142">Following method shows secure implementation of user logout:</span></span>
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

## <span data-ttu-id="99df0-143"><a id="finite-tokens"></a>Usar tempos de vida finitos para tokens SaS gerados</span><span class="sxs-lookup"><span data-stu-id="99df0-143"><a id="finite-tokens"></a>Use finite lifetimes for generated SaS tokens</span></span>

| <span data-ttu-id="99df0-144">Title</span><span class="sxs-lookup"><span data-stu-id="99df0-144">Title</span></span>                   | <span data-ttu-id="99df0-145">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99df0-145">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99df0-146">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99df0-146">**Component**</span></span>               | <span data-ttu-id="99df0-147">Dispositivo IoT</span><span class="sxs-lookup"><span data-stu-id="99df0-147">IoT Device</span></span> | 
| <span data-ttu-id="99df0-148">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99df0-148">**SDL Phase**</span></span>               | <span data-ttu-id="99df0-149">Compilação</span><span class="sxs-lookup"><span data-stu-id="99df0-149">Build</span></span> |  
| <span data-ttu-id="99df0-150">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99df0-150">**Applicable Technologies**</span></span> | <span data-ttu-id="99df0-151">Genérico</span><span class="sxs-lookup"><span data-stu-id="99df0-151">Generic</span></span> |
| <span data-ttu-id="99df0-152">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99df0-152">**Attributes**</span></span>              | <span data-ttu-id="99df0-153">N/D</span><span class="sxs-lookup"><span data-stu-id="99df0-153">N/A</span></span>  |
| <span data-ttu-id="99df0-154">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99df0-154">**References**</span></span>              | <span data-ttu-id="99df0-155">N/D</span><span class="sxs-lookup"><span data-stu-id="99df0-155">N/A</span></span>  |
| <span data-ttu-id="99df0-156">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99df0-156">**Steps**</span></span> | <span data-ttu-id="99df0-157">Tokens SaS gerados para autenticar tooAzure IoT Hub devem ter um período de expiração Finitas.</span><span class="sxs-lookup"><span data-stu-id="99df0-157">SaS tokens generated for authenticating tooAzure IoT Hub should have a finite expiry period.</span></span> <span data-ttu-id="99df0-158">Manter Olá SaS tempos de vida de token tooa toolimit mínimo Olá quantidade de tempo que podem ser reproduzidos no caso de tokens de saudação sejam comprometidos.</span><span class="sxs-lookup"><span data-stu-id="99df0-158">Keep hello SaS token lifetimes tooa minimum toolimit hello amount of time they can be replayed in case hello tokens are compromised.</span></span>|

## <span data-ttu-id="99df0-159"><a id="resource-tokens"></a>Usar tempos de vida mínimos de tokens para tokens de Recurso gerados</span><span class="sxs-lookup"><span data-stu-id="99df0-159"><a id="resource-tokens"></a>Use minimum token lifetimes for generated Resource tokens</span></span>

| <span data-ttu-id="99df0-160">Title</span><span class="sxs-lookup"><span data-stu-id="99df0-160">Title</span></span>                   | <span data-ttu-id="99df0-161">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99df0-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99df0-162">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99df0-162">**Component**</span></span>               | <span data-ttu-id="99df0-163">Azure Document DB</span><span class="sxs-lookup"><span data-stu-id="99df0-163">Azure Document DB</span></span> | 
| <span data-ttu-id="99df0-164">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99df0-164">**SDL Phase**</span></span>               | <span data-ttu-id="99df0-165">Compilação</span><span class="sxs-lookup"><span data-stu-id="99df0-165">Build</span></span> |  
| <span data-ttu-id="99df0-166">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99df0-166">**Applicable Technologies**</span></span> | <span data-ttu-id="99df0-167">Genérico</span><span class="sxs-lookup"><span data-stu-id="99df0-167">Generic</span></span> |
| <span data-ttu-id="99df0-168">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99df0-168">**Attributes**</span></span>              | <span data-ttu-id="99df0-169">N/D</span><span class="sxs-lookup"><span data-stu-id="99df0-169">N/A</span></span>  |
| <span data-ttu-id="99df0-170">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99df0-170">**References**</span></span>              | <span data-ttu-id="99df0-171">N/D</span><span class="sxs-lookup"><span data-stu-id="99df0-171">N/A</span></span>  |
| <span data-ttu-id="99df0-172">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99df0-172">**Steps**</span></span> | <span data-ttu-id="99df0-173">Reduza o timespan de saudação do valor mínimo de tooa token de recurso necessário.</span><span class="sxs-lookup"><span data-stu-id="99df0-173">Reduce hello timespan of resource token tooa minimum value required.</span></span> <span data-ttu-id="99df0-174">Tokens de recurso têm um intervalo de tempo válido padrão de uma hora.</span><span class="sxs-lookup"><span data-stu-id="99df0-174">Resource tokens have a default valid timespan of 1 hour.</span></span>|

## <span data-ttu-id="99df0-175"><a id="wsfederation-logout"></a>Implementar o logoff apropriado usando métodos WsFederation ao usar o ADFS</span><span class="sxs-lookup"><span data-stu-id="99df0-175"><a id="wsfederation-logout"></a>Implement proper logout using WsFederation methods when using ADFS</span></span>

| <span data-ttu-id="99df0-176">Title</span><span class="sxs-lookup"><span data-stu-id="99df0-176">Title</span></span>                   | <span data-ttu-id="99df0-177">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99df0-177">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99df0-178">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99df0-178">**Component**</span></span>               | <span data-ttu-id="99df0-179">ADFS</span><span class="sxs-lookup"><span data-stu-id="99df0-179">ADFS</span></span> | 
| <span data-ttu-id="99df0-180">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99df0-180">**SDL Phase**</span></span>               | <span data-ttu-id="99df0-181">Compilação</span><span class="sxs-lookup"><span data-stu-id="99df0-181">Build</span></span> |  
| <span data-ttu-id="99df0-182">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99df0-182">**Applicable Technologies**</span></span> | <span data-ttu-id="99df0-183">Genérico</span><span class="sxs-lookup"><span data-stu-id="99df0-183">Generic</span></span> |
| <span data-ttu-id="99df0-184">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99df0-184">**Attributes**</span></span>              | <span data-ttu-id="99df0-185">N/D</span><span class="sxs-lookup"><span data-stu-id="99df0-185">N/A</span></span>  |
| <span data-ttu-id="99df0-186">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99df0-186">**References**</span></span>              | <span data-ttu-id="99df0-187">N/D</span><span class="sxs-lookup"><span data-stu-id="99df0-187">N/A</span></span>  |
| <span data-ttu-id="99df0-188">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99df0-188">**Steps**</span></span> | <span data-ttu-id="99df0-189">Se o aplicativo hello depende de token do STS emitido pelo ADFS, manipulador de eventos de logout Olá deve chamar WSFederationAuthenticationModule.FederatedSignOut() método toolog usuário hello.</span><span class="sxs-lookup"><span data-stu-id="99df0-189">If hello application relies on STS token issued by ADFS, hello logout event handler should call WSFederationAuthenticationModule.FederatedSignOut() method toolog out hello user.</span></span> <span data-ttu-id="99df0-190">Também hello atual sessão deve ser destruída, e o valor do token de sessão Olá deve ser redefinido e inúteis.</span><span class="sxs-lookup"><span data-stu-id="99df0-190">Also hello current session should be destroyed, and hello session token value should be reset and nullified.</span></span>|

### <a name="example"></a><span data-ttu-id="99df0-191">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99df0-191">Example</span></span>
```C#
        [HttpPost, ValidateAntiForgeryToken]
        [Authorization]
        public ActionResult SignOut(string redirectUrl)
        {
            if (!this.User.Identity.IsAuthenticated)
            {
                return this.View("LogOff", null);
            }

            // Removes hello user profile.
            this.Session.Clear();
            this.Session.Abandon();
            HttpContext.Current.Response.Cookies.Add(new System.Web.HttpCookie("ASP.NET_SessionId", string.Empty)
                {
                    Expires = DateTime.Now.AddDays(-1D),
                    Secure = true,
                    HttpOnly = true
                });

            // Signs out at hello specified security token service (STS) by using hello WS-Federation protocol.
            Uri signOutUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Issuer);
            Uri replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm);
            if (!string.IsNullOrEmpty(redirectUrl))
            {
                replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm + redirectUrl);
            }
           //     Signs out of hello current session and raises hello appropriate events.
            var authModule = FederatedAuthentication.WSFederationAuthenticationModule;
            authModule.SignOut(false);
        //     Signs out at hello specified security token service (STS) by using hello WS-Federation
        //     protocol.            
            WSFederationAuthenticationModule.FederatedSignOut(signOutUrl, replyUrl);
            return new RedirectResult(redirectUrl);
        }
```

## <span data-ttu-id="99df0-192"><a id="proper-logout"></a>Implementar o logoff adequado ao usar o Servidor de identidade</span><span class="sxs-lookup"><span data-stu-id="99df0-192"><a id="proper-logout"></a>Implement proper logout when using Identity Server</span></span>

| <span data-ttu-id="99df0-193">Title</span><span class="sxs-lookup"><span data-stu-id="99df0-193">Title</span></span>                   | <span data-ttu-id="99df0-194">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99df0-194">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99df0-195">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99df0-195">**Component**</span></span>               | <span data-ttu-id="99df0-196">Servidor de Identidade</span><span class="sxs-lookup"><span data-stu-id="99df0-196">Identity Server</span></span> | 
| <span data-ttu-id="99df0-197">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99df0-197">**SDL Phase**</span></span>               | <span data-ttu-id="99df0-198">Compilação</span><span class="sxs-lookup"><span data-stu-id="99df0-198">Build</span></span> |  
| <span data-ttu-id="99df0-199">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99df0-199">**Applicable Technologies**</span></span> | <span data-ttu-id="99df0-200">Genérico</span><span class="sxs-lookup"><span data-stu-id="99df0-200">Generic</span></span> |
| <span data-ttu-id="99df0-201">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99df0-201">**Attributes**</span></span>              | <span data-ttu-id="99df0-202">N/D</span><span class="sxs-lookup"><span data-stu-id="99df0-202">N/A</span></span>  |
| <span data-ttu-id="99df0-203">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99df0-203">**References**</span></span>              | [<span data-ttu-id="99df0-204">Saída do IdentityServer3-Federated</span><span class="sxs-lookup"><span data-stu-id="99df0-204">IdentityServer3-Federated sign out</span></span>](https://identityserver.github.io/Documentation/docsv2/advanced/federated-signout.html) |
| <span data-ttu-id="99df0-205">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99df0-205">**Steps**</span></span> | <span data-ttu-id="99df0-206">IdentityServer oferece suporte a saudação capacidade toofederate com provedores de identidade externa.</span><span class="sxs-lookup"><span data-stu-id="99df0-206">IdentityServer supports hello ability toofederate with external identity providers.</span></span> <span data-ttu-id="99df0-207">Quando um usuário sai de um provedor de identidade upstream, dependendo do protocolo de saudação usado, talvez seja possível tooreceive uma notificação quando Olá usuário sai. Ele permite toonotify IdentityServer seus clientes para que eles também podem entrar Olá usuário out. Verifique a documentação na seção de referências de saudação para obter detalhes de implementação Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="99df0-207">When a user signs out of an upstream identity provider, depending upon hello protocol used, it might be possible tooreceive a notification when hello user signs out. It allows IdentityServer toonotify its clients so they can also sign hello user out. Check hello documentation in hello references section for hello implementation details.</span></span>|

## <span data-ttu-id="99df0-208"><a id="https-secure-cookies"></a>Os aplicativos disponíveis via HTTPS devem usar cookies seguros</span><span class="sxs-lookup"><span data-stu-id="99df0-208"><a id="https-secure-cookies"></a>Applications available over HTTPS must use secure cookies</span></span>

| <span data-ttu-id="99df0-209">Title</span><span class="sxs-lookup"><span data-stu-id="99df0-209">Title</span></span>                   | <span data-ttu-id="99df0-210">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99df0-210">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99df0-211">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99df0-211">**Component**</span></span>               | <span data-ttu-id="99df0-212">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="99df0-212">Web Application</span></span> | 
| <span data-ttu-id="99df0-213">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99df0-213">**SDL Phase**</span></span>               | <span data-ttu-id="99df0-214">Compilação</span><span class="sxs-lookup"><span data-stu-id="99df0-214">Build</span></span> |  
| <span data-ttu-id="99df0-215">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99df0-215">**Applicable Technologies**</span></span> | <span data-ttu-id="99df0-216">Genérico</span><span class="sxs-lookup"><span data-stu-id="99df0-216">Generic</span></span> |
| <span data-ttu-id="99df0-217">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99df0-217">**Attributes**</span></span>              | <span data-ttu-id="99df0-218">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="99df0-218">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="99df0-219">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99df0-219">**References**</span></span>              | <span data-ttu-id="99df0-220">[httpCookies Element (Esquema de configurações ASP.NET)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [Propriedade HttpCookie.Secure](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span><span class="sxs-lookup"><span data-stu-id="99df0-220">[httpCookies Element (ASP.NET Settings Schema)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure Property](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span></span> |
| <span data-ttu-id="99df0-221">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99df0-221">**Steps**</span></span> | <span data-ttu-id="99df0-222">Os cookies são normalmente apenas domínio toohello acessível para o qual eles foram escopo.</span><span class="sxs-lookup"><span data-stu-id="99df0-222">Cookies are normally only accessible toohello domain for which they were scoped.</span></span> <span data-ttu-id="99df0-223">Infelizmente, definição de saudação do "domínio" não inclui protocolo Olá para que cookies que são criados por HTTPS são acessíveis por meio de HTTP.</span><span class="sxs-lookup"><span data-stu-id="99df0-223">Unfortunately, hello definition of "domain" does not include hello protocol so cookies that are created over HTTPS are accessible over HTTP.</span></span> <span data-ttu-id="99df0-224">atributo "segura" Hello indica que o navegador toohello Olá cookie deve apenas ser disponibilizada via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="99df0-224">hello "secure" attribute indicates toohello browser that hello cookie should only be made available over HTTPS.</span></span> <span data-ttu-id="99df0-225">Verifique se todos os cookies definido por HTTPS usam Olá **segura** atributo.</span><span class="sxs-lookup"><span data-stu-id="99df0-225">Ensure that all cookies set over HTTPS use hello **secure** attribute.</span></span> <span data-ttu-id="99df0-226">requisito de saudação pode ser imposto no arquivo Web. config de saudação definindo Olá requireSSL atributo tootrue.</span><span class="sxs-lookup"><span data-stu-id="99df0-226">hello requirement can be enforced in hello web.config file by setting hello requireSSL attribute tootrue.</span></span> <span data-ttu-id="99df0-227">É Olá preferencial abordagem porque ele aplicará Olá **segura** atributo para todos os cookies atuais e futuros sem Olá necessidade toomake as alterações de código adicional.</span><span class="sxs-lookup"><span data-stu-id="99df0-227">It is hello preferred approach because it will enforce hello **secure** attribute for all current and future cookies without hello need toomake any additional code changes.</span></span>|

### <a name="example"></a><span data-ttu-id="99df0-228">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99df0-228">Example</span></span>
```C#
<configuration>
  <system.web>
    <httpCookies requireSSL="true"/>
  </system.web>
</configuration>
```
<span data-ttu-id="99df0-229">configuração de saudação é imposta mesmo que o HTTP é usado tooaccess Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="99df0-229">hello setting is enforced even if HTTP is used tooaccess hello application.</span></span> <span data-ttu-id="99df0-230">Se o HTTP é usado tooaccess Olá aplicativo, quebras de configuração aplicativo hello porque cookies Olá são definidos com navegador seguro de atributo e Olá Olá não enviará-los hello volta toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="99df0-230">If HTTP is used tooaccess hello application, hello setting breaks hello application because hello cookies are set with hello secure attribute and hello browser will not send them back toohello application.</span></span>

| <span data-ttu-id="99df0-231">Title</span><span class="sxs-lookup"><span data-stu-id="99df0-231">Title</span></span>                   | <span data-ttu-id="99df0-232">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99df0-232">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99df0-233">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99df0-233">**Component**</span></span>               | <span data-ttu-id="99df0-234">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="99df0-234">Web Application</span></span> | 
| <span data-ttu-id="99df0-235">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99df0-235">**SDL Phase**</span></span>               | <span data-ttu-id="99df0-236">Compilação</span><span class="sxs-lookup"><span data-stu-id="99df0-236">Build</span></span> |  
| <span data-ttu-id="99df0-237">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99df0-237">**Applicable Technologies**</span></span> | <span data-ttu-id="99df0-238">Web Forms, MVC5</span><span class="sxs-lookup"><span data-stu-id="99df0-238">Web Forms, MVC5</span></span> |
| <span data-ttu-id="99df0-239">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99df0-239">**Attributes**</span></span>              | <span data-ttu-id="99df0-240">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="99df0-240">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="99df0-241">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99df0-241">**References**</span></span>              | <span data-ttu-id="99df0-242">N/D</span><span class="sxs-lookup"><span data-stu-id="99df0-242">N/A</span></span>  |
| <span data-ttu-id="99df0-243">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99df0-243">**Steps**</span></span> | <span data-ttu-id="99df0-244">Quando Olá web aplicativo hello terceira parte confiável, e Olá IdP servidor ADFS, atributo de segurança do token de FedAuth Olá pode ser configurado por definindo o requireSSL tooTrue em `system.identityModel.services` seção de Web. config:</span><span class="sxs-lookup"><span data-stu-id="99df0-244">When hello web application is hello Relying Party, and hello IdP is ADFS server, hello FedAuth token's secure attribute can be configured by setting requireSSL tooTrue in `system.identityModel.services` section of web.config:</span></span>|

### <a name="example"></a><span data-ttu-id="99df0-245">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99df0-245">Example</span></span>
```C#
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:20:0" />
    ....  
    </federationConfiguration>
  </system.identityModel.services>
```

## <span data-ttu-id="99df0-246"><a id="cookie-definition"></a>Todo aplicativo baseado em http deve especificar http somente para definição de cookie</span><span class="sxs-lookup"><span data-stu-id="99df0-246"><a id="cookie-definition"></a>All http based application should specify http only for cookie definition</span></span>

| <span data-ttu-id="99df0-247">Title</span><span class="sxs-lookup"><span data-stu-id="99df0-247">Title</span></span>                   | <span data-ttu-id="99df0-248">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99df0-248">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99df0-249">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99df0-249">**Component**</span></span>               | <span data-ttu-id="99df0-250">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="99df0-250">Web Application</span></span> | 
| <span data-ttu-id="99df0-251">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99df0-251">**SDL Phase**</span></span>               | <span data-ttu-id="99df0-252">Compilação</span><span class="sxs-lookup"><span data-stu-id="99df0-252">Build</span></span> |  
| <span data-ttu-id="99df0-253">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99df0-253">**Applicable Technologies**</span></span> | <span data-ttu-id="99df0-254">Genérico</span><span class="sxs-lookup"><span data-stu-id="99df0-254">Generic</span></span> |
| <span data-ttu-id="99df0-255">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99df0-255">**Attributes**</span></span>              | <span data-ttu-id="99df0-256">N/D</span><span class="sxs-lookup"><span data-stu-id="99df0-256">N/A</span></span>  |
| <span data-ttu-id="99df0-257">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99df0-257">**References**</span></span>              | [<span data-ttu-id="99df0-258">Atributo Secure Cookie</span><span class="sxs-lookup"><span data-stu-id="99df0-258">Secure Cookie Attribute</span></span>](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie) |
| <span data-ttu-id="99df0-259">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99df0-259">**Steps**</span></span> | <span data-ttu-id="99df0-260">toomitigate o risco de saudação de divulgação de informações com um ataque de script entre sites (XSS), um novo atributo - httpOnly - foi introduzido toocookies e é suportado por todos os principais navegadores.</span><span class="sxs-lookup"><span data-stu-id="99df0-260">toomitigate hello risk of information disclosure with a cross-site scripting (XSS) attack, a new attribute - httpOnly - was introduced toocookies and is supported by all major browsers.</span></span> <span data-ttu-id="99df0-261">atributo de saudação especifica que um cookie não é acessível por meio de script.</span><span class="sxs-lookup"><span data-stu-id="99df0-261">hello attribute specifies that a cookie is not accessible through script.</span></span> <span data-ttu-id="99df0-262">Usando cookies HttpOnly, um aplicativo web reduz a possibilidade de saudação que informações confidenciais contidas no cookie de saudação seja roubadas por meio de script e enviadas site tooan invasor.</span><span class="sxs-lookup"><span data-stu-id="99df0-262">By using HttpOnly cookies, a web application reduces hello possibility that sensitive information contained in hello cookie can be stolen via script and sent tooan attacker's website.</span></span> |

### <a name="example"></a><span data-ttu-id="99df0-263">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99df0-263">Example</span></span>
<span data-ttu-id="99df0-264">Todos os aplicativos com base em HTTP que usam cookies devem especificar HttpOnly na definição de cookie hello, Implementando a seguinte configuração no Web. config:</span><span class="sxs-lookup"><span data-stu-id="99df0-264">All HTTP-based applications that use cookies should specify HttpOnly in hello cookie definition, by implementing following configuration in web.config:</span></span>
```XML
<system.web>
.
.
   <httpCookies requireSSL="false" httpOnlyCookies="true"/>
.
.
</system.web>
```

| <span data-ttu-id="99df0-265">Title</span><span class="sxs-lookup"><span data-stu-id="99df0-265">Title</span></span>                   | <span data-ttu-id="99df0-266">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99df0-266">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99df0-267">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99df0-267">**Component**</span></span>               | <span data-ttu-id="99df0-268">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="99df0-268">Web Application</span></span> | 
| <span data-ttu-id="99df0-269">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99df0-269">**SDL Phase**</span></span>               | <span data-ttu-id="99df0-270">Compilação</span><span class="sxs-lookup"><span data-stu-id="99df0-270">Build</span></span> |  
| <span data-ttu-id="99df0-271">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99df0-271">**Applicable Technologies**</span></span> | <span data-ttu-id="99df0-272">Formulários da Web</span><span class="sxs-lookup"><span data-stu-id="99df0-272">Web Forms</span></span> |
| <span data-ttu-id="99df0-273">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99df0-273">**Attributes**</span></span>              | <span data-ttu-id="99df0-274">N/D</span><span class="sxs-lookup"><span data-stu-id="99df0-274">N/A</span></span>  |
| <span data-ttu-id="99df0-275">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99df0-275">**References**</span></span>              | [<span data-ttu-id="99df0-276">Propriedade FormsAuthentication.RequireSSL</span><span class="sxs-lookup"><span data-stu-id="99df0-276">FormsAuthentication.RequireSSL Property</span></span>](https://msdn.microsoft.com/library/system.web.security.formsauthentication.requiressl.aspx) |
| <span data-ttu-id="99df0-277">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99df0-277">**Steps**</span></span> | <span data-ttu-id="99df0-278">Olá RequireSSL valor da propriedade é definida no arquivo de configuração de saudação para um aplicativo ASP.NET usando o atributo requireSSL de saudação do elemento de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="99df0-278">hello RequireSSL property value is set in hello configuration file for an ASP.NET application by using hello requireSSL attribute of hello configuration element.</span></span> <span data-ttu-id="99df0-279">Você pode especificar no arquivo Web. config de saudação para seu aplicativo ASP.NET se SSL (Secure Sockets Layer) é servidor de toohello de cookie tooreturn necessário Olá autenticação de formulários ao definir atributo de requireSSL hello.</span><span class="sxs-lookup"><span data-stu-id="99df0-279">You can specify in hello Web.config file for your ASP.NET application whether SSL (Secure Sockets Layer) is required tooreturn hello forms-authentication cookie toohello server by setting hello requireSSL attribute.</span></span>|

### <a name="example"></a><span data-ttu-id="99df0-280">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99df0-280">Example</span></span> 
<span data-ttu-id="99df0-281">Olá exemplo de código a seguir define Olá requireSSL atributo no arquivo Web. config de saudação.</span><span class="sxs-lookup"><span data-stu-id="99df0-281">hello following code example sets hello requireSSL attribute in hello Web.config file.</span></span>
```XML
<authentication mode="Forms">
  <forms loginUrl="member_login.aspx" cookieless="UseCookies" requireSSL="true"/>
</authentication>
```

| <span data-ttu-id="99df0-282">Title</span><span class="sxs-lookup"><span data-stu-id="99df0-282">Title</span></span>                   | <span data-ttu-id="99df0-283">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99df0-283">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99df0-284">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99df0-284">**Component**</span></span>               | <span data-ttu-id="99df0-285">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="99df0-285">Web Application</span></span> | 
| <span data-ttu-id="99df0-286">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99df0-286">**SDL Phase**</span></span>               | <span data-ttu-id="99df0-287">Compilação</span><span class="sxs-lookup"><span data-stu-id="99df0-287">Build</span></span> |  
| <span data-ttu-id="99df0-288">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99df0-288">**Applicable Technologies**</span></span> | <span data-ttu-id="99df0-289">MVC5</span><span class="sxs-lookup"><span data-stu-id="99df0-289">MVC5</span></span> |
| <span data-ttu-id="99df0-290">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99df0-290">**Attributes**</span></span>              | <span data-ttu-id="99df0-291">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="99df0-291">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="99df0-292">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99df0-292">**References**</span></span>              | [<span data-ttu-id="99df0-293">Configuração do Windows Identity Foundation (WIF) – Part II</span><span class="sxs-lookup"><span data-stu-id="99df0-293">Windows Identity Foundation (WIF) Configuration – Part II</span></span>](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/) |
| <span data-ttu-id="99df0-294">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99df0-294">**Steps**</span></span> | <span data-ttu-id="99df0-295">atributo de httpOnly tooset cookies FedAuth, o valor do atributo hideFromCsript deve ser definido tooTrue.</span><span class="sxs-lookup"><span data-stu-id="99df0-295">tooset httpOnly attribute for FedAuth cookies, hideFromCsript attribute value should be set tooTrue.</span></span> |

### <a name="example"></a><span data-ttu-id="99df0-296">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99df0-296">Example</span></span>
<span data-ttu-id="99df0-297">Configuração a seguir mostra a configuração correta de saudação:</span><span class="sxs-lookup"><span data-stu-id="99df0-297">Following configuration shows hello correct configuration:</span></span>
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

## <span data-ttu-id="99df0-298"><a id="csrf-asp"></a>Atenuar ataques CSRF (solicitação intersite forjada) em páginas Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="99df0-298"><a id="csrf-asp"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>

| <span data-ttu-id="99df0-299">Title</span><span class="sxs-lookup"><span data-stu-id="99df0-299">Title</span></span>                   | <span data-ttu-id="99df0-300">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99df0-300">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99df0-301">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99df0-301">**Component**</span></span>               | <span data-ttu-id="99df0-302">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="99df0-302">Web Application</span></span> | 
| <span data-ttu-id="99df0-303">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99df0-303">**SDL Phase**</span></span>               | <span data-ttu-id="99df0-304">Compilação</span><span class="sxs-lookup"><span data-stu-id="99df0-304">Build</span></span> |  
| <span data-ttu-id="99df0-305">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99df0-305">**Applicable Technologies**</span></span> | <span data-ttu-id="99df0-306">Genérico</span><span class="sxs-lookup"><span data-stu-id="99df0-306">Generic</span></span> |
| <span data-ttu-id="99df0-307">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99df0-307">**Attributes**</span></span>              | <span data-ttu-id="99df0-308">N/D</span><span class="sxs-lookup"><span data-stu-id="99df0-308">N/A</span></span>  |
| <span data-ttu-id="99df0-309">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99df0-309">**References**</span></span>              | <span data-ttu-id="99df0-310">N/D</span><span class="sxs-lookup"><span data-stu-id="99df0-310">N/A</span></span>  |
| <span data-ttu-id="99df0-311">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99df0-311">**Steps**</span></span> | <span data-ttu-id="99df0-312">Falsificação de solicitação entre sites (CSRF ou XSRF) é um tipo de ataque em que um invasor pode realizar ações no contexto de segurança de saudação da sessão de um usuário diferente estabelecida em um site da web.</span><span class="sxs-lookup"><span data-stu-id="99df0-312">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in hello security context of a different user's established session on a web site.</span></span> <span data-ttu-id="99df0-313">meta de saudação é toomodify ou excluir o conteúdo, se o site de destino-Olá se basear exclusivamente em cookies de sessão tooauthenticate solicitação recebida.</span><span class="sxs-lookup"><span data-stu-id="99df0-313">hello goal is toomodify or delete content, if hello targeted web site relies exclusively on session cookies tooauthenticate received request.</span></span> <span data-ttu-id="99df0-314">Um invasor pode explorar essa vulnerabilidade obtendo tooload do navegador de um usuário diferente uma URL com um comando de um site vulnerável no qual usuário Olá já estiver conectado.</span><span class="sxs-lookup"><span data-stu-id="99df0-314">An attacker could exploit this vulnerability by getting a different user's browser tooload a URL with a command from a vulnerable site on which hello user is already logged in.</span></span> <span data-ttu-id="99df0-315">Há várias maneiras para um toodo invasor que, como hospedar um site diferente que carrega um recurso de servidor vulnerável hello, ou tooclick de usuário Olá obtendo um link.</span><span class="sxs-lookup"><span data-stu-id="99df0-315">There are many ways for an attacker toodo that, such as by hosting a different web site that loads a resource from hello vulnerable server, or getting hello user tooclick a link.</span></span> <span data-ttu-id="99df0-316">ataque de saudação pode ser evitado se o servidor de saudação envia um cliente toohello token adicionais, requer Olá cliente tooinclude esse token em todas as solicitações futuras e verifica se todas as solicitações futuras incluem um token que pertence toohello sessão atual, como por usando Olá AntiForgeryToken ASP.NET ou ViewState.</span><span class="sxs-lookup"><span data-stu-id="99df0-316">hello attack can be prevented if hello server sends an additional token toohello client, requires hello client tooinclude that token in all future requests, and verifies that all future requests include a token that pertains toohello current session, such as by using hello ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="99df0-317">Title</span><span class="sxs-lookup"><span data-stu-id="99df0-317">Title</span></span>                   | <span data-ttu-id="99df0-318">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99df0-318">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99df0-319">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99df0-319">**Component**</span></span>               | <span data-ttu-id="99df0-320">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="99df0-320">Web Application</span></span> | 
| <span data-ttu-id="99df0-321">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99df0-321">**SDL Phase**</span></span>               | <span data-ttu-id="99df0-322">Compilação</span><span class="sxs-lookup"><span data-stu-id="99df0-322">Build</span></span> |  
| <span data-ttu-id="99df0-323">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99df0-323">**Applicable Technologies**</span></span> | <span data-ttu-id="99df0-324">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="99df0-324">MVC5, MVC6</span></span> |
| <span data-ttu-id="99df0-325">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99df0-325">**Attributes**</span></span>              | <span data-ttu-id="99df0-326">N/D</span><span class="sxs-lookup"><span data-stu-id="99df0-326">N/A</span></span>  |
| <span data-ttu-id="99df0-327">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99df0-327">**References**</span></span>              | [<span data-ttu-id="99df0-328">Prevenção de XSRF/CSRF no ASP.NET MVC e páginas Web</span><span class="sxs-lookup"><span data-stu-id="99df0-328">XSRF/CSRF Prevention in ASP.NET MVC and Web Pages</span></span>](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) |
| <span data-ttu-id="99df0-329">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99df0-329">**Steps**</span></span> | <span data-ttu-id="99df0-330">Formulários de anti-CSRF e ASP.NET MVC - Olá Use `AntiForgeryToken` método auxiliar em exibições; coloque um `Html.AntiForgeryToken()` em formulário hello, por exemplo,</span><span class="sxs-lookup"><span data-stu-id="99df0-330">Anti-CSRF and ASP.NET MVC forms - Use hello `AntiForgeryToken` helper method on Views; put an `Html.AntiForgeryToken()` into hello form, for example,</span></span>|

### <a name="example"></a><span data-ttu-id="99df0-331">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99df0-331">Example</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
```

### <a name="example"></a><span data-ttu-id="99df0-332">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99df0-332">Example</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="99df0-333">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99df0-333">Example</span></span>
<span data-ttu-id="99df0-334">A saudação mesmo momento, visitante de saudação do Html.AntiForgeryToken() oferece um cookie chamado __RequestVerificationToken, com o mesmo valor como valor oculto aleatório Olá mostrado acima de saudação.</span><span class="sxs-lookup"><span data-stu-id="99df0-334">At hello same time, Html.AntiForgeryToken() gives hello visitor a cookie called __RequestVerificationToken, with hello same value as hello random hidden value shown above.</span></span> <span data-ttu-id="99df0-335">Em seguida, toovalidate uma postagem de formulário de entrada, adicione o método de ação do hello [ValidateAntiForgeryToken] filtro toohello destino.</span><span class="sxs-lookup"><span data-stu-id="99df0-335">Next, toovalidate an incoming form post, add hello [ValidateAntiForgeryToken] filter toohello target action method.</span></span> <span data-ttu-id="99df0-336">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="99df0-336">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="99df0-337">Filtro de autorização que verifica se:</span><span class="sxs-lookup"><span data-stu-id="99df0-337">Authorization filter that checks that:</span></span>
* <span data-ttu-id="99df0-338">solicitação de entrada Hello tem um cookie chamado __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="99df0-338">hello incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="99df0-339">Olá solicitação de entrada tem um `Request.Form` entrada chamada __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="99df0-339">hello incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="99df0-340">Esses cookies e `Request.Form` correspondência de valores, supondo que todas as é bem, Olá solicitação passa por como normal.</span><span class="sxs-lookup"><span data-stu-id="99df0-340">These cookie and `Request.Form` values match Assuming all is well, hello request goes through as normal.</span></span> <span data-ttu-id="99df0-341">Mas, se não estiver, uma falha de autorização com a mensagem "Um token antifalsificação necessário não foi fornecido ou era inválido".</span><span class="sxs-lookup"><span data-stu-id="99df0-341">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span> 

### <a name="example"></a><span data-ttu-id="99df0-342">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99df0-342">Example</span></span>
<span data-ttu-id="99df0-343">Anti-CSRF e AJAX: token de formulário de saudação pode ser um problema para solicitações do AJAX, porque uma solicitação AJAX pode enviar dados JSON, não os dados de formulário HTML.</span><span class="sxs-lookup"><span data-stu-id="99df0-343">Anti-CSRF and AJAX: hello form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="99df0-344">Uma solução é tokens de saudação do toosend em um cabeçalho HTTP personalizado.</span><span class="sxs-lookup"><span data-stu-id="99df0-344">One solution is toosend hello tokens in a custom HTTP header.</span></span> <span data-ttu-id="99df0-345">Hello código a seguir usa os tokens de saudação do Razor sintaxe toogenerate e, em seguida, adiciona Olá tokens tooan AJAX solicitação.</span><span class="sxs-lookup"><span data-stu-id="99df0-345">hello following code uses Razor syntax toogenerate hello tokens, and then adds hello tokens tooan AJAX request.</span></span> 
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

### <a name="example"></a><span data-ttu-id="99df0-346">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99df0-346">Example</span></span>
<span data-ttu-id="99df0-347">Ao processar solicitação Olá, extrai tokens de saudação do cabeçalho de solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="99df0-347">When you process hello request, extract hello tokens from hello request header.</span></span> <span data-ttu-id="99df0-348">Chame Olá AntiForgery.Validate método toovalidate tokens de saudação.</span><span class="sxs-lookup"><span data-stu-id="99df0-348">Then call hello AntiForgery.Validate method toovalidate hello tokens.</span></span> <span data-ttu-id="99df0-349">Olá método Validate lança uma exceção se os tokens de saudação não são válidos.</span><span class="sxs-lookup"><span data-stu-id="99df0-349">hello Validate method throws an exception if hello tokens are not valid.</span></span>
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

| <span data-ttu-id="99df0-350">Title</span><span class="sxs-lookup"><span data-stu-id="99df0-350">Title</span></span>                   | <span data-ttu-id="99df0-351">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99df0-351">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99df0-352">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99df0-352">**Component**</span></span>               | <span data-ttu-id="99df0-353">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="99df0-353">Web Application</span></span> | 
| <span data-ttu-id="99df0-354">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99df0-354">**SDL Phase**</span></span>               | <span data-ttu-id="99df0-355">Compilação</span><span class="sxs-lookup"><span data-stu-id="99df0-355">Build</span></span> |  
| <span data-ttu-id="99df0-356">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99df0-356">**Applicable Technologies**</span></span> | <span data-ttu-id="99df0-357">Formulários da Web</span><span class="sxs-lookup"><span data-stu-id="99df0-357">Web Forms</span></span> |
| <span data-ttu-id="99df0-358">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99df0-358">**Attributes**</span></span>              | <span data-ttu-id="99df0-359">N/D</span><span class="sxs-lookup"><span data-stu-id="99df0-359">N/A</span></span>  |
| <span data-ttu-id="99df0-360">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99df0-360">**References**</span></span>              | [<span data-ttu-id="99df0-361">Tirar proveito dos recursos internos do ASP.NET tooFend Off ataques de Web</span><span class="sxs-lookup"><span data-stu-id="99df0-361">Take Advantage of ASP.NET Built-in Features tooFend Off Web Attacks</span></span>](https://msdn.microsoft.com/library/ms972969.aspx#securitybarriers_topic2) |
| <span data-ttu-id="99df0-362">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99df0-362">**Steps**</span></span> | <span data-ttu-id="99df0-363">Ataques CSRF em aplicativos de formulário da Web com base podem ser atenuadas definindo ViewStateUserKey tooa cadeia de caracteres aleatória que varia para cada usuário - ID de usuário ou, melhor ainda, ID de sessão.</span><span class="sxs-lookup"><span data-stu-id="99df0-363">CSRF attacks in WebForm based applications can be mitigated by setting ViewStateUserKey tooa random string that varies for each user - user ID or, better yet, session ID.</span></span> <span data-ttu-id="99df0-364">Por diversos motivos técnicos e sociais, ID de sessão é uma opção bem melhor, pois é imprevisível, atinge um tempo limite e varia de acordo com o usuário.</span><span class="sxs-lookup"><span data-stu-id="99df0-364">For a number of technical and social reasons, session ID is a much better fit because a session ID is unpredictable, times out, and varies on a per-user basis.</span></span>|

### <a name="example"></a><span data-ttu-id="99df0-365">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99df0-365">Example</span></span>
<span data-ttu-id="99df0-366">Aqui está o código de saudação necessário toohave em todas as páginas:</span><span class="sxs-lookup"><span data-stu-id="99df0-366">Here's hello code you need toohave in all of your pages:</span></span>
```C#
void Page_Init (object sender, EventArgs e) {
   ViewStateUserKey = Session.SessionID;
   :
}
```

## <span data-ttu-id="99df0-367"><a id="inactivity-lifetime"></a>Configurar sessão para tempo de vida de inatividade</span><span class="sxs-lookup"><span data-stu-id="99df0-367"><a id="inactivity-lifetime"></a>Set up session for inactivity lifetime</span></span>

| <span data-ttu-id="99df0-368">Title</span><span class="sxs-lookup"><span data-stu-id="99df0-368">Title</span></span>                   | <span data-ttu-id="99df0-369">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99df0-369">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99df0-370">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99df0-370">**Component**</span></span>               | <span data-ttu-id="99df0-371">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="99df0-371">Web Application</span></span> | 
| <span data-ttu-id="99df0-372">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99df0-372">**SDL Phase**</span></span>               | <span data-ttu-id="99df0-373">Compilação</span><span class="sxs-lookup"><span data-stu-id="99df0-373">Build</span></span> |  
| <span data-ttu-id="99df0-374">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99df0-374">**Applicable Technologies**</span></span> | <span data-ttu-id="99df0-375">Genérico</span><span class="sxs-lookup"><span data-stu-id="99df0-375">Generic</span></span> |
| <span data-ttu-id="99df0-376">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99df0-376">**Attributes**</span></span>              | <span data-ttu-id="99df0-377">N/D</span><span class="sxs-lookup"><span data-stu-id="99df0-377">N/A</span></span>  |
| <span data-ttu-id="99df0-378">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99df0-378">**References**</span></span>              | <span data-ttu-id="99df0-379">[Propriedade HttpSessionState.Timeout](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="99df0-379">[HttpSessionState.Timeout Property](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span></span> |
| <span data-ttu-id="99df0-380">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99df0-380">**Steps**</span></span> | <span data-ttu-id="99df0-381">Tempo limite da sessão representa Olá eventos que ocorrem quando um usuário não executará qualquer ação em um site da web durante um intervalo (definido pelo servidor web).</span><span class="sxs-lookup"><span data-stu-id="99df0-381">Session timeout represents hello event occurring when a user does not perform any action on a web site during a interval (defined by web server).</span></span> <span data-ttu-id="99df0-382">Olá evento no lado do servidor, altere o status de saudação do hello too'invalid de sessão de usuário ' (por exemplo "não usado mais") e instruir Olá web server toodestroy-lo (excluindo todos os dados contidos nele).</span><span class="sxs-lookup"><span data-stu-id="99df0-382">hello event, on server side, change hello status of hello user session too'invalid' (for example  "not used anymore") and instruct hello web server toodestroy it (deleting all data contained into it).</span></span> <span data-ttu-id="99df0-383">Hello exemplo de código a seguir define Olá tempo limite sessão atributo too15 minutos no arquivo Web. config de saudação.</span><span class="sxs-lookup"><span data-stu-id="99df0-383">hello following code example sets hello timeout session attribute too15 minutes in hello Web.config file.</span></span>|

### <a name="example"></a><span data-ttu-id="99df0-384">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99df0-384">Example</span></span>
<span data-ttu-id="99df0-385">``\`código XML <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration></span><span class="sxs-lookup"><span data-stu-id="99df0-385">``\`XML code <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration></span></span>
```

## <a id="threat-detection"></a>Enable Threat detection on Azure SQL
```

| <span data-ttu-id="99df0-386">Title</span><span class="sxs-lookup"><span data-stu-id="99df0-386">Title</span></span>                   | <span data-ttu-id="99df0-387">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99df0-387">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99df0-388">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99df0-388">**Component**</span></span>               | <span data-ttu-id="99df0-389">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="99df0-389">Web Application</span></span> | 
| <span data-ttu-id="99df0-390">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99df0-390">**SDL Phase**</span></span>               | <span data-ttu-id="99df0-391">Compilação</span><span class="sxs-lookup"><span data-stu-id="99df0-391">Build</span></span> |  
| <span data-ttu-id="99df0-392">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99df0-392">**Applicable Technologies**</span></span> | <span data-ttu-id="99df0-393">Formulários da Web</span><span class="sxs-lookup"><span data-stu-id="99df0-393">Web Forms</span></span> |
| <span data-ttu-id="99df0-394">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99df0-394">**Attributes**</span></span>              | <span data-ttu-id="99df0-395">N/D</span><span class="sxs-lookup"><span data-stu-id="99df0-395">N/A</span></span>  |
| <span data-ttu-id="99df0-396">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99df0-396">**References**</span></span>              | <span data-ttu-id="99df0-397">[Elemento forms para autenticação (Esquema de configuração ASP.NET)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="99df0-397">[forms Element for authentication (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span></span> |
| <span data-ttu-id="99df0-398">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99df0-398">**Steps**</span></span> | <span data-ttu-id="99df0-399">Definir minutos Olá too15 de tempo limite de cookie do tíquete de autenticação de formulários</span><span class="sxs-lookup"><span data-stu-id="99df0-399">Set hello Forms Authentication Ticket cookie timeout too15 minutes</span></span>|

### <a name="example"></a><span data-ttu-id="99df0-400">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99df0-400">Example</span></span>
<span data-ttu-id="99df0-401">``\`código XML <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span><span class="sxs-lookup"><span data-stu-id="99df0-401">``\`XML code <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span></span>
```

| Title                   | Details      |
| ----------------------- | ------------ |
| **Component**               | Web Application | 
| **SDL Phase**               | Build |  
| **Applicable Technologies** | Web Forms, MVC5 |
| **Attributes**              | EnvironmentType - OnPrem |
| **References**              | [asdeqa](https://skf.azurewebsites.net/Mitigations/Details/wefr) |
| **Steps** | When hello web application is Relying Party and ADFS is hello STS, hello lifetime of hello authentication cookies - FedAuth tokens - can be set by hello following configuration in web.config:|

### Example
```XML
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:15:0" />
      <!-- Set requireHttps=true; -->
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:39529/" realm="https://localhost:44302/" reply="https://localhost:44302/" requireHttps="true"/>
      <!--
      Use hello code below tooenable encryption-decryption of claims received from ADFS. Thumbprint value varies based on hello certificate being used.
      <serviceCertificate>
        <certificateReference findValue="4FBBBA33A1D11A9022A5BF3492FF83320007686A" storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" />
      </serviceCertificate>
      -->
    </federationConfiguration>
  </system.identityModel.services>
```

### <a name="example"></a><span data-ttu-id="99df0-402">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99df0-402">Example</span></span>
<span data-ttu-id="99df0-403">Também Olá ADFS emitido o tempo de vida do token de SAML declaração deve ser definido como too15 minutos, executando Olá comando do powershell no servidor ADFS Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="99df0-403">Also hello ADFS issued SAML claim token's lifetime should be set too15 minutes, by executing hello following powershell command on hello ADFS server:</span></span>
```C#
Set-ADFSRelyingPartyTrust -TargetName “<RelyingPartyWebApp>” -ClaimsProviderName @(“Active Directory”) -TokenLifetime 15 -AlwaysRequireAuthentication $true
```

## <span data-ttu-id="99df0-404"><a id="proper-app-logout"></a>Implementar o logout adequado do aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="99df0-404"><a id="proper-app-logout"></a>Implement proper logout from hello application</span></span>

| <span data-ttu-id="99df0-405">Title</span><span class="sxs-lookup"><span data-stu-id="99df0-405">Title</span></span>                   | <span data-ttu-id="99df0-406">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99df0-406">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99df0-407">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99df0-407">**Component**</span></span>               | <span data-ttu-id="99df0-408">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="99df0-408">Web Application</span></span> | 
| <span data-ttu-id="99df0-409">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99df0-409">**SDL Phase**</span></span>               | <span data-ttu-id="99df0-410">Compilação</span><span class="sxs-lookup"><span data-stu-id="99df0-410">Build</span></span> |  
| <span data-ttu-id="99df0-411">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99df0-411">**Applicable Technologies**</span></span> | <span data-ttu-id="99df0-412">Genérico</span><span class="sxs-lookup"><span data-stu-id="99df0-412">Generic</span></span> |
| <span data-ttu-id="99df0-413">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99df0-413">**Attributes**</span></span>              | <span data-ttu-id="99df0-414">N/D</span><span class="sxs-lookup"><span data-stu-id="99df0-414">N/A</span></span>  |
| <span data-ttu-id="99df0-415">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99df0-415">**References**</span></span>              | <span data-ttu-id="99df0-416">N/D</span><span class="sxs-lookup"><span data-stu-id="99df0-416">N/A</span></span>  |
| <span data-ttu-id="99df0-417">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99df0-417">**Steps**</span></span> | <span data-ttu-id="99df0-418">Execute sair adequado do aplicativo hello, quando o usuário pressionar botão de logoff.</span><span class="sxs-lookup"><span data-stu-id="99df0-418">Perform proper Sign Out from hello application, when user presses log out button.</span></span> <span data-ttu-id="99df0-419">Após o logoff, o aplicativo deve destruir a sessão do usuário e também redefinir e anular o valor do cookie de sessão, juntamente com a redefinição e anulação do valor do cookie de autenticação.</span><span class="sxs-lookup"><span data-stu-id="99df0-419">Upon logout, application should destroy user's session, and also reset and nullify session cookie value, along with resetting and nullifying authentication cookie value.</span></span> <span data-ttu-id="99df0-420">Além disso, quando várias sessões estão empatados tooa identidade de usuário único, eles devem ser coletivamente terminados no lado do servidor de saudação no tempo limite ou logoff.</span><span class="sxs-lookup"><span data-stu-id="99df0-420">Also, when multiple sessions are tied tooa single user identity, they must be collectively terminated on hello server side at timeout or logout.</span></span> <span data-ttu-id="99df0-421">Por fim, certifique-se de que a funcionalidade de Logoff esteja disponível em cada página.</span><span class="sxs-lookup"><span data-stu-id="99df0-421">Lastly, ensure that Logout functionality is available on every page.</span></span> |

## <span data-ttu-id="99df0-422"><a id="csrf-api"></a>Atenuar ataques CSRF (solicitação intersite forjada) em APIs da Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="99df0-422"><a id="csrf-api"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>

| <span data-ttu-id="99df0-423">Title</span><span class="sxs-lookup"><span data-stu-id="99df0-423">Title</span></span>                   | <span data-ttu-id="99df0-424">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99df0-424">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99df0-425">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99df0-425">**Component**</span></span>               | <span data-ttu-id="99df0-426">API Web</span><span class="sxs-lookup"><span data-stu-id="99df0-426">Web API</span></span> | 
| <span data-ttu-id="99df0-427">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99df0-427">**SDL Phase**</span></span>               | <span data-ttu-id="99df0-428">Compilação</span><span class="sxs-lookup"><span data-stu-id="99df0-428">Build</span></span> |  
| <span data-ttu-id="99df0-429">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99df0-429">**Applicable Technologies**</span></span> | <span data-ttu-id="99df0-430">Genérico</span><span class="sxs-lookup"><span data-stu-id="99df0-430">Generic</span></span> |
| <span data-ttu-id="99df0-431">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99df0-431">**Attributes**</span></span>              | <span data-ttu-id="99df0-432">N/D</span><span class="sxs-lookup"><span data-stu-id="99df0-432">N/A</span></span>  |
| <span data-ttu-id="99df0-433">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99df0-433">**References**</span></span>              | <span data-ttu-id="99df0-434">N/D</span><span class="sxs-lookup"><span data-stu-id="99df0-434">N/A</span></span>  |
| <span data-ttu-id="99df0-435">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99df0-435">**Steps**</span></span> | <span data-ttu-id="99df0-436">Falsificação de solicitação entre sites (CSRF ou XSRF) é um tipo de ataque em que um invasor pode realizar ações no contexto de segurança de saudação da sessão de um usuário diferente estabelecida em um site da web.</span><span class="sxs-lookup"><span data-stu-id="99df0-436">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in hello security context of a different user's established session on a web site.</span></span> <span data-ttu-id="99df0-437">meta de saudação é toomodify ou excluir o conteúdo, se o site de destino-Olá se basear exclusivamente em cookies de sessão tooauthenticate solicitação recebida.</span><span class="sxs-lookup"><span data-stu-id="99df0-437">hello goal is toomodify or delete content, if hello targeted web site relies exclusively on session cookies tooauthenticate received request.</span></span> <span data-ttu-id="99df0-438">Um invasor pode explorar essa vulnerabilidade obtendo tooload do navegador de um usuário diferente uma URL com um comando de um site vulnerável no qual usuário Olá já estiver conectado.</span><span class="sxs-lookup"><span data-stu-id="99df0-438">An attacker could exploit this vulnerability by getting a different user's browser tooload a URL with a command from a vulnerable site on which hello user is already logged in.</span></span> <span data-ttu-id="99df0-439">Há várias maneiras para um toodo invasor que, como hospedar um site diferente que carrega um recurso de servidor vulnerável hello, ou tooclick de usuário Olá obtendo um link.</span><span class="sxs-lookup"><span data-stu-id="99df0-439">There are many ways for an attacker toodo that, such as by hosting a different web site that loads a resource from hello vulnerable server, or getting hello user tooclick a link.</span></span> <span data-ttu-id="99df0-440">ataque de saudação pode ser evitado se o servidor de saudação envia um cliente toohello token adicionais, requer Olá cliente tooinclude esse token em todas as solicitações futuras e verifica se todas as solicitações futuras incluem um token que pertence toohello sessão atual, como por usando Olá AntiForgeryToken ASP.NET ou ViewState.</span><span class="sxs-lookup"><span data-stu-id="99df0-440">hello attack can be prevented if hello server sends an additional token toohello client, requires hello client tooinclude that token in all future requests, and verifies that all future requests include a token that pertains toohello current session, such as by using hello ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="99df0-441">Title</span><span class="sxs-lookup"><span data-stu-id="99df0-441">Title</span></span>                   | <span data-ttu-id="99df0-442">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99df0-442">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99df0-443">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99df0-443">**Component**</span></span>               | <span data-ttu-id="99df0-444">API Web</span><span class="sxs-lookup"><span data-stu-id="99df0-444">Web API</span></span> | 
| <span data-ttu-id="99df0-445">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99df0-445">**SDL Phase**</span></span>               | <span data-ttu-id="99df0-446">Compilação</span><span class="sxs-lookup"><span data-stu-id="99df0-446">Build</span></span> |  
| <span data-ttu-id="99df0-447">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99df0-447">**Applicable Technologies**</span></span> | <span data-ttu-id="99df0-448">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="99df0-448">MVC5, MVC6</span></span> |
| <span data-ttu-id="99df0-449">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99df0-449">**Attributes**</span></span>              | <span data-ttu-id="99df0-450">N/D</span><span class="sxs-lookup"><span data-stu-id="99df0-450">N/A</span></span>  |
| <span data-ttu-id="99df0-451">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99df0-451">**References**</span></span>              | [<span data-ttu-id="99df0-452">Impedir ataques CSRF (solicitação intersite forjada) em APIs da Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="99df0-452">Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks) |
| <span data-ttu-id="99df0-453">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99df0-453">**Steps**</span></span> | <span data-ttu-id="99df0-454">Anti-CSRF e AJAX: token de formulário de saudação pode ser um problema para solicitações do AJAX, porque uma solicitação AJAX pode enviar dados JSON, não os dados de formulário HTML.</span><span class="sxs-lookup"><span data-stu-id="99df0-454">Anti-CSRF and AJAX: hello form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="99df0-455">Uma solução é tokens de saudação do toosend em um cabeçalho HTTP personalizado.</span><span class="sxs-lookup"><span data-stu-id="99df0-455">One solution is toosend hello tokens in a custom HTTP header.</span></span> <span data-ttu-id="99df0-456">Hello código a seguir usa os tokens de saudação do Razor sintaxe toogenerate e, em seguida, adiciona Olá tokens tooan AJAX solicitação.</span><span class="sxs-lookup"><span data-stu-id="99df0-456">hello following code uses Razor syntax toogenerate hello tokens, and then adds hello tokens tooan AJAX request.</span></span> |

### <a name="example"></a><span data-ttu-id="99df0-457">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99df0-457">Example</span></span>
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

### <a name="example"></a><span data-ttu-id="99df0-458">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99df0-458">Example</span></span>
<span data-ttu-id="99df0-459">Ao processar solicitação Olá, extrai tokens de saudação do cabeçalho de solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="99df0-459">When you process hello request, extract hello tokens from hello request header.</span></span> <span data-ttu-id="99df0-460">Chame Olá AntiForgery.Validate método toovalidate tokens de saudação.</span><span class="sxs-lookup"><span data-stu-id="99df0-460">Then call hello AntiForgery.Validate method toovalidate hello tokens.</span></span> <span data-ttu-id="99df0-461">Olá método Validate lança uma exceção se os tokens de saudação não são válidos.</span><span class="sxs-lookup"><span data-stu-id="99df0-461">hello Validate method throws an exception if hello tokens are not valid.</span></span>
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

### <a name="example"></a><span data-ttu-id="99df0-462">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99df0-462">Example</span></span>
<span data-ttu-id="99df0-463">Anti-CSRF e formulários do ASP.NET MVC - Olá Use método de auxiliar AntiForgeryToken em modos de exibição; colocar um Html.AntiForgeryToken() no formulário hello, por exemplo,</span><span class="sxs-lookup"><span data-stu-id="99df0-463">Anti-CSRF and ASP.NET MVC forms - Use hello AntiForgeryToken helper method on Views; put an Html.AntiForgeryToken() into hello form, for example,</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
}
```

### <a name="example"></a><span data-ttu-id="99df0-464">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99df0-464">Example</span></span>
<span data-ttu-id="99df0-465">exemplo Hello acima produzirá algo semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="99df0-465">hello example above will output something like hello following:</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="99df0-466">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99df0-466">Example</span></span>
<span data-ttu-id="99df0-467">A saudação mesmo momento, visitante de saudação do Html.AntiForgeryToken() oferece um cookie chamado __RequestVerificationToken, com o mesmo valor como valor oculto aleatório Olá mostrado acima de saudação.</span><span class="sxs-lookup"><span data-stu-id="99df0-467">At hello same time, Html.AntiForgeryToken() gives hello visitor a cookie called __RequestVerificationToken, with hello same value as hello random hidden value shown above.</span></span> <span data-ttu-id="99df0-468">Em seguida, toovalidate uma postagem de formulário de entrada, adicione o método de ação do hello [ValidateAntiForgeryToken] filtro toohello destino.</span><span class="sxs-lookup"><span data-stu-id="99df0-468">Next, toovalidate an incoming form post, add hello [ValidateAntiForgeryToken] filter toohello target action method.</span></span> <span data-ttu-id="99df0-469">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="99df0-469">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="99df0-470">Filtro de autorização que verifica se:</span><span class="sxs-lookup"><span data-stu-id="99df0-470">Authorization filter that checks that:</span></span>
* <span data-ttu-id="99df0-471">solicitação de entrada Hello tem um cookie chamado __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="99df0-471">hello incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="99df0-472">Olá solicitação de entrada tem um `Request.Form` entrada chamada __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="99df0-472">hello incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="99df0-473">Esses cookies e `Request.Form` correspondência de valores, supondo que todas as é bem, Olá solicitação passa por como normal.</span><span class="sxs-lookup"><span data-stu-id="99df0-473">These cookie and `Request.Form` values match Assuming all is well, hello request goes through as normal.</span></span> <span data-ttu-id="99df0-474">Mas, se não estiver, uma falha de autorização com a mensagem "Um token antifalsificação necessário não foi fornecido ou era inválido".</span><span class="sxs-lookup"><span data-stu-id="99df0-474">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span>

| <span data-ttu-id="99df0-475">Title</span><span class="sxs-lookup"><span data-stu-id="99df0-475">Title</span></span>                   | <span data-ttu-id="99df0-476">Detalhes</span><span class="sxs-lookup"><span data-stu-id="99df0-476">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="99df0-477">**Componente**</span><span class="sxs-lookup"><span data-stu-id="99df0-477">**Component**</span></span>               | <span data-ttu-id="99df0-478">API Web</span><span class="sxs-lookup"><span data-stu-id="99df0-478">Web API</span></span> | 
| <span data-ttu-id="99df0-479">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="99df0-479">**SDL Phase**</span></span>               | <span data-ttu-id="99df0-480">Compilação</span><span class="sxs-lookup"><span data-stu-id="99df0-480">Build</span></span> |  
| <span data-ttu-id="99df0-481">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="99df0-481">**Applicable Technologies**</span></span> | <span data-ttu-id="99df0-482">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="99df0-482">MVC5, MVC6</span></span> |
| <span data-ttu-id="99df0-483">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="99df0-483">**Attributes**</span></span>              | <span data-ttu-id="99df0-484">Provedor de Identidade - ADFS, Provedor de Identidade - Azure AD</span><span class="sxs-lookup"><span data-stu-id="99df0-484">Identity Provider - ADFS, Identity Provider - Azure AD</span></span> |
| <span data-ttu-id="99df0-485">**Referências**</span><span class="sxs-lookup"><span data-stu-id="99df0-485">**References**</span></span>              | [<span data-ttu-id="99df0-486">Proteger uma API Web com contas individuais e logon local na API Web ASP.NET 2.2</span><span class="sxs-lookup"><span data-stu-id="99df0-486">Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2</span></span>](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api) |
| <span data-ttu-id="99df0-487">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="99df0-487">**Steps**</span></span> | <span data-ttu-id="99df0-488">Se Olá API da Web é protegido usando OAuth 2.0, em seguida, ele espera um token de portador na solicitação cabeçalho e concede acesso toohello solicitação de autorização somente se o token Olá é válido.</span><span class="sxs-lookup"><span data-stu-id="99df0-488">If hello Web API is secured using OAuth 2.0, then it expects a bearer token in Authorization request header and grants access toohello request only if hello token is valid.</span></span> <span data-ttu-id="99df0-489">Ao contrário de autenticação baseada em cookie, navegadores não anexe Olá toorequests de tokens de portador.</span><span class="sxs-lookup"><span data-stu-id="99df0-489">Unlike cookie based authentication, browsers do not attach hello bearer tokens toorequests.</span></span> <span data-ttu-id="99df0-490">Olá solicitando o cliente precisa tooexplicitly anexar o token de portador Olá no cabeçalho de solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="99df0-490">hello requesting client needs tooexplicitly attach hello bearer token in hello request header.</span></span> <span data-ttu-id="99df0-491">Portanto, para APIs Web ASP.NET protegidas usando o OAuth 2.0, os tokens de portador são considerados uma defesa contra ataques de CSRF.</span><span class="sxs-lookup"><span data-stu-id="99df0-491">Therefore, for ASP.NET Web APIs protected using OAuth 2.0, bearer tokens are considered as a defense against CSRF attacks.</span></span> <span data-ttu-id="99df0-492">Observe que se parte do MVC de saudação do aplicativo hello usa autenticação de formulários (ou seja, usa cookies), tokens antifalsificação toobe usado pelo aplicativo de web MVC hello.</span><span class="sxs-lookup"><span data-stu-id="99df0-492">Please note that if hello MVC portion of hello application uses forms authentication (i.e., uses cookies), anti-forgery tokens have toobe used by hello MVC web app.</span></span> |

### <a name="example"></a><span data-ttu-id="99df0-493">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99df0-493">Example</span></span>
<span data-ttu-id="99df0-494">Olá API da Web tem toobe informado toorely apenas em tokens de portador e não em cookies.</span><span class="sxs-lookup"><span data-stu-id="99df0-494">hello Web API has toobe informed toorely ONLY on bearer tokens and not on cookies.</span></span> <span data-ttu-id="99df0-495">Isso pode ser feito por Olá seguinte configuração em `WebApiConfig.Register` método: ' ' configuração de código C-Sharp. SuppressDefaultHostAuthentication(); config. Filters.Add (nova HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span><span class="sxs-lookup"><span data-stu-id="99df0-495">It can be done by hello following configuration in `WebApiConfig.Register` method: ``\`C-Sharp code config.SuppressDefaultHostAuthentication(); config.Filters.Add(new HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span></span>
```
hello SuppressDefaultHostAuthentication method tells Web API tooignore any authentication that happens before hello request reaches hello Web API pipeline, either by IIS or by OWIN middleware. That way, we can restrict Web API tooauthenticate only using bearer tokens.
