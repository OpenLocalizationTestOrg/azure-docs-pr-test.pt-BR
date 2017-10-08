---
title: "aaaConfigure Olá FMLE codificador toosend uma transmissão ao vivo de taxa de bits única | Microsoft Docs"
description: "Este tópico mostra como tooconfigure Olá Flash Media ao vivo codificador (FMLE) codificador toosend um canais de tooAMS de fluxo de taxa de bits única que são habilitados para codificação ao vivo."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3113f333-517a-47a1-a1b3-57e200c6b2a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: 780d911c5186ec09c784264f9a0d0c3f8059d305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-fmle-encoder-toosend-a-single-bitrate-live-stream"></a>Use Olá FMLE codificador toosend uma transmissão ao vivo de taxa de bits única
> [!div class="op_single_selector"]
> * [FMLE](media-services-configure-fmle-live-encoder.md)
> * [Elemental Live](media-services-configure-elemental-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
>
>

Este tópico mostra como Olá tooconfigure [Flash Live o codificador de mídia](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) codificador toosend tooAMS canais que são habilitados para codificação ao vivo de fluxo de uma taxa de bits única. Para obter mais informações, consulte [trabalhando com canais que é habilitado tooPerform Live codificação com o Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).

Este tutorial mostra como toomanage Azure Media Services (AMS) com a ferramenta Gerenciador de serviços na mídia do Azure (AMSE). Essa ferramenta é executada apenas em PCs com Windows. Se você estiver usando o Mac ou Linux, use Olá toocreate portal do Azure [canais](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) e [programas](media-services-portal-creating-live-encoder-enabled-channel.md).

Observe que este tutorial descreve como usar o AAC. No entanto, por padrão, o FMLE dá suporte ao AAC. Você precisaria toopurchase um plug-in para codificação AAC por exemplo, MainConcept: [AAC plug-in](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)

## <a name="prerequisites"></a>Pré-requisitos
* [Criar uma conta dos Serviços de Mídia do Azure](media-services-portal-create-account.md)
* Verifique se há um Ponto de Extremidade de Streaming em execução. Para obter mais informações, veja [Gerenciar Pontos de Extremidade de Transmissão em uma conta de Serviços de Mídia](media-services-portal-manage-streaming-endpoints.md)
* Instale a versão mais recente Olá de saudação [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) ferramenta.
* Inicie a ferramenta hello e conecte-se a conta tooyour AMS.

## <a name="tips"></a>Dicas
* Sempre que possível, use uma conexão de Internet com fio.
* Uma boa regra prática ao determinar os requisitos de largura de banda é toodouble Olá streaming taxas de bits. Embora não seja um requisito obrigatório, ela ajuda a reduzir o impacto de saudação do congestionamento da rede.
* Ao usar codificadores baseados em software, feche todos os programas desnecessários.

## <a name="create-a-channel"></a>Criar um canal
1. Na ferramenta AMSE hello, navegar toohello **Live** guia e clique com o botão direito na área de canal hello. Selecione **Criar canal...** no menu de saudação.

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. Especifique um nome de canal, Olá campo de descrição é opcional. Em configurações de canal, selecione **padrão** para Olá opção codificação ao vivo, com hello entrada do protocolo definido muito**RTMP**. Você pode deixar todas as outras configurações como estão.

    Verifique se Olá **início Olá novo canal agora** está selecionado.

3. Clique em **Criar Canal**.

   ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> canal Olá pode levar até 20 minutos toostart.
>
>

Enquanto o canal Olá é iniciado, você pode [configurar codificador Olá](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).

> [!IMPORTANT]
> Lembre-se de que a cobrança começa assim que o Canal entra em um estado pronto. Para obter mais informações, veja [Estados do canal](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

## <a id=configure_fmle_rtmp></a>Configurar Olá FMLE codificador
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

### <a name="configuration-steps"></a>Etapas da configuração
1. Navegue toohello que interface Flash Live codificador de mídia (FMLE) na máquina hello está sendo usada.

    interface Olá é uma página principal de configurações. Por favor, tome nota das recomendadas a seguir Olá configurações tooget iniciado com o streaming usando FMLE.

   * Formato: Taxa de quadros H. 264: 30,00
   * Tamanho de entrada: 1280x720
   * Taxa de bits: 5000 kbits/s (pode ser ajustada com base nas limitações de rede)  

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle3.png)

     Quando usar entrelaçada fontes, por favor, marca de seleção hello "Desentrelaçar" opção
2. Selecione Olá chave inglesa ícone próximo tooFormat, essas configurações adicionais que devem ser:

   * Perfil: Principal
   * Nível: 4.0
   * Frequência de quadro-chave: 2 segundos

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. Saudação de conjunto de configuração de áudio importante a seguir:

   * Formato: AAC
   * Taxa de exemplo: 44100 kHz
   * Taxa de bits: 192 kbps

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. Obter URL de entrada do canal de saudação em ordem tooassign-toohello FMLE **ponto de extremidade de RTMP**.

    Navegue ferramenta AMSE toohello back e verificar o status de conclusão de canal hello. Depois que o estado Olá mudou de **iniciando** muito**executando**, você pode obter a URL de entrada hello.

    Quando estiver executando o canal Olá, clique direito no nome do canal hello, navegue para baixo toohover **copiar a URL de entrada tooclipboard** e, em seguida, selecione **URL de entrada primária**.  

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. Colar essas informações no hello **FMS URL** campo da seção de saída de hello e atribua um nome de fluxo.

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle7.png)

    Para redundância adicional, repita essas etapas com hello secundário URL de entrada.
