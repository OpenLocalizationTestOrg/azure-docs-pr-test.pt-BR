---
title: "aaaAccess API de serviços de mídia do Azure com a autenticação do Active Directory do Azure | Microsoft Docs"
description: "Saiba mais sobre conceitos e as etapas tootake toouse Azure Active Directory (AD do Azure) tooauthenticate acesso toohello API de serviços de mídia do Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: bb8f75f39100dc37098260c24ab4a199ef689d46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="access-hello-azure-media-services-api-with-azure-ad-authentication"></a>Olá acesso API de serviços de mídia do Azure com a autenticação do AD do Azure
 
Olá API de serviços de mídia do Azure é uma API RESTful. Você pode usá-lo tooperform operações nos recursos de mídia usando uma API REST ou usando SDKs de cliente disponíveis. Os Serviços de Mídia do Azure oferecem um SDK de cliente dos Serviços de Mídia para o Microsoft .NET. toobe autorizado tooaccess recursos de serviços de mídia e hello API de serviços de mídia, você deve primeiro ser autenticado. 

Os Serviços de Mídia dão suporte à [autenticação baseada no Azure AD (Azure Active Directory)](../active-directory/active-directory-whatis.md). Olá serviço REST de mídia do Azure requer que o usuário hello ou aplicativo que faz solicitações da API REST Olá tenham qualquer Olá **Colaborador** ou **proprietário** tooaccess função hello recursos. Para obter mais informações, consulte [Introdução ao controle de acesso baseado em função no portal do Azure de saudação](../active-directory/role-based-access-control-what-is.md).  

> [!IMPORTANT]
> Atualmente, os serviços de mídia oferece suporte a modelo de autenticação de serviço de controle de acesso do Azure hello. No entanto, a autorização de Controle de Acesso será preterida em 1º de junho de 2018. É recomendável que você migre o modelo de autenticação toohello AD do Azure assim que possível.

Este documento fornece uma visão geral de como tooaccess Olá API de serviços de mídia usando APIs REST ou NET.

## <a name="access-control"></a>Controle de acesso

Para Olá toosucceed de solicitação de REST de mídia do Azure, usuário chamada hello deve ter uma função de Colaborador ou proprietário para Olá estar tentando tooaccess de conta de serviços de mídia.  
Somente um usuário com a função de proprietário de saudação pode dar a usuários de toonew de acesso de recursos (conta) de mídia ou aplicativos. função de Colaborador Olá pode acessar somente o recurso de mídia hello.
Solicitações não autorizadas falham, com o código de status 401. Se você vir esse código de erro, verifique se o usuário tem Olá Colaborador ou função de proprietário atribuído Olá conta de usuário Media Services. Você pode verificar isso na Olá portal do Azure. Pesquisar para sua conta de mídia e clique em Olá **controle de acesso** guia. 

![Guia Controle de acesso](./media/media-services-use-aad-auth-to-access-ams-api/media-services-access-control.png)

## <a name="types-of-authentication"></a>Tipos de autenticação 
 
Ao usar a autenticação do Azure AD com os Serviços de Mídia do Azure, você tem duas opções de autenticação:

- **Autenticação de usuário**. Autentica um usuário que está usando Olá aplicativo toointeract com recursos de serviços de mídia. aplicativo interativo Hello primeiro deve solicitar o usuário Olá Olá as credenciais de usuário. Um exemplo é um aplicativo de console de gerenciamento usado por trabalhos de codificação de toomonitor de usuários autorizados ou transmissão ao vivo. 
- **Autenticação de entidade de serviço**. Autentica um serviço. Os aplicativos que geralmente usam esse método de autenticação são aplicativos que executam serviços daemon, serviços de camada intermediária ou trabalhos agendados. Entre os exemplos estão aplicativos Web, aplicativos de funções, aplicativos lógicos, APIs e microsserviços.

### <a name="user-authentication"></a>Autenticação de usuário 

Aplicativos que devem usar o método de autenticação de usuário hello são gerenciamento ou monitoramento de aplicativos nativos: aplicativos móveis, aplicativos do Windows e aplicativos de Console. Esse tipo de solução é útil quando você deseja interação humana com o serviço de saudação em um dos seguintes cenários de saudação:

