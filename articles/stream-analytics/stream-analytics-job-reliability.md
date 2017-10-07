---
title: "Evitar interrupções de serviço com trabalhos do Stream Analytics do Azure | Microsoft Docs"
description: "Orientação sobre como tornar resilientes suas atualizações de trabalhos do Stream Analytics."
services: stream-analytics
documentationCenter: 
authors: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 3ac65c93ecb47e93e963dd9869a7af70f73b19c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="guarantee-stream-analytics-job-reliability-during-service-updates"></a>Garantir a confiabilidade do trabalho do Stream Analytics durante atualizações do serviço

Parte de ser um serviço totalmente gerenciado é Olá recurso toointroduce nova funcionalidade do serviço e melhorias em um ritmo acelerado. Como resultado, o Stream Analytics pode ter uma implantação semanal (ou mais frequente) da atualização do serviço. Independentemente de quantos testes são realizados ainda há um risco de que um trabalho existente, em execução pode ser quebradas devido toohello introdução de um bug. Para clientes que executam trabalhos de processamento de streaming crítico esses riscos necessário toobe evitado. Um mecanismo os clientes podem usar tooreduce esse risco é do Azure  **[região emparelhada](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  modelo. 

## <a name="how-do-azure-paired-regions-address-this-concern"></a>Como as regiões emparelhadas do Azure podem resolver essa questão?

O Stream Analytics garante que os trabalhos em regiões emparelhadas sejam atualizados em lotes separados. Como resultado, há um intervalo de tempo suficiente entre as atualizações de saudação quebra potencial tooidentify bugs e corrigi-los.

_Com exceção de saudação do Índia Central_ (cujo região emparelhada, Sul da Índia e não tem presença do Stream Analytics), implantação de saudação de um tooStream atualização Analytics não ocorrerá em Olá a mesma hora em um conjunto de regiões emparelhadas. Implantações em várias regiões **em Olá mesmo grupo** pode ocorrer **em Olá simultaneamente**.

artigo Olá  **[disponibilidade e regiões emparelhadas](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  tem informações mais atualizadas hello, nos quais regiões são combinadas.

Os clientes são aconselhados toodeploy trabalhos idênticos tooboth emparelhado regiões. Além disso tooStream análise interno de recursos, os clientes de monitoramento também é avisados trabalhos de saudação toomonitor como se **ambos** trabalhos de produção. Se uma quebra de toobe identificado um resultado da atualização de serviço de análise de fluxo hello, escalonar adequadamente e failover nenhuma saída de trabalho Íntegro toohello consumidores de downstream. Escalonamento de bloqueios toosupport impedirá região emparelhada Olá sejam afetados pela nova implantação de saudação e manter a integridade de saudação de trabalhos Olá emparelhado.
