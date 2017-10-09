---
title: aaaManage streaming pontos de extremidade com hello portal do Azure | Microsoft Docs
description: "Este tópico mostra como pontos de extremidade de streaming de toomanage com hello portal do Azure."
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: bb1aca25-d23a-4520-8c45-44ef3ecd5371
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: dfa9352894d37edb317a6334d7f109419deb362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-hello-azure-portal"></a>Gerenciar pontos de extremidade de streaming com hello portal do Azure

Este tópico mostra como toouse Olá pontos de extremidade de streaming do toomanage portal do Azure. 

>[!NOTE]
>Verifique se Olá de tooreview [visão geral](media-services-streaming-endpoints-overview.md) tópico. 

Para obter informações sobre como tooscale Olá ponto de extremidade de streaming, consulte [isso](media-services-portal-scale-streaming-endpoints.md) tópico.

## <a name="start-managing-streaming-endpoints"></a>Começar a gerenciar pontos de extremidade de streaming 

toostart gerenciar pontos de extremidade de streaming para sua conta, Olá a seguir.

1. Em Olá [portal do Azure](https://portal.azure.com/), selecione sua conta de serviços de mídia do Azure.
2. Em Olá **configurações** folha, selecione **pontos de extremidade de Streaming**.
   
    ![ponto de extremidade de streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints1.png)

> [!NOTE]
> Você será cobrado apenas quando seu ponto de extremidade de streaming estiver em estado de execução.

## <a name="adddelete-a-streaming-endpoint"></a>Adicionar/excluir um ponto de extremidade de streaming

>[!NOTE]
>padrão de saudação ponto de extremidade de streaming não pode ser excluído.

usando o ponto de extremidade de streaming tooadd/excluir Olá portal do Azure, Olá a seguir:

1. tooadd um ponto de extremidade de streaming, clique em Olá **+ Endpoint** na parte superior de saudação da página de saudação. 

    Convém vários pontos de extremidade de Streaming se você planejar toohave CDNs diferentes ou um CDN e acesso direto.

2. toodelete um ponto de extremidade de streaming, pressione **excluir** botão.      
3. Clique em Olá **iniciar** saudação do botão toostart ponto de extremidade de streaming.
   
    ![ponto de extremidade de streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints2.png)


## <a id="configure_streaming_endpoints"></a>Configurando Olá ponto de extremidade de Streaming
Ponto de extremidade de streaming permite Olá tooconfigure propriedades a seguir:

* Controle de acesso
* Controle de cache
* Políticas de acesso entre sites

Para obter informações detalhadas sobre essas propriedades, consulte [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).

Você pode configurar o ponto de extremidade de streaming fazendo Olá seguinte:

1. Selecione Olá deseja tooconfigure de ponto de extremidade de streaming.
2. Clique em **Configurações**.

Segue uma breve descrição dos campos de saudação.

![ponto de extremidade de streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints4.png)

1. Política de cache máximo: tooconfigure usado tempo de vida de ativos atendidas por esse ponto de extremidade. Se nenhum valor for definido, o padrão de saudação é usado. valores padrão de saudação também podem ser definidos diretamente no armazenamento do Azure. Se Azure CDN é habilitado para Olá ponto de extremidade de streaming, você não deve definir tooless de valor de política de cache de saudação de 600 segundos.  
2. Endereços IP permitidos: usados endereços IP toospecify que seriam permitidos tooconnect toohello publicado o ponto de extremidade de streaming. Se nenhum endereço IP especificado, qualquer endereço IP poderá ser capaz de tooconnect. Os endereços IP podem ser especificados como um único endereço IP (por exemplo, '10.0.0.1'), um intervalo de IP usando um endereço IP e uma máscara de sub-rede CIDR (por exemplo, '10.0.0.1/22') ou um intervalo de IPs usando um endereço IP e uma máscara de sub-rede em notação decimal com ponto (por exemplo, '10.0.0.1(255.255.255.0)').
3. Configuração de autenticação de cabeçalho de assinatura do Akamai: usado toospecify como a solicitação de autenticação de cabeçalho de assinatura de servidores Akamai está configurada. A data de validade é no formato UTC.

## <a name="scale-your-premium-streaming-endpoint"></a>Dimensionar seu ponto de extremidade de streaming

Para obter mais informações, consulte [este](media-services-portal-scale-streaming-endpoints.md) tópico.

## <a id="enable_cdn"></a>Habilitar a integração da CDN do Azure

Quando você cria uma nova conta, a integração padrão da CDN do Azure para Ponto de Extremidade de Streaming é habilitada por padrão.

Se você quiser mais tarde Olá toodisable/habilitar CDN, o ponto de extremidade de streaming deve estar no hello **interrompido** estado. Pode levar horas too2 para tooget de integração do Azure CDN Olá habilitado e Olá alterações toobe ativa em Olá todos os POPs de CDN. No entanto, você pode iniciar o ponto de extremidade de streaming e fluxo sem interrupções do ponto de extremidade de streaming de saudação e após a conclusão da integração hello, fluxo Olá será entregue de saudação CDN. Durante a saudação provisionamento período seu ponto de extremidade de streaming estará em **iniciando** estado e você pode observar degredad desempenho.

Integração CDN está habilitada em todos os execpt centros de dados do Azure Olá China e Goverment Federal regiões.

Depois de ter habilitado, Olá **controle de acesso**, **nome de host personalizado** e **autenticação da assinatura Akamai** configuração é desabilitada.
 
> [!IMPORTANT]
> A integração dos Serviços de Mídia do Azure à CDN do Azure é implementada da **Verizon na CDN do Azure** para pontos de extremidade de streaming padrão. Os pontos de extremidade de streaming Premium podem ser configurados usando todos os **tipos de preço e provedores da CDN do Azure**. Para obter mais informações sobre os recursos de CDN do Azure, consulte Olá [visão geral da CDN](../cdn/cdn-overview.md).
 
### <a name="additional-considerations"></a>Considerações adicionais

* Quando a CDN é habilitada para um ponto de extremidade de streaming, os clientes não é possível solicitar conteúdo diretamente de origem de saudação. Se você precisar Olá capacidade tootest seu conteúdo com ou sem CDN, você pode criar outro ponto de extremidade de streaming que não seja CDN habilitada.
* Seu permanece de nome de host do ponto de extremidade streaming Olá mesmo depois de habilitar a CDN. Você não precisa toomake qualquer fluxo de trabalho de serviços de mídia do tooyour de alterações depois que a CDN está habilitada. Por exemplo, se o nome de host do ponto de extremidade streaming é strasbourg.streaming.mediaservices.windows.net, depois de habilitar a CDN, Olá exata mesmo nome de host é usado.
* Para novos pontos de extremidade de streaming, você pode habilitar CDN criando um novo ponto de extremidade; para pontos de extremidade de streaming existentes, é necessário ponto de extremidade do toofirst parar hello e, em seguida, habilitar/desabilitar Olá CDN.
* O ponto de extremidade de streaming padrão pode ser configurado apenas usando o **provedor de CDN padrão da Verizon** no portal de gerenciamento do Azure. No entanto, você pode habilitar outros provedores de CDN do Azure usando APIs REST.

## <a name="configure-cdn-profile"></a>Configurar perfil de CDN

Você pode configurar o perfil CDN Olá selecionando Olá **gerenciar CDN** botão na parte superior da saudação.

![ponto de extremidade de streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints6.png)

## <a name="next-steps"></a>Próximas etapas
Examine os roteiros de aprendizagem dos Serviços de Mídia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

