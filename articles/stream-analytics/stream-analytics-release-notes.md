---
title: "Notas de versão de análise de aaaStream | Microsoft Docs"
description: "Notas de versão do Stream Analytics"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5e59f893-cd2c-43fb-9eca-c146ce637203
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/03/2017
ms.author: jeffstok
ms.openlocfilehash: 1426ebc260be19fbde60518b25501fe53d908d46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-release-notes"></a>Notas de versão do Stream Analytics

## <a name="notes-for-06142017-update-of-stream-analytics-tools-for-visual-studio"></a>Observações para atualização de 14/06/2017 das Ferramentas do Azure Stream Analytics para Visual Studio
Esta atualização é para nossas Ferramentas do Visual Studio. Esta versão contém Olá novos recursos a seguir.

| Title | Descrição |
| --- | --- |
| Suporte ao editor de scripts Java |Você pode aproveitar a experiência de editor de script hello java nativo depois de criar seu código java funções de script.|
| Exibir mensagem de erro de tempo de execução do trabalho | Se houver erros de tempo de execução durante a execução do trabalho, pode exibi-los no guia de erros de saudação ajustando a janela de tempo de exibição de saudação. Por padrão, ele mostra mensagens de erro de saudação para os últimos 30 minutos. |
| Suporte a CSV e Avro para entrada de teste local | Além de JSON, agora você pode usar formato de arquivo CSV e Avro para a entrada de teste local.|

## <a name="notes-for-05032017-update-of-stream-analytics"></a>Notas da atualização de 03/05/2017 do Stream Analytics
Esta atualização é para nossa versão de documentação da solução de problemas.

Olá [guia de solução de problemas](stream-analytics-troubleshooting-guide.md) e outros documentos foram liberados. Examine, pois o comentário é bem-vindo.

## <a name="notes-for-04242017-update-of-stream-analytics-tools-for-visual-studio"></a>Observações para atualização de 24/04/2017 das Ferramentas do Azure Stream Analytics para Visual Studio
Esta atualização é para nossas Ferramentas do Visual Studio. Esta versão contém Olá novos recursos a seguir.

| Title | Descrição |
| --- | --- |
| Exibir o resultado do teste local no Visual Studio | tooview Olá saída resultante do hello local de teste, apenas pressione ENTER na janela do console de saída de hello ou fechá-lo. resultado de saudação será mostrado em uma janela no Visual Studio, no formato de tabela. |
| Resultado local de saída no formato JSON | Quando você executa um teste local, resultado hello será gerado como formatos de arquivo CSV e JSON. |
| Visualizar dados de entradas/saídas de armazenamento de Blobs/de tabela | Clicando duas vezes em um armazenamento de blob ou tabela de entrada/saída na exibição de trabalho Olá, você pode visualizar dados hello dentro do Visual Studio facilmente. |
| Exibir mensagem de erro para entradas/saídas | Se houver algum tempo de execução erros tooyou relacionados trabalho entradas ou saídas, ele será mostrado no diagrama de trabalho Olá onde você pode passar nele toosee mensagem de erro detalhada de saudação.|


## <a name="notes-for-02012017-release-of-stream-analytics"></a>Notas de versão de 01/02/2017 do Stream Analytics
Esta versão contém Olá após a atualização.

