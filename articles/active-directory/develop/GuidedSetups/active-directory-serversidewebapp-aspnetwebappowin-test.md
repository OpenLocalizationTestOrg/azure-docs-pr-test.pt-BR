---
title: "Introdução ao servidor Web ASP.NET no Azure AD v2 – Teste | Microsoft Docs"
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
ms.openlocfilehash: 00cb963e85111274c36c3a84489894811ad2dabd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="2c692-103">Testar seu código</span><span class="sxs-lookup"><span data-stu-id="2c692-103">Test your code</span></span>

<span data-ttu-id="2c692-104">Pressione `F5` para executar o projeto no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2c692-104">Press `F5` to run your project in Visual Studio.</span></span> <span data-ttu-id="2c692-105">O navegador será aberto e direcionará você para *http://localhost:{port}*, em que você verá o botão *Entrar com uma conta da Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="2c692-105">The browser will open and direct you to *http://localhost:{port}* where you’ll see the *Sign in with Microsoft* button.</span></span> <span data-ttu-id="2c692-106">Vá em frente e clique nele para entrar.</span><span class="sxs-lookup"><span data-stu-id="2c692-106">Go ahead and click it to sign in.</span></span>

<span data-ttu-id="2c692-107">Quando estiver pronto para testar, use uma conta corporativa ou de estudante (Azure Active Directory) ou uma conta pessoal (live.com, outlook.com) para se conectar.</span><span class="sxs-lookup"><span data-stu-id="2c692-107">When you're ready to test, use a work or school (Azure Active Directory), or a personal (live.com, outlook.com) account to sign in.</span></span> 

