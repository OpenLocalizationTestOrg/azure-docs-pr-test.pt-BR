---
title: "aaaHow tooperform transmissão ao vivo usando fluxos de várias taxas de bits de toocreate de serviços de mídia do Azure com hello portal do Azure | Microsoft Docs"
description: "Este tutorial aborda você pelas etapas de saudação de criação de um canal recebe uma transmissão ao vivo de taxa de bits única e codifica o fluxo de taxa de bits toomulti usando Olá portal do Azure."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 504f74c2-3103-42a0-897b-9ff52f279e23
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 963a25b8ba4683a2ce34d9fb0e19499874b4707c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams-with-hello-azure-portal"></a>Como tooperform transmissão ao vivo usando o Azure Media Services toocreate várias taxas de bits fluxos com hello portal do Azure
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-creating-live-encoder-enabled-channel.md)
> * [.NET](media-services-dotnet-creating-live-encoder-enabled-channel.md)
> * [API REST](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

Este tutorial orienta você pelas etapas de saudação de criação de um **Channel** que recebe uma transmissão ao vivo de taxa de bits única e o codifica fluxo toomulti taxas de bits.

> [!NOTE]
> Para obter mais informações conceituais tooChannels relacionados que são habilitados para codificação ao vivo, consulte [transmissão ao vivo usando fluxos de várias taxas de bits do Azure Media Services toocreate](media-services-manage-live-encoder-enabled-channels.md).
> 
> 

## <a name="common-live-streaming-scenario"></a>Cenário comum de streaming ao vivo
Olá seguem geral de etapas envolvidas na criação de aplicativos comuns de transmissão ao vivo.

> [!NOTE]
> Atualmente, Olá máximo recomendado de duração de um evento ao vivo é 8 horas. Entre em contato com amslived em Microsoft.com se você precisar toorun um canal para períodos de tempo mais longos.
> 
> 

1. Conecte um computador de tooa de câmera de vídeo. Inicie e configure um codificador ao vivo no local que pode produzir um fluxo de taxa de bits única em um dos seguintes protocolos de saudação: RTMP, Smooth Streaming ou RTP (MPEG-TS). Para obter mais informações, consulte [Suporte RTMP dos Serviços de Mídia do Azure e Codificadores ao Vivo](http://go.microsoft.com/fwlink/?LinkId=532824).
   
    Essa etapa também pode ser realizada após a criação do canal.
2. Crie e inicie um Canal. 
3. URL de ingestão recuperar Olá canal. 
   
    URL de ingestão Olá é usado pelo Olá codificador ao vivo toosend Olá fluxo toohello canal.
4. Recupere a URL de visualização do canal hello. 
   
    Use este tooverify URL que o canal está recebendo corretamente transmissão ao vivo hello.
5. Crie um evento/programa (que também criará um ativo). 
6. Publica evento hello (que cria um localizador OnDemand para o ativo associado Olá).    
7. Inicie o evento hello quando você estiver pronto toostart transmissão e o arquivamento.
8. Opcionalmente, o codificador ao vivo Olá pode ser sinalizado toostart um anúncio. anúncio de saudação é inserido no fluxo de saída de hello.
9. Interrompa eventos hello sempre que quiser toostop streaming e arquivamento evento hello.
10. Excluir o evento de saudação (e opcionalmente exclua o ativo de saudação).   

## <a name="in-this-tutorial"></a>Neste tutorial
Neste tutorial, Olá portal do Azure é usado tooaccomplish Olá tarefas a seguir: 

1. Criar um canal que é habilitado tooperform codificação ativa.
2. Get hello URL de ingestão em ordem toosupply-toolive codificador. codificador ao vivo Olá usará este fluxo de saudação do URL tooingest em Olá canal.
3. Criar um evento/programa (e um ativo).
4. Publicar Olá ativo e obter URLs de streaming.  
5. Reproduzir o conteúdo.
6. Limpar.

## <a name="prerequisites"></a>Pré-requisitos
Olá seguem tutorial de saudação toocomplete necessária.

* toocomplete neste tutorial, você precisa de uma conta do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. 
  Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* Uma conta dos Serviços de Mídia. toocreate uma conta de serviços de mídia, consulte [criar conta](media-services-portal-create-account.md).
* Uma webcam e um codificador que possa enviar um fluxo ao vivo de taxa de bits única.

## <a name="create-a-channel"></a>Criar um canal
1. Em Olá [portal do Azure](https://portal.azure.com/), selecione os serviços de mídia e, em seguida, clique no nome da sua conta de serviços de mídia.
2. Escolha **Transmissão ao Vivo**.
3. Escolha **Criação personalizada**. Essa opção permitirá a criação de um canal habilitado para codificação ativa.
   
    ![Criar um CANAL](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-create-channel.png)
4. Clique em **Configurações**.
   
   1. Escolha Olá **codificação ao vivo** tipo de canal. Esse tipo Especifica que você deseja toocreate um canal que está habilitado para codificação ao vivo. Significa Olá taxa de bits única entrada fluxo é enviado toohello canal e codificado em um fluxo de múltiplas taxas de bits usando configurações do codificador dinâmico especificado. Para obter mais informações, consulte [transmissão ao vivo usando fluxos de várias taxas de bits do Azure Media Services toocreate](media-services-manage-live-encoder-enabled-channels.md). Clique em OK.
   2. Especifique o nome do canal.
   3. Clique em Okey na parte inferior da saudação da tela hello.
5. Selecione Olá **ingestão** guia.
   
   1. Nessa página, você pode selecionar um protocolo de streaming. Para Olá **codificação ao vivo** são do tipo de canal, opções de protocolo válido:
      
      * MP4 fragmentado de taxa de bits única (Smooth Streaming)
      * RTMP de taxa de bits única
      * RTP (MPEG-TS): fluxo de transporte de MPEG-2 por RTP.
        
        Para obter uma explicação detalhada sobre cada protocolo, consulte [transmissão ao vivo usando fluxos de várias taxas de bits do Azure Media Services toocreate](media-services-manage-live-encoder-enabled-channels.md).
        
        Você não pode alterar a opção de protocolo hello durante a saudação canal ou seus eventos/programas associados são executados. Se você precisar de protocolos diferentes, crie canais separados para cada protocolo de streaming.  
   2. Você pode aplicar a restrição de IP no hello ingestão. 
      
       Você pode definir Olá IP endereços que são permitidos tooingest um canal de vídeo toothis. Os endereços IP permitidos podem ser especificados como um endereço IP individual (por exemplo, '10.0.0.1'), um intervalo de IPs usando um endereço IP e uma máscara de sub-rede CIDR (por exemplo, ‘10.0.0.1/22’), ou um intervalo de IPs usando um endereço IP e uma máscara de sub-rede decimal com pontos (por exemplo, '10.0.0.1(255.255.252.0)').
      
       Se nenhum endereço IP for especificado e não houver definição de regra, nenhum endereço IP será permitido. tooallow qualquer endereço IP, crie uma regra e defina 0.0.0.0/0.
6. Em Olá **visualização** guia, aplicar a restrição de IP na visualização de saudação.
7. Em Olá **codificação** especifique predefinição de codificação de saudação. 
   
    Olá no momento, somente o sistema é de predefinição, você pode selecionar **padrão 720p**. toospecify um personalizado predefinido, abra um tíquete de suporte da Microsoft. Em seguida, digite o nome de saudação do hello predefinição criada para você. 

> [!NOTE]
> Atualmente, Olá canal inicial pode levar até too30 minutos. Redefinição de canal pode demorar até too5 minutos.
> 
> 

Depois de criado o canal hello, você pode clicar no canal hello e selecione **configurações** onde você pode exibir suas configurações de canais. 

Para obter mais informações, consulte [transmissão ao vivo usando fluxos de várias taxas de bits do Azure Media Services toocreate](media-services-manage-live-encoder-enabled-channels.md).

## <a name="get-ingest-urls"></a>Obter URLs de ingestão
Depois que o canal de saudação é criado, você pode obter URLs que você fornecerá o codificador ao vivo toohello de ingestão. codificador de saudação usa tooinput essas URLs uma transmissão ao vivo.

![ingesturls](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-ingest-urls.png)

## <a name="create-and-manage-events"></a>Criar e gerenciar eventos
### <a name="overview"></a>Visão geral
Um canal é associado a eventos/programas que permitem a publicação de saudação toocontrol e armazenamento de segmentos em uma transmissão ao vivo. Os canais gerenciam os eventos/programas. Olá relação de canal e programa é uma mídia tootraditional muito semelhantes em que um canal tem um fluxo constante de conteúdo e um programa está no escopo toosome atingiu o tempo de evento naquele canal.

Você pode especificar o número de saudação horas deseja tooretain Olá registrada conteúdo para evento Olá por configuração Olá **janela de arquivo** comprimento. Esse valor pode ser definido no mínimo 5 minutos tooa máximo 25 horas. Duração da janela de arquivo também determina o período de tempo que os clientes podem procurar de volta no tempo da posição atual ao vivo da saudação máximo hello. Eventos podem ser executados pelo período de tempo especificado hello, mas o conteúdo que sai da duração da janela de saudação é continuamente descartado. Esse valor dessa propriedade também determina quanto tempo cliente Olá manifestos podem crescer.

Cada evento está associado um Ativo. evento de saudação do toopublish você deve criar um localizador OnDemand para Olá associados ativo. Ter esse localizador permitirá que você toobuild uma URL de streaming que pode fornecer tooyour clientes.

Um canal dá suporte para até toothree em execução simultaneamente eventos para que você pode criar diversos arquivos de saudação mesmo fluxo de entrada. Isso permite que você toopublish e arquivamento diferentes partes de um evento, conforme necessário. Por exemplo, o requisito de negócios é tooarchive 6 horas de um evento, mas toobroadcast apenas últimos 10 minutos. tooaccomplish isso, você precisa toocreate de dois em execução simultaneamente eventos. Um evento é definido tooarchive 6 horas do evento Olá mas Olá programa não será publicado. Olá outro evento é tooarchive conjunto por 10 minutos e esse programa é publicado.

Você não deve reutilizar os programas existentes para novos eventos. Em vez disso, crie e inicie um novo programa para cada evento.

Inicie um programa do evento/quando estiver pronto toostart transmissão e o arquivamento. Interrompa eventos hello sempre que quiser toostop streaming e arquivamento evento hello. 

conteúdo toodelete arquivado, parar e excluir o evento hello e exclua ativo associado hello. Um ativo não pode ser excluído se ele é usado pelo evento Olá; evento Olá deve ser excluído primeiro. 

Mesmo depois de parar e excluir o evento hello, Olá usuários seria capaz de toostream seu conteúdo arquivado como um vídeo sob demanda, para desde que você não excluir Olá ativo.

Se você deseja tooretain Olá arquivado conteúdo, mas não tem disponível para streaming, exclua Olá localizador de streaming.

### <a name="createstartstop-events"></a>Criar/iniciar/interromper eventos
Uma vez que o fluxo de saudação que fluem para o canal de saudação no qual você pode começar Olá streaming de eventos, criando um ativo, o programa e o localizador de Streaming. Isso arquivar fluxo hello e torná-lo tooviewers disponíveis por meio do ponto de extremidade de Streaming de saudação. 

>[!NOTE]
>Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado. toostart streaming seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, Olá ponto de extremidade de streaming do qual você deseja toostream conteúdo tem toobe em Olá **executando** estado. 

Há eventos de toostart duas maneiras: 

1. De saudação **Channel** página, pressione **evento Live** tooadd um novo evento.
   
    Especifique: nome do evento, nome do ativo, janela de arquivo e opção de criptografia.
   
    ![createprogram](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-create-program.png)
   
    Se você deixou **publicar este evento ao vivo agora** marcada, Olá Olá do evento URLs de publicação será criada.
   
    Você pode pressionar **iniciar**, sempre que são eventos de saudação toostream pronto.
   
    Depois de iniciar o evento hello, você pode pressionar **inspecionar** toostart reproduzir conteúdo hello.
2. Como alternativa, você pode usar um atalho e pressione **Go Live** botão Olá **Channel** página. Isso criará um Ativo, Programa e Localizador de Streaming padrão.
   
    saudação de evento é chamada **padrão** e janela de arquivo hello é definida too8 horas.

Você pode assistir o evento publicado Olá Olá **evento ao vivo** página. 

Se você clicar em **Fora do ar**, todos os eventos ativos serão interrompidos. 

## <a name="watch-hello-event"></a>Evento de saudação de inspeção
evento de saudação toowatch, clique em **inspecionar** Olá Olá do Azure do portal ou Copiar URL de streaming e usar um player de sua escolha. 

![Criado](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-play-event.png)

Evento ao vivo converte automaticamente o conteúdo de demanda tooon eventos quando estiver parado.

## <a name="clean-up"></a>Limpar
Se você tiver concluído o fluxo de eventos e deseja tooclean recursos Olá provisionados anteriormente, execute Olá procedimento a seguir.

* Pare de enviar por push o fluxo de saudação do codificador hello.
* Pare o canal de saudação. Depois que o canal de saudação for interrompido, ele não incorrerá em todos os encargos. Quando você precisar toostart-lo novamente, ele terá hello mesma URL de ingestão para que você não precise tooreconfigure seu codificador.
* Você pode parar o ponto de extremidade de Streaming, a menos que você deseja que o arquivamento de saudação tooprovide toocontinue de evento ao vivo como um fluxo de sob demanda. Se o canal de saudação está no estado interrompido, ele não incorrerá em todos os encargos.

## <a name="view-archived-content"></a>Exibir conteúdo arquivado
Mesmo depois de parar e excluir o evento hello, Olá usuários seria capaz de toostream seu conteúdo arquivado como um vídeo sob demanda, para desde que você não excluir Olá ativo. Um ativo não pode ser excluído se ele é usado por um evento; evento Olá deve ser excluído primeiro. 

Selecione de seus ativos, toomanage **configuração** e clique em **ativos**.

![Ativos](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-assets.png)

## <a name="considerations"></a>Considerações
* Atualmente, Olá máximo recomendado de duração de um evento ao vivo é 8 horas. Entre em contato com amslived em Microsoft.com se você precisar toorun um canal para períodos de tempo mais longos.
* Certifique-se de saudação transmitir seu conteúdo de ponto de extremidade do qual você deseja toostream está em hello **executando** estado.

## <a name="next-step"></a>Próxima etapa
Revise os roteiros de aprendizagem dos Serviços de Mídia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

