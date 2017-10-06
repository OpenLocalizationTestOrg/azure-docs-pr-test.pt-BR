---
title: "aaaGet iniciado com fornecendo VoD usando Olá portal do Azure | Microsoft Docs"
description: "Este tutorial orienta você pelas etapas de saudação da implementação de um serviço básico de fornecimento de conteúdo de vídeo sob demanda (VoD) com o aplicativo de serviços de mídia do Azure (AMS) usando Olá portal do Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 6c98fcfa-39e6-43a5-83a5-d4954788f8a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 5c1c1b1f74ec1f1301120fe8e5a5ae183fe0338f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-hello-azure-portal"></a>Introdução ao fornecimento de conteúdo sob demanda usando Olá portal do Azure
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

Este tutorial orienta você pelas etapas de saudação da implementação de um serviço básico de fornecimento de conteúdo de vídeo sob demanda (VoD) com o aplicativo de serviços de mídia do Azure (AMS) usando Olá portal do Azure.

## <a name="prerequisites"></a>Pré-requisitos
Olá seguem tutorial de saudação toocomplete necessária:

* Uma conta do Azure. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/). 
* Uma conta dos Serviços de Mídia. toocreate uma conta de serviços de mídia, consulte [como tooCreate uma conta do Media Services](media-services-portal-create-account.md).

Este tutorial inclui Olá tarefas a seguir:

1. Iniciar ponto de extremidade de streaming.
2. Carregar um arquivo de vídeo.
3. Codifica o arquivo de origem de saudação em um conjunto de arquivos MP4 com taxa de bits adaptável.
4. Publica ativo hello e get streaming e URLs de download progressivo.  
5. Reproduzir o conteúdo.

## <a name="start-streaming-endpoints"></a>Iniciar pontos de extremidade de streaming 

Ao trabalhar com o Azure Media Services, um dos cenários mais comuns de saudação está entregando vídeo por meio de streaming de taxa de bits adaptável. Serviços de mídia fornecem empacotamento dinâmico, que permite que você toodeliver sua taxa de bits adaptável MP4 codificados conteúdo de streaming formatos suportados pelo Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, sem a necessidade de toostore pacote predefinido versões de cada um desses formatos de fluxo contínuo.

>[!NOTE]
>Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado. toostart streaming seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, Olá ponto de extremidade de streaming do qual você deseja toostream conteúdo tem toobe em Olá **executando** estado. 

toostart Olá ponto de extremidade de streaming, Olá a seguir:

