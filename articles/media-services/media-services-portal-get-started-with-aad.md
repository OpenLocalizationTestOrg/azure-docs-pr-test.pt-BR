---
title: "aaaGet iniciado com a autenticação do AD do Azure usando Olá portal do Azure | Microsoft Docs"
description: "Saiba como toouse hello Azure tooaccess portal do Azure Active Directory (AD do Azure) autenticação tooconsume Olá API de serviços de mídia do Azure."
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
ms.openlocfilehash: 497ad1806b3fd1262802adefb6e12b65ee9f2d61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-ad-authentication-by-using-hello-azure-portal"></a>Introdução à autenticação do AD do Azure usando Olá portal do Azure

Saiba como toouse hello Azure tooaccess portal do Azure Active Directory (AD do Azure) autenticação tooaccess Olá API de serviços de mídia do Azure.

## <a name="prerequisites"></a>Pré-requisitos

- Uma conta do Azure. Se você não tiver uma conta, comece com uma [avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/). 
- Uma conta dos Serviços de Mídia. Para obter mais informações, consulte [criar uma conta de serviços de mídia do Azure usando o portal do Azure de saudação](media-services-portal-create-account.md).
- Certifique-se de examinar Olá [acessar API do Azure Media Services visão geral de autenticação do AD do Azure](media-services-use-aad-auth-to-access-ams-api.md). 

Quando você usar a autenticação do AD Azure com Serviços de Mídia do Azure haverá duas opções de autenticação:

- **Autenticação de usuário**. Autentica um usuário que está usando Olá aplicativo toointeract com recursos de serviços de mídia. aplicativo interativo do Hello primeiro deve solicitar credenciais ao usuário Olá. Um exemplo é um aplicativo de console de gerenciamento usado por trabalhos de codificação de toomonitor de usuários autorizados ou transmissão ao vivo. 
- **Autenticação de entidade de serviço**. Autentica um serviço. Os aplicativos que geralmente usam esse método de autenticação são aplicativos que executam serviços de daemon, serviços de camada intermediária ou trabalhos agendados: aplicativos Web, aplicativos de funções, aplicativos lógicos, APIs ou um microsserviço.

> [!IMPORTANT]
> Atualmente, os serviços de mídia oferece suporte a modelo de autenticação de serviço de controle de acesso do Azure hello. No entanto, a autorização de Controle de Acesso será preterida em 1º de junho de 2018. É recomendável que você migre o modelo de autenticação toohello AD do Azure assim que possível.

## <a name="select-hello-authentication-method"></a>Selecionar método de autenticação de saudação

