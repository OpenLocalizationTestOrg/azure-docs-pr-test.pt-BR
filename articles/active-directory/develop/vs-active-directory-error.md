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
# <a name="diagnosing-errors-with-hello-azure-active-directory-connection-wizard"></a>Diagnosticando erros com hello Assistente de Conexão do Azure Active Directory
Ao detectar o código de autenticação anterior, o Assistente de saudação detectou um tipo de autenticação incompatível.   

## <a name="what-is-being-checked"></a>O que está sendo verificado?
**Observação:** toocorrectly detectar anterior código de autenticação em um projeto, Olá projeto deve ser criado.  Se este erro ocorrer e você não tiver o código de autenticação anterior em seu projeto, compile o projeto novamente e repita a operação.

### <a name="project-types"></a>Tipos de projeto
Assistente de Olá verifica o tipo de saudação do projeto que você desenvolve para que ele pode injetar a lógica de certo de autenticação de saudação no projeto de saudação.  Se houver qualquer controlador que deriva de `ApiController` no projeto hello, projeto de saudação é considerado um projeto WebAPI.  Se houver somente controladores que derivam de `MVC.Controller` no projeto hello, projeto de saudação é considerado um projeto MVC.  Não há suporte para qualquer outra coisa pelo Assistente de saudação.

### <a name="compatible-authentication-code"></a>Código de autenticação compatível
Assistente de saudação também verifica as configurações de autenticação que foi configuradas anteriormente com o Assistente de saudação ou que são compatíveis com o Assistente de saudação.  Se todas as configurações estiverem presentes, ele é considerado um caso reentrante e Olá wizard abre exibe configurações de saudação.  Se apenas algumas das configurações de saudação estiverem presentes, ele será considerado um caso de erro.

Em um projeto MVC, Olá assistente verifica qualquer Olá configurações, que resultam do uso anterior do Assistente de saudação a seguir:

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

Além disso, o Assistente de Olá verifica para qualquer Olá configurações em um projeto de API da Web, que resultam do uso anterior do Assistente de saudação a seguir:

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a>Código de autenticação incompatível
Por fim, o Assistente de saudação tenta toodetect versões de código de autenticação que foram configuradas com as versões anteriores do Visual Studio. Se você recebeu esse erro, significa que seu projeto contém um tipo de autenticação incompatível. Assistente de saudação detecta Olá seguintes tipos de autenticação de versões anteriores do Visual Studio:

* Autenticação do Windows 
* Contas Individuais de Usuário 
* Contas organizacionais 

toodetect a autenticação do Windows em um projeto MVC, Olá assistente procura Olá `authentication` elemento da sua **Web. config** arquivo.

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

toodetect a autenticação do Windows em um projeto de API da Web, Olá assistente procura Olá `IISExpressWindowsAuthentication` elemento do seu projeto **. csproj** arquivo:

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

autenticação de contas de usuário individuais toodetect, Olá assistente tem uma aparência para o elemento de pacote de saudação do seu **Packages** arquivo.

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

toodetect um formato antigo da autenticação de conta organizacional, Olá assistente procura Olá após o elemento de **Web. config**:

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

tipo de autenticação do toochange Olá, remover o tipo de autenticação incompatível hello e execute o Assistente de saudação novamente.

Para obter mais informações, consulte [Cenários de autenticação para o Azure AD](active-directory-authentication-scenarios.md).

#<a name="next-steps"></a>Próximas etapas
- [Cenários de autenticação do Azure AD](active-directory-authentication-scenarios.md)