---
title: "aaaTroubleshoot Stream Analytics do Azure com logs de diagnóstico | Microsoft Docs"
description: "Saiba como diagnóstico tooanalyze logs de análise de fluxo de trabalhos no Microsoft Azure."
keywords: 
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
ms.openlocfilehash: 600fce73636dd137f8f3a137f1d77b59b4a88801
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-stream-analytics-by-using-diagnostics-logs"></a>Solucionar problemas do Stream Analytics do Azure usando logs de diagnóstico

Ocasionalmente, um trabalho do Stream Analytics do Azure interrompe o processamento de forma inesperada. É tootroubleshoot capazes de importantes toobe nesse tipo de evento. evento Olá pode ser causado por um resultado de consulta inesperada, toodevices de conectividade ou uma interrupção inesperada de serviço. Olá logs de diagnóstico no Stream Analytics podem ajudá-lo a identificar a causa de saudação de problemas quando eles ocorrem e reduzem o tempo de recuperação.

## <a name="log-types"></a>Tipos de logs

O Stream Analytics oferece dois tipos de logs: 
* [Logs de atividades](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) (sempre ativados). Os logs de atividades fornecem informações sobre as operações realizadas nos trabalhos.
* [Logs de diagnóstico](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) (configuráveis). Os logs de diagnóstico fornecem informações mais avançadas sobre tudo o que acontece com um trabalho. Diagnóstico registra quando Olá trabalho é criado de início e fim quando Olá trabalho é excluído. Abrangem eventos quando o trabalho de saudação é atualizado e enquanto ele está em execução.

> [!NOTE]
> Você pode usar os serviços, como o armazenamento do Azure, os Hubs de eventos do Azure e Azure Log Analytics tooanalyze dados. Você é cobrado com base em Olá modelo para os serviços de preços.
>

## <a name="turn-on-diagnostics-logs"></a>Ativar os logs de diagnóstico

Os logs de diagnóstico estão **desativados** por padrão. tooturn em logs de diagnóstico, execute estas etapas:

1.  Entrar toohello portal do Azure e vá toohello folha de trabalho de streaming. Em **Monitoramento**, selecione **Logs de diagnóstico**.

    ![Logs de toodiagnostics de navegação de folha](./media/stream-analytics-job-diagnostic-logs/image1.png)  

2.  Selecione **Ativar diagnóstico**.

    ![Ativar os logs de diagnóstico](./media/stream-analytics-job-diagnostic-logs/image2.png)

3.  Em Olá **as configurações de diagnóstico** página, para **Status**, selecione **em**.

    ![Alterar o status dos logs de diagnóstico](./media/stream-analytics-job-diagnostic-logs/image3.png)

4.  Configure o hello arquivamento destino (conta de armazenamento, hub de eventos, análise de Log) que você deseja. Em seguida, selecione as categorias de saudação de logs que você deseja toocollect (execução, criação). 

5.  Salve a nova configuração de diagnóstico hello.

configuração de diagnóstico Olá entra em vigor de tootake do cerca de 10 minutos. Depois disso, Olá logs de início que aparecem no destino de arquivamento de saudação configurado (você pode vê-los em Olá **logs de diagnóstico** página):

![Logs de toodiagnostics navegação folha - destinos de arquivamento](./media/stream-analytics-job-diagnostic-logs/image4.png)

Para obter informações sobre como configurar o diagnóstico, consulte [Coletar e consumir dados de diagnóstico nos recursos do Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs).

## <a name="diagnostics-log-categories"></a>Categorias de logs de diagnóstico

Atualmente, capturamos duas categorias de logs de diagnóstico:

* **Criação**. Captura de log eventos que são relacionada toojob operações de criação: criação de trabalho, adicionando e excluindo entradas e saídas, adicionar e atualizar a consulta hello, iniciando e parando trabalho de saudação.
* **Execução**. Captura eventos que ocorrem durante a execução do trabalho:
    * Erros de conectividade
    * Erros de processamento de dados, incluindo:
        * Eventos que não estão em conformidade toohello consultar definição (tipos de campo incompatível e valores, os campos ausentes e assim por diante)
        * Erros de avaliação da expressão
    * Outros erros e eventos

## <a name="diagnostics-logs-schema"></a>Esquema dos logs de diagnóstico