- Painel de monitoramento dos trabalhos de codificação.
- Painel de monitoramento dos fluxos ao vivo.
- Aplicativo de gerenciamento de recursos de tooadminister usuários móveis ou área de trabalho em uma conta de serviços de mídia.

> [!NOTE]
> Esse método de autenticação não deve ser usado para aplicativos voltados para o consumidor. 

Um aplicativo nativo deve primeiro adquirir um token de acesso do AD do Azure e, em seguida, usá-lo quando você fizer a API de REST de serviços de mídia de toohello de solicitações HTTP. Adicione cabeçalho de solicitação de token toohello Olá acesso. 

Olá diagrama a seguir mostra um fluxo de autenticação de aplicativo interativo típico: 

![Diagrama de aplicativos nativos](./media/media-services-use-aad-auth-to-access-ams-api/media-services-native-aad-app1.png)

Olá precede o diagrama, Olá números representam fluxo Olá de solicitações de saudação em ordem cronológica.

> [!NOTE]
> Quando você usa o método de autenticação de usuário hello, todos os aplicativos compartilham Olá URI de redirecionamento de mesma ID de cliente do aplicativo nativo (padrão) e o aplicativo nativo. 

1. Solicite as credenciais a um usuário.
2. Solicite um token de acesso do AD do Azure com hello parâmetros a seguir:  

    * Ponto de extremidade do locatário do Azure AD.

        informações de locatário Olá podem ser recuperadas da saudação portal do Azure. Coloque o cursor sobre nome de saudação do usuário conectado Olá no canto superior direito da saudação.
    * URI de recurso dos Serviços de Mídia. 

        Esse URI é hello mesmo para contas de serviços de mídia que estejam no hello mesmo ambiente do Azure (por exemplo, https://rest.media.azure.net).

    * ID do cliente do aplicativo (nativo) dos Serviços de Mídia.
    * URI de redirecionamento do aplicativo (nativo) dos Serviços de Mídia.
    * URI de recurso dos Serviços de Mídia REST.
        
        Olá URI representa o ponto de extremidade da API REST de saudação (por exemplo, https://test03.restv2.westus.media.azure.net/api/).

    tooget valores desses parâmetros, consulte [usar configurações de autenticação tooaccess portal do Azure AD do Azure Olá](media-services-portal-get-started-with-aad.md) usando a opção de autenticação de usuário hello.

3. token de acesso de saudação do AD do Azure é enviado toohello cliente.
4. cliente Olá envia uma solicitação toohello API de REST de mídia do Azure com token de acesso de saudação do AD do Azure.
5. cliente Olá obtém dados de saudação do Media Services.

Para obter informações sobre como toocommunicate de autenticação toouse AD do Azure com REST solicitações usando o SDK de cliente .NET de serviços de mídia hello, consulte [tooaccess de autenticação de uso do AD do Azure Olá API de serviços de mídia com o .NET](media-services-dotnet-get-started-with-aad.md). 

Se você não estiver usando o SDK de cliente .NET de serviços de mídia hello, você deve criar manualmente uma solicitação de token de acesso do AD do Azure usando os parâmetros de saudação descritos na etapa 2. Para obter mais informações, consulte [como tooget de biblioteca de autenticação de saudação do AD do Azure toouse Olá token do AD do Azure](../active-directory/develop/active-directory-authentication-libraries.md).

### <a name="service-principal-authentication"></a>Autenticação de entidade de serviço

Os aplicativos que geralmente usam esse método de autenticação são aplicativos que executam serviços de camada intermediária e trabalhos agendados: aplicativos Web, aplicativos de funções, aplicativos lógicos, APIs e microsserviços. Esse método de autenticação também é adequado para aplicativos interativos na qual você talvez queira toouse um toomanage recursos da conta de serviço.

Quando você usa os cenários de consumidor toobuild do método de autenticação principal de serviço Olá, autenticação normalmente é manipulada na camada intermediária de saudação (por meio de alguns API) e não diretamente em um aplicativo móvel ou área de trabalho. 

toouse esse método, criar um aplicativo do AD do Azure e serviço principal em seu próprio locatário. Depois de criar o aplicativo hello, dê Olá aplicativo Colaborador ou proprietário da função acesso toohello conta do Media Services. Você pode fazer isso no hello portal do Azure, usando a CLI do Azure, ou com um script do PowerShell. Use também um aplicativo existente do Azure AD. Você pode registrar e gerenciar seu aplicativo do Azure AD e o serviço principal [no portal do Azure de saudação](media-services-portal-get-started-with-aad.md). Também faça isso usando a [CLI 2.0 do Azure](media-services-use-aad-auth-to-access-ams-api.md) ou o [PowerShell](media-services-powershell-create-and-configure-aad-app.md). 

![Aplicativos de camada intermediária](./media/media-services-use-aad-auth-to-access-ams-api/media-services-principal-service-aad-app1.png)

Depois de criar seu aplicativo do AD do Azure, você obter valores hello configurações a seguir. Você precisa destes valores para autenticação:

- ID do cliente 
- Segredo do cliente 

Nas Olá anterior figura, Olá números representam fluxo Olá de solicitações de saudação em ordem cronológica:
    
1. Um aplicativo de camada intermediária (API da web ou aplicativo web) solicita um token de acesso do AD do Azure que tenha Olá parâmetros a seguir:  

    * Ponto de extremidade do locatário do Azure AD.

        informações de locatário Olá podem ser recuperadas da saudação portal do Azure. Coloque o cursor sobre nome de saudação do usuário conectado Olá no canto superior direito da saudação.
    * URI de recurso dos Serviços de Mídia. 

        Esse URI é hello mesmo para contas de serviços de mídia que estão localizadas em Olá mesmo ambiente do Azure (por exemplo, https://rest.media.azure.net).

    * URI de recurso dos Serviços de Mídia REST.

        Olá URI representa o ponto de extremidade da API REST de saudação (por exemplo, https://test03.restv2.westus.media.azure.net/api/).

    * Valores de aplicativo do Azure AD: Olá ID do cliente e o segredo do cliente.
    
    tooget valores desses parâmetros, consulte [usar configurações de autenticação tooaccess portal do Azure AD do Azure Olá](media-services-portal-get-started-with-aad.md) usando a opção de autenticação principal do serviço de saudação.

2. token de acesso de saudação do AD do Azure é enviada a camada intermediária toohello.
4. camada intermediária Olá envia a solicitação toohello API de REST de mídia do Azure com o token do AD do Azure hello.
5. camada intermediária Olá obtém dados de saudação do Media Services.

Para obter mais informações sobre como toocommunicate de autenticação toouse AD do Azure com REST solicitações usando o SDK de cliente .NET de serviços de mídia hello, consulte [tooaccess de autenticação de uso do AD do Azure API de serviços de mídia do Azure com o .NET](media-services-dotnet-get-started-with-aad.md). 

Se você não estiver usando o SDK de cliente .NET de serviços de mídia hello, você deve criar manualmente uma solicitação de token do AD do Azure usando os parâmetros descritos na etapa 1. Para obter mais informações, consulte [como tooget de biblioteca de autenticação de saudação do AD do Azure toouse Olá token do AD do Azure](../active-directory/develop/active-directory-authentication-libraries.md).

## <a name="troubleshooting"></a>Solucionar problemas

Exceção: "o servidor remoto Olá retornou um erro: não autorizado (401)."

Solução: Para Olá toosucceed de solicitação de REST de serviços de mídia, usuário chamada hello deve ser uma função de Colaborador ou proprietário Olá estar tentando tooaccess de conta de serviços de mídia. Para obter mais informações, consulte Olá [controle de acesso](media-services-use-aad-auth-to-access-ams-api.md#access-control) seção.

## <a name="resources"></a>Recursos

Olá artigos a seguir está uma visão geral dos conceitos de autenticação do AD do Azure: 

- [Cenários de autenticação abordados pelo Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md#basics-of-authentication-in-azure-ad)
- [Adicionar, atualizar ou remover um aplicativo no Azure AD](../active-directory/develop/active-directory-integrating-applications.md)
- [Configurar e gerenciar o Controle de Acesso Baseado em Função usando o PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)

## <a name="next-steps"></a>Próximas etapas

* Usar Olá portal do Azure também[acessar tooconsume de autenticação do AD do Azure API de serviços de mídia do Azure](media-services-portal-get-started-with-aad.md).
* Usar autenticação do Azure AD também[acessar a API de serviços de mídia do Azure com o .NET](media-services-dotnet-get-started-with-aad.md).

