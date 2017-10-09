---
title: "Visão geral de ponto de extremidade do Media Services Streaming aaaAzure | Microsoft Docs"
description: "Este tópico fornece uma visão geral dos pontos de extremidade de streaming dos Serviços de Mídia do Azure."
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: 097ab5e5-24e1-4e8e-b112-be74172c2701
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: f27f590175dcc945d1d3299fc0cae5a68cfbf4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-endpoints-overview"></a>Visão geral dos pontos de extremidade de streaming 

##<a name="overview"></a>Visão geral

No Microsoft Azure Media Services AMS (), um **ponto de extremidade de Streaming** representa um serviço de streaming que pode entregar conteúdo diretamente tooa Player do cliente ou tooa rede de fornecimento de conteúdo (CDN) para melhor distribuição. Os Serviços de Mídia também fornecem integração perfeita da CDN do Azure. fluxo de saída de saudação de um serviço StreamingEndpoint pode ser uma transmissão ao vivo, um vídeo sob demanda ou download progressivo do seu ativo em sua conta de serviços de mídia. Cada conta dos Serviços de Mídia do Azure inclui um StreamingEndpoint padrão. StreamingEndpoints adicionais podem ser criadas na conta de saudação. Há duas versões do StreamingEndpoints, 1.0 e 2.0. A partir de 10 de janeiro de 2017, todas as contas AMS recém-criadas incluirão a versão 2.0 **padrão** do StreamingEndpoint. Adicional de pontos de extremidade que você adicione a conta de toothis streaming também será a versão 2.0. Essa alteração não afetará as contas existentes Olá; StreamingEndpoints existentes serão versão 1.0 e pode ser atualizado tooversion 2.0. Com essa alteração haverá alterações de comportamento, cobrança e recurso (para obter mais informações, consulte Olá **tipos e versões de Streaming** seção documentada abaixo).

Além disso, começando com a versão de hello 2.15 (lançado em janeiro de 2017), os serviços de mídia do Azure adicionados Olá entidade de ponto de extremidade de Streaming toohello propriedades a seguir: **CdnProvider**, **CdnProfile**,  **FreeTrialEndTime**, **StreamingEndpointVersion**. Para obter uma visão detalhada dessas propriedades, clique [aqui](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint). 

Quando você cria uma conta de serviços de mídia do Azure, um padrão de ponto de extremidade de streaming padrão é criado para você no hello **parado** estado. Não é possível excluir o ponto de extremidade de streaming de padrão de saudação. Dependendo Olá disponibilidade CDN do Azure na região Olá direcionada, por padrão recém-criado padrão ponto de extremidade de streaming também inclui "StandardVerizon" CDN integração do provedor. 

>[!NOTE]
>Integração da CDN do Azure pode ser desabilitada antes de iniciar o ponto de extremidade de streaming de saudação.

Este tópico fornece uma visão geral das funcionalidades Olá principais são fornecidas por pontos de extremidade de streaming.

## <a name="streaming-types-and-versions"></a>Tipos e versões de streaming

### <a name="standardpremium-types-version-20"></a>Tipos Standard/Premium (versão 2.0)

A partir da versão de janeiro de 2017 Olá dos serviços de mídia, você tem dois tipos de streaming: **padrão** e **Premium**. Esses tipos são parte da versão de ponto de extremidade de Streaming hello "2.0".

Tipo|Descrição
---|---
**Standard**|Essa é a opção de padrão de saudação que funciona para a maioria de saudação dos cenários de saudação.<br/>Com essa opção, você obtém SLA/limitada, primeiros 15 dias depois de iniciar a extremidade de streaming de saudação é gratuita.<br/>Se você criar mais de um fluxo de pontos de extremidade, somente hello primeiro um é livre para Olá primeiros 15 dias, Olá outros são cobrados assim que você iniciá-los. <br/>Observe que a avaliação gratuita só aplica toonewly criada contas de serviços de mídia e o padrão de ponto de extremidade de streaming. Pontos de extremidade de streaming existentes e Além disso criados pontos de extremidade de streaming não inclui avaliação gratuita período ainda estiverem atualizados tooversion 2.0 ou são criados como versão 2.0.
**Premium**|Esta opção é adequada para cenários profissionais que exigem maior escala ou controle.<br/>SLA variável com base na capacidade da UA (unidade de streaming) premium adquirida, pontos de extremidade de streaming dedicados residem em um ambiente isolado e não competem por recursos.

Para obter mais informações, consulte Olá **Streaming comparar tipos** seção a seguir.

### <a name="classic-type-version-10"></a>Tipo Clássico (versão 1.0)

Para usuários que criou contas AMS versão de 10 de janeiro de 2017 toohello anterior, você tem uma **clássico** tipo de um ponto de extremidade de streaming. Esse tipo é parte da saudação version "1.0" do ponto de extremidade de streaming.

