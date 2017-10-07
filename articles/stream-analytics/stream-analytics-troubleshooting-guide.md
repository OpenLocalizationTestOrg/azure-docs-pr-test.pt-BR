---
title: Guia de aaaTroubleshooting do Stream Analytics do Azure | Microsoft Docs
description: Como tootroubleshoot o trabalho do Stream Analytics
keywords: "guia de solução de problemas"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 4add48054e06a7d8eb617a08595c1be4555c59d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-azure-stream-analytics"></a>Guia de solução de problemas do Stream Analytics do Azure

Solução de problemas do Azure Stream Analytics pode aparecer toobe um esforço complexo à primeira vista. Depois de trabalhar com muitos usuários, podemos criou esse processo de saudação do guia toohelp simplificar e remova suposições Olá sobre entradas, saídas, consultas e funções.

## <a name="troubleshoot-your-stream-analytics-job"></a>Resolver problemas do trabalho do Stream Analytics

Para obter melhores resultados em seu trabalho de análise de fluxo de solução de problemas, use Olá diretrizes a seguir:

1.  Testar a conectividade:
    - Verificar a conectividade tooinputs e saídas usando Olá **Conexão de teste** botão para cada entrada e saída.

2.  Examinar os dados de entrada:
    - tooverify que dados de entrada é que fluem para o Hub de eventos, use [Service Bus Explorer](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a) tooconnect tooAzure Hub de eventos (se a entrada do Hub de eventos é usada).  
    - Saudação de uso [ **dados de exemplo** ](stream-analytics-sample-data-input.md) botão para cada entrada e baixar os dados de entrada de exemplo hello.
    - Inspecione a forma de Olá Olá exemplo dados toounderstand de dados Olá: Olá esquema e hello [tipos de dados](https://msdn.microsoft.com/library/azure/dn835065.aspx).

3.  Testar a consulta:
    - Em Olá **consulta** guia, use Olá **teste** botão consulta de saudação tootest e usar dados de exemplo hello baixado muito[teste Olá consulta](stream-analytics-test-query.md). Examine os erros e tente toocorrect-los.
    - Se você usar [ **Timestamp By**](https://msdn.microsoft.com/library/azure/mt573293.aspx), verifique se eventos Olá têm carimbos de hora maiores Olá [hora de início do trabalho](stream-analytics-out-of-order-and-late-events.md).

4.  Depurar a consulta:
    - Recrie a consulta de saudação progressivamente de agregações complexas de toomore de instrução select simples usando as etapas. toobuild a lógica de consulta Olá passo a passo, use [WITH](https://msdn.microsoft.com/library/azure/dn835049.aspx) cláusulas.
    - Use [SELECT INTO](stream-analytics-select-into.md) toodebug etapas de consulta.

5.  Elimine armadilhas comuns, como:
    - Um [ **onde** ](https://msdn.microsoft.com/library/azure/dn835048.aspx) cláusula na consulta Olá filtrou todos os eventos, impedindo que qualquer saída que está sendo gerado.
    - Quando você usa funções de janela, aguarde toosee de duração de janela inteira Olá uma saída de consulta de saudação.
    - saudação de carimbo de hora para eventos precede hora de início do trabalho hello e, portanto, eventos são descartados.

6.  Usar a ordenação de eventos:
    - Se todos os hello etapas anteriores funcionaram bem, vá toohello **configurações** folha e selecione [ **a ordenação de eventos**](stream-analytics-out-of-order-and-late-events.md). Verificar se essa política está configurada para o que faz sentido em seu cenário. Olá política é *não* aplicadas quando você usa Olá **teste** consulta de saudação do botão tootest. Esse resultado é uma diferença entre o teste no navegador em vez de executar o trabalho de saudação em produção.

7.  Depurar usando métricas:
    - Se você não obtiver nenhuma saída depois Olá esperado de duração (com base em consulta Olá), tente seguir hello:
        - Examinar [ **métricas de monitoramento** ](stream-analytics-monitoring.md) em Olá **Monitor** guia. Porque valores hello são agregados, métricas de saudação atraso por alguns minutos.
            - Se eventos de entrada > 0, o trabalho de saudação é capaz de tooread dados de entrada. Se os Eventos de Entrada não forem > 0:
                - toosee se a fonte de dados de saudação tem dados válidos, verificar usando [Service Bus Explorer](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a). Esta seleção se aplica se o trabalho de saudação é usando o Hub de eventos como entrada.
                - Verifique toosee se o formato de serialização de dados hello e codificação de dados estão como esperado.
                - Se o trabalho Olá estiver usando um Hub de eventos, verifique toosee se Olá corpo de mensagem de saudação é *nulo*.
            - Se os erros de conversão de dados > 0 e alpinismo, seguinte Olá pode ser verdadeiro:
                - trabalho de saudação pode não ser capaz de toode-serializar eventos hello.
                - Olá esquema de evento pode não corresponder Olá definido ou o esquema esperado de eventos de saudação na consulta de saudação.
                - saudação de tipos de dados de alguns dos campos de saudação no evento de saudação podem não corresponder às expectativas.
            - Se os erros de tempo de execução > 0, isso significa trabalho Olá pode receber dados hello, mas está gerando erros durante o processamento de consulta de saudação.
                - erros de saudação toofind, vá toohello [os Logs de auditoria](../azure-resource-manager/resource-group-audit.md) e filtrar *falha* status.
            - Se InputEvents > 0 e OutputEvents = 0, significa que uma das seguintes Olá for verdadeira:
                - O processamento de consulta resultou em zero evento de saída.
                - Os eventos ou seus campos podem estar malformados, resultando em nenhuma saída após o processamento da consulta.
                - trabalho Olá foi toohello de dados não é possível toopush [coletor de saída](stream-analytics-select-into.md) por motivos de conectividade ou de autenticação.
        - Em todos os Olá mencionado anteriormente casos de erro, as operações de mensagens de log explicam detalhes adicionais (incluindo o que está acontecendo), exceto em casos em que a lógica de consulta Olá filtrada todos os eventos. Se o processamento de vários eventos hello gera erros, registra logs Olá primeiro três mensagens de erro do mesmo tipo dentro de 10 minutos tooOperations de saudação do Stream Analytics. Em seguida, ele suprimirá erros idênticos adicionais com a mensagem “Os erros estão ocorrendo muito rapidamente e estão sendo suprimidos”.

8. Depurar usando os logs de auditoria e de diagnóstico:
    - Use [os Logs de auditoria](../azure-resource-manager/resource-group-audit.md)e erros de tooidentify e depuração de filtro.
    - Use [logs de diagnósticos trabalho](stream-analytics-job-diagnostic-logs.md) tooidentify e depuração de erros.

9. Examine Olá saídas:
    - Quando o status do trabalho Olá é *executando*, dependendo da duração Olá estipulado na consulta hello, você pode ver a saída de hello na fonte de dados do coletor de saudação.
    - Se você não veja as saídas que serão tooa tipo de saída específicos, redirecione tooan tipo de saída que é menos complexo, como um Blob do Azure. Usando o Gerenciador de armazenamento, verifique toosee se a saída de hello pode ser vista. Além disso, verifique se limites limitação a saída de hello estão impedindo os dados que estão sendo recebidas.

10. Use a análise de fluxo de dados com métricas do diagrama de trabalho:
    - fluxo de dados de tooanalyze e identificar problemas, use Olá [diagrama de trabalho com métricas](stream-analytics-job-diagram-with-metrics.md).

11. Abrir um caso de suporte:
    - Por fim, se tudo o mais falhar, abra um caso de suporte da Microsoft usando Olá SubscriptionID que contém seu trabalho.

## <a name="get-help"></a>Obter ajuda

Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas

* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