Todos os logs são armazenados no formato JSON. Cada entrada tem Olá campos de cadeia de caracteres a seguir:

Nome | Descrição
------- | -------
tempo real | Carimbo de hora (UTC) do log de saudação.
resourceId | ID do recurso Olá Olá operação ocorreu, em letras maiusculas. Ele inclui Olá ID da assinatura, o grupo de recursos de saudação e o nome do trabalho hello. Por exemplo, **/SUBSCRIPTIONS/6503D296-DAC1-4449-9B03-609A1F4A1C87/RESOURCEGROUPS/MY-RESOURCE-GROUP/PROVIDERS/MICROSOFT.STREAMANALYTICS/STREAMINGJOBS/MYSTREAMINGJOB**.
categoria | Categoria do log, **Execução** ou **Criação**.
operationName | Nome da operação de saudação que é registrada. Por exemplo, **enviar eventos: toomysqloutput de falha de gravação de saída SQL**.
status | Status da operação de saudação. Por exemplo, **Com Falha** ou **Com Êxito**.
level | Nível do log. Por exemplo, **Erro**, **Aviso** ou **Informativo**.
propriedades | Detalhes específicos à entrada de log, serializados como uma cadeia de caracteres JSON. Para obter mais informações, consulte Olá seções a seguir.

### <a name="execution-log-properties-schema"></a>Esquema de propriedades do log de execução

Os logs de execução trazem informações sobre eventos que ocorreram durante a execução do trabalho do Stream Analytics. esquema de saudação de propriedades varia, dependendo do tipo de saudação do evento. No momento, temos Olá seguintes tipos de logs de execução:

### <a name="data-errors"></a>Erros de dados

É qualquer erro que ocorre enquanto o trabalho hello está processando os dados nessa categoria de logs. Esses logs costumam ser criados durante operações de leitura, serialização e gravação de dados. Esses logs não incluem erros de conectividade. Os erros de conectividade são tratados como eventos genéricos.

Nome | Descrição
------- | -------
Fonte | Nome do trabalho de saudação de entrada ou saída onde ocorreu o erro de saudação.
Mensagem | Mensagem associada ao erro hello.
Tipo | Tipo de erro. Por exemplo, **DataConversionError**, **CsvParserError** ou **ServiceBusPropertyColumnMissingError**.
Dados | Contém dados úteis tooaccurately localizar a origem de saudação do erro hello. Tootruncation assunto, dependendo do tamanho.

Dependendo da saudação **operationName** valor, os erros de dados têm Olá esquema a seguir:
* **Serializar eventos**. Serializar os eventos ocorridos durante operações de leitura de eventos. Eles ocorrem quando hello dados na entrada hello não satisfazem o esquema de consulta Olá para um dos seguintes motivos:
    * *Incompatibilidade de tipos durante o evento (de) serializar*: identifica Olá campo que está causando o erro de saudação.
    * *Não é possível ler um evento, a serialização inválido*: lista informações sobre a localização de saudação nos dados de entrada hello onde ocorreu o erro de saudação. Inclui o nome do blob para entrada de blob, deslocamento e um exemplo de dados de saudação.
* **Enviar eventos**. Envia eventos ocorridos durante operações de gravação. Eles identificam Olá streaming evento que causou o erro de saudação.

### <a name="generic-events"></a>Eventos genéricos

Os eventos genéricos abrangem todo o resto.

Nome | Descrição
-------- | --------
Erro | (opcional) Informações sobre erros. Normalmente, essas são informações de exceção, se estiverem disponíveis.
Mensagem| Mensagem de log.
Tipo | Tipo de mensagem. Mapeia toointernal categorização de erros. Por exemplo, **JobValidationError** ou **BlobOutputAdapterInitializationFailure**.
ID de Correlação | [GUID](https://en.wikipedia.org/wiki/Universally_unique_identifier) que identifica exclusivamente a execução do trabalho hello. Todas as entradas de log de execução de saudação do tempo de saudação do trabalho inicia até Olá trabalho será interrompido ter Olá mesmo **ID de correlação** valor.

## <a name="next-steps"></a>Próximas etapas

* [Introdução tooStream análise](stream-analytics-introduction.md)
* [Introdução ao Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics](stream-analytics-scale-jobs.md)
* [Referência da linguagem de consulta do Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST de gerenciamento do Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
