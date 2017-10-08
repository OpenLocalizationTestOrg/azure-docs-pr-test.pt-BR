---
title: "aaaAzure AD v2 ASP.NET Web Server Introdução - teste | Microsoft Docs"
description: "Implementando a opção Entrar com uma Conta da Microsoft em uma solução ASP.NET com um aplicativo tradicional baseado em navegador da Web usando o padrão OpenID Connect"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 99c7525b9146605142180962fc2a61b3c953c064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="1ca19-103">Testar seu código</span><span class="sxs-lookup"><span data-stu-id="1ca19-103">Test your code</span></span>

<span data-ttu-id="1ca19-104">Pressione `F5` toorun seu projeto no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1ca19-104">Press `F5` toorun your project in Visual Studio.</span></span> <span data-ttu-id="1ca19-105">Olá navegador será aberto e direcioná-lo muito*http://localhost: {port}* onde você verá Olá *entrar com Microsoft* botão.</span><span class="sxs-lookup"><span data-stu-id="1ca19-105">hello browser will open and direct you too*http://localhost:{port}* where you’ll see hello *Sign in with Microsoft* button.</span></span> <span data-ttu-id="1ca19-106">Vá em frente e clique em toosign no.</span><span class="sxs-lookup"><span data-stu-id="1ca19-106">Go ahead and click it toosign in.</span></span>

<span data-ttu-id="1ca19-107">Quando estiver pronto tootest, use um trabalho ou escolar (Active Directory do Azure) ou um personal (live.com, outlook.com) conta toosign no.</span><span class="sxs-lookup"><span data-stu-id="1ca19-107">When you're ready tootest, use a work or school (Azure Active Directory), or a personal (live.com, outlook.com) account toosign in.</span></span> 

