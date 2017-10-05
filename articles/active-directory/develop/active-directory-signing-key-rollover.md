---
title: "Substituição da chave de assinatura no Azure AD | Microsoft Docs"
description: "Este artigo descreve as práticas recomendadas de substituição de chave de assinatura para o Azure Active Directory"
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
ms.openlocfilehash: 228bb9058537af1e4eb38207c376c2eb86aee68c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a><span data-ttu-id="42806-103">Substituição de chave de assinatura no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="42806-103">Signing key rollover in Azure Active Directory</span></span>
<span data-ttu-id="42806-104">Este tópico aborda o que você precisa saber sobre as chaves públicas que são usadas no Azure AD (Azure Active Directory) para assinar tokens de segurança.</span><span class="sxs-lookup"><span data-stu-id="42806-104">This topic discusses what you need to know about the public keys that are used in Azure Active Directory (Azure AD) to sign security tokens.</span></span> <span data-ttu-id="42806-105">É importante observar que essas chaves são substituídas em intervalos periódicos e, em caso de emergência, podem ser substituídas imediatamente.</span><span class="sxs-lookup"><span data-stu-id="42806-105">It is important to note that these keys rollover on a periodic basis and, in an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="42806-106">Todos os aplicativos que usam o Azure AD devem ser capazes de manipular programaticamente o processo de substituição de chave ou estabelecer um processo de substituição manual periódica.</span><span class="sxs-lookup"><span data-stu-id="42806-106">All applications that use Azure AD should be able to programmatically handle the key rollover process or establish a periodic manual rollover process.</span></span> <span data-ttu-id="42806-107">Continue lendo para entender como funcionam as chaves, como avaliar o impacto de substituição no seu aplicativo e como atualizar seu aplicativo ou estabelecer um processo de substituição manual periódica para tratar a substituição de chave, se necessário.</span><span class="sxs-lookup"><span data-stu-id="42806-107">Continue reading to understand how the keys work, how to assess the impact of the rollover to your application and how to update your application or establish a periodic manual rollover process to handle key rollover if necessary.</span></span>

