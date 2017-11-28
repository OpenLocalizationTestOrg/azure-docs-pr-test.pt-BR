---
title: "Como diagnosticar erros com o Assistente de Conexão do Azure Active Directory"
description: "O Assistente de conexão do Active Directory detectou um tipo de autenticação incompatível"
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
ms.openlocfilehash: 4f29f62b2996cae98b02c1ed5fcb59eca09301ef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="diagnosing-errors-with-the-azure-active-directory-connection-wizard"></a><span data-ttu-id="ba2c7-103">Diagnosticando erros com o Assistente de Conexão do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ba2c7-103">Diagnosing errors with the Azure Active Directory Connection Wizard</span></span>
<span data-ttu-id="ba2c7-104">Ao detectar o código de autenticação anterior, o assistente detectou um tipo de autenticação incompatível.</span><span class="sxs-lookup"><span data-stu-id="ba2c7-104">While detecting previous authentication code, the wizard detected an incompatible authentication type.</span></span>   

## <a name="what-is-being-checked"></a><span data-ttu-id="ba2c7-105">O que está sendo verificado?</span><span class="sxs-lookup"><span data-stu-id="ba2c7-105">What is being checked?</span></span>
<span data-ttu-id="ba2c7-106">**Observação:** para detectar corretamente o código de autenticação anterior em um projeto, o projeto deve ser compilado.</span><span class="sxs-lookup"><span data-stu-id="ba2c7-106">**Note:** To correctly detect previous authentication code in a project, the project must be built.</span></span>  <span data-ttu-id="ba2c7-107">Se este erro ocorrer e você não tiver o código de autenticação anterior em seu projeto, compile o projeto novamente e repita a operação.</span><span class="sxs-lookup"><span data-stu-id="ba2c7-107">If you encountered this error and you don't have a previous authentication code in your project, rebuild and try again.</span></span>

### <a name="project-types"></a><span data-ttu-id="ba2c7-108">Tipos de projeto</span><span class="sxs-lookup"><span data-stu-id="ba2c7-108">Project Types</span></span>
<span data-ttu-id="ba2c7-109">O assistente verifica o tipo de projeto que está sendo desenvolvido para que possa injetar a lógica de autenticação adequada ao projeto.</span><span class="sxs-lookup"><span data-stu-id="ba2c7-109">The wizard checks the type of project you’re developing so it can inject the right authentication logic into the project.</span></span>  <span data-ttu-id="ba2c7-110">Se houver um controlador que deriva de `ApiController` no projeto, o projeto será considerado um projeto WebAPI.</span><span class="sxs-lookup"><span data-stu-id="ba2c7-110">If there is any controller that derives from `ApiController` in the project, the project is considered a WebAPI project.</span></span>  <span data-ttu-id="ba2c7-111">Se houver apenas controladores que derivam de `MVC.Controller` no projeto, o projeto será considerado um projeto MVC.</span><span class="sxs-lookup"><span data-stu-id="ba2c7-111">If there are only controllers that derive from `MVC.Controller` in the project, the project is considered an MVC project.</span></span>  <span data-ttu-id="ba2c7-112">Qualquer outro item não tem suporte do assistente.</span><span class="sxs-lookup"><span data-stu-id="ba2c7-112">Anything else is not supported by the wizard.</span></span>

### <a name="compatible-authentication-code"></a><span data-ttu-id="ba2c7-113">Código de autenticação compatível</span><span class="sxs-lookup"><span data-stu-id="ba2c7-113">Compatible Authentication Code</span></span>
<span data-ttu-id="ba2c7-114">O assistente também verifica se as configurações de autenticação configuradas anteriormente com o assistente são compatíveis com ele.</span><span class="sxs-lookup"><span data-stu-id="ba2c7-114">The wizard also checks for authentication settings that have been previously configured with the wizard or are compatible with the wizard.</span></span>  <span data-ttu-id="ba2c7-115">Se todas as configurações estiverem presentes, ele será considerado um caso reentrante e o assistente será aberto e exibirá as configurações.</span><span class="sxs-lookup"><span data-stu-id="ba2c7-115">If all settings are present, it is considered a re-entrant case, and the wizard opens display the settings.</span></span>  <span data-ttu-id="ba2c7-116">Se apenas algumas das configurações estiverem presentes, ele será considerado um caso de erro.</span><span class="sxs-lookup"><span data-stu-id="ba2c7-116">If only some of the settings are present, it is considered an error case.</span></span>