6. Selecione **Conectar**.

> [!IMPORTANT]
> Antes de clicar em **conectar**, você **deve** Certifique-se de que o canal de saudação está pronto.
> Além disso, certifique-se de não tooleave Olá canal em um estado pronto sem uma entrada contribuição feed por mais de > 15 minutos.
>
>

## <a name="test-playback"></a>Reprodução de teste

Navegue ferramenta AMSE toohello e clique com botão direito Olá canal toobe testado. No menu de hello, passe o mouse sobre **Olá reprodução visualização** e selecione **com o Azure Media Player**.  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle8.png)

Se o fluxo de saudação aparece no player hello, codificador Olá foi tooAMS tooconnect configurado corretamente.

Se um erro é recebido, canal Olá precisará toobe redefinição e codificador configurações ajustadas. Consulte Olá [de solução de problemas](media-services-troubleshooting-live-streaming.md) tópico para obter orientação.  

## <a name="create-a-program"></a>Criar um programa
1. Depois que a reprodução do canal for confirmada, crie um programa. Em Olá **Live** guia na ferramenta AMSE hello, clique com o botão direito na área de programa hello e selecione **criar um novo programa**.  

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle9.png)
2. Nomeie o programa hello e, se necessário, ajuste Olá **duração da janela de arquivo** (os horários de too4 padrões). Você também pode especificar um local de armazenamento ou deixe como saudação padrão.  
3. Verificar Olá **início Olá programa agora** caixa.
4. Clique em **Criar Programa**.  

    >[!NOTE]
    >A criação do programa leva menos tempo do que a criação do canal.
        
5. Depois que o programa de hello está sendo executado, confirme a reprodução clique direito programa hello e navegando muito**reprodução Olá programas** e, em seguida, selecionando **com o Azure Media Player**.  
6. Depois de confirmar, clique com botão direito programa hello novamente e selecionar **copiar Olá URL de saída tooClipboard** (ou recuperar essas informações do hello **informações e configurações de programa** opção no menu de saudação).

Olá está agora pronto toobe inserido em um player ou público tooan distribuída ao vivo de exibição.  

## <a name="troubleshooting"></a>Solucionar problemas
Consulte Olá [de solução de problemas](media-services-troubleshooting-live-streaming.md) tópico para obter orientação.

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
