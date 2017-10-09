---
title: "arquivos de aaaUpload em uma conta de serviços de mídia do Azure usando Aspera | Microsoft Docs"
description: "Este tutorial orienta você pelas etapas de saudação de carregamento de arquivos em uma conta de armazenamento que está associada a uma conta de serviços de mídia usando hello * * Aspera Server na demanda * * o serviço no Azure."
services: media-services
documentationcenter: 
author: johndeu
manager: cfowler
editor: 
ms.assetid: 8812623a-b425-4a0f-9e05-0ee6c839b6f9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/17/2017
ms.author: juliako
ms.openlocfilehash: 7213f016cc1b7f262b14db7b39b478a03970d1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-aspera-server-on-demand-service-on-azure"></a>Carregar arquivos em uma conta de serviços de mídia usando Olá serviço servidor sob demanda Aspera no Azure

## <a name="overview"></a>Visão geral

**Aspera** é um software de transferência de arquivos de alta velocidade. O **Servidor Aspera sob demanda** para o Azure permite um carregamento de alta velocidade e download de arquivos grandes diretamente no armazenamento do objeto de Blob do Azure. Para obter informações sobre **Aspera On Demand**, consulte Olá [Aspera nuvem](http://cloud.asperasoft.com/) site. 
  
**Servidor sob demanda Aspera** para Azure está disponível para compra Olá [do Azure marketplace](https://azure.microsoft.com/en-us/marketplace/). Em ordem toocomplete uma compra de **servidor sob demanda Aspera** do Azure, faça logon no Azure Marketplace com seu Windows Live ID.

Este tutorial orienta você pelas etapas de saudação de carregamento de arquivos em uma conta de armazenamento que está associada a uma conta de serviços de mídia usando Olá **servidor sob demanda Aspera** serviço no Azure. 

Você pode encontrar um exemplo que mostra como toouse Azure funciona com os serviços de mídia e Aspera [aqui](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).

>[!NOTE]
>Há um limite toohello tamanho máximo com suporte para processadores de mídia (MPs) de processamento com os serviços de mídia do Azure. Consulte [isso](media-services-quotas-and-limitations.md) tópico para obter detalhes sobre a limitação de tamanho de arquivo hello.
>

## <a name="prerequisites"></a>Pré-requisitos 

toocomplete neste tutorial, você precisa:

* Uma ID do Windows Live
* Uma [conta do Azure](https://azure.microsoft.com). Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/). 
* Uma [conta de Serviços de Mídia do Azure](media-services-portal-create-account.md).

## <a name="purchase-aspera-on-demand-for-azure"></a>Comprar Aspera sob demanda para Azure

Depois de fazer logon no Azure Marketplace, siga essas toocomplete etapas básicas a compra do Aspera On Demand for Azure.

1. Pesquise por Aspera e selecione 'Servidor sob demanda'.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera001.png)

2. Examine os planos de assinatura hello e clique em 'Inscrever-se'

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera002.png)

3. Preencha as especificidades de saudação para seu servidor na assinatura de demanda.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera003.png)

4. Clique em Olá **preço** e selecione o volume mensal desejado no painel de sub hello. Em Olá **planejar detalhes** painel, selecione **Okey**. Em seguida, no hello **escolha sua camada de preços** do painel, clique em **selecione**.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera004.png)

5. Clique em **termos legais** tooview e aceitar os termos legais de saudação no painel de sub Olá. Depois de revisar os termos legais hello, clique em **compra**.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera005.png)

6. Concluir a compra de saudação clicando **criar**.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera006.png)

7. saudação do painel do Azure anunciará que ele é o provisionamento de serviço hello.  Depois de concluído com o provisionamento, você pode encontrar a nova assinatura de saudação pesquisando em seus recursos de nome de saudação do serviço de saudação. Após localizar serviço hello, clique duas vezes nele toolaunch portal de gerenciamento de serviços de saudação.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera007.png)

8. Inicie o portal de gerenciamento Aspera hello. Após localizar o novo serviço Aspera, você pode obter o portal de gerenciamento do acesso toohello, clicando-se no serviço de saudação.  Um novo painel será iniciado. De dentro desse painel novo, você precisa tooclick em Olá **nome do recurso** do seu novo serviço.  No hello captura de tela a seguir, o nome do recurso de saudação é 'AsperaTransferDemo'. Quando você clicar no nome do recurso hello, outro painel é iniciado. Nesse painel recém-lançado, você verá um link 'Gerenciar'. Clique em Olá portal de gerenciamento 'Gerenciar' link toolaunch Olá Aspera.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera008.png)

9. Clicando em Olá gerenciar link, você obterá a página de registro de toohello, que é necessária tooaccess Olá serviço.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera009.png)

10. Neste ponto, você deve ter acesso toohello Aspera service portal de gerenciamento, onde você pode criar chaves de acesso, baixar licenças e clientes Aspera, exiba o uso e saiba mais sobre Olá APIs.

    Olá seguinte captura de tela mostra a criação de acesso hello. 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera010.png)

    Olá seguinte captura de tela mostra o uso de saudação interfaces no portal de saudação de emissão de relatórios. 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera011.png)

## <a name="upload-files-with-aspera"></a>Carregar arquivos com o Aspera

1. Baixe e instale o software de cliente Aspera hello:
    
    * [Plug-in de navegador](http://downloads.asperasoft.com/connect2/)
    * [Cliente avançado](http://downloads.asperasoft.com/en/downloads/2)

2. Faça sua primeira transferência. Em ordem toouse Olá Aspera cliente tootransfer com hello Aspera serviço de transferência, você precisa fazer toocomplete Olá seguinte: 

    1. Crie uma chave de acesso, usando o portal de Aspera hello.  
    2. Download, a instalação e o cliente de Aspera de saudação de licença (o software pode ser encontrado no portal de Aspera de saudação).  

    >[!NOTE]
    >Leia Olá Aspera cliente guia para obter informações de configuração.
    
    3. Recuperar algumas informações de sua conta de armazenamento que está associada com sua conta de mídia do Azure usando Olá [portal do Azure](https://portal.azure.com/). Especificamente, o nome e chave e nome do contêiner de blob de armazenamento de saudação em toowhich deseja tooplace seu conteúdo. 

        * informações de armazenamento Olá tooget do portal de saudação: localizar sua conta de armazenamento, clique nas teclas de acesso do hello e cópia Olá nome e Olá a chave da sua conta.
        * nome do contêiner Olá tooget: localizar sua conta de armazenamento, selecione **Blobs**, selecione nome de saudação do contêiner de saudação deseja tooupload Olá conteúdo em. 

    Abaixo está a captura de tela de saudação do cliente do hello Aspera **Gerenciador de Conexão** onde você deve especificar o tipo de armazenamento 'Do Azure' hello e credenciais, bem como o contêiner de blob hello.

    ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera012.png)

## <a name="resources"></a>Recursos

Olá recursos a seguir foram mencionada neste artigo. 

* [Plug-in Connect Browser](http://downloads.asperasoft.com/connect2/)
* [Guia do Connect](http://downloads.asperasoft.com/en/documentation/8)
* [Aspera Client](http://downloads.asperasoft.com/en/downloads/2)
* [Guia do Client](http://downloads.asperasoft.com/en/documentation/2)

## <a name="next-steps"></a>Próximas etapas

Agora você pode [copiar blobs de uma conta de armazenamento para uma conta do AMS ](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

