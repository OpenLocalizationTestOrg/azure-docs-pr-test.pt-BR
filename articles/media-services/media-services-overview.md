---
title: "Visão geral dos serviços de mídia de aaaAzure | Microsoft Docs"
description: "Este tópico oferece uma visão geral dos Serviços de Mídia do Azure"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7a5e9723-c379-446b-b4d6-d0e41bd7d31f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/04/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 81f9f4d9ff75effea30c10fd09449e9d2025f377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-overview"></a>Visão geral dos Serviços de Mídia do Azure 

Serviços de mídia do Microsoft Azure é uma plataforma extensível baseada em nuvem que permite que os desenvolvedores toobuild mídia escalonável gerenciamento e entrega de aplicativos. Serviços de mídia baseia-se nas APIs de REST que permitem que você toosecurely carregar, armazenar, codificar e empacotar conteúdo de áudio ou vídeo sob demanda e ao vivo streaming entrega toovarious clientes (por exemplo, TV, PC e dispositivos móveis).

Você pode compilar fluxos de trabalho de ponta a ponta usando totalmente os serviços de mídia. Você também pode escolher toouse componentes de terceiros para algumas partes do fluxo de trabalho. Por exemplo, codifique usando um codificador de terceiros. Em seguida, carregue, proteja, empacote e entregue usando os serviços de mídia.

Você pode escolher toostream seu conteúdo ao vivo ou fornecer conteúda sob demanda. tópico de saudação também vincula a tópicos relevantes tooother.

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
Você pode exibir os roteiros de aprendizagem do AMS aqui:

* [Fluxo de trabalho do streaming ao vivo do AMS](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-live/)
* [Fluxo de trabalho do streaming sob demanda do AMS](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-on-demand/)

## <a name="prerequisites"></a>Pré-requisitos

toostart usando serviços de mídia do Azure, você deve ter o seguinte hello:

* Uma conta do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com).
* Uma conta de Serviços de Mídia do Azure. Para obter mais informações, veja [Criar conta](media-services-portal-create-account.md).
* (Opcional) Configure o ambiente de desenvolvimento. Escolha .NET ou API REST para seu ambiente de desenvolvimento. Para obter mais informações, veja [Configurar ambiente](media-services-dotnet-how-to-use.md).

    Além disso, saiba como muito[conectar programaticamente tooAMS API](media-services-use-aad-auth-to-access-ams-api.md).
* Um ponto de extremidade de streaming padrão ou premium em estado iniciado.  Para obter mais informações, consulte [Gerenciando pontos de extremidade de streaming](media-services-portal-manage-streaming-endpoints.md)

## <a name="sdks-and-tools"></a>SDKs e ferramentas

soluções de serviços de mídia toobuild, você pode usar:

* [API REST dos Serviços de Mídia](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)
* Um dos clientes disponíveis da saudação SDKs:
    * [SDK dos Serviços de Mídia do Azure para .NET](https://github.com/Azure/azure-sdk-for-media-services),
    * [SDK do Azure para Java](https://github.com/Azure/azure-sdk-for-java),
    * [SDK do PHP do Azure](https://github.com/Azure/azure-sdk-for-php),
    * [Serviços de Mídia do Azure para Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (esta é uma versão de um SDK do Node.js que não foi criada pela Microsoft. É mantido por uma comunidade e atualmente não tem 100% de cobertura de saudação AMS APIs).
* Ferramentas existentes:
    * [Portal do Azure](https://portal.azure.com/)
    * [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) ([AMSE] Gerenciador de Serviços de Mídia do Azure é um aplicativo Winforms/C# para Windows)

## <a name="concepts-and-overview"></a>Visão geral e conceitos
Para conferir os conceitos dos Serviços de Mídia do Azure, confira [Conceitos](media-services-concepts.md).

Para um como-tooseries que apresenta a você tooall Olá principais componentes de serviços de mídia do Azure, consulte [tutoriais passo a passo de serviços de mídia do Azure](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series). Esta série tem uma visão geral de conceitos e usa tarefas de toodemonstrate AMS Olá AMSE ferramenta. A ferramenta AMSE é uma ferramenta do Windows. Essa ferramenta oferece suporte à maioria das tarefas de saudação, você pode obter por meio de programação com [AMS SDK para .NET](https://github.com/Azure/azure-sdk-for-media-services), [SDK do Azure para Java](https://github.com/Azure/azure-sdk-for-java), ou [SDK PHP do Azure](https://github.com/Azure/azure-sdk-for-php).

## <a name="supported-scenarios-and-availability-of-media-services-across-data-centers"></a>Cenários com suporte e disponibilidade dos Serviços de Mídia em data centers

Para obter informações detalhadas, veja [Cenários do AMS e disponibilidade de recursos e serviços nos data centers](scenarios-and-availability.md).

## <a name="service-level-agreement-sla"></a>Contrato de nível de serviço (SLA)

* Para a Codificação dos Serviços de mídia, garantimos a disponibilidade de 99,9% de transações de API REST.
* Para streaming, atenderemos com êxito a solicitações com uma garantia de disponibilidade de 99,9% para conteúdos de mídia existentes quando um ponto de extremidade de streaming padrão ou premium for adquirido.
* Para canais ao vivo, garantimos que executar canais terão conectividade externa pelo menos 99,9% de tempo de saudação.
* Para proteção de conteúdo, garantimos que podemos com êxito atenderá solicitações de chave pelo menos 99,9% de tempo de saudação.
* Para o indexador, podemos com êxito atenderá solicitações de tarefa do indexador processadas com um codificação reservado unidade 99,9% de tempo de saudação.

Para obter mais informações, veja [SLA do Microsoft Azure](https://azure.microsoft.com/support/legal/sla/).

Para obter informações sobre a disponibilidade em data centers, consulte Olá [Avaiability](scenarios-and-availability.md#availability) seção.

## <a name="support"></a>Suporte

[Suporte do Azure](https://azure.microsoft.com/support/options/) fornece opções de suporte do Azure, incluindo os Serviços de Mídia.

## <a name="provide-feedback"></a>Fornecer comentários

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
