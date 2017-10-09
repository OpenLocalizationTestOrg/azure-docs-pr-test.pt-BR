---
title: "aaaConfigure Olá Live elementar codificador toosend uma transmissão ao vivo de taxa de bits única | Microsoft Docs"
description: "Este tópico mostra como tooconfigure Olá Live elementar codificador toosend um canais de tooAMS de fluxo de taxa de bits única que são habilitados para codificação ao vivo."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 9c6bf6a9-6273-4fdd-9477-f0e565280b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: cenkd;anilmur;juliako
ms.openlocfilehash: 9a5de6189bfb123768a9da038b8c8db69cf85e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-elemental-live-encoder-toosend-a-single-bitrate-live-stream"></a>Use Olá Live elementar codificador toosend uma transmissão ao vivo de taxa de bits única
> [!div class="op_single_selector"]
> * [Elemental Live](media-services-configure-elemental-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

Este tópico mostra como Olá tooconfigure [Live elementar](http://www.elementaltechnologies.com/products/elemental-live) codificador toosend tooAMS canais que são habilitados para codificação ao vivo de fluxo de uma taxa de bits única.  Para obter mais informações, consulte [trabalhando com canais que é habilitado tooPerform Live codificação com o Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).

Este tutorial mostra como toomanage Azure Media Services (AMS) com a ferramenta Gerenciador de serviços na mídia do Azure (AMSE). Essa ferramenta é executada apenas em PCs com Windows. Se você estiver usando o Mac ou Linux, use Olá toocreate portal do Azure [canais](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) e [programas](media-services-portal-creating-live-encoder-enabled-channel.md).

## <a name="prerequisites"></a>Pré-requisitos
* Deve ter um conhecimento prático do usando o Live elementar web interface toocreate eventos ao vivo.
* [Criar uma conta dos Serviços de Mídia do Azure](media-services-portal-create-account.md)
* Verifique se há um Ponto de Extremidade de Streaming em execução. Para obter mais informações, veja [Gerenciar Pontos de Extremidade de Transmissão em uma conta de Serviços de Mídia](media-services-portal-manage-streaming-endpoints.md).
* Instale a versão mais recente Olá de saudação [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) ferramenta.
* Inicie a ferramenta hello e conecte-se a conta tooyour AMS.

## <a name="tips"></a>Dicas
* Sempre que possível, use uma conexão de Internet com fio.
* Uma boa regra prática ao determinar os requisitos de largura de banda é toodouble Olá streaming taxas de bits. Embora não seja um requisito obrigatório, ela ajuda a reduzir o impacto de saudação do congestionamento da rede.
* Ao usar codificadores baseados em software, feche todos os programas desnecessários.

## <a name="elemental-live-with-rtp-ingest"></a>Elemental Live com ingestão de RTP
Esta seção mostra como tooconfigure Olá elementar codificador ao vivo que envia uma taxa de bits única fluxo ao vivo sobre RTP.  Para saber mais, consulte [Fluxo MPEG TS por RTP](media-services-manage-live-encoder-enabled-channels.md#channel).

### <a name="create-a-channel"></a>Criar um canal

1. Na ferramenta AMSE hello, navegar toohello **Live** guia e clique com o botão direito na área de canal hello. Selecione **Criar canal...** no menu de saudação.

    ![Elementares](./media/media-services-elemental-live-encoder/media-services-elemental1.png)

2. Especifique um nome de canal, Olá campo de descrição é opcional. Em configurações de canal, selecione **padrão** para Olá opção codificação ao vivo, com hello entrada do protocolo definido muito**RTP (MPEG-TS)**. Você pode deixar todas as outras configurações como estão.

    Verifique se Olá **início Olá novo canal agora** está selecionado.

3. Clique em **Criar Canal**.

   ![Elementares](./media/media-services-elemental-live-encoder/media-services-elemental12.png)

> [!NOTE]
> canal Olá pode levar até 20 minutos toostart.
>
>

Enquanto o canal Olá é iniciado, você pode [configurar codificador Olá](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).

> [!IMPORTANT]
> Lembre-se de que a cobrança começa assim que o Canal entra em um estado pronto. Para obter mais informações, veja [Estados do canal](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

### <a id=configure_elemental_rtp></a>Configurar Olá Live elementar codificador
Neste tutorial Olá seguintes configurações de saída são usadas. Olá restante desta seção descreve etapas de configuração em mais detalhes.

**Vídeo**:

* Codec: H.264
* Perfil: Alto (nível 4.0)
* Taxa de bits: 5.000 kbps
* Quadro-chave: 2 segundos (60 segundos)
* Taxa de quadros: 30

**Áudio**:

* Codec: AAC (LC)
* Taxa de bits: 192 kbps
* Taxa de amostragem: 44,1 kHz

#### <a name="configuration-steps"></a>Etapas da configuração
1. Navegue toohello **Live elementar** interface da web e configurar o codificador Olá para **UDP/TS** streaming.
2. Depois de criar um novo evento, role para baixo toohello saída grupos e adicionar Olá **UDP/TS** grupo de saídas.
3. Crie uma nova saída selecionando **Nova Transmissão** e clicando em **Adicionar Saída**.  

    ![Elementares](./media/media-services-elemental-live-encoder/media-services-elemental13.png)

   > [!NOTE]
   > É recomendável evento elementar Olá tem código de tempo de saudação definido muito codificador de saudação do "relógio do sistema" toohelp reconectar-se no caso de saudação de uma falha de fluxo.
   >
   >
4. Agora que hello saída foi criada, clique em **adicionar fluxo**. configurações de saída de Hello agora podem ser configuradas.
5. Role para baixo toohello "Fluxo 1" que acabou de criar, clique em Olá **vídeo** guia Olá esquerda e expanda Olá **avançado** seção de configurações.

    ![Elementares](./media/media-services-elemental-live-encoder/media-services-elemental4.png)

    Enquanto Live elementar tem uma ampla gama de personalização disponíveis, hello configurações a seguir são recomendadas para começar a trabalhar com o streaming tooAMS.

   * Resolução: 1280 x 720
   * Taxa de quadros: 30
   * Tamanho de GOP: 60 quadros
   * Modo de entrelaçamento: Progressivo
   * Taxa de bits: 5000000 bits/s (Isso pode ser ajustado baseado nas limitações de rede)

    ![Elementares](./media/media-services-elemental-live-encoder/media-services-elemental5.png)

1. Obter URL de entrada do canal de saudação.

    Navegue ferramenta AMSE toohello back e verificar o status de conclusão de canal hello. Depois que o estado Olá mudou de **iniciando** muito**executando**, você pode obter a URL de entrada hello.

    Quando estiver executando o canal Olá, clique direito no nome do canal hello, navegue para baixo toohover **copiar a URL de entrada tooclipboard** e, em seguida, selecione **URL de entrada primária**.  

    ![Elementares](./media/media-services-elemental-live-encoder/media-services-elemental6.png)
2. Colar essas informações no hello **destino principal** campo de saudação Elemental. Todas as outras configurações podem permanecer padrão hello.

    ![Elementares](./media/media-services-elemental-live-encoder/media-services-elemental14.png)

    Para redundância adicional, repita essas etapas com hello secundário URL de entrada criando uma guia de "Saída" separada para Streaming de UDP/TS.
3. Clique em **criar** (se um novo evento foi criado) ou **atualização** (se estiver editando um evento já existente) e, em seguida, continue toostart codificador de saudação.

> [!IMPORTANT]
> Antes de clicar em **iniciar** na interface de web Live elementar hello, você **deve** Certifique-se de que o canal de saudação está pronto.
> Além disso, certifique-se de não tooleave Olá canal em um estado pronto sem um evento por mais de > 15 minutos.
>
>

Após execução de fluxo de saudação de 30 segundos, navegue para reprodução de teste e a ferramenta AMSE toohello back.  

### <a name="test-playback"></a>Reprodução de teste

Navegue ferramenta AMSE toohello e clique com botão direito Olá canal toobe testado. No menu de hello, passe o mouse sobre **Olá reprodução visualização** e selecione **com o Azure Media Player**.  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental8.png)

Se o fluxo de saudação aparece no player hello, codificador Olá foi tooAMS tooconnect configurado corretamente.

Se um erro é recebido, canal Olá precisará toobe redefinição e codificador configurações ajustadas. Consulte Olá [de solução de problemas](media-services-troubleshooting-live-streaming.md) tópico para obter orientação.   

### <a name="create-a-program"></a>Criar um programa
1. Depois que a reprodução do canal for confirmada, crie um programa. Em Olá **Live** guia na ferramenta AMSE hello, clique com o botão direito na área de programa hello e selecione **criar um novo programa**.  

    ![Elementares](./media/media-services-elemental-live-encoder/media-services-elemental9.png)
2. Nomeie o programa hello e, se necessário, ajuste Olá **duração da janela de arquivo** (os horários de too4 padrões). Você também pode especificar um local de armazenamento ou deixe como saudação padrão.  
3. Verificar Olá **início Olá programa agora** caixa.
4. Clique em **Criar Programa**.  

    >[!NOTE]
    > A criação do programa leva menos tempo do que a criação do canal.   
      
5. Depois que o programa de hello está sendo executado, confirme a reprodução clique direito programa hello e navegando muito**reprodução Olá programas** e, em seguida, selecionando **com o Azure Media Player**.  
6. Depois de confirmar, clique com botão direito programa hello novamente e selecionar **copiar Olá URL de saída tooClipboard** (ou recuperar essas informações do hello **informações e configurações de programa** opção no menu de saudação).

Olá está agora pronto toobe inserido em um player ou público tooan distribuída ao vivo de exibição.  

## <a name="troubleshooting"></a>Solucionar problemas
Consulte Olá [de solução de problemas](media-services-troubleshooting-live-streaming.md) tópico para obter orientação.

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