1. Faça logon em Olá [portal do Azure](https://portal.azure.com/).
2. Na janela de configurações de saudação, clique em pontos de extremidade de Streaming. 
3. Clique em padrão Olá ponto de extremidade de streaming. 

    saudação padrão detalhes do ponto de EXTREMIDADE de STREAMING de janela é exibida.

4. Clique o ícone de início de saudação.
5. Clique em Olá toosave de botão de salvar suas alterações.

## <a name="upload-files"></a>Carregar arquivos
toostream vídeos usando serviços de mídia do Azure, você precisa de vídeos de origem do tooupload hello, codificá-los em várias taxas de bits e publicar resultados de saudação. primeira etapa de saudação é abordada nesta seção. 

1. Em Olá **configuração** janela, clique em **ativos**.
   
    ![Carregar arquivos](./media/media-services-portal-vod-get-started/media-services-upload.png)
2. Clique em Olá **carregar** botão.
   
    Olá **carregar um ativo de vídeo** janela é exibida.
   
   > [!NOTE]
   > Não há nenhuma limitação de tamanho do arquivo.
   > 
   > 
3. Procurar vídeo toohello desejado no seu computador, selecioná-la e Okey de ocorrências.  
   
    Olá upload é iniciado e você pode ver o progresso de saudação em nome do arquivo hello.  

Após a conclusão do carregamento de saudação, você ver novo ativo de saudação listado no hello **ativos** janela. 

## <a name="encode-assets"></a>Codificar ativos

Ao trabalhar com um dos cenários mais comuns de saudação está entregando uma taxa de bits adaptável streaming tooyour clientes de serviços de mídia do Azure. Serviços de mídia oferece suporte a saudação seguintes tecnologias de streaming de taxa de bits adaptável: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH. tooprepare vídeos para streaming de taxa de bits adaptável, você precisa tooencode sua fonte de vídeo em arquivos de várias taxas de bits. Você deve usar o hello **codificador de mídia padrão** tooencode codificador seus vídeos.  

Serviços de mídia também fornecem empacotamento dinâmico, que permite que você toodeliver seus MP4s de múltiplas taxas de bits nos seguintes formatos de streaming de saudação: MPEG DASH, HLS, Smooth Streaming, sem a necessidade de toorepackage nesses formatos de fluxo contínuo. Com o empacotamento dinâmico, você só precisa toostore e pagamento para arquivos de saudação em único formato de armazenamento e os serviços de mídia cria e serve a resposta apropriada hello, com base nas solicitações de um cliente.

tootake proveito do empacotamento dinâmico, você precisa de tooencode seu arquivo de origem em um conjunto de arquivos MP4 com múltiplas taxas de bits (etapas de codificação Olá são demonstradas posteriormente nesta seção).

### <a name="toouse-hello-portal-tooencode"></a>toouse Olá portal tooencode
Esta seção descreve Olá etapas tooencode seu conteúdo com o codificador de mídia padrão.

1. Em Olá **configurações** janela, selecione **ativos**.  
2. Em Olá **ativos** janela, ativo Olá selecione que você gostaria que tooencode.
3. Olá pressione **Encode** botão.
4. Em Olá **codificar um ativo** janela, processador "Padrão de codificador de mídia" hello select e uma predefinição. Para saber mais sobre as predefinições, confira [Gerar automaticamente uma escada de taxa de bits](media-services-autogen-bitrate-ladder-with-mes.md) e [Predefinições de tarefa para MES](media-services-mes-presets-overview.md). Se você planejar toocontrol quais predefinição de codificação é usada, lembre-se disso: é importante tooselect Olá predefinição mais apropriado para o vídeo de entrada. Por exemplo, se você souber o vídeo de entrada com uma resolução de 1920 x 1080 pixels, você pode usar hello "H264 taxas de bits múltiplas 1080p" predefinido. Se você tiver um vídeo de baixa resolução (640 x 360), não deverá usar a predefinição "H264 Múltiplas Taxas de Bits 1080p".
   
   Para facilitar o gerenciamento, você tem uma opção da edição nome Olá Olá ativo de saída e o nome de saudação do trabalho de saudação.
   
   ![Codificar ativos](./media/media-services-portal-vod-get-started/media-services-encode1.png)
5. Pressione **Criar**.

### <a name="monitor-encoding-job-progress"></a>Monitorar o andamento do trabalho de codificação
progresso de saudação toomonitor de saudação codificação de trabalho, clique em **configurações** (na parte superior de saudação da página de saudação) e, em seguida, selecione **trabalhos**.

![Trabalhos](./media/media-services-portal-vod-get-started/media-services-jobs.png)

## <a name="publish-content"></a>Publicar conteúdo
tooprovide o usuário com uma URL que pode ser usado toostream ou baixar o conteúdo, você primeiro precisa muito "Publicar" seu ativo, criando um localizador. Os localizadores fornecem acesso toofiles contidos em Olá ativo. Os Serviços de Mídia oferecem suporte a dois tipos de localizadores: 

* Transmitindo os localizadores (OnDemandOrigin), usados para streaming adaptável (por exemplo, toostream MPEG DASH, HLS ou Smooth Streaming). toocreate um localizador de transmissão seu ativo deve conter um arquivo. ISM. 
* Localizadores progressivos (SAS), usados para a entrega de vídeo por meio do download progressivo.

Uma URL de streaming tem Olá formato a seguir e você pode usá-lo tooplay ativos do Smooth Streaming.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

Acrescentar toobuild uma URL de streaming de HLS (format = m3u8-aapl) toohello URL.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

Acrescentar toobuild um MPEG DASH URL de streaming (formato = mpd-tempo-csf) toohello URL.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


Uma URL SAS tem Olá formato a seguir.

    {blob container name}/{asset name}/{file name}/{SAS signature}

> [!NOTE]
> Se você usou os localizadores de portal toocreate Olá antes de março de 2015, os localizadores com uma data de validade de dois anos foram criados.  
> 
> 

tooupdate uma data de expiração em um localizador, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) ou [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs. Quando você atualizar a data de expiração de saudação de um localizador SAS, Olá URL é alterado.

### <a name="toouse-hello-portal-toopublish-an-asset"></a>toouse de saudação portal toopublish um ativo
toouse de saudação portal toopublish um ativo, Olá a seguir:

1. Selecione **Configurações** > **Ativos**.
2. Selecione Olá ativo que você deseja toopublish.
3. Clique em Olá **publicar** botão.
4. Selecione o tipo de localizador de saudação.
5. Pressione **Adicionar**.
   
    ![Publicar](./media/media-services-portal-vod-get-started/media-services-publish1.png)

Olá URL é adicionado a lista toohello de **publicado URLs**.

## <a name="play-content-from-hello-portal"></a>Reproduzir conteúdo do portal de saudação
Olá, portal do Azure fornece um player de conteúdo que você pode usar tootest o vídeo.

Clique em vídeo Olá desejado e clique em Olá **reproduzir** botão.

![Publicar](./media/media-services-portal-vod-get-started/media-services-play.png)

Algumas considerações se aplicam:

* toobegin streaming, iniciar execução Olá **padrão** ponto de extremidade de streaming.
* Certifique-se de saudação vídeo foi publicada.
* Isso **Media player** reproduz do ponto de extremidade de streaming de padrão de saudação. Se você quiser tooplay de não-padrão streaming de ponto de extremidade, clique toocopy Olá URL e use outro player. Por exemplo, o [Player dos Serviços de Mídia do Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

## <a name="next-steps"></a>Próximas etapas
Examine os roteiros de aprendizagem dos Serviços de Mídia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