1. Em Olá [portal do Azure](https://portal.azure.com/), selecione sua conta de serviços de mídia.
2. Selecione como tooconnect toohello API de serviços de mídia.

    ![Selecione a página do método de conexão](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started01.png)

## <a name="user-authentication"></a>Autenticação de usuário

tooconnect toohello API de serviços de mídia usando Olá a opção de autenticação de usuário, aplicativo de cliente Olá precisa toorequest um token do AD do Azure que tem Olá parâmetros a seguir:  

* Ponto de extremidade de locatário do Azure AD
* URI de recursos dos Serviços de Mídia
* ID do cliente do aplicativo (nativo) dos Serviços de Mídia 
* URI de redirecionamento do aplicativo (nativo) dos Serviços de Mídia 
* URI de recurso dos Serviços de Mídia REST

Você pode obter valores de saudação para esses parâmetros no hello **API de serviços de mídia com a autenticação do usuário** página. 

![Conecte-se com a página de autenticação de usuário](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started02.png)

Se você conectar toohello API de serviços de mídia usando Olá SDK do Media Services Microsoft .NET, Olá necessário valores são tooyou disponível como parte da saudação SDK. Para obter mais informações, consulte [tooaccess de autenticação de uso do AD do Azure Olá API de serviços de mídia do Azure com o .NET](media-services-dotnet-get-started-with-aad.md).

Se você não estiver usando o SDK de cliente .NET de serviços de mídia Olá, você deve criar manualmente uma solicitação de token do AD do Azure usando os parâmetros de saudação discutidos anteriormente. Para obter mais informações, consulte [como tooget de biblioteca de autenticação de saudação do AD do Azure toouse Olá token do AD do Azure](../active-directory/develop/active-directory-authentication-libraries.md).

## <a name="service-principal-authentication"></a>Autenticação de entidade de serviço

tooconnect toohello API de serviços de mídia usando Olá opção principal do serviço, seu aplicativo de camada intermediária (API da web ou aplicativo web) precisa toorequest um token do AD do Azure que tem Olá parâmetros a seguir:  

* Ponto de extremidade de locatário do Azure AD
* URI de recursos dos Serviços de Mídia 
* URI de recurso dos Serviços de Mídia REST
* Valores de aplicativo do Azure AD: Olá **ID do cliente** e **segredo do cliente**

Você pode obter valores de saudação para esses parâmetros no hello **conectar tooMedia API de serviços com a entidade de serviço** página. Use este toocreate página Azure um novo aplicativo do AD ou tooselect um existente. Depois de selecionar o aplicativo do Azure AD Olá, você pode obter ID saudação do cliente (ID do aplicativo) e gerar valores de segredo (chave) de cliente hello. 

![Conecte-se com a página da entidade de serviço](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started04.png)

Olá quando **entidade de serviço** folha é aberto, o aplicativo do Azure AD de primeiro hello que atenda aos critérios a seguir de saudação é selecionado:

- Trata-se de um aplicativo do AD Azure registrado.
- Ele tem permissões de Colaborador ou controle de acesso de Owner Role-Based na conta de saudação.

Depois de criar ou selecionar um aplicativo do AD do Azure, você pode criar e copiar um segredo do cliente (chave) e Olá ID do cliente (ID do aplicativo). ID do cliente e o segredo do cliente Olá são token de acesso de saudação tooget necessário nesse cenário.

Se você não tiver permissões toocreate AD do Azure aplicativos em seu domínio, controles de aplicativo do AD do Azure Olá da folha de saudação não são mostrados, e uma mensagem de aviso é exibida.

Se você conectar toohello API de serviços de mídia usando o SDK do Media Services .NET de hello, consulte [tooaccess de autenticação de uso do AD do Azure Olá API de serviços de mídia do Azure com o .NET](media-services-dotnet-get-started-with-aad.md).

Se você não estiver usando o SDK de cliente .NET de serviços de mídia hello, você deve criar manualmente uma solicitação de token do AD do Azure usando os parâmetros de saudação discutidos anteriormente. Para obter mais informações, consulte [como tooget de biblioteca de autenticação de saudação do AD do Azure toouse Olá token do AD do Azure](../active-directory/develop/active-directory-authentication-libraries.md).

### <a name="get-hello-client-id-and-client-secret"></a>Obter segredo do cliente e a ID de cliente de saudação

Depois de selecionar um aplicativo AD do Azure existente ou selecione Olá opção toocreate um novo, Olá botões a seguir são exibidos:

![Botão de gerenciar permissões e botão de gerenciar aplicativo](./media/media-services-portal-get-started-with-aad/media-services-portal-manage.png)

Olá tooopen folha de aplicativo do AD do Azure, clique em **gerenciar aplicativo**. Em Olá **gerenciar aplicativo** folha, você pode obter a ID do cliente do aplicativo hello (ID do aplicativo). toogenerate um segredo do cliente (chave), selecione **chaves**.

![Gerenciar a opção Chaves da folha do aplicativo](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started06.png) 

### <a name="manage-permissions-and-hello-application"></a>Gerenciar permissões e o aplicativo hello

Depois de selecionar o aplicativo do AD do Azure hello, você pode gerenciar permissões e o aplicativo hello. tooset a sua tooaccess de aplicativo do AD do Azure outros aplicativos, clique em **gerenciar permissões**. Para tarefas de gerenciamento, como alterar as chaves e as URLs de resposta ou manifesto do aplicativo do tooedit Olá, clique em **gerenciar aplicativo**.

### <a name="edit-hello-apps-settings-or-manifest"></a>Editar configurações do aplicativo hello ou manifesto

configurações do aplicativo do tooedit hello ou o manifesto, clique em **gerenciar aplicativo**.

![Gerenciar a página do aplicativo](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started05.png)

## <a name="next-steps"></a>Próximas etapas

Introdução ao [carregando arquivos tooyour conta](media-services-portal-upload-files.md).