<span data-ttu-id="ba2c7-117">Em um projeto do MVC, o assistente verifica qualquer uma das configurações a seguir, fruto do uso anterior do assistente:</span><span class="sxs-lookup"><span data-stu-id="ba2c7-117">In an MVC project, the wizard checks for any of the following settings, which result from previous use of the wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

<span data-ttu-id="ba2c7-118">Além disso, o assistente verifica qualquer uma das configurações a seguir em um projeto de API da Web, fruto do uso anterior do assistente:</span><span class="sxs-lookup"><span data-stu-id="ba2c7-118">In addition, the wizard checks for any of the following settings in a Web API project, which result from previous use of the wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a><span data-ttu-id="ba2c7-119">Código de autenticação incompatível</span><span class="sxs-lookup"><span data-stu-id="ba2c7-119">Incompatible Authentication Code</span></span>
<span data-ttu-id="ba2c7-120">Por fim, o assistente tenta detectar versões do código de autenticação que foram configuradas com versões anteriores do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ba2c7-120">Finally, the wizard attempts to detect versions of authentication code that have been configured with previous versions of Visual Studio.</span></span> <span data-ttu-id="ba2c7-121">Se você recebeu esse erro, significa que seu projeto contém um tipo de autenticação incompatível.</span><span class="sxs-lookup"><span data-stu-id="ba2c7-121">If you received this error, it means your project contains an incompatible authentication type.</span></span> <span data-ttu-id="ba2c7-122">O assistente detecta os seguintes tipos de autenticação de versões anteriores do Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="ba2c7-122">The wizard detects the following types of authentication from previous versions of Visual Studio:</span></span>

* <span data-ttu-id="ba2c7-123">Autenticação do Windows</span><span class="sxs-lookup"><span data-stu-id="ba2c7-123">Windows Authentication</span></span> 
* <span data-ttu-id="ba2c7-124">Contas Individuais de Usuário</span><span class="sxs-lookup"><span data-stu-id="ba2c7-124">Individual User Accounts</span></span> 
* <span data-ttu-id="ba2c7-125">Contas organizacionais</span><span class="sxs-lookup"><span data-stu-id="ba2c7-125">Organizational Accounts</span></span> 

<span data-ttu-id="ba2c7-126">Para detectar a Autenticação do Windows em um projeto MVC, o assistente procura pelo elemento `authentication` de seu arquivo **web.config** .</span><span class="sxs-lookup"><span data-stu-id="ba2c7-126">To detect Windows Authentication in an MVC project, the wizard looks for the `authentication` element from your **web.config** file.</span></span>

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="ba2c7-127">Para detectar a Autenticação do Windows em um projeto da API da Web, o assistente procura pelo elemento `IISExpressWindowsAuthentication` do arquivo **.csproj** de seu projeto:</span><span class="sxs-lookup"><span data-stu-id="ba2c7-127">To detect Windows Authentication in a Web API project, the wizard looks for the `IISExpressWindowsAuthentication` element from your project's **.csproj** file:</span></span>

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

<span data-ttu-id="ba2c7-128">Para detectar a autenticação de contas de usuário individual, o assistente procura o elemento de pacote de seu arquivo **Packages.config** .</span><span class="sxs-lookup"><span data-stu-id="ba2c7-128">To detect Individual User Accounts authentication, the wizard looks for the package element from your **Packages.config** file.</span></span>

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

<span data-ttu-id="ba2c7-129">Para detectar uma forma anterior de Autenticação de conta organizacional, o assistente procura o seguinte elemento **web.config**:</span><span class="sxs-lookup"><span data-stu-id="ba2c7-129">To detect an old form of Organizational Account authentication, the wizard looks for the following element from **web.config**:</span></span>

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="ba2c7-130">Para alterar o tipo de autenticação, remova o tipo de autenticação incompatível e execute o assistente novamente.</span><span class="sxs-lookup"><span data-stu-id="ba2c7-130">To change the authentication type, remove the incompatible authentication type and run the wizard again.</span></span>

<span data-ttu-id="ba2c7-131">Para obter mais informações, consulte [Cenários de autenticação para o Azure AD](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="ba2c7-131">For more information, see [Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md).</span></span>

#<a name="next-steps"></a><span data-ttu-id="ba2c7-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ba2c7-132">Next steps</span></span>
- [<span data-ttu-id="ba2c7-133">Cenários de autenticação do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba2c7-133">Authentication Scenarios for Azure AD</span></span>](active-directory-authentication-scenarios.md)