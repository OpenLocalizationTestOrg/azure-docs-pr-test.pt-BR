---
title: "erros de toodiagnose aaaHow com hello Assistente de Conexão do Azure Active Directory"
description: "Assistente de conexão do active directory Olá detectou um tipo de autenticação incompatível"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: dd89ea63-4e45-4da1-9642-645b9309670a
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/05/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: f71c5b41457c0c8db05042e8d5f723e58ad11844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnosing-errors-with-hello-azure-active-directory-connection-wizard"></a><span data-ttu-id="db7c2-103">Diagnosticando erros com hello Assistente de Conexão do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="db7c2-103">Diagnosing errors with hello Azure Active Directory Connection Wizard</span></span>
<span data-ttu-id="db7c2-104">Ao detectar o código de autenticação anterior, o Assistente de saudação detectou um tipo de autenticação incompatível.</span><span class="sxs-lookup"><span data-stu-id="db7c2-104">While detecting previous authentication code, hello wizard detected an incompatible authentication type.</span></span>   

## <a name="what-is-being-checked"></a><span data-ttu-id="db7c2-105">O que está sendo verificado?</span><span class="sxs-lookup"><span data-stu-id="db7c2-105">What is being checked?</span></span>
<span data-ttu-id="db7c2-106">**Observação:** toocorrectly detectar anterior código de autenticação em um projeto, Olá projeto deve ser criado.</span><span class="sxs-lookup"><span data-stu-id="db7c2-106">**Note:** toocorrectly detect previous authentication code in a project, hello project must be built.</span></span>  <span data-ttu-id="db7c2-107">Se este erro ocorrer e você não tiver o código de autenticação anterior em seu projeto, compile o projeto novamente e repita a operação.</span><span class="sxs-lookup"><span data-stu-id="db7c2-107">If you encountered this error and you don't have a previous authentication code in your project, rebuild and try again.</span></span>

### <a name="project-types"></a><span data-ttu-id="db7c2-108">Tipos de projeto</span><span class="sxs-lookup"><span data-stu-id="db7c2-108">Project Types</span></span>
<span data-ttu-id="db7c2-109">Assistente de Olá verifica o tipo de saudação do projeto que você desenvolve para que ele pode injetar a lógica de certo de autenticação de saudação no projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="db7c2-109">hello wizard checks hello type of project you’re developing so it can inject hello right authentication logic into hello project.</span></span>  <span data-ttu-id="db7c2-110">Se houver qualquer controlador que deriva de `ApiController` no projeto hello, projeto de saudação é considerado um projeto WebAPI.</span><span class="sxs-lookup"><span data-stu-id="db7c2-110">If there is any controller that derives from `ApiController` in hello project, hello project is considered a WebAPI project.</span></span>  <span data-ttu-id="db7c2-111">Se houver somente controladores que derivam de `MVC.Controller` no projeto hello, projeto de saudação é considerado um projeto MVC.</span><span class="sxs-lookup"><span data-stu-id="db7c2-111">If there are only controllers that derive from `MVC.Controller` in hello project, hello project is considered an MVC project.</span></span>  <span data-ttu-id="db7c2-112">Não há suporte para qualquer outra coisa pelo Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="db7c2-112">Anything else is not supported by hello wizard.</span></span>

### <a name="compatible-authentication-code"></a><span data-ttu-id="db7c2-113">Código de autenticação compatível</span><span class="sxs-lookup"><span data-stu-id="db7c2-113">Compatible Authentication Code</span></span>
<span data-ttu-id="db7c2-114">Assistente de saudação também verifica as configurações de autenticação que foi configuradas anteriormente com o Assistente de saudação ou que são compatíveis com o Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="db7c2-114">hello wizard also checks for authentication settings that have been previously configured with hello wizard or are compatible with hello wizard.</span></span>  <span data-ttu-id="db7c2-115">Se todas as configurações estiverem presentes, ele é considerado um caso reentrante e Olá wizard abre exibe configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="db7c2-115">If all settings are present, it is considered a re-entrant case, and hello wizard opens display hello settings.</span></span>  <span data-ttu-id="db7c2-116">Se apenas algumas das configurações de saudação estiverem presentes, ele será considerado um caso de erro.</span><span class="sxs-lookup"><span data-stu-id="db7c2-116">If only some of hello settings are present, it is considered an error case.</span></span>