Se seu **versão "1.0"** ponto de extremidade de streaming tem > = 1 premium (SU), as unidades de streaming será o ponto de extremidade de streaming premium e fornecerá todos os recursos de AMS (assim como Olá **padrão/Premium** tipo) sem etapas adicionais de configuração.

>[!NOTE]
>Pontos de extremidade de streaming **Clássicos** (versão “1.0” e 0 UA) fornecem recursos limitados e não incluem um SLA. É recomendável toomigrate muito**padrão** digite tooget uma melhor experiência e toouse de recursos, como empacotamento dinâmico ou criptografia e outros recursos que acompanham o hello **padrão** tipo. toomigrate toohello **padrão** digite, vá toohello [portal do Azure](https://portal.azure.com/) e selecione **aceitação tooStandard**. Para obter mais informações sobre migração, consulte Olá [migração](#migration-between-types) seção.
>
>Lembre-se de que essa operação não pode ser revertida e tem um impacto no preço.
>
 
## <a name="comparing-streaming-types"></a>Comparando tipos de streaming

### <a name="versions"></a>Versões

|Tipo|StreamingEndpointVersion|ScaleUnits|CDN|Cobrança|Contrato de Nível de Serviço| 
|--------------|----------|-----------------|-----------------|-----------------|-----------------|    
|Clássico|1.0|0|ND|Grátis|ND|
|Ponto de Extremidade de Streaming Standard|2,0|0|Sim|Pago|Sim|
|Unidades de Streaming Premium|1.0|>0|Sim|Pago|Sim|
|Unidades de Streaming Premium|2,0|>0|Sim|Pago|Sim|

### <a name="features"></a>Recursos

Recurso|Standard|Premium
---|---|---
Gratuito pelos primeiros 15 dias| Sim |Não
Taxa de transferência |Backup too600 Mbps quando a CDN do Azure não é usada. Escala com CDN.|200 Mbps por UA (unidade de streaming). Escala com CDN.
Contrato de Nível de Serviço | 99.9|99,9 (200 Mbps por UA).
CDN|Azure CDN, CDN de terceiros ou sem CDN.|Azure CDN, CDN de terceiros ou sem CDN.
A cobrança é rateada| Diário|Diário
Criptografia dinâmica|Sim|Sim
Empacotamento dinâmico|Sim|Sim
Escala|Auto é dimensionado a taxa de transferência toohello direcionado.|Unidades de streaming adicionais
Filtragem de IP/G20/Host personalizado|Sim|Sim
Download progressivo|Sim|Sim
Uso recomendado |Recomendado para a grande maioria Olá dos cenários de streaming.|Uso profissional.<br/>Se você achar que pode ter necessidades além do Standard. Entre em contato conosco (amsstreaming em microsoft.com) se você espera ter uma audiência simultânea superior a 50.000 visualizadores.


## <a name="migration-between-types"></a>Migração entre tipos

Da | muito| Ação
---|---|---
Clássico|Standard|Necessidade de tooopt
Clássico|Premium| Escala (unidades de streaming adicionais)
Standard/Premium|Clássico|Não disponível (se a versão do ponto de extremidade de streaming for 1.0. É permitido tooclassic toochange com configuração scaleunits muito "0")
Standard (com/sem CDN)|Premium com hello mesmas configurações|Permitido em Olá **iniciado** estado. (por meio do Portal do Azure)
Premium (com/sem CDN)|Standard com hello mesmas configurações|Permitido em Olá **iniciado** estado (por meio do portal do Azure)
Standard (com/sem CDN)|Premium com configuração diferente|Permitido em Olá **interrompido** estado (por meio do portal do Azure). Não é permitida no estado de execução de saudação.
Premium (com/sem CDN)|Standard com configuração diferente|Permitido em Olá **interrompido** estado (por meio do portal do Azure). Não é permitida no estado de execução de saudação.
Versão 1.0 com UA > = 1 com CDN|Standard/Premium sem qualquer CDN|Permitido em Olá **interrompido** estado. Não é permitido em Olá **iniciado** estado.
Versão 1.0 com UA > = 1 com CDN|Standard com/sem CDN|Permitido em Olá **interrompido** estado. Não é permitido em Olá **iniciado** estado. A CDN da Versão 1.0 será excluída e uma nova será criada e iniciada.
Versão 1.0 com UA > = 1 com CDN|Premium com/sem CDN|Permitido em Olá **interrompido** estado. Não é permitido em Olá **iniciado** estado. A CDN Clássica será excluída e uma nova será criada e iniciada.

## <a name="next-steps"></a>Próximas etapas
Examine os roteiros de aprendizagem dos Serviços de Mídia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

