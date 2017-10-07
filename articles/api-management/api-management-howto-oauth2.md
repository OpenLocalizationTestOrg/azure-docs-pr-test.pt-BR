---
title: contas de desenvolvedor aaaAuthorize usando OAuth 2.0 no gerenciamento de API do Azure | Microsoft Docs
description: "Saiba como usuários tooauthorize usando OAuth 2.0 no gerenciamento de API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 78c48247-64f0-4708-b2d0-98b61a821283
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 934901dd6df399470a3257bf7a3a9b9fb5f40d5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-oauth-20-in-azure-api-management"></a>Como desenvolvedor de tooauthorize contas usando OAuth 2.0 no gerenciamento de API do Azure
Suportam a várias APIs [OAuth 2.0](http://oauth.net/2/) toosecure Olá API e certifique-se de que apenas usuários válidos tenham acesso, e eles podem acessar apenas os recursos toowhich que estão qualificado. No Console de desenvolvedor de interativo do gerenciamento de API do Azure toouse ordem, com essas APIs, Olá serviço permite que você tooconfigure sua toowork de instância de serviço com o OAuth 2.0 habilitado API.

## <a name="prerequisites"> </a>Pré-requisitos
Este guia mostra como tooconfigure seu toouse de instância de serviço de gerenciamento de API autorização do OAuth 2.0 para desenvolvedor de contas, mas não mostram como provedor tooconfigure an OAuth 2.0. configuração de saudação para cada provedor é diferente, embora Olá etapas são semelhantes, e Olá necessárias informações usadas na configuração OAuth 2.0 em sua instância de serviço de gerenciamento de API do OAuth 2.0 Olá mesmo. Este tópico mostra exemplos ao usar o Active Directory do Azure como um provedor OAuth 2.0.

> [!NOTE]
> Para obter mais informações sobre como configurar o OAuth 2.0 usando o Active Directory do Azure, consulte Olá [WebApp-GraphAPI-DotNet] [ WebApp-GraphAPI-DotNet] exemplo.
> 
> 

## <a name="step1"> </a>Configurar um servidor de autorização do OAuth 2.0 no Gerenciamento de API
tooget iniciado, clique em **portal do publicador** em hello Portal do Azure para seu serviço de gerenciamento de API.

![Portal do editor][api-management-management-console]

> [!NOTE]
> Se você ainda não tiver criado uma instância do serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [Introdução ao gerenciamento de API do Azure] [ Get started with Azure API Management] tutorial.
> 
> 

Clique em **segurança** de saudação **gerenciamento de API** menu da esquerda, clique em de saudação **OAuth 2.0**e, em seguida, clique em **Adicionar servidor de autorização**.

![OAuth 2.0][api-management-oauth2]

Depois de clicar em **Adicionar servidor de autorização**, Olá novo formulário de servidor de autorização é exibido.

![Novo servidor][api-management-oauth2-server-1]

Insira um nome e uma descrição opcional na Olá **nome** e **descrição** campos. 

> [!NOTE]
> Esses campos são o servidor de autorização de saudação OAuth 2.0 tooidentify usado na instância de serviço de gerenciamento de API atual hello e seus valores não vêm do servidor de saudação OAuth 2.0.
> 
> 

Digite hello **URL de página de registro de cliente**. Esta página é onde os usuários podem criar e gerenciar suas contas e varia de acordo com o provedor de saudação OAuth 2.0 usado. Olá **URL de página de registro de cliente** pontos toohello página que os usuários podem usar toocreate e configurar suas próprias contas para provedores OAuth 2.0 que dão suporte ao gerenciamento de contas de usuário. Algumas organizações não configurar ou usar essa funcionalidade, mesmo se o provedor de saudação OAuth 2.0 dá suporte a ele. Se seu provedor OAuth 2.0 não tem gerenciamento de usuários de contas configuradas, insira uma URL de espaço reservado como Olá URL da sua empresa ou uma URL como `https://placeholder.contoso.com`.

a próxima seção saudação do formulário Olá contém Olá **tipos de concessão de código de autorização**, **URL de ponto de extremidade de autorização**, e **método de solicitação de autorização** configurações.

![Novo servidor][api-management-oauth2-server-2]

Especifique a saudação **tipos de concessão de código de autorização** verificando tipos Olá desejado. **código de autorização** é especificado por padrão.

Digite hello **URL de ponto de extremidade de autorização**. Active Directory do Azure, essa URL será semelhante toohello seguinte URL, onde `<client_id>` é substituído por id do cliente Olá que identifica o servidor de aplicativos toohello OAuth 2.0.

`https://login.microsoftonline.com/<client_id>/oauth2/authorize`

Olá **método de solicitação de autorização** Especifica como a solicitação de autorização de saudação será enviada server toohello OAuth 2.0. O **GET** é selecionado por padrão.

Olá próxima seção é onde hello **URL de ponto de extremidade de Token**, **métodos de autenticação de cliente**, **token de acesso de envio de método**, e **escopopadrão** especificados.

![Novo servidor][api-management-oauth2-server-3]

Para um servidor do Azure Active Directory OAuth 2.0, Olá **URL de ponto de extremidade de Token** terá Olá seguinte formato, onde `<APPID>` tem o formato de saudação do `yourapp.onmicrosoft.com`.

`https://login.microsoftonline.com/<APPID>/oauth2/token`

Olá a configuração padrão para **métodos de autenticação de cliente** é **básica**, e **token de acesso de envio de método** é **cabeçalho de autorização**. Esses valores são configurados nessa seção do formulário hello, juntamente com hello **escopo padrão**.

Olá **as credenciais do cliente** seção contém Olá **ID do cliente** e **segredo do cliente**, que é obtido durante o processo de criação e configuração de saudação do seu OAuth 2.0 servidor. Uma vez Olá **ID do cliente** e **segredo do cliente** forem especificados, hello **redirect_uri** para Olá **código de autorização** é gerado. Esse URI é a URL de resposta de saudação tooconfigure usado na configuração de servidor OAuth 2.0.

![Novo servidor][api-management-oauth2-server-4]

Se **tipos de concessão de código de autorização** está definido muito**senha do proprietário do recurso**, Olá **as credenciais de senha de proprietário do recurso** seção é toospecify usada as credenciais; Caso contrário, você pode deixar em branco.

![Novo servidor][api-management-oauth2-server-5]

Depois que o formulário de saudação for concluído, clique em **salvar** configuração do servidor de autorização toosave Olá OAuth 2.0 do API de gerenciamento. Depois que a configuração do servidor de saudação for salvo, você pode configurar APIs toouse essa configuração, conforme mostrado na próxima seção, Olá.

## <a name="step2"></a>Configurar toouse uma API autorização do usuário OAuth 2.0
Clique em **APIs** de saudação **gerenciamento de API** Olá menu à esquerda, clique em nome de saudação da API de saudação desejada **segurança**e, em seguida, marque caixa Olá **OAuth 2.0**.

![Autorização do usuário][api-management-user-authorization]

Selecione Olá desejado **servidor de autorização** na lista suspensa de saudação e clique em **salvar**.

![Autorização do usuário][api-management-user-authorization-save]

## <a name="step3"></a>Teste autorização do usuário Olá OAuth 2.0 no Portal do desenvolvedor da saudação
Depois que você configurou o servidor de autorização OAuth 2.0 e configurou sua API toouse nesse servidor, você pode testá-lo indo toohello Portal do desenvolvedor e chamar uma API.  Clique em **portal do desenvolvedor** no menu superior direito da saudação.

![Portal do desenvolvedor][api-management-developer-portal-menu]

Clique em **APIs** no menu superior hello e selecione **Echo API**.

![API de Eco][api-management-apis-echo-api]

> [!NOTE]
> Se você tiver apenas uma API configurada ou conta tooyour visível, clique em APIs leva você diretamente toohello operações para essa API.
> 
> 

Selecione Olá **obter recursos** operação, clique em **abrir o Console**e, em seguida, selecione **código de autorização** Olá suspenso.

![Abrir console][api-management-open-console]

Quando **código de autorização** é selecionada, uma janela pop-up será exibida com hello formulário de inscrição do provedor de saudação OAuth 2.0. Neste exemplo, formulário de entrada hello é fornecido pelo Active Directory do Azure.

> [!NOTE]
> Se você tiver pop-ups desabilitado, você será solicitado a tooenable-los pelo navegador hello. Depois que você ativá-los, selecione **código de autorização** novamente e hello formulário de entrada será exibido.
> 
> 

![Entrar][api-management-oauth2-signin]

Depois de ter entrado, Olá **cabeçalhos de solicitação** são preenchidas com um `Authorization : Bearer` cabeçalho que autoriza a solicitação de saudação.

![Token do cabeçalho da solicitação][api-management-request-header-token]

Agora você pode configurar valores de saudação desejado para Olá restantes parâmetros e enviar solicitação de saudação. 

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre como usar o OAuth 2.0 e o gerenciamento de API, consulte o seguinte de saudação vídeo e acompanha [artigo](api-management-howto-protect-backend-with-aad.md).

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-oauth2/api-management-management-console.png
[api-management-oauth2]: ./media/api-management-howto-oauth2/api-management-oauth2.png
[api-management-user-authorization]: ./media/api-management-howto-oauth2/api-management-user-authorization.png
[api-management-user-authorization-save]: ./media/api-management-howto-oauth2/api-management-user-authorization-save.png
[api-management-oauth2-signin]: ./media/api-management-howto-oauth2/api-management-oauth2-signin.png
[api-management-request-header-token]: ./media/api-management-howto-oauth2/api-management-request-header-token.png
[api-management-developer-portal-menu]: ./media/api-management-howto-oauth2/api-management-developer-portal-menu.png
[api-management-open-console]: ./media/api-management-howto-oauth2/api-management-open-console.png
[api-management-oauth2-server-1]: ./media/api-management-howto-oauth2/api-management-oauth2-server-1.png
[api-management-oauth2-server-2]: ./media/api-management-howto-oauth2/api-management-oauth2-server-2.png
[api-management-oauth2-server-3]: ./media/api-management-howto-oauth2/api-management-oauth2-server-3.png
[api-management-oauth2-server-4]: ./media/api-management-howto-oauth2/api-management-oauth2-server-4.png
[api-management-oauth2-server-5]: ./media/api-management-howto-oauth2/api-management-oauth2-server-5.png
[api-management-apis-echo-api]: ./media/api-management-howto-oauth2/api-management-apis-echo-api.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