## <a name="overview-of-signing-keys-in-azure-ad"></a><span data-ttu-id="42806-108">Visão geral das chaves de assinatura no Azure AD</span><span class="sxs-lookup"><span data-stu-id="42806-108">Overview of signing keys in Azure AD</span></span>
<span data-ttu-id="42806-109">O Azure AD usa criptografia de chave pública criada nos padrões da indústria para estabelecer a confiança entre ela e os aplicativos que a utilizam.</span><span class="sxs-lookup"><span data-stu-id="42806-109">Azure AD uses public-key cryptography built on industry standards to establish trust between itself and the applications that use it.</span></span> <span data-ttu-id="42806-110">Em termos práticos, isso funciona da seguinte maneira: o Azure AD usa uma chave de assinatura que consiste em um par de chaves público e privado.</span><span class="sxs-lookup"><span data-stu-id="42806-110">In practical terms, this works in the following way: Azure AD uses a signing key that consists of a public and private key pair.</span></span> <span data-ttu-id="42806-111">Quando um usuário entra em um aplicativo que usa o Azure AD para autenticação, este cria um token de segurança que contém informações sobre o usuário.</span><span class="sxs-lookup"><span data-stu-id="42806-111">When a user signs in to an application that uses Azure AD for authentication, Azure AD creates a security token that contains information about the user.</span></span> <span data-ttu-id="42806-112">Esse token é assinado pelo Azure AD usando sua chave privada antes de ser enviado para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="42806-112">This token is signed by Azure AD using its private key before it is sent back to the application.</span></span> <span data-ttu-id="42806-113">Para verificar se o token é válido e se realmente se origina do Azure AD, o aplicativo deverá validar a assinatura do token usando a chave pública exposta pelo Azure AD que está contida no [documento de descoberta do OpenID Connect](http://openid.net/specs/openid-connect-discovery-1_0.html) do locatário ou o [documento de metadados federados do locatário SAML/WS-Fed](active-directory-federation-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="42806-113">To verify that the token is valid and actually originated from Azure AD, the application must validate the token’s signature using the public key exposed by Azure AD that is contained in the tenant’s [OpenID Connect discovery document](http://openid.net/specs/openid-connect-discovery-1_0.html) or SAML/WS-Fed [federation metadata document](active-directory-federation-metadata.md).</span></span>

<span data-ttu-id="42806-114">Para fins de segurança, a chave de assinatura do Azure AD é substituída periodicamente e, em caso de emergência, pode ser substituída imediatamente.</span><span class="sxs-lookup"><span data-stu-id="42806-114">For security purposes, Azure AD’s signing key rolls on a periodic basis and, in the case of an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="42806-115">Um aplicativo que se integra ao Azure AD deve estar preparado para lidar com um evento de substituição de chave, independentemente da frequência em que pode ocorrer.</span><span class="sxs-lookup"><span data-stu-id="42806-115">Any application that integrates with Azure AD should be prepared to handle a key rollover event no matter how frequently it may occur.</span></span> <span data-ttu-id="42806-116">Se não tiver, e o aplicativo tentar usar uma chave expirada para verificar a assinatura em um token, a solicitação falhará.</span><span class="sxs-lookup"><span data-stu-id="42806-116">If it doesn’t, and your application attempts to use an expired key to verify the signature on a token, the sign-in request will fail.</span></span>

<span data-ttu-id="42806-117">Sempre há mais de uma chave pública válida disponível no documento de descoberta do OpenID Connect e no documento de metadados de federação.</span><span class="sxs-lookup"><span data-stu-id="42806-117">There is always more than one valid key available in the OpenID Connect discovery document and the federation metadata document.</span></span> <span data-ttu-id="42806-118">O aplicativo deve estar preparado para usar qualquer uma das chaves especificadas no documento, já que uma das chaves pode ser substituída em breve, a outra pode ser a sua substituta e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="42806-118">Your application should be prepared to use any of the keys specified in the document, since one key may be rolled soon, another may be its replacement, and so forth.</span></span>

## <a name="how-to-assess-if-your-application-will-be-affected-and-what-to-do-about-it"></a><span data-ttu-id="42806-119">Como avaliar se o aplicativo será afetado e o que fazer com ele</span><span class="sxs-lookup"><span data-stu-id="42806-119">How to assess if your application will be affected and what to do about it</span></span>
<span data-ttu-id="42806-120">Como o seu aplicativo lida com a substituição de chave depende de variáveis como o tipo de aplicativo ou que protocolo de identidade e biblioteca foi usado.</span><span class="sxs-lookup"><span data-stu-id="42806-120">How your application handles key rollover depends on variables such as the type of application or what identity protocol and library was used.</span></span> <span data-ttu-id="42806-121">As seções a seguir avaliam se os tipos mais comuns de aplicativos são afetados pela substituição de chave e fornecem diretrizes sobre como atualizar o aplicativo para dar suporte à substituição automática ou à atualização manual da chave.</span><span class="sxs-lookup"><span data-stu-id="42806-121">The sections below assess whether the most common types of applications are impacted by the key rollover and provide guidance on how to update the application to support automatic rollover or manually update the key.</span></span>

* [<span data-ttu-id="42806-122">Aplicativos cliente nativos que acessam recursos</span><span class="sxs-lookup"><span data-stu-id="42806-122">Native client applications accessing resources</span></span>](#nativeclient)
* [<span data-ttu-id="42806-123">Aplicativos/APIs Web que acessam recursos</span><span class="sxs-lookup"><span data-stu-id="42806-123">Web applications / APIs accessing resources</span></span>](#webclient)
* [<span data-ttu-id="42806-124">Aplicativos/APIs Web que protegem recursos e criam usando os Serviços de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="42806-124">Web applications / APIs protecting resources and built using Azure App Services</span></span>](#appservices)
* [<span data-ttu-id="42806-125">Aplicativos/APIs Web que protegem recursos usando .NET OWIN OpenID Connect, WS-Fed ou o middleware WindowsAzureActiveDirectoryBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="42806-125">Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>](#owin)
* [<span data-ttu-id="42806-126">Aplicativos/APIs Web protegendo recursos usando .NET Core OpenID Connect ou o middleware JwtBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="42806-126">Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>](#owincore)
* [<span data-ttu-id="42806-127">Aplicativos/APIs Web que protegem recursos usando o módulo passport-azure-ad do Node.js</span><span class="sxs-lookup"><span data-stu-id="42806-127">Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>](#passport)
* [<span data-ttu-id="42806-128">Aplicativos/APIs Web que protegem recursos e que foram criados com o Visual Studio 2015 ou o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="42806-128">Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>](#vs2015)
* [<span data-ttu-id="42806-129">Aplicativos/APIs Web que protegem recursos e que foram criados com o Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="42806-129">Web applications protecting resources and created with Visual Studio 2013</span></span>](#vs2013)
* [<span data-ttu-id="42806-130">APIs Web que protegem recursos e que foram criados com o Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="42806-130">Web APIs protecting resources and created with Visual Studio 2013</span></span>](#vs2013_webapi)
* [<span data-ttu-id="42806-131">Aplicativos Web que protegem recursos e que foram criados com o Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="42806-131">Web applications protecting resources and created with Visual Studio 2012</span></span>](#vs2012)
* [<span data-ttu-id="42806-132">Aplicativos Web que protegem recursos e que foram criados com o Visual Studio 2010, 2008 ou usando o Windows Identity Foundation</span><span class="sxs-lookup"><span data-stu-id="42806-132">Web applications protecting resources and created with Visual Studio 2010, 2008 o using Windows Identity Foundation</span></span>](#vs2010)
* [<span data-ttu-id="42806-133">Aplicativos/APIs Web que protegem recursos usando quaisquer outras bibliotecas ou implementando manualmente qualquer um dos protocolos com suporte</span><span class="sxs-lookup"><span data-stu-id="42806-133">Web applications / APIs protecting resources using any other libraries or manually implementing any of the supported protocols</span></span>](#other)

<span data-ttu-id="42806-134">Esta diretriz **não** é aplicável:</span><span class="sxs-lookup"><span data-stu-id="42806-134">This guidance is **not** applicable for:</span></span>

* <span data-ttu-id="42806-135">Os aplicativos adicionados da Galeria de Aplicativos do Azure AD (incluindo os Personalizados) têm diretrizes separadas em relação às chaves de assinatura.</span><span class="sxs-lookup"><span data-stu-id="42806-135">Applications added from Azure AD Application Gallery (including Custom) have separate guidance with regards to signing keys.</span></span> [<span data-ttu-id="42806-136">Mais informações.</span><span class="sxs-lookup"><span data-stu-id="42806-136">More information.</span></span>](../active-directory-sso-certs.md)
* <span data-ttu-id="42806-137">Os aplicativos locais publicados por meio do proxy de aplicativo não precisam se preocupar com as chaves de assinatura.</span><span class="sxs-lookup"><span data-stu-id="42806-137">On-premises applications published via application proxy don't have to worry about signing keys.</span></span>

### <span data-ttu-id="42806-138"><a name="nativeclient"></a>Aplicativos cliente nativos que acessam recursos</span><span class="sxs-lookup"><span data-stu-id="42806-138"><a name="nativeclient"></a>Native client applications accessing resources</span></span>
<span data-ttu-id="42806-139">Aplicativos que só acessam recursos (ou seja,</span><span class="sxs-lookup"><span data-stu-id="42806-139">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="42806-140">Microsoft Graph, KeyVault, API do Outlook e outras APIs Microsoft), geralmente só obtêm um token e o passam para o proprietário do recurso.</span><span class="sxs-lookup"><span data-stu-id="42806-140">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along to the resource owner.</span></span> <span data-ttu-id="42806-141">Já que eles não estão protegendo recursos, não inspecionam o token e, portanto, não é necessário garantir que ele esteja adequadamente assinado.</span><span class="sxs-lookup"><span data-stu-id="42806-141">Given that they are not protecting any resources, they do not inspect the token and therefore do not need to ensure it is properly signed.</span></span>

<span data-ttu-id="42806-142">Os aplicativos cliente nativos, tanto da área de trabalho como móveis, entram nessa categoria e, portanto, não são afetados pela substituição.</span><span class="sxs-lookup"><span data-stu-id="42806-142">Native client applications, whether desktop or mobile, fall into this category and are thus not impacted by the rollover.</span></span>

### <span data-ttu-id="42806-143"><a name="webclient"></a>Aplicativos/APIs Web que acessam recursos</span><span class="sxs-lookup"><span data-stu-id="42806-143"><a name="webclient"></a>Web applications / APIs accessing resources</span></span>
<span data-ttu-id="42806-144">Aplicativos que só acessam recursos (ou seja,</span><span class="sxs-lookup"><span data-stu-id="42806-144">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="42806-145">Microsoft Graph, KeyVault, API do Outlook e outras APIs Microsoft), geralmente só obtêm um token e o passam para o proprietário do recurso.</span><span class="sxs-lookup"><span data-stu-id="42806-145">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along to the resource owner.</span></span> <span data-ttu-id="42806-146">Já que eles não estão protegendo recursos, não inspecionam o token e, portanto, não é necessário garantir que ele esteja adequadamente assinado.</span><span class="sxs-lookup"><span data-stu-id="42806-146">Given that they are not protecting any resources, they do not inspect the token and therefore do not need to ensure it is properly signed.</span></span>

<span data-ttu-id="42806-147">Os aplicativos Web e as APIs Web que estão usando o fluxo somente para aplicativo (credenciais de cliente/certificado de cliente), entram nessa categoria e, portanto, não são afetados pela substituição.</span><span class="sxs-lookup"><span data-stu-id="42806-147">Web applications and web APIs that are using the app-only flow (client credentials / client certificate), fall into this category and are thus not impacted by the rollover.</span></span>

### <span data-ttu-id="42806-148"><a name="appservices"></a>Aplicativos/APIs Web que protegem recursos e criam usando os Serviços de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="42806-148"><a name="appservices"></a>Web applications / APIs protecting resources and built using Azure App Services</span></span>
<span data-ttu-id="42806-149">A funcionalidade de Autenticação/Autorização (EasyAuth) dos Serviços de Aplicativo do Azure já tem a lógica necessária para tratar a substituição de chave automaticamente.</span><span class="sxs-lookup"><span data-stu-id="42806-149">Azure App Services' Authentication / Authorization (EasyAuth) functionality already has the necessary logic to handle key rollover automatically.</span></span>

### <span data-ttu-id="42806-150"><a name="owin"></a>Aplicativos/APIs Web que protegem recursos usando .NET OWIN OpenID Connect, WS-Fed ou o middleware WindowsAzureActiveDirectoryBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="42806-150"><a name="owin"></a>Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>
<span data-ttu-id="42806-151">Se seu aplicativo estiver usando o .NET OWIN OpenID Connect, WS-Fed ou o middleware WindowsAzureActiveDirectoryBearerAuthentication, ele já terá a lógica necessária para tratar a substituição de chave automaticamente.</span><span class="sxs-lookup"><span data-stu-id="42806-151">If your application is using the .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="42806-152">Você pode confirmar que seu aplicativo está usando qualquer um desses ao procurar qualquer um dos trechos no Startup.cs ou Startup.Auth.cs do seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="42806-152">You can confirm that your application is using any of these by looking for any of the following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

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

### <span data-ttu-id="42806-153"><a name="owincore"></a>Aplicativos/APIs Web protegendo recursos usando .NET Core OpenID Connect ou o middleware JwtBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="42806-153"><a name="owincore"></a>Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>
<span data-ttu-id="42806-154">Se seu aplicativo estiver usando o .NET Core OWIN OpenID Connect ou o middleware JwtBearerAuthentication, ele já terá a lógica necessária para tratar a substituição de chave automaticamente.</span><span class="sxs-lookup"><span data-stu-id="42806-154">If your application is using the .NET Core OWIN OpenID Connect  or JwtBearerAuthentication middleware, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="42806-155">Você pode confirmar que seu aplicativo está usando qualquer um desses ao procurar qualquer um dos trechos no Startup.cs ou Startup.Auth.cs do seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="42806-155">You can confirm that your application is using any of these by looking for any of the following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

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

### <span data-ttu-id="42806-156"><a name="passport"></a>Aplicativos/APIs Web que protegem recursos usando o módulo passport-azure-ad do Node.js</span><span class="sxs-lookup"><span data-stu-id="42806-156"><a name="passport"></a>Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>
<span data-ttu-id="42806-157">Se seu aplicativo estiver usando o módulo passport-ad do Node.js, ele já terá a lógica necessária para tratar a substituição de chave automaticamente.</span><span class="sxs-lookup"><span data-stu-id="42806-157">If your application is using the Node.js passport-ad module, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="42806-158">Você pode confirmar que seu aplicativo tem passport-ad pesquisando o trecho a seguir no app.js do seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="42806-158">You can confirm that your application passport-ad by searching for the following snippet in your application's app.js</span></span>

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <span data-ttu-id="42806-159"><a name="vs2015"></a>Aplicativos/APIs Web que protegem recursos e que foram criados com o Visual Studio 2015 ou o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="42806-159"><a name="vs2015"></a>Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>
<span data-ttu-id="42806-160">Se o aplicativo tiver sido criado usando um modelo de aplicativo Web no Visual Studio 2015 ou no Visual Studio 2017 e você tiver selecionado **Contas Corporativas e de Estudante** no menu **Alterar Autenticação**, ele já terá a lógica necessária para manipular a substituição de chave automaticamente.</span><span class="sxs-lookup"><span data-stu-id="42806-160">If your application was built using a web application template in Visual Studio 2015 or Visual Studio 2017 and you selected **Work And School Accounts** from the **Change Authentication** menu, it already has the necessary logic to handle key rollover automatically.</span></span> <span data-ttu-id="42806-161">Essa lógica, incorporada ao middleware OWIN OpenID Connect, recupera e armazena em cache as chaves de documento de descoberta OpenID Connect e as atualiza periodicamente.</span><span class="sxs-lookup"><span data-stu-id="42806-161">This logic, embedded in the OWIN OpenID Connect middleware, retrieves and caches the keys from the OpenID Connect discovery document and periodically refreshes them.</span></span>

<span data-ttu-id="42806-162">Se você tiver adicionado a autenticação à sua solução manualmente, talvez seu aplicativo não tenha a lógica de substituição de chave necessária.</span><span class="sxs-lookup"><span data-stu-id="42806-162">If you added authentication to your solution manually, your application might not have the necessary key rollover logic.</span></span> <span data-ttu-id="42806-163">Você precisará escrevê-la por conta própria ou seguir as etapas em [Aplicativos/APIs Web que usam quaisquer outras bibliotecas ou que implementam manualmente qualquer um dos protocolos com suporte](#other).</span><span class="sxs-lookup"><span data-stu-id="42806-163">You will need to write it yourself, or follow the steps in [Web applications / APIs using any other libraries or manually implementing any of the supported protocols.](#other).</span></span>

### <span data-ttu-id="42806-164"><a name="vs2013"></a>Aplicativos/APIs Web que protegem recursos e que foram criados com o Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="42806-164"><a name="vs2013"></a>Web applications protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="42806-165">Se seu aplicativo tiver sido criado usando um modelo de aplicativo Web no Visual Studio 2013 e você selecionou **Contas Organizacionais** no menu **Alterar Autenticação**, ele já tem a lógica necessária para tratar da substituição de chave automaticamente.</span><span class="sxs-lookup"><span data-stu-id="42806-165">If your application was built using a web application template in Visual Studio 2013 and you selected **Organizational Accounts** from the **Change Authentication** menu, it already has the necessary logic to handle key rollover automatically.</span></span> <span data-ttu-id="42806-166">Essa lógica armazena o identificador exclusivo da sua organização e as informações de chave de autenticação em duas tabelas de banco de dados associadas ao projeto.</span><span class="sxs-lookup"><span data-stu-id="42806-166">This logic stores your organization’s unique identifier and the signing key information in two database tables associated with the project.</span></span> <span data-ttu-id="42806-167">Você pode encontrar a cadeia de conexão para o banco de dados no arquivo Web.config do projeto.</span><span class="sxs-lookup"><span data-stu-id="42806-167">You can find the connection string for the database in the project’s Web.config file.</span></span>

<span data-ttu-id="42806-168">Se você tiver adicionado a autenticação à sua solução manualmente, talvez seu aplicativo não tenha a lógica de substituição de chave necessária.</span><span class="sxs-lookup"><span data-stu-id="42806-168">If you added authentication to your solution manually, your application might not have the necessary key rollover logic.</span></span> <span data-ttu-id="42806-169">Você precisará escrevê-la por conta própria ou seguir as etapas em [Aplicativos/APIs Web que usam quaisquer outras bibliotecas ou que implementam manualmente qualquer um dos protocolos com suporte](#other).</span><span class="sxs-lookup"><span data-stu-id="42806-169">You will need to write it yourself, or follow the steps in [Web applications / APIs using any other libraries or manually implementing any of the supported protocols.](#other).</span></span>

<span data-ttu-id="42806-170">As etapas a seguir o ajudarão a verificar se a lógica está funcionando corretamente em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="42806-170">The following steps will help you verify that the logic is working properly in your application.</span></span>

1. <span data-ttu-id="42806-171">No Visual Studio 2013, abra a solução e clique na guia **Gerenciador de Servidores** na janela à direita.</span><span class="sxs-lookup"><span data-stu-id="42806-171">In Visual Studio 2013, open the solution, and then click on the **Server Explorer** tab on the right window.</span></span>
2. <span data-ttu-id="42806-172">Expanda **Conexões de Dados**, **DefaultConnection** e **Tabelas**.</span><span class="sxs-lookup"><span data-stu-id="42806-172">Expand **Data Connections**, **DefaultConnection**, and then **Tables**.</span></span> <span data-ttu-id="42806-173">Localize a tabela **IssuingAuthorityKeys**, clique com o botão direito do mouse e clique em **Mostrar Dados da Tabela**.</span><span class="sxs-lookup"><span data-stu-id="42806-173">Locate the **IssuingAuthorityKeys** table, right-click it, and then click **Show Table Data**.</span></span>
3. <span data-ttu-id="42806-174">Na tabela **IssuingAuthorityKeys** , haverá pelo menos uma linha, que corresponde ao valor de impressão digital da chave.</span><span class="sxs-lookup"><span data-stu-id="42806-174">In the **IssuingAuthorityKeys** table, there will be at least one row, which corresponds to the thumbprint value for the key.</span></span> <span data-ttu-id="42806-175">Exclua todas as linhas na tabela.</span><span class="sxs-lookup"><span data-stu-id="42806-175">Delete any rows in the table.</span></span>
4. <span data-ttu-id="42806-176">Clique com botão direito do mouse na tabela **Locatários** e clique em **Mostrar Dados da Tabela**.</span><span class="sxs-lookup"><span data-stu-id="42806-176">Right-click the **Tenants** table, and then click **Show Table Data**.</span></span>
5. <span data-ttu-id="42806-177">Na tabela **Locatários** , haverá pelo menos uma linha, que corresponde a um identificador de locatário de diretório exclusivo.</span><span class="sxs-lookup"><span data-stu-id="42806-177">In the **Tenants** table, there will be at least one row, which corresponds to a unique directory tenant identifier.</span></span> <span data-ttu-id="42806-178">Exclua todas as linhas na tabela.</span><span class="sxs-lookup"><span data-stu-id="42806-178">Delete any rows in the table.</span></span> <span data-ttu-id="42806-179">Se você não excluir as linhas em ambas as tabelas **Locatários** e **IssuingAuthorityKeys**, obterá um erro no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="42806-179">If you don't delete the rows in both the **Tenants** table and **IssuingAuthorityKeys** table, you will get an error at runtime.</span></span>
6. <span data-ttu-id="42806-180">Compile e execute o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="42806-180">Build and run the application.</span></span> <span data-ttu-id="42806-181">Depois de entrar na sua conta, você poderá interromper o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="42806-181">After you have logged in to your account, you can stop the application.</span></span>
7. <span data-ttu-id="42806-182">Volte para o **Gerenciador de Servidores** e examine os valores das tabelas **IssuingAuthorityKeys** e **Locatários**.</span><span class="sxs-lookup"><span data-stu-id="42806-182">Return to the **Server Explorer** and look at the values in the **IssuingAuthorityKeys** and **Tenants** table.</span></span> <span data-ttu-id="42806-183">Você notará que eles foram repopulados automaticamente com as informações apropriadas do documento de metadados federados.</span><span class="sxs-lookup"><span data-stu-id="42806-183">You’ll notice that they have been automatically repopulated with the appropriate information from the federation metadata document.</span></span>

### <span data-ttu-id="42806-184"><a name="vs2013"></a>APIs Web que protegem recursos e que foram criados com o Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="42806-184"><a name="vs2013"></a>Web APIs protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="42806-185">Se você tiver criado um aplicativo de API Web usando um modelo de aplicativo de API Web no Visual Studio 2013 e selecionou **Contas Organizacionais** no menu **Alterar Autenticação**, já terá a lógica necessária no seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="42806-185">If you created a web API application in Visual Studio 2013 using the Web API template, and then selected **Organizational Accounts** from the **Change Authentication** menu, you already have the necessary logic in your application.</span></span>

<span data-ttu-id="42806-186">Se você configurou a autenticação manualmente, siga as instruções abaixo para saber como configurar sua API Web para atualizar as informações de chave automaticamente.</span><span class="sxs-lookup"><span data-stu-id="42806-186">If you manually configured authentication, follow the instructions below to learn how to configure your Web API to automatically update its key information.</span></span>

<span data-ttu-id="42806-187">O trecho de código a seguir demonstra como obter as últimas chaves de documento de metadados federados e usar o [Manipulador de Token JWT](https://msdn.microsoft.com/library/dn205065.aspx) para validar o token.</span><span class="sxs-lookup"><span data-stu-id="42806-187">The following code snippet demonstrates how to get the latest keys from the federation metadata document, and then use the [JWT Token Handler](https://msdn.microsoft.com/library/dn205065.aspx) to validate the token.</span></span> <span data-ttu-id="42806-188">O trecho de código pressupõe que você usará seu próprio mecanismo de cache para persistir a chave e validar futuros tokens do Azure AD, seja em um banco de dados, em um arquivo de configuração ou em outro lugar.</span><span class="sxs-lookup"><span data-stu-id="42806-188">The code snippet assumes that you will use your own caching mechanism for persisting the key to validate future tokens from Azure AD, whether it be in a database, configuration file, or elsewhere.</span></span>

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

        // Validates the JWT Token that's part of the Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in the Azure Classic Portal]",
                ValidIssuer = "[The issuer for the token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache the signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from the specified metadata document.
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
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in the metadata");
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

### <span data-ttu-id="42806-189"><a name="vs2012"></a>Aplicativos Web que protegem recursos e que foram criados com o Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="42806-189"><a name="vs2012"></a>Web applications protecting resources and created with Visual Studio 2012</span></span>
<span data-ttu-id="42806-190">Se seu aplicativo foi criado no Visual Studio 2012, você provavelmente usou a Ferramenta de Identidade e Acesso para configurar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="42806-190">If your application was built in Visual Studio 2012, you probably used the Identity and Access Tool to configure your application.</span></span> <span data-ttu-id="42806-191">Também é provável que você esteja usando o [VINR (registro de nome de emissor validador)](https://msdn.microsoft.com/library/dn205067.aspx).</span><span class="sxs-lookup"><span data-stu-id="42806-191">It’s also likely that you are using the [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span></span> <span data-ttu-id="42806-192">O VINR é responsável por manter informações sobre os provedores de identidade confiável (Azure AD) e as chaves usadas para validar tokens emitidos por eles.</span><span class="sxs-lookup"><span data-stu-id="42806-192">The VINR is responsible for maintaining information about trusted identity providers (Azure AD) and the keys used to validate tokens issued by them.</span></span> <span data-ttu-id="42806-193">O VINR também facilita a atualização automática das informações fundamentais armazenadas em um arquivo Web.config baixando o documento de metadados federados mais recente associado ao seu diretório, verificando se a configuração está desatualizada em relação ao documento mais recente e atualizando o aplicativo para usar a nova chave conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="42806-193">The VINR also makes it easy to automatically update the key information stored in a Web.config file by downloading the latest federation metadata document associated with your directory, checking if the configuration is out of date with the latest document, and updating the application to use the new key as necessary.</span></span>

<span data-ttu-id="42806-194">Se você criou seu aplicativo usando um dos exemplos de código ou documentação passo a passo fornecidos pela Microsoft, a lógica de substituição de chave já estará incluída no seu projeto.</span><span class="sxs-lookup"><span data-stu-id="42806-194">If you created your application using any of the code samples or walkthrough documentation provided by Microsoft, the key rollover logic is already included in your project.</span></span> <span data-ttu-id="42806-195">Você notará que o código a seguir já existe em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="42806-195">You will notice that the code below already exists in your project.</span></span> <span data-ttu-id="42806-196">Se seu aplicativo não tiver essa lógica, siga as etapas abaixo para adicioná-la e verificar se ela está funcionando corretamente.</span><span class="sxs-lookup"><span data-stu-id="42806-196">If your application does not already have this logic, follow the steps below to add it and to verify that it’s working correctly.</span></span>

1. <span data-ttu-id="42806-197">No **Gerenciador de Soluções**, adicione uma referência ao assembly **System.IdentityModel** ao projeto apropriado.</span><span class="sxs-lookup"><span data-stu-id="42806-197">In **Solution Explorer**, add a reference to the **System.IdentityModel** assembly for the appropriate project.</span></span>
2. <span data-ttu-id="42806-198">Abra o arquivo **Global.asax.cs** e adicione o seguinte usando diretivas:</span><span class="sxs-lookup"><span data-stu-id="42806-198">Open the **Global.asax.cs** file and add the following using directives:</span></span>
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. <span data-ttu-id="42806-199">Adicione o seguinte método ao arquivo **Global.asax.cs** :</span><span class="sxs-lookup"><span data-stu-id="42806-199">Add the following method to the **Global.asax.cs** file:</span></span>
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. <span data-ttu-id="42806-200">Invoque o método **RefreshValidationSettings()** no método **Application_Start()** em **Global.asax.cs** conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="42806-200">Invoke the **RefreshValidationSettings()** method in the **Application_Start()** method in **Global.asax.cs** as shown:</span></span>
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

<span data-ttu-id="42806-201">Depois que você tiver seguido as etapas, o Web.config do seu aplicativo será atualizado com as últimas informações do documento de metadados federados, incluindo as últimas chaves.</span><span class="sxs-lookup"><span data-stu-id="42806-201">Once you have followed these steps, your application’s Web.config will be updated with the latest information from the federation metadata document, including the latest keys.</span></span> <span data-ttu-id="42806-202">Essa atualização ocorrerá sempre que o pool de aplicativos for reciclado no IIS. Por padrão, o IIS é definido para reciclar aplicativos a cada 29 horas.</span><span class="sxs-lookup"><span data-stu-id="42806-202">This update will occur every time your application pool recycles in IIS; by default IIS is set to recycle applications every 29 hours.</span></span>

<span data-ttu-id="42806-203">Siga as etapas abaixo para verificar se a lógica de substituição de chave está funcionando.</span><span class="sxs-lookup"><span data-stu-id="42806-203">Follow the steps below to verify that the key rollover logic is working.</span></span>

1. <span data-ttu-id="42806-204">Após ter verificado que seu aplicativo está usando o código acima, abra o arquivo **Web.config** e navegue até o bloco **<issuerNameRegistry>** procurando especificamente as poucas linhas abaixo:</span><span class="sxs-lookup"><span data-stu-id="42806-204">After you have verified that your application is using the code above, open the **Web.config** file and navigate to the **<issuerNameRegistry>** block, specifically looking for the following few lines:</span></span>
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. <span data-ttu-id="42806-205">Na tabela **<add thumbprint=””>** , altere o valor de impressão digital, substituindo um caractere por um diferente.</span><span class="sxs-lookup"><span data-stu-id="42806-205">In the **<add thumbprint=””>** setting, change the thumbprint value by replacing any character with a different one.</span></span> <span data-ttu-id="42806-206">Salve o arquivo **Web.config** .</span><span class="sxs-lookup"><span data-stu-id="42806-206">Save the **Web.config** file.</span></span>
3. <span data-ttu-id="42806-207">Crie o aplicativo e o execute.</span><span class="sxs-lookup"><span data-stu-id="42806-207">Build the application, and then run it.</span></span> <span data-ttu-id="42806-208">Se você consegue completar o processo de logon, seu aplicativo está atualizando a chave com êxito baixando as informações necessárias do documento de metadados federados do diretório.</span><span class="sxs-lookup"><span data-stu-id="42806-208">If you can complete the sign-in process, your application is successfully updating the key by downloading the required information from your directory’s federation metadata document.</span></span> <span data-ttu-id="42806-209">Se você estiver tendo problemas ao entrar, verifique se as alterações em seu aplicativo estão corretas lendo o tópico [Adicionando logon ao seu aplicativo Web usando o Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) ou baixando e inspecionando o seguinte exemplo de código: [Aplicativo de nuvem multilocatário do Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span><span class="sxs-lookup"><span data-stu-id="42806-209">If you are having issues signing in, ensure the changes in your application are correct by reading the [Adding Sign-On to Your Web Application Using Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) topic, or downloading and inspecting the following code sample: [Multi-Tenant Cloud Application for Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span></span>

### <span data-ttu-id="42806-210"><a name="vs2010"></a>Os aplicativos Web que protegem recursos e que foram criados com o Visual Studio 2008 ou 2010 e o Windows Identity Foundation (WIF) v1.0 para .NET 3.5</span><span class="sxs-lookup"><span data-stu-id="42806-210"><a name="vs2010"></a>Web applications protecting resources and created with Visual Studio 2008 or 2010 and Windows Identity Foundation (WIF) v1.0 for .NET 3.5</span></span>
<span data-ttu-id="42806-211">Se você criou um aplicativo no WIF v 1.0, nenhum mecanismo foi fornecido para atualizar automaticamente a configuração do seu aplicativo e usar uma nova chave.</span><span class="sxs-lookup"><span data-stu-id="42806-211">If you built an application on WIF v1.0, there is no provided mechanism to automatically refresh your application’s configuration to use a new key.</span></span>

* <span data-ttu-id="42806-212">*Maneira mais fácil* Use a ferramenta FedUtil incluída no SDK do WIF, que pode recuperar o documento de metadados mais recente e atualizar sua configuração.</span><span class="sxs-lookup"><span data-stu-id="42806-212">*Easiest way* Use the FedUtil tooling included in the WIF SDK, which can retrieve the latest metadata document and update your configuration.</span></span>
* <span data-ttu-id="42806-213">Atualize seu aplicativo para .NET 4.5, que inclui a versão mais recente do WIF localizado no namespace System.</span><span class="sxs-lookup"><span data-stu-id="42806-213">Update your application to .NET 4.5, which includes the newest version of WIF located in the System namespace.</span></span> <span data-ttu-id="42806-214">Você pode usar o [VINR (registro de nome de emissor validador)](https://msdn.microsoft.com/library/dn205067.aspx) para executar as atualizações automáticas da configuração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="42806-214">You can then use the [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) to perform automatic updates of the application’s configuration.</span></span>
* <span data-ttu-id="42806-215">Execute uma substituição manual de acordo com as instruções ao final deste documento de diretrizes.</span><span class="sxs-lookup"><span data-stu-id="42806-215">Perform a manual rollover as per the instructions at the end of this guidance document.</span></span>

<span data-ttu-id="42806-216">Instruções para usar o FedUtil para atualizar sua configuração:</span><span class="sxs-lookup"><span data-stu-id="42806-216">Instructions to use the FedUtil to update your configuration:</span></span>

1. <span data-ttu-id="42806-217">Verifique se você tem o SDK do WIF v 1.0 instalado na máquina de desenvolvimento para o Visual Studio 2008 ou 2010.</span><span class="sxs-lookup"><span data-stu-id="42806-217">Verify that you have the WIF v1.0 SDK installed on your development machine for Visual Studio 2008 or 2010.</span></span> <span data-ttu-id="42806-218">Você pode [baixá-lo daqui](https://www.microsoft.com/en-us/download/details.aspx?id=4451) se ainda não estiver instalado.</span><span class="sxs-lookup"><span data-stu-id="42806-218">You can [download it from here](https://www.microsoft.com/en-us/download/details.aspx?id=4451) if you have not yet installed it.</span></span>
2. <span data-ttu-id="42806-219">No Visual Studio, abra a solução, clique com o botão direito do mouse no projeto aplicável e selecione **Atualizar metadados federados**.</span><span class="sxs-lookup"><span data-stu-id="42806-219">In Visual Studio, open the solution, and then right-click the applicable project and select **Update federation metadata**.</span></span> <span data-ttu-id="42806-220">Se essa opção não estiver disponível, o FedUtil e/ou o WIF v 1.0 SDK não foram instalados.</span><span class="sxs-lookup"><span data-stu-id="42806-220">If this option is not available, FedUtil and/or the WIF v1.0 SDK has not been installed.</span></span>
3. <span data-ttu-id="42806-221">No aviso, selecione **Atualizar** para começar a atualizar os metadados federados.</span><span class="sxs-lookup"><span data-stu-id="42806-221">From the prompt, select **Update** to begin updating your federation metadata.</span></span> <span data-ttu-id="42806-222">Se você tiver acesso ao ambiente de servidor onde o aplicativo está hospedado, você pode opcionalmente usar o [agendador de atualização automática de metadados](https://msdn.microsoft.com/library/ee517272.aspx)do FedUtil.</span><span class="sxs-lookup"><span data-stu-id="42806-222">If you have access to the server environment where the application is hosted, you can optionally use FedUtil’s [automatic metadata update scheduler](https://msdn.microsoft.com/library/ee517272.aspx).</span></span>
4. <span data-ttu-id="42806-223">Clique em **Concluir** para concluir o processo de atualização.</span><span class="sxs-lookup"><span data-stu-id="42806-223">Click **Finish** to complete the update process.</span></span>

### <span data-ttu-id="42806-224"><a name="other"></a>Aplicativos/APIs Web que protegem recursos usando quaisquer outras bibliotecas ou implementando manualmente qualquer um dos protocolos com suporte</span><span class="sxs-lookup"><span data-stu-id="42806-224"><a name="other"></a>Web applications / APIs protecting resources using any other libraries or manually implementing any of the supported protocols</span></span>
<span data-ttu-id="42806-225">Se você estiver usando alguma outra biblioteca ou se tiver implementado manualmente qualquer um dos protocolos com suporte, precisará examinar a biblioteca ou a implementação para garantir que a chave esteja sendo recuperada do documento de descoberta OpenID Connect ou do documento de metadados de federação.</span><span class="sxs-lookup"><span data-stu-id="42806-225">If you are using some other library or manually implemented any of the supported protocols, you'll need to review the library or your implementation to ensure that the key is being retrieved from either the OpenID Connect discovery document or the federation metadata document.</span></span> <span data-ttu-id="42806-226">Uma maneira de verificar isso é fazer uma pesquisa no seu código ou no código da biblioteca de quaisquer chamadas para o documento de descoberta OpenID ou para o documento de metadados de federação.</span><span class="sxs-lookup"><span data-stu-id="42806-226">One way to check for this is to do a search in your code or the library's code for any calls out to either the OpenID discovery document or the federation metadata document.</span></span>

<span data-ttu-id="42806-227">Se a chave estiver sendo armazenada em algum lugar ou codificada em seu aplicativo, você poderá recuperar manualmente a chave e atualizá-la de forma adequada ao executar uma substituição manual de acordo com as instruções ao final deste documento de diretrizes.</span><span class="sxs-lookup"><span data-stu-id="42806-227">If they key is being stored somewhere or hardcoded in your application, you can manually retrieve the key and update it accordingly by perform a manual rollover as per the instructions at the end of this guidance document.</span></span> <span data-ttu-id="42806-228">**É altamente incentivado que você aprimore seu aplicativo para dar suporte à substituição automática** usando qualquer um dos tópicos de abordagens neste artigo para evitar transtornos futuros e sobrecarga caso o Azure AD aumente a cadência de sua substituição ou tenha uma substituição fora de banda de emergência.</span><span class="sxs-lookup"><span data-stu-id="42806-228">**It is strongly encouraged that you enhance your application to support automatic rollover** using any of the approaches outline in this article to avoid future disruptions and overhead if Azure AD increases it's rollover cadence or has an emergency out-of-band rollover.</span></span>

## <a name="how-to-test-your-application-to-determine-if-it-will-be-affected"></a><span data-ttu-id="42806-229">Como testar o aplicativo para determinar se ele será afetado</span><span class="sxs-lookup"><span data-stu-id="42806-229">How to test your application to determine if it will be affected</span></span>
<span data-ttu-id="42806-230">Você pode validar se o aplicativo oferece suporte à substituição automática da chave baixando os scripts e seguindo as instruções [neste repositório GitHub.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span><span class="sxs-lookup"><span data-stu-id="42806-230">You can validate whether your application supports automatic key rollover by downloading the scripts and following the instructions in [this GitHub repository.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span></span>

## <a name="how-to-perform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a><span data-ttu-id="42806-231">Como executar uma substituição manual se seu aplicativo não oferecer suporte à substituição automática</span><span class="sxs-lookup"><span data-stu-id="42806-231">How to perform a manual rollover if you application does not support automatic rollover</span></span>
<span data-ttu-id="42806-232">Se seu aplicativo **não** der suporte à substituição automática, será necessário estabelecer um processo que monitore periodicamente as chaves de assinatura do Azure AD e execute uma substituição manual de forma adequada.</span><span class="sxs-lookup"><span data-stu-id="42806-232">If your application does **not** support automatic rollover, you will need to establish a process that periodically monitors Azure AD's signing keys and performs a manual rollover accordingly.</span></span> <span data-ttu-id="42806-233">[Este repositório GitHub](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contém scripts e instruções sobre como fazer isso.</span><span class="sxs-lookup"><span data-stu-id="42806-233">[This GitHub repository](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contains scripts and instructions on how to do this.</span></span>

