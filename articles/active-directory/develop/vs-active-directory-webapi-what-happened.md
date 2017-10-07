---
title: "aaaChanges feita tooa WebApi projeto quando você se conectar tooAzure AD | Microsoft Docs"
description: "Descreve o que acontece tooyour WebApi projeto quando você conectar tooAzure AD usando o Visual Studio"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 57630aee-26a2-4326-9dbb-ea2a66daa8b0
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 1ea77b6c75b2dc273219fa6c43f02c7a7c5312ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-webapi-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="f444e-103">O projeto de WebApi toomy com (Visual Studio do Azure Active Directory conectado serviço)</span><span class="sxs-lookup"><span data-stu-id="f444e-103">What happened toomy WebApi project (Visual Studio Azure Active Directory connected service)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f444e-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="f444e-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="f444e-105">O que aconteceu</span><span class="sxs-lookup"><span data-stu-id="f444e-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="f444e-106">Referências foram adicionadas</span><span class="sxs-lookup"><span data-stu-id="f444e-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="f444e-107">Referências do pacote NuGet</span><span class="sxs-lookup"><span data-stu-id="f444e-107">NuGet package references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a><span data-ttu-id="f444e-108">Referências .NET</span><span class="sxs-lookup"><span data-stu-id="f444e-108">.NET references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a><span data-ttu-id="f444e-109">Alterações de código</span><span class="sxs-lookup"><span data-stu-id="f444e-109">Code changes</span></span>
### <a name="code-files-were-added-tooyour-project"></a><span data-ttu-id="f444e-110">Arquivos de código foram adicionados tooyour projeto</span><span class="sxs-lookup"><span data-stu-id="f444e-110">Code files were added tooyour project</span></span>
<span data-ttu-id="f444e-111">Uma classe de inicialização de autenticação, **App_Start/Startup.Auth.cs** foi adicionado tooyour projeto que contém a lógica de inicialização para a autenticação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f444e-111">An authentication startup class, **App_Start/Startup.Auth.cs** was added tooyour project containing startup logic for Azure AD authentication.</span></span>

### <a name="startup-code-was-added-tooyour-project"></a><span data-ttu-id="f444e-112">Código de inicialização foi adicionado tooyour projeto</span><span class="sxs-lookup"><span data-stu-id="f444e-112">Startup code was added tooyour project</span></span>
<span data-ttu-id="f444e-113">Se você já tinha uma classe de inicialização em seu projeto, Olá **configuração** método foi atualizada tooinclude uma chamada muito`ConfigureAuth(app)`.</span><span class="sxs-lookup"><span data-stu-id="f444e-113">If you already had a Startup class in your project, hello **Configuration** method was updated tooinclude a call too`ConfigureAuth(app)`.</span></span> <span data-ttu-id="f444e-114">Caso contrário, uma classe de inicialização foi adicionada tooyour projeto.</span><span class="sxs-lookup"><span data-stu-id="f444e-114">Otherwise, a Startup class was added tooyour project.</span></span>

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a><span data-ttu-id="f444e-115">Seu arquivo app.config ou web.config possui novos valores de configuração.</span><span class="sxs-lookup"><span data-stu-id="f444e-115">Your app.config or web.config file has new configuration values.</span></span>
<span data-ttu-id="f444e-116">Olá entradas de configuração a seguir foram adicionada.</span><span class="sxs-lookup"><span data-stu-id="f444e-116">hello following configuration entries have been added.</span></span>

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="hello App ID Uri from hello wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a><span data-ttu-id="f444e-117">Um aplicativo do Azure AD foi criado</span><span class="sxs-lookup"><span data-stu-id="f444e-117">An Azure AD App was created</span></span>
<span data-ttu-id="f444e-118">Um aplicativo do AD do Azure foi criado no diretório de saudação que você selecionou no Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="f444e-118">An Azure AD Application was created in hello directory that you selected in hello wizard.</span></span>

[<span data-ttu-id="f444e-119">Saiba mais sobre o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="f444e-119">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="f444e-120">Se verifiquei *desabilitar a autenticação de contas de usuário individuais*, quais alterações adicionais foram feitas toomy projeto?</span><span class="sxs-lookup"><span data-stu-id="f444e-120">If I checked *disable Individual User Accounts authentication*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="f444e-121">Referências ao pacote NuGet foram removidas e arquivos foram removidos e copiados.</span><span class="sxs-lookup"><span data-stu-id="f444e-121">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="f444e-122">Dependendo do estado de saudação do seu projeto, você pode ter toomanually remover referências adicionais ou arquivos ou modificar o código conforme apropriado.</span><span class="sxs-lookup"><span data-stu-id="f444e-122">Depending on hello state of your project, you may have toomanually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="f444e-123">Referências ao pacotes NuGet removidas (para aquelas presentes)</span><span class="sxs-lookup"><span data-stu-id="f444e-123">NuGet package references removed (for those present)</span></span>
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="f444e-124">Arquivos de código copiados e removidos (para aqueles presentes)</span><span class="sxs-lookup"><span data-stu-id="f444e-124">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="f444e-125">Cada um dos seguintes arquivos foi feita e removida do projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="f444e-125">Each of following files was backed up and removed from hello project.</span></span> <span data-ttu-id="f444e-126">Arquivos de backup estão localizados em uma pasta de 'Backup' na raiz de saudação do diretório do projeto hello.</span><span class="sxs-lookup"><span data-stu-id="f444e-126">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="f444e-127">Arquivos de código copiados (para aqueles presentes)</span><span class="sxs-lookup"><span data-stu-id="f444e-127">Code files backed up (for those present)</span></span>
<span data-ttu-id="f444e-128">Cada um dos seguintes arquivos foi copiado antes de ser substituído.</span><span class="sxs-lookup"><span data-stu-id="f444e-128">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="f444e-129">Arquivos de backup estão localizados em uma pasta de 'Backup' na raiz de saudação do diretório do projeto hello.</span><span class="sxs-lookup"><span data-stu-id="f444e-129">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="f444e-130">Se verifiquei *ler dados do diretório*, quais alterações adicionais foram feitas toomy projeto?</span><span class="sxs-lookup"><span data-stu-id="f444e-130">If I checked *Read directory data*, what additional changes were made toomy project?</span></span>
### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a><span data-ttu-id="f444e-131">Outras alterações foram feitas tooyour App. config ou Web. config</span><span class="sxs-lookup"><span data-stu-id="f444e-131">Additional changes were made tooyour app.config or web.config</span></span>
<span data-ttu-id="f444e-132">Olá seguintes entradas de configuração adicionais foram adicionadas.</span><span class="sxs-lookup"><span data-stu-id="f444e-132">hello following additional configuration entries have been added.</span></span>

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="f444e-133">Seu aplicativo Active Directory do Azure foi atualizado</span><span class="sxs-lookup"><span data-stu-id="f444e-133">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="f444e-134">Seu aplicativo do Azure Active Directory foi atualizada tooinclude Olá *ler dados do diretório* permissão e uma chave adicional foi criado, que foi usado como Olá *ida: senha* em Olá `web.config` arquivo.</span><span class="sxs-lookup"><span data-stu-id="f444e-134">Your Azure Active Directory App was updated tooinclude hello *Read directory data* permission and an additional key was created which was then used as hello *ida:Password* in hello `web.config` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f444e-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f444e-135">Next steps</span></span>
- [<span data-ttu-id="f444e-136">Saiba mais sobre o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="f444e-136">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

