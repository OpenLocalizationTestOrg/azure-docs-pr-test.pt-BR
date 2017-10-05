---
title: "Alterações feitas em um projeto de MVC quando você se conecta ao Azure AD | Microsoft Docs"
description: "Descreve o que acontece ao seu projeto do MVC quando você se conecta ao AD do Azure usando os serviços conectados do Visual Studio"
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
ms.openlocfilehash: 095411a7fc854f4dce11921adb0f57c5389a8e13
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-mvc-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="5a415-103">O que aconteceu com meu projeto do MVC (serviço conectado do Active Directory do Azure do Visual Studio)?</span><span class="sxs-lookup"><span data-stu-id="5a415-103">What happened to my MVC project (Visual Studio Azure Active Directory connected service)?</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5a415-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="5a415-104">Getting Started</span></span>](vs-active-directory-dotnet-getting-started.md)
> * [<span data-ttu-id="5a415-105">O que aconteceu</span><span class="sxs-lookup"><span data-stu-id="5a415-105">What Happened</span></span>](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="5a415-106">Referências foram adicionadas</span><span class="sxs-lookup"><span data-stu-id="5a415-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="5a415-107">Referências do pacote NuGet</span><span class="sxs-lookup"><span data-stu-id="5a415-107">NuGet package references</span></span>
* <span data-ttu-id="5a415-108">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="5a415-108">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="5a415-109">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="5a415-109">**Microsoft.Owin**</span></span>
* <span data-ttu-id="5a415-110">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="5a415-110">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="5a415-111">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="5a415-111">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="5a415-112">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="5a415-112">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="5a415-113">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="5a415-113">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="5a415-114">**Owin**</span><span class="sxs-lookup"><span data-stu-id="5a415-114">**Owin**</span></span>
* <span data-ttu-id="5a415-115">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="5a415-115">**System.IdentityModel.Tokens.Jwt**</span></span>

### <a name="net-references"></a><span data-ttu-id="5a415-116">Referências .NET</span><span class="sxs-lookup"><span data-stu-id="5a415-116">.NET references</span></span>
* <span data-ttu-id="5a415-117">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="5a415-117">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="5a415-118">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="5a415-118">**Microsoft.Owin**</span></span>
* <span data-ttu-id="5a415-119">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="5a415-119">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="5a415-120">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="5a415-120">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="5a415-121">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="5a415-121">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="5a415-122">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="5a415-122">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="5a415-123">**Owin**</span><span class="sxs-lookup"><span data-stu-id="5a415-123">**Owin**</span></span>
* <span data-ttu-id="5a415-124">**System.IdentityModel**</span><span class="sxs-lookup"><span data-stu-id="5a415-124">**System.IdentityModel**</span></span>
* <span data-ttu-id="5a415-125">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="5a415-125">**System.IdentityModel.Tokens.Jwt**</span></span>
* <span data-ttu-id="5a415-126">**System.Runtime.Serialization**</span><span class="sxs-lookup"><span data-stu-id="5a415-126">**System.Runtime.Serialization**</span></span>

## <a name="code-has-been-added"></a><span data-ttu-id="5a415-127">Um código foi adicionado</span><span class="sxs-lookup"><span data-stu-id="5a415-127">Code has been added</span></span>
### <a name="code-files-were-added-to-your-project"></a><span data-ttu-id="5a415-128">Arquivos de código foram adicionados ao seu projeto</span><span class="sxs-lookup"><span data-stu-id="5a415-128">Code files were added to your project</span></span>
<span data-ttu-id="5a415-129">Uma classe de inicialização de autenticação **App_Start/Startup.Auth.cs** foi adicionada ao seu projeto contendo lógica de inicialização para autenticação do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5a415-129">An authentication startup class, **App_Start/Startup.Auth.cs** was added to your project containing startup logic for Azure AD authentication.</span></span> <span data-ttu-id="5a415-130">Além disso, uma classe de controlador, Controllers/AccountController.cs, foi adicionada, contendo os métodos **SignIn()** e **SignOut()**.</span><span class="sxs-lookup"><span data-stu-id="5a415-130">Also, a controller class, Controllers/AccountController.cs was added which contains **SignIn()** and **SignOut()** methods.</span></span> <span data-ttu-id="5a415-131">Por fim, uma exibição parcial, **Views/Shared/_LoginPartial.cshtml**, foi adicionada, contendo um link de ação para SignIn/SignOut.</span><span class="sxs-lookup"><span data-stu-id="5a415-131">Finally, a partial view, **Views/Shared/_LoginPartial.cshtml** was added containing an action link for SignIn/SignOut.</span></span>

### <a name="startup-code-was-added-to-your-project"></a><span data-ttu-id="5a415-132">O código de inicialização foi adicionado ao seu projeto</span><span class="sxs-lookup"><span data-stu-id="5a415-132">Startup code was added to your project</span></span>
<span data-ttu-id="5a415-133">Se você já tiver uma classe Startup em seu projeto, o método **Configuration** terá sido atualizado para incluir uma chamada para **ConfigureAuth(app)**.</span><span class="sxs-lookup"><span data-stu-id="5a415-133">If you already had a Startup class in your project, the **Configuration** method was updated to include a call to **ConfigureAuth(app)**.</span></span> <span data-ttu-id="5a415-134">Caso contrário, uma classe Startup foi adicionada ao projeto.</span><span class="sxs-lookup"><span data-stu-id="5a415-134">Otherwise, a Startup class was added to your project.</span></span>

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a><span data-ttu-id="5a415-135">Seu app.config ou web.config tem novos valores de configuração</span><span class="sxs-lookup"><span data-stu-id="5a415-135">Your app.config or web.config has new configuration values</span></span>
<span data-ttu-id="5a415-136">As entradas de configuração a seguir foram adicionadas.</span><span class="sxs-lookup"><span data-stu-id="5a415-136">The following configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientId" value="ClientId from the new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="The selected Azure AD Domain" />
        <add key="ida:TenantId" value="The Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a><span data-ttu-id="5a415-137">Foi criado um aplicativo do Azure Active Directory (AD)</span><span class="sxs-lookup"><span data-stu-id="5a415-137">An Azure Active Directory (AD) App was created</span></span>
<span data-ttu-id="5a415-138">Um Aplicativo Azure AD foi criado no diretório selecionado no assistente.</span><span class="sxs-lookup"><span data-stu-id="5a415-138">An Azure AD Application was created in the directory that you selected in the wizard.</span></span>

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="5a415-139">Se eu marquei *Desabilitar autenticação de Contas de usuários individuais*, quais alterações adicionais foram feitas ao meu projeto?</span><span class="sxs-lookup"><span data-stu-id="5a415-139">If I checked *disable Individual User Accounts authentication*, what additional changes were made to my project?</span></span>
<span data-ttu-id="5a415-140">Referências ao pacote NuGet foram removidas e arquivos foram removidos e copiados.</span><span class="sxs-lookup"><span data-stu-id="5a415-140">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="5a415-141">Dependendo do estado do seu projeto, você terá de remover manualmente referências ou arquivos adicionais ou modificar o código conforme apropriado.</span><span class="sxs-lookup"><span data-stu-id="5a415-141">Depending on the state of your project, you may have to manually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="5a415-142">Referências ao pacotes NuGet removidas (para aquelas presentes)</span><span class="sxs-lookup"><span data-stu-id="5a415-142">NuGet package references removed (for those present)</span></span>
* <span data-ttu-id="5a415-143">**Microsoft.AspNet.Identity.Core**</span><span class="sxs-lookup"><span data-stu-id="5a415-143">**Microsoft.AspNet.Identity.Core**</span></span>
* <span data-ttu-id="5a415-144">**Microsoft.AspNet.Identity.EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="5a415-144">**Microsoft.AspNet.Identity.EntityFramework**</span></span>
* <span data-ttu-id="5a415-145">**Microsoft.AspNet.Identity.Owin**</span><span class="sxs-lookup"><span data-stu-id="5a415-145">**Microsoft.AspNet.Identity.Owin**</span></span>

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="5a415-146">Arquivos de código copiados e removidos (para aqueles presentes)</span><span class="sxs-lookup"><span data-stu-id="5a415-146">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="5a415-147">Cada um dos seguintes arquivos foi copiado e removido do projeto.</span><span class="sxs-lookup"><span data-stu-id="5a415-147">Each of following files was backed up and removed from the project.</span></span> <span data-ttu-id="5a415-148">Arquivos de backup estão localizados em uma pasta “Backup” na raiz do diretório do projeto.</span><span class="sxs-lookup"><span data-stu-id="5a415-148">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* <span data-ttu-id="5a415-149">**App_Start\IdentityConfig.cs**</span><span class="sxs-lookup"><span data-stu-id="5a415-149">**App_Start\IdentityConfig.cs**</span></span>
* <span data-ttu-id="5a415-150">**Controllers\ManageController.cs**</span><span class="sxs-lookup"><span data-stu-id="5a415-150">**Controllers\ManageController.cs**</span></span>
* <span data-ttu-id="5a415-151">**Models\IdentityModels.cs**</span><span class="sxs-lookup"><span data-stu-id="5a415-151">**Models\IdentityModels.cs**</span></span>
* <span data-ttu-id="5a415-152">**Models\ManageViewModels.cs**</span><span class="sxs-lookup"><span data-stu-id="5a415-152">**Models\ManageViewModels.cs**</span></span>

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="5a415-153">Arquivos de código copiados (para aqueles presentes)</span><span class="sxs-lookup"><span data-stu-id="5a415-153">Code files backed up (for those present)</span></span>
<span data-ttu-id="5a415-154">Cada um dos seguintes arquivos foi copiado antes de ser substituído.</span><span class="sxs-lookup"><span data-stu-id="5a415-154">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="5a415-155">Arquivos de backup estão localizados em uma pasta “Backup” na raiz do diretório do projeto.</span><span class="sxs-lookup"><span data-stu-id="5a415-155">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* <span data-ttu-id="5a415-156">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="5a415-156">**Startup.cs**</span></span>
* <span data-ttu-id="5a415-157">**App_Start\Startup.Auth.cs**</span><span class="sxs-lookup"><span data-stu-id="5a415-157">**App_Start\Startup.Auth.cs**</span></span>
* <span data-ttu-id="5a415-158">**Controllers\AccountController.cs**</span><span class="sxs-lookup"><span data-stu-id="5a415-158">**Controllers\AccountController.cs**</span></span>
* <span data-ttu-id="5a415-159">**Views\Shared\_LoginPartial.cshtml**</span><span class="sxs-lookup"><span data-stu-id="5a415-159">**Views\Shared\_LoginPartial.cshtml**</span></span>

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="5a415-160">Se eu tiver marcado *Ler dados do diretório*, quais alterações adicionais foram feitas ao meu projeto?</span><span class="sxs-lookup"><span data-stu-id="5a415-160">If I checked *Read directory data*, what additional changes were made to my project?</span></span>
<span data-ttu-id="5a415-161">Referências extras foram adicionadas.</span><span class="sxs-lookup"><span data-stu-id="5a415-161">Additional references have been added.</span></span>

### <a name="additional-nuget-package-references"></a><span data-ttu-id="5a415-162">Referências adicionais do pacote do NuGet</span><span class="sxs-lookup"><span data-stu-id="5a415-162">Additional NuGet package references</span></span>
* <span data-ttu-id="5a415-163">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="5a415-163">**EntityFramework**</span></span>
* <span data-ttu-id="5a415-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="5a415-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="5a415-165">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="5a415-165">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="5a415-166">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="5a415-166">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="5a415-167">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="5a415-167">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="5a415-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="5a415-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="5a415-169">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="5a415-169">**System.Spatial**</span></span>

### <a name="additional-net-references"></a><span data-ttu-id="5a415-170">Referências adicionais do .NET</span><span class="sxs-lookup"><span data-stu-id="5a415-170">Additional .NET references</span></span>
* <span data-ttu-id="5a415-171">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="5a415-171">**EntityFramework**</span></span>
* <span data-ttu-id="5a415-172">**EntityFramework.SqlServer**</span><span class="sxs-lookup"><span data-stu-id="5a415-172">**EntityFramework.SqlServer**</span></span>
* <span data-ttu-id="5a415-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="5a415-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="5a415-174">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="5a415-174">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="5a415-175">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="5a415-175">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="5a415-176">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="5a415-176">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="5a415-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="5a415-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="5a415-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span><span class="sxs-lookup"><span data-stu-id="5a415-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span></span>
* <span data-ttu-id="5a415-179">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="5a415-179">**System.Spatial**</span></span>

### <a name="additional-code-files-were-added-to-your-project"></a><span data-ttu-id="5a415-180">Arquivos de código adicional foram adicionados ao seu projeto</span><span class="sxs-lookup"><span data-stu-id="5a415-180">Additional Code files were added to your project</span></span>
<span data-ttu-id="5a415-181">Dois arquivos foram adicionados para dar suporte ao caching de token: **Models\ADALTokenCache.cs** e **Models\ApplicationDbContext.cs**.</span><span class="sxs-lookup"><span data-stu-id="5a415-181">Two files were added to support token caching: **Models\ADALTokenCache.cs** and **Models\ApplicationDbContext.cs**.</span></span>  <span data-ttu-id="5a415-182">Um controlador e uma exibição extras foram adicionados para ilustrar o acesso às informações de perfil do usuário usando as APIs de gráfico do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a415-182">An additional controller and view were added to illustrate accessing user profile information using Azure graph APIs.</span></span>  <span data-ttu-id="5a415-183">Esses arquivos são **Controllers\UserProfileController.cs** e**Views\UserProfile\Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="5a415-183">These files are **Controllers\UserProfileController.cs** and **Views\UserProfile\Index.cshtml**.</span></span>

### <a name="additional-startup-code-was-added-to-your-project"></a><span data-ttu-id="5a415-184">Um código de inicialização extra foi adicionado ao seu projeto</span><span class="sxs-lookup"><span data-stu-id="5a415-184">Additional Startup code was added to your project</span></span>
<span data-ttu-id="5a415-185">No arquivo **startup.auth.cs**, um novo objeto **OpenIdConnectAuthenticationNotifications** foi adicionado ao membro **Notifications** de **OpenIdConnectAuthenticationOptions**.</span><span class="sxs-lookup"><span data-stu-id="5a415-185">In the **startup.auth.cs** file, a new **OpenIdConnectAuthenticationNotifications** object was added to the **Notifications** member of the **OpenIdConnectAuthenticationOptions**.</span></span>  <span data-ttu-id="5a415-186">Isso serve para habilitar o recebimento do código do OAuth e a troca dele por um token de acesso.</span><span class="sxs-lookup"><span data-stu-id="5a415-186">This is to enable receiving the OAuth code and exchanging it for an access token.</span></span>

### <a name="additional-changes-were-made-to-your-appconfig-or-webconfig"></a><span data-ttu-id="5a415-187">Foram feitas alterações adicionais em sua app.config ou web.config</span><span class="sxs-lookup"><span data-stu-id="5a415-187">Additional changes were made to your app.config or web.config</span></span>
<span data-ttu-id="5a415-188">As outras entradas de configuração a seguir foram adicionadas.</span><span class="sxs-lookup"><span data-stu-id="5a415-188">The following additional configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

<span data-ttu-id="5a415-189">As seções de configuração e a cadeia de conexão a seguir foram adicionadas.</span><span class="sxs-lookup"><span data-stu-id="5a415-189">The following configuration sections and connection string have been added.</span></span>

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


### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="5a415-190">Seu aplicativo Active Directory do Azure foi atualizado</span><span class="sxs-lookup"><span data-stu-id="5a415-190">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="5a415-191">Seu Aplicativo do Azure Active Directory foi atualizado para incluir a permissão *Ler dados do diretório* e uma chave adicional foi criada, que foi então usada como o *ida:ClientSecret* no arquivo **web.config**.</span><span class="sxs-lookup"><span data-stu-id="5a415-191">Your Azure Active Directory App was updated to include the *Read directory data* permission and an additional key was created which was then used as the *ida:ClientSecret* in the **web.config** file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a415-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5a415-192">Next steps</span></span>
- [<span data-ttu-id="5a415-193">Saiba mais sobre o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="5a415-193">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

