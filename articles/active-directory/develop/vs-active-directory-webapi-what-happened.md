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
# <a name="what-happened-toomy-webapi-project-visual-studio-azure-active-directory-connected-service"></a>O projeto de WebApi toomy com (Visual Studio do Azure Active Directory conectado serviço)
> [!div class="op_single_selector"]
> * [Introdução](vs-active-directory-webapi-getting-started.md)
> * [O que aconteceu](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a>Referências foram adicionadas
### <a name="nuget-package-references"></a>Referências do pacote NuGet
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a>Referências .NET
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a>Alterações de código
### <a name="code-files-were-added-tooyour-project"></a>Arquivos de código foram adicionados tooyour projeto
Uma classe de inicialização de autenticação, **App_Start/Startup.Auth.cs** foi adicionado tooyour projeto que contém a lógica de inicialização para a autenticação do AD do Azure.

### <a name="startup-code-was-added-tooyour-project"></a>Código de inicialização foi adicionado tooyour projeto
Se você já tinha uma classe de inicialização em seu projeto, Olá **configuração** método foi atualizada tooinclude uma chamada muito`ConfigureAuth(app)`. Caso contrário, uma classe de inicialização foi adicionada tooyour projeto.

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a>Seu arquivo app.config ou web.config possui novos valores de configuração.
Olá entradas de configuração a seguir foram adicionada.

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="hello App ID Uri from hello wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a>Um aplicativo do Azure AD foi criado
Um aplicativo do AD do Azure foi criado no diretório de saudação que você selecionou no Assistente de saudação.

[Saiba mais sobre o Active Directory do Azure](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a>Se verifiquei *desabilitar a autenticação de contas de usuário individuais*, quais alterações adicionais foram feitas toomy projeto?
Referências ao pacote NuGet foram removidas e arquivos foram removidos e copiados. Dependendo do estado de saudação do seu projeto, você pode ter toomanually remover referências adicionais ou arquivos ou modificar o código conforme apropriado.

### <a name="nuget-package-references-removed-for-those-present"></a>Referências ao pacotes NuGet removidas (para aquelas presentes)
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a>Arquivos de código copiados e removidos (para aqueles presentes)
Cada um dos seguintes arquivos foi feita e removida do projeto de saudação. Arquivos de backup estão localizados em uma pasta de 'Backup' na raiz de saudação do diretório do projeto hello.

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a>Arquivos de código copiados (para aqueles presentes)
Cada um dos seguintes arquivos foi copiado antes de ser substituído. Arquivos de backup estão localizados em uma pasta de 'Backup' na raiz de saudação do diretório do projeto hello.

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a>Se verifiquei *ler dados do diretório*, quais alterações adicionais foram feitas toomy projeto?
### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a>Outras alterações foram feitas tooyour App. config ou Web. config
Olá seguintes entradas de configuração adicionais foram adicionadas.

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a>Seu aplicativo Active Directory do Azure foi atualizado
Seu aplicativo do Azure Active Directory foi atualizada tooinclude Olá *ler dados do diretório* permissão e uma chave adicional foi criado, que foi usado como Olá *ida: senha* em Olá `web.config` arquivo.

## <a name="next-steps"></a>Próximas etapas
- [Saiba mais sobre o Active Directory do Azure](https://azure.microsoft.com/services/active-directory/)

