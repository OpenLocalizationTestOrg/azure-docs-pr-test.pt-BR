---
title: "aaaConfigure Olá NewTek TriCaster codificador toosend uma transmissão ao vivo de taxa de bits única | Microsoft Docs"
description: "Este tópico mostra como Olá tooconfigure Tricaster canais ao vivo codificador toosend uma taxa de bits única fluxo tooAMS que são habilitados para codificação ao vivo."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 8973181a-3059-471a-a6bb-ccda7d3ff297
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkd;anilmur
ms.openlocfilehash: 57dcf62a6a76b04e69f147a738be78ccb3c3ecdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-newtek-tricaster-encoder-toosend-a-single-bitrate-live-stream"></a>Use Olá NewTek TriCaster codificador toosend uma transmissão ao vivo de taxa de bits única
> [!div class="op_single_selector"]
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Elemental Live](media-services-configure-elemental-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

Este tópico mostra como Olá tooconfigure [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) canais ao vivo codificador toosend uma taxa de bits única fluxo tooAMS que são habilitados para codificação ao vivo. Para obter mais informações, consulte [trabalhando com canais que é habilitado tooPerform Live codificação com o Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).

Este tutorial mostra como toomanage Azure Media Services (AMS) com a ferramenta Gerenciador de serviços na mídia do Azure (AMSE). Essa ferramenta é executada apenas em PCs com Windows. Se você estiver usando o Mac ou Linux, use Olá toocreate portal do Azure [canais](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) e [programas](media-services-portal-creating-live-encoder-enabled-channel.md).

> [!NOTE]
> Quando usar Tricaster para envio em uma contribuição feed tooAMS canais que são habilitados para codificação ao vivo, pode haver problemas de áudio/vídeo em seu evento ao vivo se você usar determinados recursos do Tricaster, como Recortar entre feeds de rápida ou alternância de slates . Olá AMS equipe está trabalhando para corrigir esses problemas, até lá, é recomendável não toouse esses recursos.
>
>

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

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster1.png)

2. Especifique um nome de canal, Olá campo de descrição é opcional. Em configurações de canal, selecione **padrão** para Olá opção codificação ao vivo, com hello entrada do protocolo definido muito**RTMP**. Você pode deixar todas as outras configurações como estão.

    Verifique se Olá **início Olá novo canal agora** está selecionado.

3. Clique em **Criar Canal**.

   ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster2.png)

> [!NOTE]
> canal Olá pode levar até 20 minutos toostart.
>
>

Enquanto o canal Olá é iniciado, você pode [configurar codificador Olá](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).

> [!IMPORTANT]
> Lembre-se de que a cobrança começa assim que o Canal entra em um estado pronto. Para obter mais informações, veja [Estados do canal](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

## <a id=configure_tricaster_rtmp></a>Configurar Olá NewTek TriCaster codificador
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
1. Crie um novo projeto do **NewTek TriCaster** dependendo de qual fonte de entrada de vídeo está sendo usada.
2. Uma vez no projeto, localize Olá **fluxo** botão e, em seguida, clique em Olá engrenagem ícone próximo tooit tooaccess Olá fluxo configuração menu.

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster3.png)
3. Depois que o menu de saudação for aberto, clique em **novo** sob o título de Conexão hello. Quando solicitado para o tipo de conexão hello, selecione **Adobe Flash**.

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster4.png)
4. Clique em **OK**.
5. Um perfil de FMLE agora pode ser importado clicando Olá seta do menu suspenso em **perfil Streaming** e navegar muito**procurar**.

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster5.png)
6. Navegue toowhere Olá configurado FMLE perfil foi salvo.
7. Selecione-o e pressione **OK**.

    Quando o perfil de saudação é carregado, continue toohello próxima etapa.
8. Obter URL de entrada do canal de saudação em ordem tooassign-toohello Tricaster **ponto de extremidade de RTMP**.

    Navegue ferramenta AMSE toohello back e verificar o status de conclusão de canal hello. Depois que o estado Olá mudou de **iniciando** muito**executando**, você pode obter a URL de entrada hello.

    Quando estiver executando o canal Olá, clique direito no nome do canal hello, navegue para baixo toohover **copiar a URL de entrada tooclipboard** e, em seguida, selecione **URL de entrada primária**.  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster6.png)
9. Colar essas informações no hello **local** campo em **Flash Server** no projeto de Tricaster hello. Também atribuir um nome de fluxo em Olá **identificação do fluxo** campo.

    Se as informações de fluxo foi adicionadas o perfil FMLE toohello, ele também pode ser importado toothis seção clicando **importar configurações**, navegando toohello salvada FMLE perfil e clicando em **Okey**. campos de Flash Server relevantes Olá devem preencher com informações de saudação do FMLE.

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster7.png)
10. Quando terminar, clique em **Okey** na parte inferior da saudação da tela hello. Quando entradas de áudio e vídeo em Olá Tricaster estiverem prontas, iniciar streaming tooAMS clicando Olá **fluxo** botão.

     ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster11.png)

> [!IMPORTANT]
> Antes de clicar em **fluxo**, você **deve** Certifique-se de que o canal de saudação está pronto.
> Além disso, certifique-se de não tooleave Olá canal em um estado pronto sem uma entrada contribuição feed por mais de > 15 minutos.
>
>

## <a name="test-playback"></a>Reprodução de teste
Navegue ferramenta AMSE toohello e clique com botão direito Olá canal toobe testado. No menu de hello, passe o mouse sobre **Olá reprodução visualização** e selecione **com o Azure Media Player**.  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster8.png)

Se o fluxo de saudação aparece no player hello, codificador Olá foi tooAMS tooconnect configurado corretamente.

Se um erro é recebido, canal Olá precisará toobe redefinição e codificador configurações ajustadas. Consulte Olá [de solução de problemas](media-services-troubleshooting-live-streaming.md) tópico para obter orientação.  

## <a name="create-a-program"></a>Criar um programa
1. Depois que a reprodução do canal for confirmada, crie um programa. Em Olá **Live** guia na ferramenta AMSE hello, clique com o botão direito na área de programa hello e selecione **criar um novo programa**.  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster9.png)
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

## <a name="next-step"></a>Próxima etapa
Revise os roteiros de aprendizagem dos Serviços de Mídia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
