---
title: aaaDiagnose e resolver problemas | Microsoft Docs
description: "Este tutorial aborda como toodiagnose e solucionar problemas em seu ambiente de informações da série de tempo"
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/24/2017
ms.author: venkatja
ms.openlocfilehash: 00893d4bec497f5f8bf7093be5b96f1844446d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-and-solve-problems-in-your-time-series-insights-environment"></a>Diagnosticar e resolver problemas no ambiente do Time Series Insights

## <a name="i-dont-see-my-data"></a>Não vejo meus dados
Aqui estão algumas razões por que você não pode ver os dados no seu ambiente Olá [portal do Azure Insights de série de tempo](https://insights.timeseries.azure.com).

### <a name="your-event-source-doesnt-have-data-in-json-format"></a>A origem do evento não tem dados no formato JSON
Atualmente, o Azure Time Series Insights dá suporte apenas a dados JSON. Para obter exemplos do JSON, consulte [Formas de JSON com suporte](time-series-insights-send-events.md#supported-json-shapes).

### <a name="when-you-registered-your-event-source-you-didnt-provide-hello-key-that-has-hello-required-permission"></a>Ao registrar a origem do evento, você não fornecer a chave Olá que tenha permissão de saudação necessária
* Para um hub IoT, você precisa de chave de saudação tooprovide com **serviço conectar** permissão.

   ![Permissão de conexão de serviço do Hub IoT](media/diagnose-and-solve-problems/iothub-serviceconnect-permissions.png)

   Conforme mostrado na saudação anterior a imagem, qualquer uma das políticas de saudação **iothubowner** e **service** funcionaria, pois ambos têm **serviço se conectar** permissão.
* Para um hub de eventos, você precisa de chave de saudação tooprovide com **escutar** permissão.

   ![Permissão de escuta do hub de eventos](media/diagnose-and-solve-problems/eventhub-listen-permissions.png)

   Conforme mostrado na saudação anterior a imagem, qualquer uma das políticas de saudação **ler** e **gerenciar** funcionaria, pois ambos têm **escutar** permissão.

### <a name="hello-provided-consumer-group-is-not-exclusive-tootime-series-insights"></a>Olá fornecido o grupo de consumidores não é exclusivo tooTime série Insights
Para um hub IoT ou um hub de eventos, durante o registro solicitamos que você toospecify grupo de consumidores de saudação que deve ser usado para ler os dados. Esse grupo de consumidores não deve ser compartilhado. Se ele for compartilhado, hub de eventos subjacente Olá automaticamente desconecta um dos leitores Olá aleatoriamente.

## <a name="i-see-my-data-but-theres-a-lag"></a>Consigo ver meus dados, mas há um retardo
Aqui estão os motivos pelos quais você pode receber dados parciais no seu ambiente Olá [portal Insights de série de tempo](https://insights.timeseries.azure.com).

### <a name="your-environment-is-getting-throttled"></a>O ambiente está ficando restrito
Olá limitação é aplicada com base no tipo de SKU e a capacidade do ambiente de saudação. Todas as fontes de evento no ambiente de saudação compartilham essa capacidade. Se a origem do evento Olá para o hub IoT ou hub de eventos é enviar dados além dos limites de saudação imposta, você verá a limitação e um atraso.

Olá diagrama a seguir mostra um ambiente de informações da série de tempo que tenha um SKU de S1 e a capacidade de 3. Ele pode ingressar 3 milhões de eventos por dia.

![Capacidade atual do SKU do ambiente](media/diagnose-and-solve-problems/environment-sku-current-capacity.png)

Suponha que esse ambiente é ingestão de mensagens de um hub de eventos com taxa de entrada hello mostrada no diagrama a seguir de saudação:

![Taxa de entrada de exemplo para um hub de eventos](media/diagnose-and-solve-problems/eventhub-ingress-rate.png)

Conforme mostrado no diagrama hello, taxa diária de entrada hello está ~ 67,000 mensagens. Essa taxa converte aproximadamente too46 mensagens a cada minuto. Se cada mensagem de hub de eventos é bidimensional tooa único evento de informações da série de tempo, esse ambiente não vê nenhuma limitação. Se cada mensagem de hub de eventos é bidimensional too100 eventos de informações da série de tempo, em seguida, 4,600 eventos devem ser incluídos a cada minuto. Um ambiente de SKU S1 que tem uma capacidade 3 pode ingressar apenas 2.100 eventos por minuto (1 milhão de eventos por dia = 700 eventos por minuto em 3 unidades = 2.100 eventos por minuto). Portanto você pode ver um atraso toothrottling vencimento. 

Para obter um entendimento de alto nível sobre como funciona a lógica de nivelamento, consulte a seção [Formas de JSON com suporte](time-series-insights-send-events.md#supported-json-shapes).

#### <a name="recommended-steps"></a>Etapas recomendadas
latência de saudação toofix, Olá aumentar capacidade do SKU do seu ambiente. Para obter mais informações, consulte [como tooscale seu ambiente de tempo série Insights](time-series-insights-how-to-scale-your-environment.md).

### <a name="youre-pushing-historical-data-and-causing-slow-ingress"></a>Você está enviando dados históricos e causando a entrada lenta
Se você estiver se conectando a uma origem do evento existente, é provável que o Hub IoT ou o hub de eventos já contenha dados. Portanto ambiente Olá inicia dados entre o início de saudação do período de retenção de mensagem da fonte de evento hello. 

Esse comportamento é o comportamento padrão de saudação e não pode ser substituído. Você pode envolver a limitação e pode demorar um pouco toocatch backup sobre a ingestão de dados históricos.

#### <a name="recommended-steps"></a>Etapas recomendadas
latência de saudação toofix, Olá execute as etapas a seguir:
1. Aumente Olá SKU capacidade toohello valor máximo permitido (10, neste caso). Depois de capacidade de saudação é aumentada, processo de entrada hello inicia aproximando muito mais rápido. Você pode visualizar rapidamente como estamos obtendo por meio do gráfico de disponibilidade Olá Olá [portal Insights de série de tempo](https://insights.timeseries.azure.com). Você é cobrado para Olá maior capacidade.
2. Depois de latência de saudação é detectada, diminua a taxa de entrada normal Olá SKU capacidade tooyour voltar.

## <a name="my-event-sources-timestamp-property-name-setting-doesnt-work"></a>A configuração *nome da propriedade do carimbo de data/hora* de minha origem do evento não funciona
Verifique se o hello nome e valor atendem toohello regras a seguir:
* nome de propriedade de carimbo de hora Olá _diferencia maiusculas de minúsculas_.
* valor da propriedade timestamp Olá que vêm de sua fonte de evento, como uma cadeia de caracteres JSON, deve ter o formato de saudação _AAAA-MM-ddTHH. FFFFFFFK_. Um exemplo de uma cadeia de caracteres desse tipo é “2008-04-12T12:53Z”.
