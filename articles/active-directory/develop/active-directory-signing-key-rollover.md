---
title: "aaaSigning substituição de chave no AD do Azure | Microsoft Docs"
description: "Este artigo aborda Olá práticas recomendadas de substituição de chave de assinatura do Azure Active Directory"
services: active-directory
documentationcenter: .net
author: dstrockis
manager: krassk
editor: 
ms.assetid: ed964056-0723-42fe-bb69-e57323b9407f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ac6ade7f3ba2fbd22ea6d447aa5d07a2d6bdd451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a><span data-ttu-id="87cad-103">Substituição de chave de assinatura no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="87cad-103">Signing key rollover in Azure Active Directory</span></span>
<span data-ttu-id="87cad-104">Este tópico discute o que você precisa tooknow sobre as chaves públicas hello são usadas em tokens de segurança do Azure Active Directory (AD do Azure) toosign.</span><span class="sxs-lookup"><span data-stu-id="87cad-104">This topic discusses what you need tooknow about hello public keys that are used in Azure Active Directory (Azure AD) toosign security tokens.</span></span> <span data-ttu-id="87cad-105">É importante toonote que essas chaves são substituídas em uma base periódica e, em caso de emergência, poderia ser acumulados imediatamente.</span><span class="sxs-lookup"><span data-stu-id="87cad-105">It is important toonote that these keys rollover on a periodic basis and, in an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="87cad-106">Todos os aplicativos que usam o AD do Azure devem ser capaz de tooprogrammatically identificador Olá substituição de chave processo ou estabelecer um processo de substituição manual periódica.</span><span class="sxs-lookup"><span data-stu-id="87cad-106">All applications that use Azure AD should be able tooprogrammatically handle hello key rollover process or establish a periodic manual rollover process.</span></span> <span data-ttu-id="87cad-107">Continuar a ler toounderstand como as chaves de saudação funcionam, como tooassess Olá impacto do aplicativo de tooyour de substituição hello e tooupdate seu aplicativo ou estabelecer uma sobreposição da chave de substituição manual periódica processo toohandle, se necessário.</span><span class="sxs-lookup"><span data-stu-id="87cad-107">Continue reading toounderstand how hello keys work, how tooassess hello impact of hello rollover tooyour application and how tooupdate your application or establish a periodic manual rollover process toohandle key rollover if necessary.</span></span>

