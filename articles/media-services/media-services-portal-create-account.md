---
title: "aaaCreate uma conta de serviços de mídia do Azure com hello portal do Azure | Microsoft Docs"
description: "Este tutorial orienta você pelas etapas de saudação da criação de uma conta de serviços de mídia do Azure com hello portal do Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: c551e158-aad6-47b4-931e-b46260b3ee4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: juliako
ms.openlocfilehash: fdad93d5d470fc08380670ec0f6c2d33468b1492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-media-services-account-using-hello-azure-portal"></a>Criar uma conta de serviços de mídia do Azure usando Olá portal do Azure
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-create-account.md)
> * [PowerShell](media-services-manage-with-powershell.md)
> * [REST](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> toocomplete neste tutorial, você precisa de uma conta do Azure. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

Olá portal do Azure fornece uma maneira tooquickly criar uma conta de serviços de mídia do Azure (AMS). Você pode usar tooaccess sua conta dos serviços de mídia que permitem a você toostore, criptografar, codificar, gerenciar e transmitir o conteúdo de mídia no Azure. Em tempo de saudação você criar uma conta de serviços de mídia, você também criar uma conta de armazenamento associado (ou use uma existente) em Olá mesma região geográfica Olá conta do Media Services.

Este artigo explica alguns conceitos comuns e mostra como a conta toocreate os serviços de mídia com hello portal do Azure.

## <a name="concepts"></a>Conceitos
O acesso aos Serviços de Mídia requer duas contas associadas:

* Uma conta dos Serviços de Mídia. O dá conta acessar tooa conjunto de serviços de mídia baseados em nuvem que estão disponíveis no Azure. Uma conta de Serviços de Mídia não armazena o conteúdo de mídia real. Em vez disso, ele armazena metadados sobre conteúdo de mídia hello e trabalhos de processamento de mídia na sua conta. Em tempo de saudação que criar conta hello, você deve selecionar uma região de serviços de mídia disponível. região Olá selecionada é um data center que armazena registros de metadados Olá para sua conta.
  
* Uma conta de armazenamento do Azure. Contas de armazenamento devem estar localizadas no hello mesma região geográfica Olá conta do Media Services. Quando você criar uma conta de serviços de mídia, você pode escolher uma conta de armazenamento existente no hello mesma região, ou você pode criar uma nova conta de armazenamento Olá mesma região. Se você excluir uma conta de serviços de mídia, blobs de saudação em sua conta de armazenamento relacionados não são excluídos.

> [!NOTE]
> Para saber mais sobre a disponibilidade de recursos dos Serviços de Mídia do Azure em regiões diferentes, veja [disponibilidade de recursos do AMS em data centers](scenarios-and-availability.md#availability).

## <a name="create-an-ams-account"></a>Criar uma conta do AMS
etapas de saudação nesta seção mostram como toocreate um AMS conta.

1. Faça logon em Olá [portal do Azure](https://portal.azure.com/).
2. Clique em **+ Novo** > **Web + Móvel** > **Serviços de Mídia**.
   
    ![Criar Serviços de Mídia](./media/media-services-create-account/media-services-new1.png)
3. Em **CRIAR CONTA DOS SERVIÇOS DE MÍDIA** , insira os valores necessários.
   
    ![Criar Serviços de Mídia](./media/media-services-create-account/media-services-new3.png)
   
   1. Em **nome da conta**, digite nome Olá de nova conta de AMS hello. Um nome de conta de serviços de mídia é todas as letras minúsculas ou números sem espaços e 3 caracteres too24.
   2. Na assinatura, selecione entre Olá diferentes assinaturas do Azure que você tem acesso ao.
   3. Em **grupo de recursos**, selecione Olá recursos novos ou existentes.  Um grupo de recursos é uma coleção de recursos que compartilham o ciclo de vida, as permissões e as políticas. Saiba mais [aqui](../azure-resource-manager/resource-group-overview.md#resource-groups).
   4. Em **local**, selecione Olá região geográfica que será registros de mídia e metadados de saudação de toostore usada para sua conta de serviços de mídia. Esta região serão usados tooprocess e transmitir sua mídia. Somente Olá Media Services regiões disponíveis aparecem na caixa de lista suspensa de saudação. 
   5. Em **conta de armazenamento**, selecione um armazenamento de blob de tooprovide da conta de armazenamento saudação do conteúdo de mídia na sua conta de serviços de mídia. Você pode selecionar uma conta de armazenamento existente na Olá mesma região geográfica que sua conta de serviços de mídia, ou você pode criar uma conta de armazenamento. Uma nova conta de armazenamento é criada no hello mesma região. regras de saudação para conta de armazenamento são nomes Olá mesmo para contas de serviços de mídia.
      
       Saiba mais sobre o armazenamento [aqui](../storage/common/storage-introduction.md).
   6. Selecione **toodashboard Pin** progresso de saudação toosee de implantação de conta hello.
4. Clique em **criar** na parte inferior de saudação do formulário de saudação.
   
    Depois que a conta de saudação é criada com êxito, carrega a página Visão geral. Olá conta de saudação de tabela de ponto de extremidade de streaming terão um padrão de saudação do ponto de extremidade de streaming **parado** estado. 

    >[!NOTE]
    >Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado. toostart streaming seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, Olá ponto de extremidade de streaming do qual você deseja toostream conteúdo tem toobe em Olá **executando** estado. 
   
## <a name="toomanage-your-ams-account"></a>toomanage sua conta AMS

toomanage sua conta AMS (por exemplo, conectar-se toohello API AMS programaticamente, carregar vídeos, codificar ativos, configurar a proteção de conteúdo, monitorar o andamento do trabalho) selecione **configurações** em Olá esquerda do portal de saudação. De saudação **configurações**, navegar tooone de folhas disponíveis hello (por exemplo: **acesso à API**, **ativos**, **trabalhos**, **Proteção de conteúdo**).


## <a name="next-steps"></a>Próximas etapas

Agora você pode carregar arquivos em sua conta do AMS. Para saber mais, veja [Carregar arquivos](media-services-portal-upload-files.md).

Se você planejar tooaccess API AMS programaticamente, consulte [Olá acesso API de serviços de mídia do Azure com a autenticação do AD do Azure](media-services-use-aad-auth-to-access-ams-api.md).

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

