---
title: "aaaManage política de cache do Azure CDN no Azure Media Services | Microsoft Docs"
description: "Saiba como toomanage política de cache do Azure CDN no Azure Media Services."
services: media-services,cdn
documentationcenter: .NET
author: juliako
manager: erikre
editor: 
ms.assetid: be33aecc-6dbe-43d7-a056-10ba911e0e94
ms.service: media-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/04/2017
ms.author: juliako
ms.openlocfilehash: 4c7ee2922fcbb5727e10fbe44fc6e61b79f6917c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-cdn-caching-policy-in-azure-media-services"></a>Gerenciar a política de caching da CDN do Azure nos Serviços de Mídia do Azure
Os Serviços de Mídia do Azure fornecem streaming adaptável e download progressivo com base em HTTP. Streaming com base em HTTP é altamente escalonável, com os benefícios do armazenamento em cache em camadas proxy e CDN, bem como armazenamento em cache no lado do cliente. Pontos de extremidade de streaming fornecem recursos de streaming gerais e também a configuração de cabeçalhos de cache HTTP. Pontos de extremidade de streaming definem o Controle de Cache HTTP: cabeçalhos idade máxima e Vencimento. Saiba mais sobre os cabeçalhos de cache HTTP em [W3.org](http://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html).

## <a name="default-caching-headers"></a>Cabeçalhos de armazenamento em cache padrão
Por padrão, os pontos de extremidade de streaming aplicam cabeçalhos de cache de 3 dias para dados de streaming sob demanda (fragmentos/partes reais de mídia) e manifesto (lista de reprodução). Para transmissão ao vivo, os pontos de extremidade de streaming aplicam cabeçalhos de cache de 3 dias para solicitações de dados (fragmentos/partes reais de mídia) e cabeçalho de cache de 2 segundos para solicitações de manifesto (lista de reprodução). Quando a demanda tooon (arquivamento dinâmico) ativa o programa ao vivo aplicam cabeçalhos de cache streaming sob demanda.

## <a name="azure-cdn-integration"></a>Integração da CDN com o Azure
Os Serviços de Mídia do Azure fornecem [CDN integrada](https://azure.microsoft.com/updates/azure-media-services-now-fully-integrated-with-azure-cdn/) para pontos de extremidade de streaming. Cabeçalhos cache-control se aplica a saudação mesma maneira que tooCDN de pontos de extremidade de streaming habilitados pontos de extremidade de streaming. Azure usa CDN streaming internamente o ponto de extremidade configurado cache valores toodefine Olá tempo de vida do hello objetos armazenados em cache e também usa essa cabeçalhos de cache de entrega do valor tooset hello. Ao usar o CDN habilitado pontos de extremidade de streaming não é recomendável tooset valores de cache pequeno. Definir valores pequenos diminuir o desempenho de saudação e reduzir o benefício de saudação da CDN. Não é permitido tooset cabeçalhos de cache menores que 600 segundos para CDN habilitada pontos de extremidade de streaming.

> [!IMPORTANT]
>Os Serviços de Mídia do Azure têm integração completa com o Azure CDN. Com um único clique, você pode integrar todos os Olá disponíveis do Azure CDN provedores (Akamai e Verizon) tooyour incluindo produtos CDN Standard e Premium do ponto de extremidade de streaming. Para saber mais, veja este [anúncio](https://azure.microsoft.com/blog/standardstreamingendpoint/).
> 
> Encargos de dados do tooCDN de ponto de extremidade de streaming só obtém desabilitado se hello CDN é habilitada pelo ponto de extremidade de APIs de streaming ou usando a seção de ponto de extremidade streaming do portal de gerenciamento do Azure. Integração manual ou diretamente a criação de um ponto de extremidade CDN usando APIs de CDN ou seção portal não desabilitará encargos de saudação de dados.

## <a name="configuring-cache-headers-with-azure-media-services"></a>Configurando os cabeçalhos de cache com os Serviços de Mídia do Azure
Você pode usar o portal de gerenciamento do Azure ou valores de cabeçalho de cache de tooconfigure de APIs de serviços de mídia do Azure.

1. cabeçalhos de cache tooconfigure usando o gerenciamento de portal, consulte muito[como pontos de extremidade de Streaming tooManage](../media-services/media-services-portal-manage-streaming-endpoints.md) Olá Configurando de seção ponto de extremidade de Streaming.
2. API REST dos Serviços de Mídia do Azure, [StreamingEndpoint](https://msdn.microsoft.com/library/azure/dn783468.aspx#StreamingEndpointCacheControl).
3. SDK do .NET dos Serviços de Mídia do Azure, [Propriedades de StreamingEndpointCacheControl](http://go.microsoft.com/fwlink/?LinkId=615302).

## <a name="cache-configuration-precedence-order"></a>Ordem de precedência de configuração do cache
1. O valor de cache configurado dos Serviços de Mídia do Azure substitui o valor padrão.
2. Se não houver configuração manual, os valores padrão serão aplicados.
3. Por padrão, 2 segundos cabeçalhos cache aplica toolive streaming manifest(playlist), independentemente da configuração de mídia do Azure ou armazenamento do Azure e substituindo desse valor não está disponível.

