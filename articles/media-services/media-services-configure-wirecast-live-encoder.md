---
title: "aaaConfigure Olá toosend de codificador Telestream Wirecast uma transmissão ao vivo de taxa de bits única | Microsoft Docs"
description: "Este tópico mostra como Olá tooconfigure Wirecast canais ao vivo codificador toosend uma taxa de bits única fluxo tooAMS que são habilitados para codificação ao vivo. "
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 0d2f1e81-51a6-4ca9-894a-6dfa51ce4c70
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: e373f6c08232c652e65db584ded409c405d8cffe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-wirecast-encoder-toosend-a-single-bitrate-live-stream"></a>Use Olá Wirecast codificador toosend uma transmissão ao vivo de taxa de bits única
> [!div class="op_single_selector"]
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [Elemental Live](media-services-configure-elemental-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

Este tópico mostra como Olá tooconfigure [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) canais ao vivo codificador toosend uma taxa de bits única fluxo tooAMS que são habilitados para codificação ao vivo.  Para obter mais informações, consulte [trabalhando com canais que é habilitado tooPerform Live codificação com o Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).

Este tutorial mostra como toomanage Azure Media Services (AMS) com a ferramenta Gerenciador de serviços na mídia do Azure (AMSE). Essa ferramenta é executada apenas em PCs com Windows. Se você estiver usando o Mac ou Linux, use Olá toocreate portal do Azure [canais](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) e [programas](media-services-portal-creating-live-encoder-enabled-channel.md).

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

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast1.png)

2. Especifique um nome de canal, Olá campo de descrição é opcional. Em configurações de canal, selecione **padrão** para Olá opção codificação ao vivo, com hello entrada do protocolo definido muito**RTMP**. Você pode deixar todas as outras configurações como estão.

    Verifique se Olá **início Olá novo canal agora** está selecionado.

3. Clique em **Criar Canal**.

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast2.png)

> [!NOTE]
> canal Olá pode levar até 20 minutos toostart.
>
>

Enquanto o canal Olá é iniciado, você pode [configurar codificador Olá](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).

> [!IMPORTANT]
> Lembre-se de que a cobrança começa assim que o Canal entra em um estado pronto. Para obter mais informações, veja [Estados do canal](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

## <a id=configure_wirecast_rtmp></a>Configurar Olá codificador Telestream Wirecast
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
1. Abra aplicativo Telestream Wirecast Olá Olá máquina que está sendo usado e configurado para streaming de RTMP.
2. Configurar saída de hello navegando toohello **saída** guia e selecionando **configurações de saída...** .

    Verifique se Olá **destino de saída** está definido muito**servidor RTMP**.
3. Clique em **OK**.
4. Na página de configurações do hello, defina Olá **destino** campo toobe **Azure Media Services**.

    Olá perfil de codificação é pré-selecionada muito**Azure h. 264 720 p 16:9 (1280x720)**. toocustomize essas configurações, selecione Olá toohello de ícone de engrenagem direito da saudação lista suspensa e, em seguida, escolha **nova predefinição**.

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast3.png)
5. Configure as predefinições do codificador.

    Olá nome predefinido e verificar as configurações recomendada a seguir hello:

    **Vídeo**

   * Codificador: MainConcept H.264
   * Quadros por segundo: 30
   * Taxa de bits média: 5.000 kbits/s (Pode ser ajustada com base nas limitações de rede)
   * Perfil: Principal
   * Quadro chave: a cada 60 quadros

    **Áudio**

   * Taxa de bits de destino: 192 kbits/s
   * Taxa de amostragem: 44,100 kHz

     ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast4.png)
6. Pressione **Salvar**.

    campo de codificação Olá agora tem disponíveis para seleção do perfil de saudação recém-criado.

    Certifique-se de novo perfil de saudação está selecionado.
7. Obter URL de entrada do canal de saudação em ordem tooassign-toohello Wirecast **ponto de extremidade de RTMP**.

    Navegue ferramenta AMSE toohello back e verificar o status de conclusão de canal hello. Depois que o estado Olá mudou de **iniciando** muito**executando**, você pode obter a URL de entrada hello.

    Quando estiver executando o canal Olá, clique direito no nome do canal hello, navegue para baixo toohover **copiar a URL de entrada tooclipboard** e, em seguida, selecione **URL de entrada primária**.  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast6.png)
8. Em Olá Wirecast **configurações de saída** janela, colar essas informações no hello **endereço** campo da seção de saída de hello e atribua um nome de fluxo.

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast5.png)

1. Selecione **OK**.
2. Em Olá principal **Wirecast** , confirme as fontes de entrada de áudio e vídeo estiverem prontos e, em seguida, pressionar **fluxo** no canto superior esquerdo de saudação.

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast7.png)

> [!IMPORTANT]
> Antes de clicar em **fluxo**, você **deve** Certifique-se de que o canal de saudação está pronto.
> Além disso, certifique-se de não tooleave Olá canal em um estado pronto sem uma entrada contribuição feed por mais de > 15 minutos.
>
>

## <a name="test-playback"></a>Reprodução de teste

Navegue ferramenta AMSE toohello e clique com botão direito Olá canal toobe testado. No menu de hello, passe o mouse sobre **Olá reprodução visualização** e selecione **com o Azure Media Player**.  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast8.png)

Se o fluxo de saudação aparece no player hello, codificador Olá foi tooAMS tooconnect configurado corretamente.

Se um erro é recebido, canal Olá precisará toobe redefinição e codificador configurações ajustadas. Consulte Olá [de solução de problemas](media-services-troubleshooting-live-streaming.md) tópico para obter orientação.  

## <a name="create-a-program"></a>Criar um programa
1. Depois que a reprodução do canal for confirmada, crie um programa. Em Olá **Live** guia na ferramenta AMSE hello, clique com o botão direito na área de programa hello e selecione **criar um novo programa**.  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast9.png)
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