![Janela do navegador Entrar com uma Conta da Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![Janela do navegador Entrar com uma Conta da Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a><span data-ttu-id="1ca19-110">Resultados esperados</span><span class="sxs-lookup"><span data-stu-id="1ca19-110">Expected results</span></span>
<span data-ttu-id="1ca19-111">Depois de entrar, o usuário de saudação é redirecionado toohello home page do seu site da web que é hello URL HTTPS especificado em suas informações de registro de aplicativo no hello Portal de registro de aplicativo do Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1ca19-111">After sign-in, hello user is redirected toohello home page of your web site which is hello HTTPS URL specified in your application registration information in hello Microsoft Application Registration Portal.</span></span> <span data-ttu-id="1ca19-112">Essa página agora mostrará *Olá {User}* e toosign-out de um link e declarações do usuário link toosee hello – que é um controlador de autorização do link toohello criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1ca19-112">This page now shows *Hello {User}* and a link toosign-out, and a link toosee hello user’s claims – which is a link toohello Authorize controller created earlier.</span></span>

### <a name="see-users-claims"></a><span data-ttu-id="1ca19-113">Consultar as declarações do usuário</span><span class="sxs-lookup"><span data-stu-id="1ca19-113">See user's claims</span></span>
<span data-ttu-id="1ca19-114">Selecione as declarações do usuário do hello hiperlink toosee hello.</span><span class="sxs-lookup"><span data-stu-id="1ca19-114">Select hello hyperlink toosee hello user's claims.</span></span> <span data-ttu-id="1ca19-115">Isso leva você toohello controlador e o modo de exibição que só está disponível toousers que são autenticadas.</span><span class="sxs-lookup"><span data-stu-id="1ca19-115">This leads you toohello controller and view that is only available toousers that are authenticated.</span></span>

#### <a name="expected-results"></a><span data-ttu-id="1ca19-116">Resultados esperados</span><span class="sxs-lookup"><span data-stu-id="1ca19-116">Expected results</span></span>
 <span data-ttu-id="1ca19-117">Você deve ver uma tabela que contém propriedades básicas de saudação do usuário Olá conectado:</span><span class="sxs-lookup"><span data-stu-id="1ca19-117">You should see a table containing hello basic properties of hello logged user:</span></span>

| <span data-ttu-id="1ca19-118">Propriedade</span><span class="sxs-lookup"><span data-stu-id="1ca19-118">Property</span></span> | <span data-ttu-id="1ca19-119">Valor</span><span class="sxs-lookup"><span data-stu-id="1ca19-119">Value</span></span> | <span data-ttu-id="1ca19-120">Descrição</span><span class="sxs-lookup"><span data-stu-id="1ca19-120">Description</span></span>|
|---|---|---|
| <span data-ttu-id="1ca19-121">Nome</span><span class="sxs-lookup"><span data-stu-id="1ca19-121">Name</span></span> | <span data-ttu-id="1ca19-122">{Nome completo do usuário}</span><span class="sxs-lookup"><span data-stu-id="1ca19-122">{User Full Name}</span></span> | <span data-ttu-id="1ca19-123">primeiro e o último nome de usuário Olá</span><span class="sxs-lookup"><span data-stu-id="1ca19-123">hello user’s first and last name</span></span>
|<span data-ttu-id="1ca19-124">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="1ca19-124">Username</span></span> | <span>user@domain.com</span>| <span data-ttu-id="1ca19-125">saudação de nome de usuário usado tooidentify usuário de saudação conectado</span><span class="sxs-lookup"><span data-stu-id="1ca19-125">hello username used tooidentify hello logged user</span></span>
| <span data-ttu-id="1ca19-126">Assunto</span><span class="sxs-lookup"><span data-stu-id="1ca19-126">Subject</span></span>| <span data-ttu-id="1ca19-127">{Subject}</span><span class="sxs-lookup"><span data-stu-id="1ca19-127">{Subject}</span></span>|<span data-ttu-id="1ca19-128">Uma cadeia de caracteres toouniquely identificar logon do usuário Olá entre Olá web</span><span class="sxs-lookup"><span data-stu-id="1ca19-128">A string toouniquely identify hello user logon across hello web</span></span>|
| <span data-ttu-id="1ca19-129">ID do locatário</span><span class="sxs-lookup"><span data-stu-id="1ca19-129">Tenant ID</span></span>| <span data-ttu-id="1ca19-130">{Guid}</span><span class="sxs-lookup"><span data-stu-id="1ca19-130">{Guid}</span></span>| <span data-ttu-id="1ca19-131">Um *guid* toouniquely representar a organização do Active Directory do Azure do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="1ca19-131">A *guid* toouniquely represent hello user’s Azure Active Directory organization.</span></span>|

<span data-ttu-id="1ca19-132">Além disso, você verá uma tabela, incluindo todas as declarações de usuário incluídas na solicitação de autenticação.</span><span class="sxs-lookup"><span data-stu-id="1ca19-132">In addition, you will see a table including all user claims included in authentication request.</span></span> <span data-ttu-id="1ca19-133">Para obter uma lista de todas as declarações em um Token de ID e uma explicação, veja este [artigo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "Lista de declarações no Token de ID").</span><span class="sxs-lookup"><span data-stu-id="1ca19-133">For a list of all claims in an Id Token and explanation please see this [article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "List of Claims in Id Token").</span></span>


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a><span data-ttu-id="1ca19-134">Testar o acesso a um método que tem um atributo *[Authorize]* (opcional)</span><span class="sxs-lookup"><span data-stu-id="1ca19-134">Test accessing a method that has an *[Authorize]* attribute (Optional)</span></span>
<span data-ttu-id="1ca19-135">Nesta etapa, você será controlador de teste ao acessar Olá autenticado como um usuário anônimo:</span><span class="sxs-lookup"><span data-stu-id="1ca19-135">In this step, you will test accessing hello Authenticated controller as an anonymous user:</span></span><br/>
<span data-ttu-id="1ca19-136">Selecione Olá vincular toosign-out Olá usuário e o processo de logout Olá concluída.</span><span class="sxs-lookup"><span data-stu-id="1ca19-136">Select hello link toosign-out hello user and complete hello sign-out process.</span></span><br/>
<span data-ttu-id="1ca19-137">Agora no navegador, digite http://localhost: {port} / autenticado tooaccess seu controlador que é protegida com hello `[Authorize]` atributo</span><span class="sxs-lookup"><span data-stu-id="1ca19-137">Now in your browser, type http://localhost:{port}/authenticated tooaccess your controller that is protected with hello `[Authorize]` attribute</span></span>

#### <a name="expected-results"></a><span data-ttu-id="1ca19-138">Resultados esperados</span><span class="sxs-lookup"><span data-stu-id="1ca19-138">Expected results</span></span>
<span data-ttu-id="1ca19-139">Você deve receber um prompt Olá exigindo o modo de exibição tooauthenticate toosee hello.</span><span class="sxs-lookup"><span data-stu-id="1ca19-139">You should receive hello prompt requiring you tooauthenticate toosee hello view.</span></span>

## <a name="additional-information"></a><span data-ttu-id="1ca19-140">Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="1ca19-140">Additional information</span></span>

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a><span data-ttu-id="1ca19-141">Proteger todo o seu site</span><span class="sxs-lookup"><span data-stu-id="1ca19-141">Protect your entire web site</span></span>
<span data-ttu-id="1ca19-142">tooprotect todo o site da web, adicionar Olá `AuthorizeAttribute` muito`GlobalFilters` na `Global.asax` `Application_Start` método:</span><span class="sxs-lookup"><span data-stu-id="1ca19-142">tooprotect your entire web site, add hello `AuthorizeAttribute` too`GlobalFilters` in `Global.asax` `Application_Start` method:</span></span>

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> <span data-ttu-id="1ca19-143">**Como toorestrict os usuários somente uma organização toosign no aplicativo tooyour**</span><span class="sxs-lookup"><span data-stu-id="1ca19-143">**How toorestrict users from only one organization toosign in tooyour application**</span></span>

> <span data-ttu-id="1ca19-144">Por padrão, as contas pessoais (incluindo outlook.com, live.com e outros), bem como contas corporativas e de estudantes de qualquer empresa ou organização que foi integrado ao Active Directory do Azure podem entrar no aplicativo tooyour.</span><span class="sxs-lookup"><span data-stu-id="1ca19-144">By default, personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory can sign-in tooyour application.</span></span> 

> <span data-ttu-id="1ca19-145">Se você quiser que seu aplicativo tooaccept entradas de apenas uma organização do Active Directory do Azure, substitua Olá `Tenant` parâmetro em *Web. config* de `Common` toohello nome do locatário da organização hello – exemplo, *contoso.onmicrosoft.com*. Depois disso, alterar Olá `ValidateIssuer` argumento em sua *classe de inicialização OWIN* muito`true`.</span><span class="sxs-lookup"><span data-stu-id="1ca19-145">If you want your application tooaccept sign-ins from only one Azure Active Directory organization, replace hello `Tenant` parameter in *web.config* from `Common` toohello tenant name of hello organization – example, *contoso.onmicrosoft.com*. After that, change hello `ValidateIssuer` argument in your *OWIN Startup class* too`true`.</span></span>

> <span data-ttu-id="1ca19-146">tooallow usuários de apenas uma lista de organizações específicas, defina `ValidateIssuer` tootrue e use Olá `ValidIssuers` parâmetro toospecify uma lista das organizações.</span><span class="sxs-lookup"><span data-stu-id="1ca19-146">tooallow users from only a list of specific organizations, set `ValidateIssuer` tootrue and use hello `ValidIssuers` parameter toospecify a list of organizations.</span></span>

> <span data-ttu-id="1ca19-147">Outra opção é um método personalizado de tooimplement emissores de saudação toovalidate usando o parâmetro IssuerValidator.</span><span class="sxs-lookup"><span data-stu-id="1ca19-147">Another option is tooimplement a custom method toovalidate hello issuers using IssuerValidator parameter.</span></span> <span data-ttu-id="1ca19-148">Para saber mais sobre `TokenValidationParameters`, veja [este artigo do MSDN](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters").</span><span class="sxs-lookup"><span data-stu-id="1ca19-148">For more information about `TokenValidationParameters`, please see [this](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters MSDN article") MSDN article.</span></span>

