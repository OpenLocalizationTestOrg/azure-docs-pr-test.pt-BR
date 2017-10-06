---
title: "tooa aaaChanges feitas MVC projeto quando você se conectar tooAzure AD | Microsoft Docs"
description: "Descreve o que acontece projeto MVC de tooyour quando você se conectar tooAzure AD através dos serviços do Visual Studio conectado"
services: active-directory
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 8b24adde-547e-4ffe-824a-2029ba210216
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 5e6d4ce5331eacca5fc83429017ae454fadcc8e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-mvc-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="1d6b2-103">O projeto do MVC com toomy (Visual Studio do Azure Active Directory conectado serviço)?</span><span class="sxs-lookup"><span data-stu-id="1d6b2-103">What happened toomy MVC project (Visual Studio Azure Active Directory connected service)?</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1d6b2-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="1d6b2-104">Getting Started</span></span>](vs-active-directory-dotnet-getting-started.md)
> * [<span data-ttu-id="1d6b2-105">O que aconteceu</span><span class="sxs-lookup"><span data-stu-id="1d6b2-105">What Happened</span></span>](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="1d6b2-106">Referências foram adicionadas</span><span class="sxs-lookup"><span data-stu-id="1d6b2-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="1d6b2-107">Referências do pacote NuGet</span><span class="sxs-lookup"><span data-stu-id="1d6b2-107">NuGet package references</span></span>
* <span data-ttu-id="1d6b2-108">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-108">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="1d6b2-109">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-109">**Microsoft.Owin**</span></span>
* <span data-ttu-id="1d6b2-110">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-110">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="1d6b2-111">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-111">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="1d6b2-112">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-112">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="1d6b2-113">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-113">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="1d6b2-114">**Owin**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-114">**Owin**</span></span>
* <span data-ttu-id="1d6b2-115">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-115">**System.IdentityModel.Tokens.Jwt**</span></span>

### <a name="net-references"></a><span data-ttu-id="1d6b2-116">Referências .NET</span><span class="sxs-lookup"><span data-stu-id="1d6b2-116">.NET references</span></span>
* <span data-ttu-id="1d6b2-117">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-117">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="1d6b2-118">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-118">**Microsoft.Owin**</span></span>
* <span data-ttu-id="1d6b2-119">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-119">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="1d6b2-120">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-120">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="1d6b2-121">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-121">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="1d6b2-122">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-122">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="1d6b2-123">**Owin**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-123">**Owin**</span></span>
* <span data-ttu-id="1d6b2-124">**System.IdentityModel**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-124">**System.IdentityModel**</span></span>
* <span data-ttu-id="1d6b2-125">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-125">**System.IdentityModel.Tokens.Jwt**</span></span>
* <span data-ttu-id="1d6b2-126">**System.Runtime.Serialization**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-126">**System.Runtime.Serialization**</span></span>

## <a name="code-has-been-added"></a><span data-ttu-id="1d6b2-127">Um código foi adicionado</span><span class="sxs-lookup"><span data-stu-id="1d6b2-127">Code has been added</span></span>
### <a name="code-files-were-added-tooyour-project"></a><span data-ttu-id="1d6b2-128">Arquivos de código foram adicionados tooyour projeto</span><span class="sxs-lookup"><span data-stu-id="1d6b2-128">Code files were added tooyour project</span></span>
<span data-ttu-id="1d6b2-129">Uma classe de inicialização de autenticação, **App_Start/Startup.Auth.cs** foi adicionado tooyour projeto que contém a lógica de inicialização para a autenticação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d6b2-129">An authentication startup class, **App_Start/Startup.Auth.cs** was added tooyour project containing startup logic for Azure AD authentication.</span></span> <span data-ttu-id="1d6b2-130">Além disso, uma classe de controlador, Controllers/AccountController.cs, foi adicionada, contendo os métodos **SignIn()** e **SignOut()**.</span><span class="sxs-lookup"><span data-stu-id="1d6b2-130">Also, a controller class, Controllers/AccountController.cs was added which contains **SignIn()** and **SignOut()** methods.</span></span> <span data-ttu-id="1d6b2-131">Por fim, uma exibição parcial, **Views/Shared/_LoginPartial.cshtml**, foi adicionada, contendo um link de ação para SignIn/SignOut.</span><span class="sxs-lookup"><span data-stu-id="1d6b2-131">Finally, a partial view, **Views/Shared/_LoginPartial.cshtml** was added containing an action link for SignIn/SignOut.</span></span>

### <a name="startup-code-was-added-tooyour-project"></a><span data-ttu-id="1d6b2-132">Código de inicialização foi adicionado tooyour projeto</span><span class="sxs-lookup"><span data-stu-id="1d6b2-132">Startup code was added tooyour project</span></span>
<span data-ttu-id="1d6b2-133">Se você já tinha uma classe de inicialização em seu projeto, Olá **configuração** método foi atualizada tooinclude uma chamada muito**ConfigureAuth(app)**.</span><span class="sxs-lookup"><span data-stu-id="1d6b2-133">If you already had a Startup class in your project, hello **Configuration** method was updated tooinclude a call too**ConfigureAuth(app)**.</span></span> <span data-ttu-id="1d6b2-134">Caso contrário, uma classe de inicialização foi adicionada tooyour projeto.</span><span class="sxs-lookup"><span data-stu-id="1d6b2-134">Otherwise, a Startup class was added tooyour project.</span></span>

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a><span data-ttu-id="1d6b2-135">Seu app.config ou web.config tem novos valores de configuração</span><span class="sxs-lookup"><span data-stu-id="1d6b2-135">Your app.config or web.config has new configuration values</span></span>
<span data-ttu-id="1d6b2-136">Olá entradas de configuração a seguir foram adicionada.</span><span class="sxs-lookup"><span data-stu-id="1d6b2-136">hello following configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="hello selected Azure AD Domain" />
        <add key="ida:TenantId" value="hello Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a><span data-ttu-id="1d6b2-137">Foi criado um aplicativo do Azure Active Directory (AD)</span><span class="sxs-lookup"><span data-stu-id="1d6b2-137">An Azure Active Directory (AD) App was created</span></span>
<span data-ttu-id="1d6b2-138">Um aplicativo do AD do Azure foi criado no diretório de saudação que você selecionou no Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d6b2-138">An Azure AD Application was created in hello directory that you selected in hello wizard.</span></span>

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="1d6b2-139">Se verifiquei *desabilitar a autenticação de contas de usuário individuais*, quais alterações adicionais foram feitas toomy projeto?</span><span class="sxs-lookup"><span data-stu-id="1d6b2-139">If I checked *disable Individual User Accounts authentication*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="1d6b2-140">Referências ao pacote NuGet foram removidas e arquivos foram removidos e copiados.</span><span class="sxs-lookup"><span data-stu-id="1d6b2-140">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="1d6b2-141">Dependendo do estado de saudação do seu projeto, você pode ter toomanually remover referências adicionais ou arquivos ou modificar o código conforme apropriado.</span><span class="sxs-lookup"><span data-stu-id="1d6b2-141">Depending on hello state of your project, you may have toomanually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="1d6b2-142">Referências ao pacotes NuGet removidas (para aquelas presentes)</span><span class="sxs-lookup"><span data-stu-id="1d6b2-142">NuGet package references removed (for those present)</span></span>
* <span data-ttu-id="1d6b2-143">**Microsoft.AspNet.Identity.Core**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-143">**Microsoft.AspNet.Identity.Core**</span></span>
* <span data-ttu-id="1d6b2-144">**Microsoft.AspNet.Identity.EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-144">**Microsoft.AspNet.Identity.EntityFramework**</span></span>
* <span data-ttu-id="1d6b2-145">**Microsoft.AspNet.Identity.Owin**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-145">**Microsoft.AspNet.Identity.Owin**</span></span>

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="1d6b2-146">Arquivos de código copiados e removidos (para aqueles presentes)</span><span class="sxs-lookup"><span data-stu-id="1d6b2-146">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="1d6b2-147">Cada um dos seguintes arquivos foi feita e removida do projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d6b2-147">Each of following files was backed up and removed from hello project.</span></span> <span data-ttu-id="1d6b2-148">Arquivos de backup estão localizados em uma pasta de 'Backup' na raiz de saudação do diretório do projeto hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b2-148">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* <span data-ttu-id="1d6b2-149">**App_Start\IdentityConfig.cs**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-149">**App_Start\IdentityConfig.cs**</span></span>
* <span data-ttu-id="1d6b2-150">**Controllers\ManageController.cs**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-150">**Controllers\ManageController.cs**</span></span>
* <span data-ttu-id="1d6b2-151">**Models\IdentityModels.cs**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-151">**Models\IdentityModels.cs**</span></span>
* <span data-ttu-id="1d6b2-152">**Models\ManageViewModels.cs**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-152">**Models\ManageViewModels.cs**</span></span>

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="1d6b2-153">Arquivos de código copiados (para aqueles presentes)</span><span class="sxs-lookup"><span data-stu-id="1d6b2-153">Code files backed up (for those present)</span></span>
<span data-ttu-id="1d6b2-154">Cada um dos seguintes arquivos foi copiado antes de ser substituído.</span><span class="sxs-lookup"><span data-stu-id="1d6b2-154">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="1d6b2-155">Arquivos de backup estão localizados em uma pasta de 'Backup' na raiz de saudação do diretório do projeto hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b2-155">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* <span data-ttu-id="1d6b2-156">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-156">**Startup.cs**</span></span>
* <span data-ttu-id="1d6b2-157">**App_Start\Startup.Auth.cs**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-157">**App_Start\Startup.Auth.cs**</span></span>
* <span data-ttu-id="1d6b2-158">**Controllers\AccountController.cs**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-158">**Controllers\AccountController.cs**</span></span>
* <span data-ttu-id="1d6b2-159">**Views\Shared\_LoginPartial.cshtml**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-159">**Views\Shared\_LoginPartial.cshtml**</span></span>

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="1d6b2-160">Se verifiquei *ler dados do diretório*, quais alterações adicionais foram feitas toomy projeto?</span><span class="sxs-lookup"><span data-stu-id="1d6b2-160">If I checked *Read directory data*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="1d6b2-161">Referências extras foram adicionadas.</span><span class="sxs-lookup"><span data-stu-id="1d6b2-161">Additional references have been added.</span></span>

### <a name="additional-nuget-package-references"></a><span data-ttu-id="1d6b2-162">Referências adicionais do pacote do NuGet</span><span class="sxs-lookup"><span data-stu-id="1d6b2-162">Additional NuGet package references</span></span>
* <span data-ttu-id="1d6b2-163">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-163">**EntityFramework**</span></span>
* <span data-ttu-id="1d6b2-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="1d6b2-165">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-165">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="1d6b2-166">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-166">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="1d6b2-167">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-167">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="1d6b2-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="1d6b2-169">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-169">**System.Spatial**</span></span>

### <a name="additional-net-references"></a><span data-ttu-id="1d6b2-170">Referências adicionais do .NET</span><span class="sxs-lookup"><span data-stu-id="1d6b2-170">Additional .NET references</span></span>
* <span data-ttu-id="1d6b2-171">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-171">**EntityFramework**</span></span>
* <span data-ttu-id="1d6b2-172">**EntityFramework.SqlServer**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-172">**EntityFramework.SqlServer**</span></span>
* <span data-ttu-id="1d6b2-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="1d6b2-174">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-174">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="1d6b2-175">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-175">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="1d6b2-176">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-176">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="1d6b2-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="1d6b2-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span></span>
* <span data-ttu-id="1d6b2-179">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-179">**System.Spatial**</span></span>

### <a name="additional-code-files-were-added-tooyour-project"></a><span data-ttu-id="1d6b2-180">Arquivos de código adicionais foram adicionados tooyour projeto</span><span class="sxs-lookup"><span data-stu-id="1d6b2-180">Additional Code files were added tooyour project</span></span>
<span data-ttu-id="1d6b2-181">Dois arquivos foram adicionados toosupport cache de token: **Models\ADALTokenCache.cs** e **Models\ApplicationDbContext.cs**.</span><span class="sxs-lookup"><span data-stu-id="1d6b2-181">Two files were added toosupport token caching: **Models\ADALTokenCache.cs** and **Models\ApplicationDbContext.cs**.</span></span>  <span data-ttu-id="1d6b2-182">Um controlador adicional e o modo de exibição foram adicionados tooillustrate acessando informações de perfil de usuário usando o Azure graph APIs.</span><span class="sxs-lookup"><span data-stu-id="1d6b2-182">An additional controller and view were added tooillustrate accessing user profile information using Azure graph APIs.</span></span>  <span data-ttu-id="1d6b2-183">Esses arquivos são **Controllers\UserProfileController.cs** e**Views\UserProfile\Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="1d6b2-183">These files are **Controllers\UserProfileController.cs** and **Views\UserProfile\Index.cshtml**.</span></span>

### <a name="additional-startup-code-was-added-tooyour-project"></a><span data-ttu-id="1d6b2-184">Código de inicialização adicional foi adicionado tooyour projeto</span><span class="sxs-lookup"><span data-stu-id="1d6b2-184">Additional Startup code was added tooyour project</span></span>
<span data-ttu-id="1d6b2-185">Em Olá **startup.auth.cs** arquivo, uma nova **OpenIdConnectAuthenticationNotifications** objeto foi adicionado toohello **notificações** membro da saudação  **OpenIdConnectAuthenticationOptions**.</span><span class="sxs-lookup"><span data-stu-id="1d6b2-185">In hello **startup.auth.cs** file, a new **OpenIdConnectAuthenticationNotifications** object was added toohello **Notifications** member of hello **OpenIdConnectAuthenticationOptions**.</span></span>  <span data-ttu-id="1d6b2-186">Isso é tooenable recebimento Olá OAuth código e trocá-lo por um token de acesso.</span><span class="sxs-lookup"><span data-stu-id="1d6b2-186">This is tooenable receiving hello OAuth code and exchanging it for an access token.</span></span>

### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a><span data-ttu-id="1d6b2-187">Outras alterações foram feitas tooyour App. config ou Web. config</span><span class="sxs-lookup"><span data-stu-id="1d6b2-187">Additional changes were made tooyour app.config or web.config</span></span>
<span data-ttu-id="1d6b2-188">Olá seguintes entradas de configuração adicionais foram adicionadas.</span><span class="sxs-lookup"><span data-stu-id="1d6b2-188">hello following additional configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

<span data-ttu-id="1d6b2-189">Olá seguintes seções de configuração e a cadeia de caracteres de conexão foram adicionadas.</span><span class="sxs-lookup"><span data-stu-id="1d6b2-189">hello following configuration sections and connection string have been added.</span></span>

    <configSections>
        <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
        <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
    </configSections>
    <connectionStrings>
        <add name="DefaultConnection" connectionString="Data Source=(localdb)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\aspnet-[AppName + Generated Id].mdf;Initial Catalog=aspnet-[AppName + Generated Id];Integrated Security=True" providerName="System.Data.SqlClient" />
    </connectionStrings>
    <entityFramework>
        <defaultConnectionFactory type="System.Data.Entity.Infrastructure.LocalDbConnectionFactory, EntityFramework">
          <parameters>
            <parameter value="mssqllocaldb" />
          </parameters>
        </defaultConnectionFactory>
        <providers>
          <provider invariantName="System.Data.SqlClient" type="System.Data.Entity.SqlServer.SqlProviderServices, EntityFramework.SqlServer" />
        </providers>
    </entityFramework>


### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="1d6b2-190">Seu aplicativo Active Directory do Azure foi atualizado</span><span class="sxs-lookup"><span data-stu-id="1d6b2-190">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="1d6b2-191">Seu aplicativo do Azure Active Directory foi atualizada tooinclude Olá *ler dados do diretório* permissão e uma chave adicional foi criado, que foi usado como Olá *ida: ClientSecret* em Olá  **Web. config** arquivo.</span><span class="sxs-lookup"><span data-stu-id="1d6b2-191">Your Azure Active Directory App was updated tooinclude hello *Read directory data* permission and an additional key was created which was then used as hello *ida:ClientSecret* in hello **web.config** file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d6b2-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1d6b2-192">Next steps</span></span>
- [<span data-ttu-id="1d6b2-193">Saiba mais sobre o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="1d6b2-193">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