| Title | Descrição |
| --- | --- |
| Introdução a UDF (Funções definidas pelo usuário) do JavaScript |[As Funções definidas pelo usuário de Java](stream-analytics-javascript-user-defined-functions.md) agora estão disponíveis para proporcionar mais flexibilidade na criação de consultas. |
| Apresentação das ferramentas para Visual Studio e Stream Analytics |[As Ferramentas para Visual Studio](stream-analytics-tools-for-visual-studio.md) agora estão disponíveis para depuração e com mais utilitários. |
| Apresentação do registro em log de diagnóstico |[O Registro em log de diagnóstico](stream-analytics-job-diagnostic-logs.md) agora está disponível para mais opções de solução de problemas. |
| Introdução às Funções Geoespaciais |As [Funções Geoespaciais](http://msdn.microsoft.com/library/mt778980(Azure.100).aspx) agora estão disponíveis para o público geral. |

## <a name="notes-for-04152016-release-of-stream-analytics"></a>Notas de versão de 15/04/2016 do Stream Analytics
Esta versão contém Olá após a atualização.

| Title | Descrição |
| --- | --- |
| Disponibilidade geral para saídas do Power BI |[Saídas do Power BI](stream-analytics-power-bi-dashboard.md) agora estão em disponibilidade geral. expiração de autorização de 90 dias Olá para o Power BI foi removida. Para obter mais informações sobre cenários em que a autorização precisa toobe renovado consulte Olá [renovar autorização](stream-analytics-power-bi-dashboard.md#renew-authorization) seção de criação de um painel do Power BI. |

## <a name="notes-for-03032016-release-of-stream-analytics"></a>Notas de versão de 03/03/2016 do Stream Analytics
Esta versão contém Olá após a atualização.

| Title | Descrição |
| --- | --- |
| Novos itens de linguagem de consulta de Stream Analytics |SAQL agora tem [GetType](https://msdn.microsoft.com/library/azure/mt643890.aspx "GetType MSDN Page"), [TRY_CAST](https://msdn.microsoft.com/library/azure/mt643735.aspx "TRY_CAST MSDN Page") e [REGEXMATCH](https://msdn.microsoft.com/library/azure/mt643891.aspx "REGEXMATCH MSDN Page"). |

## <a name="notes-for-12102015-release-of-stream-analytics"></a>Notas de versão de 10/12/2015 do Stream Analytics
Esta versão contém Olá após a atualização.

| Title | Descrição |
| --- | --- |
| Atualização de versão da API REST |versão da API REST Olá foi atualizada too2015-10-01. Detalhes podem ser encontrados no MSDN em [Referência de API REST do gerenciamento do Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx) e [Integração do Machine Learning ao Stream Analytics](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md). |
| Integração de Azure Machine Learning |Com essa versão, é fornecido suporte para funções definidas pelo usuário do Azure Machine Learning. Consulte Olá [tutorial](stream-analytics-machine-learning-integration-tutorial.md) para mais informações, bem como Olá [comunicado do blog geral](http://blogs.technet.com/b/machinelearning/archive/2015/12/10/apply-azure-ml-as-a-function-in-azure-stream-analytics.aspx). |

## <a name="notes-for-11122015-release-of-stream-analytics"></a>Notas de versão de 12/11/2015 do Stream Analytics
Esta versão contém Olá após a atualização.

| Title | Descrição |
| --- | --- |
| Novo comportamento de SELECT |Selecione no Stream Analytics foi estendido tooallow * como um acessador de propriedade de um registro aninhado. Para obter mais informações, consulte [http://msdn.microsoft.com/library/mt622759.aspx](http://msdn.microsoft.com/library/mt622759.aspx "Tipos de dados complexos"). |

## <a name="notes-for-10222015-release-of-stream-analytics"></a>Notas de versão de 22/10/2015 do Stream Analytics
Esta versão contém Olá atualizações a seguir.

| Title | Descrição |
| --- | --- |
| Recursos adicionais de linguagem de consulta |Análise de fluxo foi expandida a linguagem de consulta hello, incluindo Olá recursos a seguir: [ABS](https://msdn.microsoft.com/library/azure/mt574054.aspx), [CEILING](https://msdn.microsoft.com/library/azure/mt605286.aspx), [EXP](https://msdn.microsoft.com/library/azure/mt605289.aspx), [ANDAR](https://msdn.microsoft.com/library/azure/mt605240.aspx), [POWER](https://msdn.microsoft.com/library/azure/mt605287.aspx), [sinal](https://msdn.microsoft.com/library/azure/mt605290.aspx), [quadrado](https://msdn.microsoft.com/library/azure/mt605288.aspx), e [SQRT](https://msdn.microsoft.com/library/azure/mt605238.aspx). |
| Limitações de agregação removidas |Esta versão remove a limitação de saudação de 15 agregações em uma consulta. Agora, não há nenhum toohello limitar o número de agregações por consulta. |
| Acréscimo do recurso System.Timestamp a GROUP BY |Olá [GROUP BY](https://msdn.microsoft.com/library/azure/dn835023.aspx) função agora permite o window_type ou [timestamp](https://msdn.microsoft.com/library/azure/mt598501.aspx). |
| Acréscimo de OFFSET para janelas com Cascata e Salto |Por padrão, janelas [Em Cascata](https://msdn.microsoft.com/library/azure/dn835055.aspx) e [De Salto](https://msdn.microsoft.com/library/azure/dn835041.aspx) são alinhadas com tempo zero (01/01/0001 12:00:00 AM UTC). Olá novo (opcional) 'offsetsize' permite especificar um deslocamento personalizados (ou alinhamento). |

## <a name="notes-for-09292015-release-of-stream-analytics"></a>Notas de versão de 29/09/2015 do Stream Analytics
Esta versão contém Olá atualizações a seguir.

| Title | Descrição |
| --- | --- |
| Visualização Pública do Azure IoT Suite |Análise de fluxo está incluída no hello visualização pública do hello Azure IoT Suite. |
| Integração no Portal do Azure |Na presença de toocontinued adição no portal de gerenciamento do Azure hello, análise de fluxo é agora integrada Olá [Portal do Azure](https://azure.microsoft.com/overview/preview-portal/). Observe que a funcionalidade do Stream Analytics no portal de visualização de saudação atualmente é que um subconjunto da funcionalidade de saudação oferecidos no portal de gerenciamento do Azure hello, sem suporte para teste de consulta no navegador, que Power BI de saída de configuração e navegação tooor criar um novo recursos de entrada e saídos em assinaturas você tem acesso. |
| Suporte para a saída do Cosmos DB |Trabalhos do Stream Analytics agora podem produzir muito[o banco de dados do Azure Cosmos](https://azure.microsoft.com/services/documentdb/). |
| Suporte para a entrada do Hub IoT |Os trabalhos do Stream Analytics agora podem ingerir dados dos Hubs IoT. |
| TIMESTAMP BY para eventos heterogêneos |Quando um único fluxo de dados contém vários tipos de eventos com carimbos de hora em campos diferentes, você pode agora usar [TIMESTAMP BY](http://msdn.microsoft.com/library/mt573293.aspx) com campos de carimbo de hora diferente de toospecify de expressões para cada caso. |

## <a name="notes-for-09102015-release-of-stream-analytics"></a>Notas de versão de 10/09/2015 do Stream Analytics
Esta versão contém Olá atualizações a seguir.

| Title | Descrição |
| --- | --- |
| Suporte para grupos do PowerBI |tooenable compartilhamento de dados com outros usuários do Power BI, análise de fluxo de trabalhos podem agora gravar muito[PowerBI grupos](stream-analytics-define-outputs.md#power-bi) dentro de sua conta do Power BI. |

## <a name="notes-for-08202015-release-of-stream-analytics"></a>Notas de versão de 20/08/2015 do Stream Analytics
Esta versão contém Olá atualizações a seguir.

| Title | Descrição |
| --- | --- |
| Função LAST adicionada |Olá [último](http://msdn.microsoft.com/library/mt421186.aspx) função agora está disponível em trabalhos do Stream Analytics, permitindo que você tooretrieve evento mais recente do hello em um fluxo de eventos em um determinado período. |
| Novas funções de matriz |As funções de matriz [GetArrayElement](http://msdn.microsoft.com/library/mt270218.aspx), [GetArrayElements](http://msdn.microsoft.com/library/mt298451.aspx) e [GetArrayLength](http://msdn.microsoft.com/library/mt270226.aspx) agora estão disponíveis. |
| Novas funções de registro |As funções de registro [GetRecordProperties](http://msdn.microsoft.com/library/mt270221.aspx) e [GetRecordPropertyValue](http://msdn.microsoft.com/library/mt270220.aspx) agora estão disponíveis. |

## <a name="notes-for-07302015-release-of-stream-analytics"></a>Notas de versão de 30/07/2015 do Stream Analytics
Esta versão contém Olá atualizações a seguir.

| Title | Descrição |
| --- | --- |
| Id da Org Power BI dissociada da Id do Azure |Esse recurso habilita a [saída do Power BI](stream-analytics-power-bi-dashboard.md) para trabalhos de ASA em qualquer tipo de conta do Azure (Live ID ou Org ID). Além disso, você pode ter uma Id da Org para sua conta do Azure e usar uma diferente para autorizar a saída do Power BI. |
| Suporte para saída de filas do barramento de serviço |[Filas do Barramento de Serviço](stream-analytics-define-outputs.md#service-bus-queues) agora estão disponíveis nos trabalhos do Stream Analytics. |
| Suporte para saída de filas de tópicos do Barramento de Serviço |[Tópicos do Barramento de Serviço](stream-analytics-define-outputs.md#service-bus-topics) agora estão disponíveis nos trabalhos do Stream Analytics. |

## <a name="notes-for-07092015-release-of-stream-analytics"></a>Notas de versão de 09/07/2015 do Stream Analytics
Esta versão contém Olá atualizações a seguir.

| Title | Descrição |
| --- | --- |
| Particionamento de saída de blob personalizado |Saídas de armazenamento de blob permitem uma frequência de saudação toospecify opção essa saída blobs são gravados e estrutura de saudação e o formato da saudação estrutura de pasta do caminho de dados de saída. |

## <a name="notes-for-05032015-release-of-stream-analytics"></a>Notas de versão de 03/05/2015 do Stream Analytics
Esta versão contém Olá atualizações a seguir.

| Title | Descrição |
| --- | --- |
| Maior valor máximo aumentado da janela de tolerância inoperante |tamanho máximo Olá Olá janela de tolerância de fora de ordem agora é 59:59 (mm: ss) |
| Formato de saída JSON: linha separada ou matriz |Agora há uma opção na saída tooBlob armazenamento ou Hub de eventos toooutput como uma matriz de objetos JSON ou separar objetos JSON com uma nova linha. |

## <a name="notes-for-04162015-release-of-stream-analytics"></a>Notas de versão de 16/04/2015 do Stream Analytics
| Title | Descrição |
| --- | --- |
| Atraso na configuração da conta de Armazenamento do Azure |Ao criar um trabalho de análise de fluxo em uma região para Olá primeira vez, será possível toocreate solicitada uma nova conta de armazenamento ou especificar uma conta existente para o monitoramento de trabalhos do Stream Analytics nessa região. Vencimento toolatency na configuração de monitoramento, criar outro trabalho de análise de fluxo no hello mesma região dentro de 30 minutos solicitará Olá especificando de uma segunda conta de armazenamento em vez de Mostrar Olá recentemente tiver configurado um no armazenamento de monitoramento de saudação Lista suspensa da conta. tooavoid criando uma conta de armazenamento desnecessária, aguarde 30 minutos depois de criar um trabalho em uma região para Olá primeira vez antes de provisionar trabalhos adicionais nessa região. |
| Atualização de trabalho |Neste momento, análise de fluxo não oferece suporte ao vivo edições toohello definição ou configuração de um trabalho em execução. Em ordem toochange Olá entrada, saída, consulta, escala ou configuração de um trabalho em execução, você deve parar trabalho hello. |
| Tipos de dados inferidos da fonte de entrada |Se uma instrução CREATE TABLE não for usada, o tipo de entrada hello é derivado do formato de entrada, por exemplo, todos os campos de CSV são cadeia de caracteres. Campos necessidade toobe explicitamente convertido tipo certo de toohello usando uma função de CONVERSÃO de saudação em erros de incompatibilidade de tipo de tooavoid de ordem. |
| Os campos ausentes são enviados como valores nulos |Fazendo referência a um campo que não está presente na fonte de entrada hello resultará em valores nulos no evento de saída de hello. |
| As instruções WITH devem preceder as instruções SELECT |Na consulta, as instruções SELECT devem seguir subconsultas definidas em instruções WITH. |
| Problema de memória insuficiente |Reiniciar trabalhos de análise de fluxo com uma grande tolerância para eventos fora de ordem e/ou manter que uma grande quantidade de estado pode causar Olá toorun de trabalho da memória, resultando em um trabalho de consultas complexas. Olá iniciar e parar operações ficarão visíveis nos logs de operação do trabalho hello. tooavoid esse comportamento, a consulta de saudação de escala fora por várias partições. Em uma versão futura, essa limitação será tratada por meio da redução do desempenho nos trabalhos afetados em vez de reiniciá-los. |
| Grandes entradas de blob sem carimbo de data/hora de carga podem causar o problema de memória insuficiente |Consumindo grandes arquivos do armazenamento de Blob pode causar toocrash de trabalhos do Stream Analytics, se um campo de carimbo de hora não for especificado por meio de TIMESTAMP BY. tooavoid esse problema, manter cada blob abaixo de 10MB de tamanho. |
| Limitação de volume de eventos de Banco de Dados SQL |Ao usar o banco de dados SQL como um destino de saída, muito grandes volumes de dados de saída podem causar tootime de trabalho do Stream Analytics Olá out. tooresolve esse problema, ou reduzir o volume de saída de hello usando agregações ou operadores de filtro, ou escolha o armazenamento de BLOBs do Azure ou Hubs de evento como um destino de saída. |
| Os conjuntos de dados do PowerBI só podem conter uma tabela |O PowerBI não oferece suporte a mais de uma tabela em um determinado conjunto de dados. |

## <a name="get-help"></a>Obter ajuda
Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
