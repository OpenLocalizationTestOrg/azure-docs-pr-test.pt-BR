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
# <a name="what-happened-toomy-mvc-project-visual-studio-azure-active-directory-connected-service"></a>O projeto do MVC com toomy (Visual Studio do Azure Active Directory conectado serviço)?
> [!div class="op_single_selector"]
> * [Introdução](vs-active-directory-dotnet-getting-started.md)
> * [O que aconteceu](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a>Referências foram adicionadas
### <a name="nuget-package-references"></a>Referências do pacote NuGet
* **Microsoft.IdentityModel.Protocol.Extensions**
* **Microsoft.Owin**
* **Microsoft.Owin.Host.SystemWeb**
* **Microsoft.Owin.Security**
* **Microsoft.Owin.Security.Cookies**
* **Microsoft.Owin.Security.OpenIdConnect**
* **Owin**
* **System.IdentityModel.Tokens.Jwt**

### <a name="net-references"></a>Referências .NET
* **Microsoft.IdentityModel.Protocol.Extensions**
* **Microsoft.Owin**
* **Microsoft.Owin.Host.SystemWeb**
* **Microsoft.Owin.Security**
* **Microsoft.Owin.Security.Cookies**
* **Microsoft.Owin.Security.OpenIdConnect**
* **Owin**
* **System.IdentityModel**
* **System.IdentityModel.Tokens.Jwt**
* **System.Runtime.Serialization**

## <a name="code-has-been-added"></a>Um código foi adicionado
### <a name="code-files-were-added-tooyour-project"></a>Arquivos de código foram adicionados tooyour projeto
Uma classe de inicialização de autenticação, **App_Start/Startup.Auth.cs** foi adicionado tooyour projeto que contém a lógica de inicialização para a autenticação do AD do Azure. Além disso, uma classe de controlador, Controllers/AccountController.cs, foi adicionada, contendo os métodos **SignIn()** e **SignOut()**. Por fim, uma exibição parcial, **Views/Shared/_LoginPartial.cshtml**, foi adicionada, contendo um link de ação para SignIn/SignOut.

### <a name="startup-code-was-added-tooyour-project"></a>Código de inicialização foi adicionado tooyour projeto
Se você já tinha uma classe de inicialização em seu projeto, Olá **configuração** método foi atualizada tooinclude uma chamada muito**ConfigureAuth(app)**. Caso contrário, uma classe de inicialização foi adicionada tooyour projeto.

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a>Seu app.config ou web.config tem novos valores de configuração
Olá entradas de configuração a seguir foram adicionada.

    <appSettings>
        <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="hello selected Azure AD Domain" />
        <add key="ida:TenantId" value="hello Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a>Foi criado um aplicativo do Azure Active Directory (AD)
Um aplicativo do AD do Azure foi criado no diretório de saudação que você selecionou no Assistente de saudação.

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a>Se verifiquei *desabilitar a autenticação de contas de usuário individuais*, quais alterações adicionais foram feitas toomy projeto?
Referências ao pacote NuGet foram removidas e arquivos foram removidos e copiados. Dependendo do estado de saudação do seu projeto, você pode ter toomanually remover referências adicionais ou arquivos ou modificar o código conforme apropriado.

### <a name="nuget-package-references-removed-for-those-present"></a>Referências ao pacotes NuGet removidas (para aquelas presentes)
* **Microsoft.AspNet.Identity.Core**
* **Microsoft.AspNet.Identity.EntityFramework**
* **Microsoft.AspNet.Identity.Owin**

### <a name="code-files-backed-up-and-removed-for-those-present"></a>Arquivos de código copiados e removidos (para aqueles presentes)
Cada um dos seguintes arquivos foi feita e removida do projeto de saudação. Arquivos de backup estão localizados em uma pasta de 'Backup' na raiz de saudação do diretório do projeto hello.

* **App_Start\IdentityConfig.cs**
* **Controllers\ManageController.cs**
* **Models\IdentityModels.cs**
* **Models\ManageViewModels.cs**

### <a name="code-files-backed-up-for-those-present"></a>Arquivos de código copiados (para aqueles presentes)
Cada um dos seguintes arquivos foi copiado antes de ser substituído. Arquivos de backup estão localizados em uma pasta de 'Backup' na raiz de saudação do diretório do projeto hello.

* **Startup.cs**
* **App_Start\Startup.Auth.cs**
* **Controllers\AccountController.cs**
* **Views\Shared\_LoginPartial.cshtml**

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a>Se verifiquei *ler dados do diretório*, quais alterações adicionais foram feitas toomy projeto?
Referências extras foram adicionadas.

### <a name="additional-nuget-package-references"></a>Referências adicionais do pacote do NuGet
* **EntityFramework**
* **Microsoft.Azure.ActiveDirectory.GraphClient**
* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.IdentityModel.Clients.ActiveDirectory**
* **System.Spatial**

### <a name="additional-net-references"></a>Referências adicionais do .NET
* **EntityFramework**
* **EntityFramework.SqlServer**
* **Microsoft.Azure.ActiveDirectory.GraphClient**
* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.IdentityModel.Clients.ActiveDirectory**
* **Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**
* **System.Spatial**

### <a name="additional-code-files-were-added-tooyour-project"></a>Arquivos de código adicionais foram adicionados tooyour projeto
Dois arquivos foram adicionados toosupport cache de token: **Models\ADALTokenCache.cs** e **Models\ApplicationDbContext.cs**.  Um controlador adicional e o modo de exibição foram adicionados tooillustrate acessando informações de perfil de usuário usando o Azure graph APIs.  Esses arquivos são **Controllers\UserProfileController.cs** e**Views\UserProfile\Index.cshtml**.

### <a name="additional-startup-code-was-added-tooyour-project"></a>Código de inicialização adicional foi adicionado tooyour projeto
Em Olá **startup.auth.cs** arquivo, uma nova **OpenIdConnectAuthenticationNotifications** objeto foi adicionado toohello **notificações** membro da saudação  **OpenIdConnectAuthenticationOptions**.  Isso é tooenable recebimento Olá OAuth código e trocá-lo por um token de acesso.

### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a>Outras alterações foram feitas tooyour App. config ou Web. config
Olá seguintes entradas de configuração adicionais foram adicionadas.

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

Olá seguintes seções de configuração e a cadeia de caracteres de conexão foram adicionadas.

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


### <a name="your-azure-active-directory-app-was-updated"></a>Seu aplicativo Active Directory do Azure foi atualizado
Seu aplicativo do Azure Active Directory foi atualizada tooinclude Olá *ler dados do diretório* permissão e uma chave adicional foi criado, que foi usado como Olá *ida: ClientSecret* em Olá  **Web. config** arquivo.

## <a name="next-steps"></a>Próximas etapas
- [Saiba mais sobre o Active Directory do Azure](https://azure.microsoft.com/services/active-directory/)

