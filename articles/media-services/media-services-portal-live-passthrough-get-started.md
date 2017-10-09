---
title: "fluxo de aaaLive com codificadores locais usando Olá portal do Azure | Microsoft Docs"
description: "Este tutorial orienta você pelas etapas de saudação de criação de um canal que está configurado para uma entrega de passagem."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6f4acd95-cc64-4dd9-9e2d-8734707de326
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 1fb341e022f66f33903e13e07d3e84c0216cad77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-with-on-premises-encoders-using-hello-azure-portal"></a>Como tooperform a transmissão ao vivo com local codificadores usando Olá portal do Azure
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-live-passthrough-get-started.md)
> * [.NET](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

Este tutorial orienta você pelas etapas de saudação do uso de saudação toocreate portal do Azure uma **Channel** que está configurado para uma entrega de passagem. 

## <a name="prerequisites"></a>Pré-requisitos
Olá seguem tutorial de saudação toocomplete necessária:

* Uma conta do Azure. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/). 
* Uma conta dos Serviços de Mídia. toocreate uma conta de serviços de mídia, consulte [como tooCreate uma conta do Media Services](media-services-portal-create-account.md).
* Uma Webcam. Por exemplo, [Codificador Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm).

É altamente recomendável Olá tooreview artigos a seguir:

