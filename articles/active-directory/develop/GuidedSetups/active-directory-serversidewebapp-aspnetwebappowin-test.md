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
## <a name="test-your-code"></a>Testar seu código

Pressione `F5` toorun seu projeto no Visual Studio. Olá navegador será aberto e direcioná-lo muito*http://localhost: {port}* onde você verá Olá *entrar com Microsoft* botão. Vá em frente e clique em toosign no.

Quando estiver pronto tootest, use um trabalho ou escolar (Active Directory do Azure) ou um personal (live.com, outlook.com) conta toosign no. 

![Janela do navegador Entrar com uma Conta da Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![Janela do navegador Entrar com uma Conta da Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a>Resultados esperados
Depois de entrar, o usuário de saudação é redirecionado toohello home page do seu site da web que é hello URL HTTPS especificado em suas informações de registro de aplicativo no hello Portal de registro de aplicativo do Microsoft. Essa página agora mostrará *Olá {User}* e toosign-out de um link e declarações do usuário link toosee hello – que é um controlador de autorização do link toohello criado anteriormente.

### <a name="see-users-claims"></a>Consultar as declarações do usuário
Selecione as declarações do usuário do hello hiperlink toosee hello. Isso leva você toohello controlador e o modo de exibição que só está disponível toousers que são autenticadas.

#### <a name="expected-results"></a>Resultados esperados
 Você deve ver uma tabela que contém propriedades básicas de saudação do usuário Olá conectado:

| Propriedade | Valor | Descrição|
|---|---|---|
| Nome | {Nome completo do usuário} | primeiro e o último nome de usuário Olá
|Nome de Usuário | <span>user@domain.com</span>| saudação de nome de usuário usado tooidentify usuário de saudação conectado
| Assunto| {Subject}|Uma cadeia de caracteres toouniquely identificar logon do usuário Olá entre Olá web|
| ID do locatário| {Guid}| Um *guid* toouniquely representar a organização do Active Directory do Azure do usuário hello.|

Além disso, você verá uma tabela, incluindo todas as declarações de usuário incluídas na solicitação de autenticação. Para obter uma lista de todas as declarações em um Token de ID e uma explicação, veja este [artigo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "Lista de declarações no Token de ID").


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a>Testar o acesso a um método que tem um atributo *[Authorize]* (opcional)
Nesta etapa, você será controlador de teste ao acessar Olá autenticado como um usuário anônimo:<br/>
Selecione Olá vincular toosign-out Olá usuário e o processo de logout Olá concluída.<br/>
Agora no navegador, digite http://localhost: {port} / autenticado tooaccess seu controlador que é protegida com hello `[Authorize]` atributo

#### <a name="expected-results"></a>Resultados esperados
Você deve receber um prompt Olá exigindo o modo de exibição tooauthenticate toosee hello.

## <a name="additional-information"></a>Informações adicionais

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a>Proteger todo o seu site
tooprotect todo o site da web, adicionar Olá `AuthorizeAttribute` muito`GlobalFilters` na `Global.asax` `Application_Start` método:

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> **Como toorestrict os usuários somente uma organização toosign no aplicativo tooyour**

> Por padrão, as contas pessoais (incluindo outlook.com, live.com e outros), bem como contas corporativas e de estudantes de qualquer empresa ou organização que foi integrado ao Active Directory do Azure podem entrar no aplicativo tooyour. 

> Se você quiser que seu aplicativo tooaccept entradas de apenas uma organização do Active Directory do Azure, substitua Olá `Tenant` parâmetro em *Web. config* de `Common` toohello nome do locatário da organização hello – exemplo, *contoso.onmicrosoft.com*. Depois disso, alterar Olá `ValidateIssuer` argumento em sua *classe de inicialização OWIN* muito`true`.

> tooallow usuários de apenas uma lista de organizações específicas, defina `ValidateIssuer` tootrue e use Olá `ValidIssuers` parâmetro toospecify uma lista das organizações.

> Outra opção é um método personalizado de tooimplement emissores de saudação toovalidate usando o parâmetro IssuerValidator. Para saber mais sobre `TokenValidationParameters`, veja [este artigo do MSDN](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters").

