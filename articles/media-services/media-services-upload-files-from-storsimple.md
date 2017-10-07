---
title: "arquivos de aaaUpload em uma conta de serviços de mídia do Azure do Azure StorSimple | Microsoft Docs"
description: "Este artigo fornece uma breve visão geral do Gerenciador de Dados do Azure StorSimple. artigo Olá também vincula tootutorials que mostram como dados de tooextract do StorSimple e carregá-lo como ativos tooan conta de serviços de mídia do Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1dd09328-262b-43ef-8099-73241b49a925
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/27/2017
ms.author: juliako
ms.openlocfilehash: 7e9712aa480106bbd5fcc63eaecf0418b24a8bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-an-azure-media-services-account-from-azure-storsimple"></a>Carregar arquivos em uma conta dos Serviços de Mídia do Azure do Azure StorSimple

Este artigo fornece uma breve visão geral do Gerenciador de Dados do Azure StorSimple. artigo Olá também vincula tootutorials que mostram como dados de tooextract do StorSimple e carregar esses dados como ativos tooan conta de serviços de mídia do Azure (AMS).

> 
> [!NOTE]
> O Gerenciador de Dados do Azure StorSimple está em visualização privada. 
> 

## <a name="overview"></a>Visão geral

Nos serviços de mídia, você pode carregar seus arquivos digitais em um ativo. Olá ativo pode conter vídeo, áudio, imagens, coleções de miniaturas, texto rastreia e legenda codificada arquivos (e Olá metadados sobre esses arquivos.) Depois que forem carregados arquivos hello, seu conteúdo é armazenado com segurança na nuvem de saudação para processamento adicional e streaming.

[O Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) usa armazenamento em nuvem como uma extensão da saudação solução local e automaticamente dados de camadas de armazenamento de local de saudação e armazenamento em nuvem. o dispositivo StorSimple Olá dedupes e compacta os dados antes de enviá-la nuvem toohello tornando muito eficiente para o envio de nuvem de toohello arquivos grandes. Olá [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) serviço fornece APIs que permitem a você tooextract dados do StorSimple e apresentá-lo como ativos AMS.

## <a name="get-started"></a>Introdução

1. [Criar uma conta de serviços de mídia](media-services-portal-create-account.md) em que deseja que os ativos de saudação tootransfer.
2. Inscreva-se para a visualização do Gerenciador de dados, conforme descrito em Olá [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) artigo.
3. Crie uma conta do Gerenciador de Dados do StorSimple.
4. Crie um trabalho de transformação de dados que, quando executado, extrai dados de um dispositivo StorSimple e os transfere para uma conta do AMS como ativos. 

    Quando o trabalho de saudação inicia a execução, uma fila de armazenamento é criada. Essa fila é populada com mensagens sobre blobs transformados à medida que elas estejam prontas. nome da saudação dessa fila é Olá igual ao nome de Olá Olá da definição do trabalho. Você pode usar essa fila toodetermine quando como ativo está pronto e chamar sua toorun de operação de serviços de mídia desejado. Por exemplo, você pode usar este tootrigger fila uma função do Azure que contém um código de serviços de mídia necessário hello.

## <a name="see-also"></a>Consulte também

[Use Olá .net SDK tootrigger trabalhos em Olá Gerenciador de dados](../storsimple/storsimple-data-manager-dotnet-jobs.md)

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Próximas etapas

Agora você pode codificar seus ativos carregados. Para saber mais, veja [Codificar ativos](media-services-portal-encode.md).