* [Suporte RTMP dos Serviços de Mídia do Azure e Codificadores Ativos.](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [Visão geral da transmissão ao vivo usando os Serviços de Mídia do Azure](media-services-manage-channels-overview.md)
* [Transmissão ao vivo com codificadores locais que criam fluxos com múltiplas taxas de bits](media-services-live-streaming-with-onprem-encoders.md)

## <a id="scenario"></a>Cenário comum de streaming ao vivo
Olá, etapas a seguir descrevem tarefas envolvidas na criação comuns aplicativos de transmissão ao vivo que usam canais que são configurados para entrega de passagem. Este tutorial mostra como toocreate e gerenciar um canal de passagem e eventos ao vivo.

>[!NOTE]
>Certifique-se de saudação streaming do qual você deseja que o conteúdo de toostream de ponto de extremidade está em Olá **executando** estado. 
    
1. Conecte um computador de tooa de câmera de vídeo. Inicie e configure um codificador ao vivo local que gere um fluxo RTMP com múltiplas taxas de bits ou MP4 Fragmentado. Para obter mais informações, consulte [Suporte RTMP dos Serviços de Mídia do Azure e Codificadores ao Vivo](http://go.microsoft.com/fwlink/?LinkId=532824).
   
    Essa etapa também pode ser realizada após a criação do canal.
2. Crie e inicie um Canal de passagem.
3. URL de ingestão recuperar Olá canal. 
   
    URL de ingestão Olá é usado pelo Olá codificador ao vivo toosend Olá fluxo toohello canal.
4. Recupere a URL de visualização do canal hello. 
   
    Use este tooverify URL que o canal está recebendo corretamente transmissão ao vivo hello.
5. Crie um evento ao vivo/programa. 
   
    Quando usar hello portal do Azure, criar um evento ao vivo também cria um ativo. 

6. Inicie programa da evento hello quando você estiver pronto toostart transmissão e o arquivamento.
7. Opcionalmente, o codificador ao vivo Olá pode ser sinalizado toostart um anúncio. anúncio de saudação é inserido no fluxo de saída de hello.
8. Pare Olá evento/programa sempre que quiser toostop streaming e arquivamento evento hello.
9. Excluir o programa da evento hello (e opcionalmente exclua o ativo de saudação).     

> [!IMPORTANT]
> Examine [transmissão ao vivo com codificadores locais que criam fluxos de várias taxas de bits](media-services-live-streaming-with-onprem-encoders.md) toolearn sobre conceitos e considerações relacionadas streaming toolive com codificadores locais e canais de passagem.
> 
> 

## <a name="tooview-notifications-and-errors"></a>erros e tooview notificações
Se você quiser tooview notificações e os erros produzidos por Olá portal do Azure, clique no ícone de notificação de saudação.

![Notificações](./media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a>Criar e iniciar canais de passagem e eventos
Um canal é associado a eventos/programas que permitem a publicação de saudação toocontrol e armazenamento de segmentos em uma transmissão ao vivo. Os canais gerenciam os eventos. 

Você pode especificar o número de saudação horas deseja tooretain Olá registrada conteúdo para programa hello por configuração Olá **janela de arquivo** comprimento. Esse valor pode ser definido no mínimo 5 minutos tooa máximo 25 horas. Duração da janela de arquivo também determina o período de tempo que os clientes podem procurar de volta no tempo da posição atual ao vivo da saudação máximo hello. Eventos podem ser executados pelo período de tempo especificado hello, mas o conteúdo que sai da duração da janela de saudação é continuamente descartado. Esse valor dessa propriedade também determina quanto tempo cliente Olá manifestos podem crescer.

Cada evento está associado um ativo. evento de saudação toopublish, você deve criar um localizador OnDemand para ativo Olá associado. Ter esse localizador permite toobuild uma URL de streaming que pode fornecer tooyour clientes.

Um canal dá suporte para até toothree em execução simultaneamente eventos para que você pode criar diversos arquivos de saudação mesmo fluxo de entrada. Isso permite que você toopublish e arquivamento diferentes partes de um evento, conforme necessário. Por exemplo, o requisito de negócios é tooarchive 6 horas de um programa, mas toobroadcast apenas últimos 10 minutos. tooaccomplish isso, você precisa toocreate dois programas em execução simultaneamente. Um programa está definido tooarchive 6 horas do evento Olá mas Olá programa não será publicado. Olá outro programa é tooarchive conjunto por 10 minutos e esse programa é publicado.

Você não deve reutilizar os eventos existentes ao vivo. Em vez disso, crie e inicie um novo evento para cada evento.

Inicie o evento hello quando você estiver pronto toostart transmissão e o arquivamento. Pare o programa de saudação sempre que quiser toostop streaming e arquivamento evento hello. 

conteúdo toodelete arquivado, parar e excluir o evento hello e exclua ativo associado hello. Um ativo não pode ser excluído se ele é usado por um evento; evento Olá deve ser excluído primeiro. 

Mesmo depois de parar e excluir o evento hello, Olá usuários seria capaz de toostream seu conteúdo arquivado como um vídeo sob demanda, para desde que você não excluir Olá ativo.

Se você deseja tooretain Olá arquivado conteúdo, mas não tem disponível para streaming, exclua Olá localizador de streaming.

### <a name="toouse-hello-portal-toocreate-a-channel"></a>toouse de saudação portal toocreate um canal
Esta seção mostra como Olá toouse **criação rápida** opção toocreate um canal de passagem.

Para obter mais detalhes sobre os canais de passagem, veja [Transmissão ao vivo com codificadores locais que criam fluxos de múltiplas taxas de bits](media-services-live-streaming-with-onprem-encoders.md).

1. Em Olá [portal do Azure](https://portal.azure.com/), selecione sua conta de serviços de mídia do Azure.
2. Em Olá **configurações** janela, clique em **transmissão ao vivo**. 
   
    ![Introdução](./media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    Olá **transmissão ao vivo** janela é exibida.
3. Clique em **criação rápida** toocreate um canal de passagem com hello RTMP de protocolo de ingestão.
   
    Olá **criar um novo canal** janela é exibida.
4. Dê um nome de canal novo hello e clique em **criar**. 
   
    Isso cria um canal de passagem com hello protocolo de ingestão RTMP.

## <a name="create-events"></a>Criar eventos
1. Selecione um toowhich de canal que você deseja tooadd um evento.
2. Pressione o botão **Evento ao Vivo** .

![Evento](./media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a>Obter URLs de ingestão
Depois que o canal de saudação é criado, você pode obter URLs que você fornecerá o codificador ao vivo toohello de ingestão. codificador de saudação usa tooinput essas URLs uma transmissão ao vivo.

![Criado](./media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-hello-event"></a>Evento de saudação de inspeção
evento de saudação toowatch, clique em **inspecionar** Olá Olá do Azure do portal ou Copiar URL de streaming e usar um player de sua escolha. 

![Criado](./media/media-services-portal-passthrough-get-started/media-services-default-event.png)

Evento ao vivo automaticamente obter conteúdo de demanda tooon convertido quando parado.

## <a name="clean-up"></a>Limpar
Para obter mais detalhes sobre os canais de passagem, veja [Transmissão ao vivo com codificadores locais que criam fluxos de múltiplas taxas de bits](media-services-live-streaming-with-onprem-encoders.md).

* Um canal pode ser interrompido somente quando todos os eventos/programas no canal Olá foram interrompidos.  Depois que o canal de saudação for interrompido, ele não incorrerá em todos os encargos. Quando você precisar toostart-lo novamente, ele terá hello mesma URL de ingestão para que você não precise tooreconfigure seu codificador.
* Um canal pode ser excluído somente quando todos os eventos ao vivo no canal Olá tem sido excluídos.

## <a name="view-archived-content"></a>Exibir conteúdo arquivado
Mesmo depois de parar e excluir o evento hello, Olá usuários seria capaz de toostream seu conteúdo arquivado como um vídeo sob demanda, para desde que você não excluir Olá ativo. Um ativo não pode ser excluído se ele é usado por um evento; evento Olá deve ser excluído primeiro. 

Selecione de seus ativos, toomanage **configuração** e clique em **ativos**.

![Ativos](./media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a>Próxima etapa
Revise os roteiros de aprendizagem dos Serviços de Mídia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