![Janela do navegador Entrar com uma Conta da Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![Janela do navegador Entrar com uma Conta da Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a><span data-ttu-id="2c692-110">Resultados esperados</span><span class="sxs-lookup"><span data-stu-id="2c692-110">Expected results</span></span>
<span data-ttu-id="2c692-111">Depois de se conectar, o usuário é redirecionado para a home page do site, que é a URL HTTPS especificada nas informações de registro do aplicativo no Portal de Registro de Aplicativos da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2c692-111">After sign-in, the user is redirected to the home page of your web site which is the HTTPS URL specified in your application registration information in the Microsoft Application Registration Portal.</span></span> <span data-ttu-id="2c692-112">Essa página agora mostra *Olá, {User}* e um link para a saída, além de um link para consultar as declarações do usuário – que é um link para o controlador Autorizar criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2c692-112">This page now shows *Hello {User}* and a link to sign-out, and a link to see the user’s claims – which is a link to the Authorize controller created earlier.</span></span>

### <a name="see-users-claims"></a><span data-ttu-id="2c692-113">Consultar as declarações do usuário</span><span class="sxs-lookup"><span data-stu-id="2c692-113">See user's claims</span></span>
<span data-ttu-id="2c692-114">Selecione o hiperlink para consultar as declarações do usuário.</span><span class="sxs-lookup"><span data-stu-id="2c692-114">Select the hyperlink to see the user's claims.</span></span> <span data-ttu-id="2c692-115">Isso leva você para o controlador e a exibição que está disponível somente para usuários autenticados.</span><span class="sxs-lookup"><span data-stu-id="2c692-115">This leads you to the controller and view that is only available to users that are authenticated.</span></span>

#### <a name="expected-results"></a><span data-ttu-id="2c692-116">Resultados esperados</span><span class="sxs-lookup"><span data-stu-id="2c692-116">Expected results</span></span>
 <span data-ttu-id="2c692-117">Você deverá ver uma tabela que contém as propriedades básicas do usuário conectado:</span><span class="sxs-lookup"><span data-stu-id="2c692-117">You should see a table containing the basic properties of the logged user:</span></span>

| <span data-ttu-id="2c692-118">Propriedade</span><span class="sxs-lookup"><span data-stu-id="2c692-118">Property</span></span> | <span data-ttu-id="2c692-119">Valor</span><span class="sxs-lookup"><span data-stu-id="2c692-119">Value</span></span> | <span data-ttu-id="2c692-120">Descrição</span><span class="sxs-lookup"><span data-stu-id="2c692-120">Description</span></span>|
|---|---|---|
| <span data-ttu-id="2c692-121">Nome</span><span class="sxs-lookup"><span data-stu-id="2c692-121">Name</span></span> | <span data-ttu-id="2c692-122">{Nome completo do usuário}</span><span class="sxs-lookup"><span data-stu-id="2c692-122">{User Full Name}</span></span> | <span data-ttu-id="2c692-123">Nome e sobrenome do usuário</span><span class="sxs-lookup"><span data-stu-id="2c692-123">The user’s first and last name</span></span>
|<span data-ttu-id="2c692-124">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="2c692-124">Username</span></span> | <span>user@domain.com</span>| <span data-ttu-id="2c692-125">O nome de usuário usado para identificar o usuário conectado</span><span class="sxs-lookup"><span data-stu-id="2c692-125">The username used to identify the logged user</span></span>
| <span data-ttu-id="2c692-126">Assunto</span><span class="sxs-lookup"><span data-stu-id="2c692-126">Subject</span></span>| <span data-ttu-id="2c692-127">{Subject}</span><span class="sxs-lookup"><span data-stu-id="2c692-127">{Subject}</span></span>|<span data-ttu-id="2c692-128">Uma cadeia de caracteres para identificar exclusivamente o logon do usuário na Web</span><span class="sxs-lookup"><span data-stu-id="2c692-128">A string to uniquely identify the user logon across the web</span></span>|
| <span data-ttu-id="2c692-129">ID do locatário</span><span class="sxs-lookup"><span data-stu-id="2c692-129">Tenant ID</span></span>| <span data-ttu-id="2c692-130">{Guid}</span><span class="sxs-lookup"><span data-stu-id="2c692-130">{Guid}</span></span>| <span data-ttu-id="2c692-131">Um *guid* para representar exclusivamente a organização do Azure Active Directory do usuário.</span><span class="sxs-lookup"><span data-stu-id="2c692-131">A *guid* to uniquely represent the user’s Azure Active Directory organization.</span></span>|

<span data-ttu-id="2c692-132">Além disso, você verá uma tabela, incluindo todas as declarações de usuário incluídas na solicitação de autenticação.</span><span class="sxs-lookup"><span data-stu-id="2c692-132">In addition, you will see a table including all user claims included in authentication request.</span></span> <span data-ttu-id="2c692-133">Para obter uma lista de todas as declarações em um Token de ID e uma explicação, veja este [artigo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "Lista de declarações no Token de ID").</span><span class="sxs-lookup"><span data-stu-id="2c692-133">For a list of all claims in an Id Token and explanation please see this [article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "List of Claims in Id Token").</span></span>


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a><span data-ttu-id="2c692-134">Testar o acesso a um método que tem um atributo *[Authorize]* (opcional)</span><span class="sxs-lookup"><span data-stu-id="2c692-134">Test accessing a method that has an *[Authorize]* attribute (Optional)</span></span>
<span data-ttu-id="2c692-135">Nesta etapa, você testará o acesso ao controlador Autenticado como um usuário anônimo:</span><span class="sxs-lookup"><span data-stu-id="2c692-135">In this step, you will test accessing the Authenticated controller as an anonymous user:</span></span><br/>
<span data-ttu-id="2c692-136">Selecione o link para desconectar o usuário e concluir o processo de saída.</span><span class="sxs-lookup"><span data-stu-id="2c692-136">Select the link to sign-out the user and complete the sign-out process.</span></span><br/>
<span data-ttu-id="2c692-137">Agora no navegador, digite http://localhost:{port}/authenticated para acessar o controlador que está protegido com o atributo `[Authorize]`</span><span class="sxs-lookup"><span data-stu-id="2c692-137">Now in your browser, type http://localhost:{port}/authenticated to access your controller that is protected with the `[Authorize]` attribute</span></span>

#### <a name="expected-results"></a><span data-ttu-id="2c692-138">Resultados esperados</span><span class="sxs-lookup"><span data-stu-id="2c692-138">Expected results</span></span>
<span data-ttu-id="2c692-139">Você deverá receber o prompt exigindo a autenticação para ver a exibição.</span><span class="sxs-lookup"><span data-stu-id="2c692-139">You should receive the prompt requiring you to authenticate to see the view.</span></span>

## <a name="additional-information"></a><span data-ttu-id="2c692-140">Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="2c692-140">Additional information</span></span>

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a><span data-ttu-id="2c692-141">Proteger todo o seu site</span><span class="sxs-lookup"><span data-stu-id="2c692-141">Protect your entire web site</span></span>
<span data-ttu-id="2c692-142">Para proteger todo o seu site, adicione o `AuthorizeAttribute` a `GlobalFilters` no método `Global.asax` `Application_Start`:</span><span class="sxs-lookup"><span data-stu-id="2c692-142">To protect your entire web site, add the `AuthorizeAttribute` to `GlobalFilters` in `Global.asax` `Application_Start` method:</span></span>

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> <span data-ttu-id="2c692-143">**Como restringir os usuários a somente uma organização para entrar em seu aplicativo**</span><span class="sxs-lookup"><span data-stu-id="2c692-143">**How to restrict users from only one organization to sign in to your application**</span></span>

> <span data-ttu-id="2c692-144">Por padrão, contas pessoais (incluindo outlook.com, live.com e outras), bem como contas corporativas ou de estudante de qualquer empresa ou organização que foi integrada ao Azure Active Directory, podem entrar no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2c692-144">By default, personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory can sign-in to your application.</span></span> 

> <span data-ttu-id="2c692-145">Se você desejar que o aplicativo aceite conexões de apenas uma organização do Azure Active Directory, substitua o parâmetro `Tenant` em *web.config* de `Common` para o nome de locatário da organização – por exemplo, *contoso.onmicrosoft.com*.</span><span class="sxs-lookup"><span data-stu-id="2c692-145">If you want your application to accept sign-ins from only one Azure Active Directory organization, replace the `Tenant` parameter in *web.config* from `Common` to the tenant name of the organization – example, *contoso.onmicrosoft.com*.</span></span> <span data-ttu-id="2c692-146">Depois disso, altere o argumento `ValidateIssuer` na *Classe de Inicialização OWIN* para `true`.</span><span class="sxs-lookup"><span data-stu-id="2c692-146">After that, change the `ValidateIssuer` argument in your *OWIN Startup class* to `true`.</span></span>

> <span data-ttu-id="2c692-147">Para permitir usuários apenas de uma lista de organizações específicas, defina `ValidateIssuer` como verdadeiro e use o parâmetro `ValidIssuers` para especificar uma lista de organizações.</span><span class="sxs-lookup"><span data-stu-id="2c692-147">To allow users from only a list of specific organizations, set `ValidateIssuer` to true and use the `ValidIssuers` parameter to specify a list of organizations.</span></span>

> <span data-ttu-id="2c692-148">Outra opção é implementar um método personalizado para validar os emissores usando o parâmetro IssuerValidator.</span><span class="sxs-lookup"><span data-stu-id="2c692-148">Another option is to implement a custom method to validate the issuers using IssuerValidator parameter.</span></span> <span data-ttu-id="2c692-149">Para saber mais sobre `TokenValidationParameters`, veja [este artigo do MSDN](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters").</span><span class="sxs-lookup"><span data-stu-id="2c692-149">For more information about `TokenValidationParameters`, please see [this](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters MSDN article") MSDN article.</span></span>