## <a name="overview-of-signing-keys-in-azure-ad"></a><span data-ttu-id="87cad-108">Visão geral das chaves de assinatura no Azure AD</span><span class="sxs-lookup"><span data-stu-id="87cad-108">Overview of signing keys in Azure AD</span></span>
<span data-ttu-id="87cad-109">AD do Azure usa criptografia de chave pública criada na indústria padrões tooestablish confiança entre ele mesmo e Olá aplicativos que o utilizam.</span><span class="sxs-lookup"><span data-stu-id="87cad-109">Azure AD uses public-key cryptography built on industry standards tooestablish trust between itself and hello applications that use it.</span></span> <span data-ttu-id="87cad-110">Em termos práticos, isso funciona em Olá seguinte caminho: AD do Azure usa uma chave de assinatura que consiste em um par de chaves público e privado.</span><span class="sxs-lookup"><span data-stu-id="87cad-110">In practical terms, this works in hello following way: Azure AD uses a signing key that consists of a public and private key pair.</span></span> <span data-ttu-id="87cad-111">Quando um usuário entra no aplicativo tooan que usa o AD do Azure para autenticação, o AD do Azure cria um token de segurança que contém informações sobre o usuário hello.</span><span class="sxs-lookup"><span data-stu-id="87cad-111">When a user signs in tooan application that uses Azure AD for authentication, Azure AD creates a security token that contains information about hello user.</span></span> <span data-ttu-id="87cad-112">Esse token é assinado pelo AD do Azure usando sua chave privada antes de serem enviado back toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="87cad-112">This token is signed by Azure AD using its private key before it is sent back toohello application.</span></span> <span data-ttu-id="87cad-113">tooverify Olá token seja válido e realmente originado do AD do Azure, o aplicativo hello deve validar a assinatura do token hello usando a chave pública do hello exposto pelo AD do Azure que está contido no locatário Olá [documentodedescobertadeOpenIDConnect](http://openid.net/specs/openid-connect-discovery-1_0.html) ou SAML/WS-Fed [documento de metadados de Federação](active-directory-federation-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="87cad-113">tooverify that hello token is valid and actually originated from Azure AD, hello application must validate hello token’s signature using hello public key exposed by Azure AD that is contained in hello tenant’s [OpenID Connect discovery document](http://openid.net/specs/openid-connect-discovery-1_0.html) or SAML/WS-Fed [federation metadata document](active-directory-federation-metadata.md).</span></span>

<span data-ttu-id="87cad-114">Para fins de segurança do AD do Azure assinatura acumula chave periodicamente e, no caso de saudação de uma emergência, poderia ser acumulados imediatamente.</span><span class="sxs-lookup"><span data-stu-id="87cad-114">For security purposes, Azure AD’s signing key rolls on a periodic basis and, in hello case of an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="87cad-115">Qualquer aplicativo que se integra ao AD do Azure deve ser preparado toohandle um evento de substituição de chave não importa a frequência, isso pode ocorrer.</span><span class="sxs-lookup"><span data-stu-id="87cad-115">Any application that integrates with Azure AD should be prepared toohandle a key rollover event no matter how frequently it may occur.</span></span> <span data-ttu-id="87cad-116">Se não, e seu aplicativo tenta toouse uma assinatura de saudação tooverify chave expiradas em um token, a solicitação de entrada hello falhará.</span><span class="sxs-lookup"><span data-stu-id="87cad-116">If it doesn’t, and your application attempts toouse an expired key tooverify hello signature on a token, hello sign-in request will fail.</span></span>

<span data-ttu-id="87cad-117">Sempre há mais de uma chave válida disponível no documento de descoberta de OpenID Connect hello e documento de metadados de Federação hello.</span><span class="sxs-lookup"><span data-stu-id="87cad-117">There is always more than one valid key available in hello OpenID Connect discovery document and hello federation metadata document.</span></span> <span data-ttu-id="87cad-118">Seu aplicativo deve estar preparado toouse qualquer uma das chaves de saudação especificado no documento hello, porque uma chave pode ser substituída em breve, outra pode ser seu substituição e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="87cad-118">Your application should be prepared toouse any of hello keys specified in hello document, since one key may be rolled soon, another may be its replacement, and so forth.</span></span>

## <a name="how-tooassess-if-your-application-will-be-affected-and-what-toodo-about-it"></a><span data-ttu-id="87cad-119">Como tooassess se seu aplicativo será afetado e quais toodo sobre ele</span><span class="sxs-lookup"><span data-stu-id="87cad-119">How tooassess if your application will be affected and what toodo about it</span></span>
<span data-ttu-id="87cad-120">Como o seu aplicativo lida com a substituição de chave depende de variáveis como tipo de saudação do aplicativo ou o protocolo de identidade e a biblioteca foi usado.</span><span class="sxs-lookup"><span data-stu-id="87cad-120">How your application handles key rollover depends on variables such as hello type of application or what identity protocol and library was used.</span></span> <span data-ttu-id="87cad-121">seções de saudação abaixo avaliam se tipos mais comuns de saudação de aplicativos são afetados pela substituição de chave hello e fornecem orientação sobre como tooupdate Olá substituição automática do aplicativo toosupport ou atualizar manualmente a chave de saudação.</span><span class="sxs-lookup"><span data-stu-id="87cad-121">hello sections below assess whether hello most common types of applications are impacted by hello key rollover and provide guidance on how tooupdate hello application toosupport automatic rollover or manually update hello key.</span></span>

* [<span data-ttu-id="87cad-122">Aplicativos cliente nativos que acessam recursos</span><span class="sxs-lookup"><span data-stu-id="87cad-122">Native client applications accessing resources</span></span>](#nativeclient)
* [<span data-ttu-id="87cad-123">Aplicativos/APIs Web que acessam recursos</span><span class="sxs-lookup"><span data-stu-id="87cad-123">Web applications / APIs accessing resources</span></span>](#webclient)
* [<span data-ttu-id="87cad-124">Aplicativos/APIs Web que protegem recursos e criam usando os Serviços de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="87cad-124">Web applications / APIs protecting resources and built using Azure App Services</span></span>](#appservices)
* [<span data-ttu-id="87cad-125">Aplicativos/APIs Web que protegem recursos usando .NET OWIN OpenID Connect, WS-Fed ou o middleware WindowsAzureActiveDirectoryBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="87cad-125">Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>](#owin)
* [<span data-ttu-id="87cad-126">Aplicativos/APIs Web protegendo recursos usando .NET Core OpenID Connect ou o middleware JwtBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="87cad-126">Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>](#owincore)
* [<span data-ttu-id="87cad-127">Aplicativos/APIs Web que protegem recursos usando o módulo passport-azure-ad do Node.js</span><span class="sxs-lookup"><span data-stu-id="87cad-127">Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>](#passport)
* [<span data-ttu-id="87cad-128">Aplicativos/APIs Web que protegem recursos e que foram criados com o Visual Studio 2015 ou o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="87cad-128">Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>](#vs2015)
* [<span data-ttu-id="87cad-129">Aplicativos/APIs Web que protegem recursos e que foram criados com o Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="87cad-129">Web applications protecting resources and created with Visual Studio 2013</span></span>](#vs2013)
* [<span data-ttu-id="87cad-130">APIs Web que protegem recursos e que foram criados com o Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="87cad-130">Web APIs protecting resources and created with Visual Studio 2013</span></span>](#vs2013_webapi)
* [<span data-ttu-id="87cad-131">Aplicativos Web que protegem recursos e que foram criados com o Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="87cad-131">Web applications protecting resources and created with Visual Studio 2012</span></span>](#vs2012)
* [<span data-ttu-id="87cad-132">Aplicativos Web que protegem recursos e que foram criados com o Visual Studio 2010, 2008 ou usando o Windows Identity Foundation</span><span class="sxs-lookup"><span data-stu-id="87cad-132">Web applications protecting resources and created with Visual Studio 2010, 2008 o using Windows Identity Foundation</span></span>](#vs2010)
* [<span data-ttu-id="87cad-133">Aplicativos da Web / APIs de proteção de recursos usando qualquer outras bibliotecas de ou implementar manualmente qualquer Olá protocolos suportados</span><span class="sxs-lookup"><span data-stu-id="87cad-133">Web applications / APIs protecting resources using any other libraries or manually implementing any of hello supported protocols</span></span>](#other)

<span data-ttu-id="87cad-134">Esta diretriz **não** é aplicável:</span><span class="sxs-lookup"><span data-stu-id="87cad-134">This guidance is **not** applicable for:</span></span>

* <span data-ttu-id="87cad-135">Aplicativos adicionados da Galeria de aplicativo do Azure AD (incluindo personalizada) têm diretrizes separado com relação toosigning chaves.</span><span class="sxs-lookup"><span data-stu-id="87cad-135">Applications added from Azure AD Application Gallery (including Custom) have separate guidance with regards toosigning keys.</span></span> [<span data-ttu-id="87cad-136">Mais informações.</span><span class="sxs-lookup"><span data-stu-id="87cad-136">More information.</span></span>](../active-directory-sso-certs.md)
* <span data-ttu-id="87cad-137">Local aplicativos publicados por meio do proxy de aplicativo não tem tooworry sobre chaves de assinatura.</span><span class="sxs-lookup"><span data-stu-id="87cad-137">On-premises applications published via application proxy don't have tooworry about signing keys.</span></span>

### <span data-ttu-id="87cad-138"><a name="nativeclient"></a>Aplicativos cliente nativos que acessam recursos</span><span class="sxs-lookup"><span data-stu-id="87cad-138"><a name="nativeclient"></a>Native client applications accessing resources</span></span>
<span data-ttu-id="87cad-139">Aplicativos que só acessam recursos (ou seja,</span><span class="sxs-lookup"><span data-stu-id="87cad-139">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="87cad-140">Microsoft Graph, KeyVault, API do Outlook e outras APIs Microsoft) geralmente apenas obter um token e passá-lo pelo proprietário do recurso toohello.</span><span class="sxs-lookup"><span data-stu-id="87cad-140">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along toohello resource owner.</span></span> <span data-ttu-id="87cad-141">Considerando que eles não estão protegendo todos os recursos, eles não inspecionam token hello e, portanto, não é necessário tooensure que está assinado corretamente.</span><span class="sxs-lookup"><span data-stu-id="87cad-141">Given that they are not protecting any resources, they do not inspect hello token and therefore do not need tooensure it is properly signed.</span></span>

<span data-ttu-id="87cad-142">Aplicativos cliente nativo, se o desktop ou mobile, entram nessa categoria e, portanto, não são afetados por substituição hello.</span><span class="sxs-lookup"><span data-stu-id="87cad-142">Native client applications, whether desktop or mobile, fall into this category and are thus not impacted by hello rollover.</span></span>

### <span data-ttu-id="87cad-143"><a name="webclient"></a>Aplicativos/APIs Web que acessam recursos</span><span class="sxs-lookup"><span data-stu-id="87cad-143"><a name="webclient"></a>Web applications / APIs accessing resources</span></span>
<span data-ttu-id="87cad-144">Aplicativos que só acessam recursos (ou seja,</span><span class="sxs-lookup"><span data-stu-id="87cad-144">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="87cad-145">Microsoft Graph, KeyVault, API do Outlook e outras APIs Microsoft) geralmente apenas obter um token e passá-lo pelo proprietário do recurso toohello.</span><span class="sxs-lookup"><span data-stu-id="87cad-145">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along toohello resource owner.</span></span> <span data-ttu-id="87cad-146">Considerando que eles não estão protegendo todos os recursos, eles não inspecionam token hello e, portanto, não é necessário tooensure que está assinado corretamente.</span><span class="sxs-lookup"><span data-stu-id="87cad-146">Given that they are not protecting any resources, they do not inspect hello token and therefore do not need tooensure it is properly signed.</span></span>

<span data-ttu-id="87cad-147">Aplicativos da Web e APIs que estão usando o fluxo de saudação somente de aplicativo web (as credenciais do cliente / certificado do cliente), se enquadram nessa categoria e, portanto, não são afetadas por substituição hello.</span><span class="sxs-lookup"><span data-stu-id="87cad-147">Web applications and web APIs that are using hello app-only flow (client credentials / client certificate), fall into this category and are thus not impacted by hello rollover.</span></span>

### <span data-ttu-id="87cad-148"><a name="appservices"></a>Aplicativos/APIs Web que protegem recursos e criam usando os Serviços de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="87cad-148"><a name="appservices"></a>Web applications / APIs protecting resources and built using Azure App Services</span></span>
<span data-ttu-id="87cad-149">Autenticação dos serviços de aplicativo do Azure funcionalidade de autorização (EasyAuth) já tem substituição de chave Olá lógica necessária toohandle automaticamente.</span><span class="sxs-lookup"><span data-stu-id="87cad-149">Azure App Services' Authentication / Authorization (EasyAuth) functionality already has hello necessary logic toohandle key rollover automatically.</span></span>

### <span data-ttu-id="87cad-150"><a name="owin"></a>Aplicativos/APIs Web que protegem recursos usando .NET OWIN OpenID Connect, WS-Fed ou o middleware WindowsAzureActiveDirectoryBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="87cad-150"><a name="owin"></a>Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>
<span data-ttu-id="87cad-151">Se seu aplicativo estiver usando Olá .NET OWIN OpenID Connect, WS-Fed ou middleware WindowsAzureActiveDirectoryBearerAuthentication, ela já tem substituição de chave Olá lógica necessária toohandle automaticamente.</span><span class="sxs-lookup"><span data-stu-id="87cad-151">If your application is using hello .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="87cad-152">Você pode confirmar que o aplicativo está usando qualquer um desses procurando qualquer Olá trechos de código em seu aplicativo Startup.cs ou Startup.Auth.cs a seguir</span><span class="sxs-lookup"><span data-stu-id="87cad-152">You can confirm that your application is using any of these by looking for any of hello following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseWsFederationAuthentication(
    new WsFederationAuthenticationOptions
    {
     // ...
     });
```
```
 app.UseWindowsAzureActiveDirectoryBearerAuthentication(
     new WindowsAzureActiveDirectoryBearerAuthenticationOptions
     {
     // ...
     });
```

### <span data-ttu-id="87cad-153"><a name="owincore"></a>Aplicativos/APIs Web protegendo recursos usando .NET Core OpenID Connect ou o middleware JwtBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="87cad-153"><a name="owincore"></a>Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>
<span data-ttu-id="87cad-154">Se seu aplicativo estiver usando Olá .NET Core OWIN OpenID Connect ou middleware JwtBearerAuthentication, ela já tem substituição de chave Olá lógica necessária toohandle automaticamente.</span><span class="sxs-lookup"><span data-stu-id="87cad-154">If your application is using hello .NET Core OWIN OpenID Connect  or JwtBearerAuthentication middleware, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="87cad-155">Você pode confirmar que o aplicativo está usando qualquer um desses procurando qualquer Olá trechos de código em seu aplicativo Startup.cs ou Startup.Auth.cs a seguir</span><span class="sxs-lookup"><span data-stu-id="87cad-155">You can confirm that your application is using any of these by looking for any of hello following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseJwtBearerAuthentication(
    new JwtBearerAuthenticationOptions
    {
     // ...
     });
```

### <span data-ttu-id="87cad-156"><a name="passport"></a>Aplicativos/APIs Web que protegem recursos usando o módulo passport-azure-ad do Node.js</span><span class="sxs-lookup"><span data-stu-id="87cad-156"><a name="passport"></a>Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>
<span data-ttu-id="87cad-157">Se seu aplicativo estiver usando o módulo de passport ad Node. js hello, ela já tem substituição de chave Olá lógica necessária toohandle automaticamente.</span><span class="sxs-lookup"><span data-stu-id="87cad-157">If your application is using hello Node.js passport-ad module, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="87cad-158">Você pode confirmar que seu aplicativo passport-ad pesquisando Olá seguindo o trecho de código em app.js seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="87cad-158">You can confirm that your application passport-ad by searching for hello following snippet in your application's app.js</span></span>

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <span data-ttu-id="87cad-159"><a name="vs2015"></a>Aplicativos/APIs Web que protegem recursos e que foram criados com o Visual Studio 2015 ou o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="87cad-159"><a name="vs2015"></a>Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>
<span data-ttu-id="87cad-160">Se seu aplicativo foi criado usando um modelo de aplicativo da web no Visual Studio 2015 ou Visual Studio de 2017 e selecionado **contas de trabalho e escolares** de saudação **alterar autenticação** menu, ele já tem a substituição de chave Olá lógica necessária toohandle automaticamente.</span><span class="sxs-lookup"><span data-stu-id="87cad-160">If your application was built using a web application template in Visual Studio 2015 or Visual Studio 2017 and you selected **Work And School Accounts** from hello **Change Authentication** menu, it already has hello necessary logic toohandle key rollover automatically.</span></span> <span data-ttu-id="87cad-161">Esta lógica, inserida no middleware OWIN OpenID Connect hello, recupera e armazena em cache chaves de saudação do documento de descoberta de OpenID Connect hello e atualiza periodicamente.</span><span class="sxs-lookup"><span data-stu-id="87cad-161">This logic, embedded in hello OWIN OpenID Connect middleware, retrieves and caches hello keys from hello OpenID Connect discovery document and periodically refreshes them.</span></span>

<span data-ttu-id="87cad-162">Se você adicionou a solução de autenticação tooyour manualmente, seu aplicativo pode não ter lógica de substituição de chave necessária hello.</span><span class="sxs-lookup"><span data-stu-id="87cad-162">If you added authentication tooyour solution manually, your application might not have hello necessary key rollover logic.</span></span> <span data-ttu-id="87cad-163">Você precisará toowrite-lo por conta própria ou Olá siga as etapas em [aplicativos Web APIs usando quaisquer outras bibliotecas de ou implementar manualmente qualquer Olá suporte protocolos.](#other).</span><span class="sxs-lookup"><span data-stu-id="87cad-163">You will need toowrite it yourself, or follow hello steps in [Web applications / APIs using any other libraries or manually implementing any of hello supported protocols.](#other).</span></span>

### <span data-ttu-id="87cad-164"><a name="vs2013"></a>Aplicativos/APIs Web que protegem recursos e que foram criados com o Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="87cad-164"><a name="vs2013"></a>Web applications protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="87cad-165">Se seu aplicativo foi criado usando um modelo de aplicativo da web no Visual Studio 2013 e você tiver selecionado **contas organizacionais** de saudação **alterar autenticação** menu, ele já tem Olá necessário toohandle lógica de substituição de chave automaticamente.</span><span class="sxs-lookup"><span data-stu-id="87cad-165">If your application was built using a web application template in Visual Studio 2013 and you selected **Organizational Accounts** from hello **Change Authentication** menu, it already has hello necessary logic toohandle key rollover automatically.</span></span> <span data-ttu-id="87cad-166">Esta lógica armazena o identificador exclusivo da sua organização e hello assinar informações chave em duas tabelas de banco de dados associados ao projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="87cad-166">This logic stores your organization’s unique identifier and hello signing key information in two database tables associated with hello project.</span></span> <span data-ttu-id="87cad-167">Você pode encontrar a cadeia de caracteres de conexão de saudação para banco de dados de saudação no arquivo de Web. config do projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="87cad-167">You can find hello connection string for hello database in hello project’s Web.config file.</span></span>

<span data-ttu-id="87cad-168">Se você adicionou a solução de autenticação tooyour manualmente, seu aplicativo pode não ter lógica de substituição de chave necessária hello.</span><span class="sxs-lookup"><span data-stu-id="87cad-168">If you added authentication tooyour solution manually, your application might not have hello necessary key rollover logic.</span></span> <span data-ttu-id="87cad-169">Você precisará toowrite-lo por conta própria ou Olá siga as etapas em [aplicativos Web APIs usando quaisquer outras bibliotecas de ou implementar manualmente qualquer Olá suporte protocolos.](#other).</span><span class="sxs-lookup"><span data-stu-id="87cad-169">You will need toowrite it yourself, or follow hello steps in [Web applications / APIs using any other libraries or manually implementing any of hello supported protocols.](#other).</span></span>

<span data-ttu-id="87cad-170">Olá, as etapas a seguir o ajudará a verificar se a lógica de saudação está funcionando corretamente em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="87cad-170">hello following steps will help you verify that hello logic is working properly in your application.</span></span>

1. <span data-ttu-id="87cad-171">No Visual Studio 2013, Olá solução aberta e, em seguida, clique em Olá **Server Explorer** guia na janela direita hello.</span><span class="sxs-lookup"><span data-stu-id="87cad-171">In Visual Studio 2013, open hello solution, and then click on hello **Server Explorer** tab on hello right window.</span></span>
2. <span data-ttu-id="87cad-172">Expanda **Conexões de Dados**, **DefaultConnection** e **Tabelas**.</span><span class="sxs-lookup"><span data-stu-id="87cad-172">Expand **Data Connections**, **DefaultConnection**, and then **Tables**.</span></span> <span data-ttu-id="87cad-173">Localizar Olá **IssuingAuthorityKeys** de tabela, clique duas vezes e, em seguida, clique em **Mostrar dados da tabela**.</span><span class="sxs-lookup"><span data-stu-id="87cad-173">Locate hello **IssuingAuthorityKeys** table, right-click it, and then click **Show Table Data**.</span></span>
3. <span data-ttu-id="87cad-174">Em Olá **IssuingAuthorityKeys** da tabela, haverá pelo menos uma linha, que corresponde a toohello o valor de impressão digital da chave de saudação.</span><span class="sxs-lookup"><span data-stu-id="87cad-174">In hello **IssuingAuthorityKeys** table, there will be at least one row, which corresponds toohello thumbprint value for hello key.</span></span> <span data-ttu-id="87cad-175">Exclua todas as linhas na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="87cad-175">Delete any rows in hello table.</span></span>
4. <span data-ttu-id="87cad-176">Saudação de atalho **locatários** de tabela e, em seguida, clique em **Mostrar dados da tabela**.</span><span class="sxs-lookup"><span data-stu-id="87cad-176">Right-click hello **Tenants** table, and then click **Show Table Data**.</span></span>
5. <span data-ttu-id="87cad-177">Em Olá **locatários** da tabela, haverá pelo menos uma linha, que corresponde a tooa identificador do locatário de diretório exclusivo.</span><span class="sxs-lookup"><span data-stu-id="87cad-177">In hello **Tenants** table, there will be at least one row, which corresponds tooa unique directory tenant identifier.</span></span> <span data-ttu-id="87cad-178">Exclua todas as linhas na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="87cad-178">Delete any rows in hello table.</span></span> <span data-ttu-id="87cad-179">Se você não excluir linhas de saudação em ambos os Olá **locatários** tabela e **IssuingAuthorityKeys** tabela, você obterá um erro em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="87cad-179">If you don't delete hello rows in both hello **Tenants** table and **IssuingAuthorityKeys** table, you will get an error at runtime.</span></span>
6. <span data-ttu-id="87cad-180">Compilar e executar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="87cad-180">Build and run hello application.</span></span> <span data-ttu-id="87cad-181">Depois de fazer logon na conta de tooyour, você pode interromper o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="87cad-181">After you have logged in tooyour account, you can stop hello application.</span></span>
7. <span data-ttu-id="87cad-182">Retornar toohello **Server Explorer** e examinar valores Olá Olá **IssuingAuthorityKeys** e **locatários** tabela.</span><span class="sxs-lookup"><span data-stu-id="87cad-182">Return toohello **Server Explorer** and look at hello values in hello **IssuingAuthorityKeys** and **Tenants** table.</span></span> <span data-ttu-id="87cad-183">Você observará que eles foram repopulados automaticamente com informações apropriadas de saudação do documento de metadados de Federação hello.</span><span class="sxs-lookup"><span data-stu-id="87cad-183">You’ll notice that they have been automatically repopulated with hello appropriate information from hello federation metadata document.</span></span>

### <span data-ttu-id="87cad-184"><a name="vs2013"></a>APIs Web que protegem recursos e que foram criados com o Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="87cad-184"><a name="vs2013"></a>Web APIs protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="87cad-185">Se você criou um aplicativo de API da web no Visual Studio 2013 usando o modelo de API da Web hello e, em seguida, selecionado **contas organizacionais** de saudação **alterar autenticação** menu, você já tiver Olá lógica necessária em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="87cad-185">If you created a web API application in Visual Studio 2013 using hello Web API template, and then selected **Organizational Accounts** from hello **Change Authentication** menu, you already have hello necessary logic in your application.</span></span>

<span data-ttu-id="87cad-186">Se você configurou manualmente a autenticação, siga as instruções de saudação abaixo toolearn como tooconfigure tooautomatically sua API da Web atualizar suas informações de chave.</span><span class="sxs-lookup"><span data-stu-id="87cad-186">If you manually configured authentication, follow hello instructions below toolearn how tooconfigure your Web API tooautomatically update its key information.</span></span>

<span data-ttu-id="87cad-187">Olá trecho de código a seguir demonstra como tooget Olá últimas chaves de documento de metadados de Federação Olá e, em seguida, usar Olá [manipulador de Token de JWT](https://msdn.microsoft.com/library/dn205065.aspx) toovalidate token de saudação.</span><span class="sxs-lookup"><span data-stu-id="87cad-187">hello following code snippet demonstrates how tooget hello latest keys from hello federation metadata document, and then use hello [JWT Token Handler](https://msdn.microsoft.com/library/dn205065.aspx) toovalidate hello token.</span></span> <span data-ttu-id="87cad-188">trecho de código Olá pressupõe que você usará seus próprio cache de mecanismo para persistir Olá chave toovalidate futuro tokens do AD do Azure, se estiver em um banco de dados, arquivo de configuração ou em outro lugar.</span><span class="sxs-lookup"><span data-stu-id="87cad-188">hello code snippet assumes that you will use your own caching mechanism for persisting hello key toovalidate future tokens from Azure AD, whether it be in a database, configuration file, or elsewhere.</span></span>

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IdentityModel.Tokens;
using System.Configuration;
using System.Security.Cryptography.X509Certificates;
using System.Xml;
using System.IdentityModel.Metadata;
using System.ServiceModel.Security;
using System.Threading;

namespace JWTValidation
{
    public class JWTValidator
    {
        private string MetadataAddress = "[Your Federation Metadata document address goes here]";

        // Validates hello JWT Token that's part of hello Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in hello Azure Classic Portal]",
                ValidIssuer = "[hello issuer for hello token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache hello signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from hello specified metadata document.
        public List<X509SecurityToken> GetSigningCertificates(string metadataAddress)
        {
            List<X509SecurityToken> tokens = new List<X509SecurityToken>();

            if (metadataAddress == null)
            {
                throw new ArgumentNullException(metadataAddress);
            }

            using (XmlReader metadataReader = XmlReader.Create(metadataAddress))
            {
                MetadataSerializer serializer = new MetadataSerializer()
                {
                    // Do not disable for production code
                    CertificateValidationMode = X509CertificateValidationMode.None
                };

                EntityDescriptor metadata = serializer.ReadMetadata(metadataReader) as EntityDescriptor;

                if (metadata != null)
                {
                    SecurityTokenServiceDescriptor stsd = metadata.RoleDescriptors.OfType<SecurityTokenServiceDescriptor>().First();

                    if (stsd != null)
                    {
                        IEnumerable<X509RawDataKeyIdentifierClause> x509DataClauses = stsd.Keys.Where(key => key.KeyInfo != null && (key.Use == KeyType.Signing || key.Use == KeyType.Unspecified)).
                                                             Select(key => key.KeyInfo.OfType<X509RawDataKeyIdentifierClause>().First());

                        tokens.AddRange(x509DataClauses.Select(token => new X509SecurityToken(new X509Certificate2(token.GetX509RawData()))));
                    }
                    else
                    {
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in hello metadata");
                    }
                }
                else
                {
                    throw new Exception("Invalid Federation Metadata document");
                }
            }
            return tokens;
        }
    }
}
```

### <span data-ttu-id="87cad-189"><a name="vs2012"></a>Aplicativos Web que protegem recursos e que foram criados com o Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="87cad-189"><a name="vs2012"></a>Web applications protecting resources and created with Visual Studio 2012</span></span>
<span data-ttu-id="87cad-190">Se seu aplicativo foi compilado no Visual Studio 2012, você provavelmente usou hello identidade e tooconfigure da ferramenta de acesso a seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="87cad-190">If your application was built in Visual Studio 2012, you probably used hello Identity and Access Tool tooconfigure your application.</span></span> <span data-ttu-id="87cad-191">Também é provável que você está usando Olá [do registro de nome de emissor Validando (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span><span class="sxs-lookup"><span data-stu-id="87cad-191">It’s also likely that you are using hello [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span></span> <span data-ttu-id="87cad-192">Olá VINR é responsável por manter informações sobre provedores de identidade confiável (AD do Azure) e chaves Olá usado toovalidate tokens emitidos por eles.</span><span class="sxs-lookup"><span data-stu-id="87cad-192">hello VINR is responsible for maintaining information about trusted identity providers (Azure AD) and hello keys used toovalidate tokens issued by them.</span></span> <span data-ttu-id="87cad-193">Olá VINR também torna fácil tooautomatically atualização Olá informações de chave armazenadas em um arquivo Web. config baixando hello mais recente federação documento de metadados associado ao diretório, verificando se a configuração hello está desatualizada com hello mais recente documento e atualização Olá toouse Olá nova chave de aplicativo conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="87cad-193">hello VINR also makes it easy tooautomatically update hello key information stored in a Web.config file by downloading hello latest federation metadata document associated with your directory, checking if hello configuration is out of date with hello latest document, and updating hello application toouse hello new key as necessary.</span></span>

<span data-ttu-id="87cad-194">Se você criou seu aplicativo usando qualquer um dos exemplos de código hello ou documentação passo a passo fornecida pela Microsoft, a lógica de substituição de chave Olá já está incluída em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="87cad-194">If you created your application using any of hello code samples or walkthrough documentation provided by Microsoft, hello key rollover logic is already included in your project.</span></span> <span data-ttu-id="87cad-195">Você observará que o código de saudação abaixo já existe em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="87cad-195">You will notice that hello code below already exists in your project.</span></span> <span data-ttu-id="87cad-196">Se seu aplicativo ainda não tiver esta lógica, siga as etapas de saudação abaixo tooadd-lo e tooverify que ele está funcionando corretamente.</span><span class="sxs-lookup"><span data-stu-id="87cad-196">If your application does not already have this logic, follow hello steps below tooadd it and tooverify that it’s working correctly.</span></span>

1. <span data-ttu-id="87cad-197">Em **Solution Explorer**, adicione uma referência toohello **System. IdentityModel** assembly para o projeto apropriado do hello.</span><span class="sxs-lookup"><span data-stu-id="87cad-197">In **Solution Explorer**, add a reference toohello **System.IdentityModel** assembly for hello appropriate project.</span></span>
2. <span data-ttu-id="87cad-198">Olá abrir **Global.asax.cs** de arquivo e adicione o seguinte hello usando diretivas:</span><span class="sxs-lookup"><span data-stu-id="87cad-198">Open hello **Global.asax.cs** file and add hello following using directives:</span></span>
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. <span data-ttu-id="87cad-199">Adicionar Olá após o método toohello **Global.asax.cs** arquivo:</span><span class="sxs-lookup"><span data-stu-id="87cad-199">Add hello following method toohello **Global.asax.cs** file:</span></span>
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. <span data-ttu-id="87cad-200">Invocar Olá **Refreshvalidationsettings** método hello **Application_Start ()** método **Global.asax.cs** conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="87cad-200">Invoke hello **RefreshValidationSettings()** method in hello **Application_Start()** method in **Global.asax.cs** as shown:</span></span>
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

<span data-ttu-id="87cad-201">Depois de seguir essas etapas, Web. config do seu aplicativo será atualizada com informações mais recentes de saudação do documento de metadados de Federação hello, incluindo chaves mais recentes hello.</span><span class="sxs-lookup"><span data-stu-id="87cad-201">Once you have followed these steps, your application’s Web.config will be updated with hello latest information from hello federation metadata document, including hello latest keys.</span></span> <span data-ttu-id="87cad-202">Essa atualização ocorrerá sempre que recicla o pool de aplicativos no IIS; Por padrão o IIS é definido toorecycle aplicativos cada 29 horas.</span><span class="sxs-lookup"><span data-stu-id="87cad-202">This update will occur every time your application pool recycles in IIS; by default IIS is set toorecycle applications every 29 hours.</span></span>

<span data-ttu-id="87cad-203">Siga as próximas etapas, Olá tooverify Olá lógica de substituição de chave está funcionando.</span><span class="sxs-lookup"><span data-stu-id="87cad-203">Follow hello steps below tooverify that hello key rollover logic is working.</span></span>

1. <span data-ttu-id="87cad-204">Depois de ter verificado que seu aplicativo está usando código Olá acima, abra Olá **Web. config** de arquivo e navegue toohello  **<issuerNameRegistry>**  bloco, especificamente procurando Olá algumas linhas a seguir:</span><span class="sxs-lookup"><span data-stu-id="87cad-204">After you have verified that your application is using hello code above, open hello **Web.config** file and navigate toohello **<issuerNameRegistry>** block, specifically looking for hello following few lines:</span></span>
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. <span data-ttu-id="87cad-205">Em Olá  **<add thumbprint=””>**  definir, alterar o valor de impressão digital de hello, substituindo qualquer caractere por um diferente.</span><span class="sxs-lookup"><span data-stu-id="87cad-205">In hello **<add thumbprint=””>** setting, change hello thumbprint value by replacing any character with a different one.</span></span> <span data-ttu-id="87cad-206">Salvar Olá **Web. config** arquivo.</span><span class="sxs-lookup"><span data-stu-id="87cad-206">Save hello **Web.config** file.</span></span>
3. <span data-ttu-id="87cad-207">Criar um aplicativo hello e, em seguida, executá-lo.</span><span class="sxs-lookup"><span data-stu-id="87cad-207">Build hello application, and then run it.</span></span> <span data-ttu-id="87cad-208">Se você pode concluir o processo de entrada hello, seu aplicativo estará atualizando com êxito chave Olá Baixando informações necessárias de saudação do documento de metadados de Federação do diretório.</span><span class="sxs-lookup"><span data-stu-id="87cad-208">If you can complete hello sign-in process, your application is successfully updating hello key by downloading hello required information from your directory’s federation metadata document.</span></span> <span data-ttu-id="87cad-209">Se você estiver tendo problemas para entrar, certifique-se de alterações de saudação em seu aplicativo estão corretas, lendo Olá [tooYour adicionar logon usando o aplicativo Web Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) tópico, ou baixe e inspecione Olá exemplo de código a seguir: [ Aplicativo de nuvem multilocatário para Active Directory do Azure](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span><span class="sxs-lookup"><span data-stu-id="87cad-209">If you are having issues signing in, ensure hello changes in your application are correct by reading hello [Adding Sign-On tooYour Web Application Using Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) topic, or downloading and inspecting hello following code sample: [Multi-Tenant Cloud Application for Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span></span>

### <span data-ttu-id="87cad-210"><a name="vs2010"></a>Os aplicativos Web que protegem recursos e que foram criados com o Visual Studio 2008 ou 2010 e o Windows Identity Foundation (WIF) v1.0 para .NET 3.5</span><span class="sxs-lookup"><span data-stu-id="87cad-210"><a name="vs2010"></a>Web applications protecting resources and created with Visual Studio 2008 or 2010 and Windows Identity Foundation (WIF) v1.0 for .NET 3.5</span></span>
<span data-ttu-id="87cad-211">Se você criou um aplicativo no WIF v 1.0, não há nenhuma atualização do mecanismo fornecido tooautomatically toouse de configuração do aplicativo uma nova chave.</span><span class="sxs-lookup"><span data-stu-id="87cad-211">If you built an application on WIF v1.0, there is no provided mechanism tooautomatically refresh your application’s configuration toouse a new key.</span></span>

* <span data-ttu-id="87cad-212">*A maneira mais fácil* usar Olá FedUtil ferramentas incluídas no hello WIF SDK, que pode recuperar o documento de metadados mais recente hello e atualizar sua configuração.</span><span class="sxs-lookup"><span data-stu-id="87cad-212">*Easiest way* Use hello FedUtil tooling included in hello WIF SDK, which can retrieve hello latest metadata document and update your configuration.</span></span>
* <span data-ttu-id="87cad-213">Atualize seu too.NET aplicativo 4.5, que inclui a versão mais recente de saudação do WIF localizado no namespace do sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="87cad-213">Update your application too.NET 4.5, which includes hello newest version of WIF located in hello System namespace.</span></span> <span data-ttu-id="87cad-214">Você pode usar Olá [do registro de nome de emissor Validando (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform as atualizações automáticas de configuração do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="87cad-214">You can then use hello [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform automatic updates of hello application’s configuration.</span></span>
* <span data-ttu-id="87cad-215">Execute a substituição de um manual conforme as instruções de saudação final Olá deste documento orientação.</span><span class="sxs-lookup"><span data-stu-id="87cad-215">Perform a manual rollover as per hello instructions at hello end of this guidance document.</span></span>

<span data-ttu-id="87cad-216">Instruções toouse Olá FedUtil tooupdate sua configuração:</span><span class="sxs-lookup"><span data-stu-id="87cad-216">Instructions toouse hello FedUtil tooupdate your configuration:</span></span>

1. <span data-ttu-id="87cad-217">Verifique se você tem Olá WIF v 1.0 SDK instalado no computador de desenvolvimento para Visual Studio 2008 ou 2010.</span><span class="sxs-lookup"><span data-stu-id="87cad-217">Verify that you have hello WIF v1.0 SDK installed on your development machine for Visual Studio 2008 or 2010.</span></span> <span data-ttu-id="87cad-218">Você pode [baixá-lo daqui](https://www.microsoft.com/en-us/download/details.aspx?id=4451) se ainda não estiver instalado.</span><span class="sxs-lookup"><span data-stu-id="87cad-218">You can [download it from here](https://www.microsoft.com/en-us/download/details.aspx?id=4451) if you have not yet installed it.</span></span>
2. <span data-ttu-id="87cad-219">No Visual Studio, abra a solução Olá e, em seguida, clique com botão direito Olá aplicável e selecione **atualizar metadados de Federação**.</span><span class="sxs-lookup"><span data-stu-id="87cad-219">In Visual Studio, open hello solution, and then right-click hello applicable project and select **Update federation metadata**.</span></span> <span data-ttu-id="87cad-220">Se essa opção não estiver disponível, FedUtil e/ou Olá WIF v 1.0 SDK não foi instalado.</span><span class="sxs-lookup"><span data-stu-id="87cad-220">If this option is not available, FedUtil and/or hello WIF v1.0 SDK has not been installed.</span></span>
3. <span data-ttu-id="87cad-221">No prompt de saudação, selecione **atualização** toobegin atualizar seus metadados de Federação.</span><span class="sxs-lookup"><span data-stu-id="87cad-221">From hello prompt, select **Update** toobegin updating your federation metadata.</span></span> <span data-ttu-id="87cad-222">Se você tiver um ambiente de servidor toohello de acesso onde o aplicativo hello está hospedado, opcionalmente, você pode usar do FedUtil [Agendador de atualização automática de metadados](https://msdn.microsoft.com/library/ee517272.aspx).</span><span class="sxs-lookup"><span data-stu-id="87cad-222">If you have access toohello server environment where hello application is hosted, you can optionally use FedUtil’s [automatic metadata update scheduler](https://msdn.microsoft.com/library/ee517272.aspx).</span></span>
4. <span data-ttu-id="87cad-223">Clique em **concluir** toocomplete processo de atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="87cad-223">Click **Finish** toocomplete hello update process.</span></span>

### <span data-ttu-id="87cad-224"><a name="other"></a>Aplicativos da Web / APIs de proteção de recursos usando qualquer outras bibliotecas de ou implementar manualmente qualquer Olá protocolos suportados</span><span class="sxs-lookup"><span data-stu-id="87cad-224"><a name="other"></a>Web applications / APIs protecting resources using any other libraries or manually implementing any of hello supported protocols</span></span>
<span data-ttu-id="87cad-225">Se você estiver usando alguma outra biblioteca ou implementado manualmente qualquer um dos protocolos Olá com suporte, você precisará de biblioteca de saudação tooreview ou tooensure sua implementação que Olá chave está sendo recuperado do documento de descoberta de OpenID Connect hello ou hello documento de metadados de Federação.</span><span class="sxs-lookup"><span data-stu-id="87cad-225">If you are using some other library or manually implemented any of hello supported protocols, you'll need tooreview hello library or your implementation tooensure that hello key is being retrieved from either hello OpenID Connect discovery document or hello federation metadata document.</span></span> <span data-ttu-id="87cad-226">Toocheck unidirecional para isso é toodo uma pesquisa em seu código ou o código da biblioteca de saudação para todas as chamadas de documento de descoberta de OpenID tooeither hello ou documento de metadados de Federação hello.</span><span class="sxs-lookup"><span data-stu-id="87cad-226">One way toocheck for this is toodo a search in your code or hello library's code for any calls out tooeither hello OpenID discovery document or hello federation metadata document.</span></span>

<span data-ttu-id="87cad-227">Se eles chave é armazenada em ou codificado no seu aplicativo, você pode manualmente recupere chave hello e ele adequadamente ao executar a substituição de um manual conforme as instruções de saudação final Olá deste documento Guia de atualização.</span><span class="sxs-lookup"><span data-stu-id="87cad-227">If they key is being stored somewhere or hardcoded in your application, you can manually retrieve hello key and update it accordingly by perform a manual rollover as per hello instructions at hello end of this guidance document.</span></span> <span data-ttu-id="87cad-228">**Ele é incentivado fortemente que você aperfeiçoe a substituição automática do aplicativo toosupport** usando qualquer um dos Olá abordagens da estrutura de tópicos neste interrupções futuras do artigo tooavoid e sobrecarga de AD do Azure aumenta o ritmo da substituição ou possui um substituição de emergência fora de banda.</span><span class="sxs-lookup"><span data-stu-id="87cad-228">**It is strongly encouraged that you enhance your application toosupport automatic rollover** using any of hello approaches outline in this article tooavoid future disruptions and overhead if Azure AD increases it's rollover cadence or has an emergency out-of-band rollover.</span></span>

## <a name="how-tootest-your-application-toodetermine-if-it-will-be-affected"></a><span data-ttu-id="87cad-229">Como tootest toodetermine seu aplicativo se serão afetado</span><span class="sxs-lookup"><span data-stu-id="87cad-229">How tootest your application toodetermine if it will be affected</span></span>
<span data-ttu-id="87cad-230">Você pode validar se o aplicativo oferece suporte a substituição da chave automática baixando scripts hello e seguindo as instruções de saudação do [este repositório GitHub.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span><span class="sxs-lookup"><span data-stu-id="87cad-230">You can validate whether your application supports automatic key rollover by downloading hello scripts and following hello instructions in [this GitHub repository.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span></span>

## <a name="how-tooperform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a><span data-ttu-id="87cad-231">Como tooperform uma substituição manual se seu aplicativo não oferece suporte a substituição automática</span><span class="sxs-lookup"><span data-stu-id="87cad-231">How tooperform a manual rollover if you application does not support automatic rollover</span></span>
<span data-ttu-id="87cad-232">Se seu aplicativo **não** suporte a substituição automática, será necessário tooestablish chaves de um processo que periodicamente de assinatura de monitores AD do Azure e executa a substituição de um manual adequadamente.</span><span class="sxs-lookup"><span data-stu-id="87cad-232">If your application does **not** support automatic rollover, you will need tooestablish a process that periodically monitors Azure AD's signing keys and performs a manual rollover accordingly.</span></span> <span data-ttu-id="87cad-233">[Esse repositório GitHub](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contém scripts e instruções sobre como toodo isso.</span><span class="sxs-lookup"><span data-stu-id="87cad-233">[This GitHub repository](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contains scripts and instructions on how toodo this.</span></span>