<span data-ttu-id="db7c2-117">Em um projeto MVC, Olá assistente verifica qualquer Olá configurações, que resultam do uso anterior do Assistente de saudação a seguir:</span><span class="sxs-lookup"><span data-stu-id="db7c2-117">In an MVC project, hello wizard checks for any of hello following settings, which result from previous use of hello wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

<span data-ttu-id="db7c2-118">Além disso, o Assistente de Olá verifica para qualquer Olá configurações em um projeto de API da Web, que resultam do uso anterior do Assistente de saudação a seguir:</span><span class="sxs-lookup"><span data-stu-id="db7c2-118">In addition, hello wizard checks for any of hello following settings in a Web API project, which result from previous use of hello wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a><span data-ttu-id="db7c2-119">Código de autenticação incompatível</span><span class="sxs-lookup"><span data-stu-id="db7c2-119">Incompatible Authentication Code</span></span>
<span data-ttu-id="db7c2-120">Por fim, o Assistente de saudação tenta toodetect versões de código de autenticação que foram configuradas com as versões anteriores do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="db7c2-120">Finally, hello wizard attempts toodetect versions of authentication code that have been configured with previous versions of Visual Studio.</span></span> <span data-ttu-id="db7c2-121">Se você recebeu esse erro, significa que seu projeto contém um tipo de autenticação incompatível.</span><span class="sxs-lookup"><span data-stu-id="db7c2-121">If you received this error, it means your project contains an incompatible authentication type.</span></span> <span data-ttu-id="db7c2-122">Assistente de saudação detecta Olá seguintes tipos de autenticação de versões anteriores do Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="db7c2-122">hello wizard detects hello following types of authentication from previous versions of Visual Studio:</span></span>

* <span data-ttu-id="db7c2-123">Autenticação do Windows</span><span class="sxs-lookup"><span data-stu-id="db7c2-123">Windows Authentication</span></span> 
* <span data-ttu-id="db7c2-124">Contas Individuais de Usuário</span><span class="sxs-lookup"><span data-stu-id="db7c2-124">Individual User Accounts</span></span> 
* <span data-ttu-id="db7c2-125">Contas organizacionais</span><span class="sxs-lookup"><span data-stu-id="db7c2-125">Organizational Accounts</span></span> 

<span data-ttu-id="db7c2-126">toodetect a autenticação do Windows em um projeto MVC, Olá assistente procura Olá `authentication` elemento da sua **Web. config** arquivo.</span><span class="sxs-lookup"><span data-stu-id="db7c2-126">toodetect Windows Authentication in an MVC project, hello wizard looks for hello `authentication` element from your **web.config** file.</span></span>

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="db7c2-127">toodetect a autenticação do Windows em um projeto de API da Web, Olá assistente procura Olá `IISExpressWindowsAuthentication` elemento do seu projeto **. csproj** arquivo:</span><span class="sxs-lookup"><span data-stu-id="db7c2-127">toodetect Windows Authentication in a Web API project, hello wizard looks for hello `IISExpressWindowsAuthentication` element from your project's **.csproj** file:</span></span>

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

<span data-ttu-id="db7c2-128">autenticação de contas de usuário individuais toodetect, Olá assistente tem uma aparência para o elemento de pacote de saudação do seu **Packages** arquivo.</span><span class="sxs-lookup"><span data-stu-id="db7c2-128">toodetect Individual User Accounts authentication, hello wizard looks for hello package element from your **Packages.config** file.</span></span>

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

<span data-ttu-id="db7c2-129">toodetect um formato antigo da autenticação de conta organizacional, Olá assistente procura Olá após o elemento de **Web. config**:</span><span class="sxs-lookup"><span data-stu-id="db7c2-129">toodetect an old form of Organizational Account authentication, hello wizard looks for hello following element from **web.config**:</span></span>

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="db7c2-130">tipo de autenticação do toochange Olá, remover o tipo de autenticação incompatível hello e execute o Assistente de saudação novamente.</span><span class="sxs-lookup"><span data-stu-id="db7c2-130">toochange hello authentication type, remove hello incompatible authentication type and run hello wizard again.</span></span>

<span data-ttu-id="db7c2-131">Para obter mais informações, consulte [Cenários de autenticação para o Azure AD](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="db7c2-131">For more information, see [Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md).</span></span>

#<a name="next-steps"></a><span data-ttu-id="db7c2-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="db7c2-132">Next steps</span></span>
- [<span data-ttu-id="db7c2-133">Cenários de autenticação do Azure AD</span><span class="sxs-lookup"><span data-stu-id="db7c2-133">Authentication Scenarios for Azure AD</span></span>](active-directory-authentication-scenarios.md)