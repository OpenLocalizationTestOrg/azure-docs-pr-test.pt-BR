---
title: "aaaAzure Mobile Engagement Troubleshooting Guide - análise"
description: "Solução para problemas de Análise, Monitoramento, Segmentação e Painel no Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04a7020a-ad74-4491-be69-0bd574890029
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 69c6ff8f5c8540f8ba8b85b9ffec55acc59329fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-analytics-monitoring-segmentation-and-dashboard-issues"></a>Guia de solução para problemas de Análise, Monitoramento, Segmentação e Painel
Olá, estes são os problemas possíveis podem ser encontrados em como o Azure Mobile Engagement reúne informações sobre dispositivos, aplicativos e usuários.

## <a name="missingdelayed-information"></a>Informações Ausentes/Atrasadas
### <a name="issue"></a>Problema
* As informações ficam atrasadas ao aparecerem na Análise, Segmentação ou Painel.
* Faltam informações no Monitoramento.
* As informações estão ausentes na Análise, Segmentação ou Painel.
* Limite de segmentação atingido.

### <a name="causes"></a>Causas
* Você pode usar o hello análise de API, API de Monitor, e segmentos API toosee se todos os dados que você está ausente da saudação da interface do usuário é visível por meio de APIs de saudação.
* Se Olá SDK do Azure Mobile Engagement não estiver integrado corretamente em seu aplicativo não será capaz de toosee informações Olá Analytics, segmentação, monitoramento ou painéis.
* Os segmentos não podem ser alterados depois de criados; os segmentos só podem ser "clonados" (copiados) ou "destruídos" (excluídos). Os segmentos podem conter apenas 10 critérios.
* Olá melhor maneira tootest faltando informações de monitoramento é toosetup um dispositivo de teste, desinstalar e/ou reinstalar o aplicativo hello no dispositivo de teste de saudação.
* As informações são atualizadas a cada 24 horas para a Análise, Segmentação ou Painéis.
* Informações em novos segmentos não podem ser exibidas até 24 horas após eles são criados, mesmo se o segmento de saudação se baseia em informações anteriores.
* Filtrar seus dados de análise de saudação da interface do usuário mostrará todos os exemplos desse tipo, independentemente da versão de saudação do seu aplicativo (por exemplo as "Falhas" filtradas pelo nome aparecerão a partir das versões 1 e 2 de seu aplicativo).
* Hello período de tempo para análise é baseado nas Olá data dos usuários Olá configurações de dispositivo, para que um usuário cujo telefone tiver date de hello definida incorretamente pode aparecer em Olá errado período de tempo.
* Nenhum lado servidor dados são registrados quando você usar o botão de saudação muito "testar" envia, somente os dados serão registrados para campanhas de push real.

## <a name="cant-locate-items-in-ui"></a>Não é possível localizar itens na interface do usuário
### <a name="issue"></a>Problema
* Não é possível criar segmentos com base em certos critérios incorporados ou de marca de informações do aplicativo personalizado.
* Não é possível localizar certos critérios incorporados ou de marca de informações do aplicativo personalizado na Análise, Monitoramento ou Painéis.
* Não é possível interpretar Olá dados em análises, monitoramento, segmentação ou painéis.

### <a name="causes"></a>Causas
* Alguns itens internos e informações de aplicativo marcas só estão disponíveis como critérios de envio, mas não podem ser adicionadas tooa segmento ou visíveis de análise, monitoramento ou painel. 
* Para baseado em itens e informações de aplicativo tooa segmento as marcas que não podem ser adicionadas, você precisará toosetup lista de critérios em cada Olá tooperform de campanha mesmo funcionar como destino com base em um segmento de direcionamento.
* Consulte menus de contexto Olá nas seções painéis, monitoramento, a segmentação e análise Olá Olá interface de usuário do Azure Mobile Engagement para obter mais ajuda e como tooinformation.

## <a name="crash-troubleshooting"></a>Solucionar problemas de falhas
### <a name="issue"></a>Problema
* Falhas do Aplicativo que aparecem na Análise, Monitoramento ou Painel.

### <a name="causes"></a>Causas
* tootroubleshoot vistos no painel, monitoramento ou análise de falhas de aplicativo verifique se toocheck Olá notas para problemas conhecidos com versões anteriores do SDK de saudação.
* toofurther solucionar falhas executam um evento de um dispositivo de teste com seu aplicativo seja instalado e procure a ID do dispositivo na seção hello "monitorar eventos de –" hello Azure Mobile Engagement interface de usuário de aplicativo. Em seguida, execute o evento Olá que está causando toocrash seu aplicativo e pesquisar informações adicionais na Olá seção "Monitor – falhas" hello interface de usuário do Azure Mobile Engagement. 

