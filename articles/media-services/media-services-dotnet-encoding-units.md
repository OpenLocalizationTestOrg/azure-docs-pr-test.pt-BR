---
title: "mídia aaaScale processamento adicionando unidades de codificação - Azure |  Microsoft Docs"
description: "Saiba como unidades de codificação tooadd toohow com .NET"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 33f7625a-966a-4f06-bc09-bccd6e2a42b5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;milangada;
ms.openlocfilehash: b9f71a6487c5d136319a38a1598d60edfaa81b9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-encoding-with-net-sdk"></a>Como tooscale codificação com o SDK .NET
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-scale-media-processing.md)
> * [.NET](media-services-dotnet-encoding-units.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>Visão geral
> [!IMPORTANT]
> Verifique se Olá de tooreview [visão geral](media-services-scale-media-processing-overview.md) tooget tópico para obter mais informações sobre como dimensionar um tópico de processamento de mídia.
> 
> 

toochange Olá reservado hello e tipo de número de unidade usando o SDK do .NET, de unidades reservadas de codificação Olá a seguir:

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds tooS1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a>Abrindo um tíquete de suporte
Por padrão, todas as contas de serviços de mídia podem dimensionar tooup too25 codificação e 5 sob demanda unidades reservadas de Streaming. Você pode solicitar um limite mais alto abrindo um tíquete de suporte.

### <a name="open-a-support-ticket"></a>Abra um tíquete de suporte
tooopen um tíquete de suporte Olá a seguir:

1. Clique em [Obter suporte](https://manage.windowsazure.com/?getsupport=true). Se você não estiver conectado, você vai ser tooenter solicitada suas credenciais.
2. Selecione sua assinatura.
3. Em tipo de suporte, selecione "Técnico".
4. Clique em "Criar Tíquete".
5. Selecione "Azure Media Services" na lista de produtos Olá apresentada na próxima página de saudação.
6. Selecione um "tipo de problema" que é apropriado para o seu problema.
7. Clique em Continuar.
8. Siga as instruções na próxima página e, em seguida, insira os detalhes sobre o problema.
9. Clique em enviar um tíquete de saudação tooopen.

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

