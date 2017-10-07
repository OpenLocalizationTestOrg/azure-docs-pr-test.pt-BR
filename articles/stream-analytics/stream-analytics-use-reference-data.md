---
title: "tabelas de pesquisa e dados de referência de aaaUse no Stream Analytics | Microsoft Docs"
description: "Usar dados de referência em uma consulta do Stream Analytics"
keywords: "tabela de pesquisa, dados de referência"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 06103be5-553a-4da1-8a8d-3be9ca2aff54
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: fb1d18fba920db5e097d0c95d333e8e8390d1589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-reference-data-or-lookup-tables-in-a-stream-analytics-input-stream"></a>Usando dados de referência e tabelas de pesquisa em um fluxo de entrada do Stream Analytics
Dados de referência (também conhecido como uma tabela de pesquisa) são um conjunto finito de dados estáticos ou redução de alteração por natureza, usado tooperform uma pesquisa ou toocorrelate com o fluxo de dados. use toomake de dados de referência em seu trabalho do Stream Analytics do Azure, você geralmente usará um [Join de dados de referência](https://msdn.microsoft.com/library/azure/dn949258.aspx) em sua consulta. Análise de fluxo usa o armazenamento de BLOBs do Azure como camada de armazenamento Olá para dados de referência e com a referência do Azure Data Factory dados podem ser transformados e/ou copiados tooAzure armazenamento de Blob, para uso como dados de referência de [qualquer número de baseado em nuvem e armazenamentos de dados local](../data-factory/data-factory-data-movement-activities.md). Dados de referência são modelados como uma sequência de blobs (definido na configuração de entrada hello) em ordem crescente de saudação especificada no nome do blob de saudação de data/hora. Ele **somente** dá suporte à adição toohello final da sequência de saudação usando um valor de data/hora **maior** de Olá especificado pelo último blob de saudação na sequência de saudação.

Análise de fluxo tem um **limite de 100 MB por blob** mas trabalhos podem processar vários blobs de referência usando Olá **padrão de caminho** propriedade.


## <a name="configuring-reference-data"></a>Configurando os dados de referência
tooconfigure seus dados de referência, é necessário primeiro toocreate uma entrada que é do tipo **dados de referência**. tabela de saudação abaixo explica cada propriedade que você precisará tooprovide ao criar a entrada de dados de referência de saudação com sua descrição:


<table>
<tbody>
<tr>
<td>Nome da Propriedade</td>
<td>Descrição</td>
</tr>
<tr>
<td>Alias de entrada</td>
<td>Um nome amigável que será usado na Olá trabalho consulta tooreference entrada.</td>
</tr>
<tr>
<td>Conta de armazenamento</td>
<td>nome de Olá Olá da conta de armazenamento onde se encontram seus blobs. Se ele estiver no hello mesma assinatura que o trabalho do Stream Analytics, selecione-a na lista suspensa hello.</td>
</tr>
<tr>
<td>Chave da conta de armazenamento</td>
<td>chave de segredo do Hello associado à conta de armazenamento hello. Isso é preenchido automaticamente se conta de armazenamento Olá estiver em Olá mesma assinatura que o trabalho do Stream Analytics.</td>
</tr>
<tr>
<td>Contêiner de armazenamento</td>
<td>Os contêineres fornecem um agrupamento lógico para os blobs armazenados no hello serviço Blob do Microsoft Azure. Quando você carregar um blob de toohello serviço Blob, você deve especificar um contêiner de blob.</td>
</tr>
<tr>
<td>Padrão de caminho</td>
<td>caminho de saudação usado toolocate seus blobs dentro do contêiner especificado hello. No caminho hello, você pode escolher toospecify uma ou mais instâncias de saudação 2 variáveis a seguir:<BR>{data}, {hora}<BR>Exemplo 1: products/{data}/{hora}/product-list.csv<BR>Exemplo 2: products/{data}/product-list.csv
</tr>
<tr>
<td>Formato de data [opcional]</td>
<td>Se você tiver usado o {date} dentro de saudação padrão de caminho que você especificou, você pode selecionar o formato de data de saudação na qual seus blobs são organizados de saudação lista suspensa de formatos com suporte.<BR>Exemplo: AAAA/MM/DD, MM/DD/AAAA etc.</td>
</tr>
<tr>
<td>Formato de hora [opcional]</td>
<td>Se você tiver usado o {time} dentro de saudação padrão de caminho que você especificou, você pode selecionar o formato de hora Olá na qual seus blobs são organizados de saudação lista suspensa de formatos com suporte.<BR>Exemplo: HH, HH/mm ou HH-mm</td>
</tr>
<tr>
<td>Formato de serialização do evento</td>
<td>toomake que suas consultas funcionem de maneira Olá esperada, o Stream Analytics precisa tooknow qual formato de serialização que você está usando para fluxos de dados de entrada. Para dados de referência, formatos de saudação com suporte são CSV e JSON.</td>
</tr>
<tr>
<td>Codificação</td>
<td>UTF-8 é Olá somente suporte para formato de codificação no momento</td>
</tr>
</tbody>
</table>

## <a name="generating-reference-data-on-a-schedule"></a>Gerar dados de referência em uma agenda
Se seus dados de referência são um conjunto de dados de alteração lenta, suporte à atualização de dados de referência é habilitado especificando um padrão de caminho na configuração de entrada hello usando Olá {date} e tokens de substituição {time}. Análise de fluxo seleciona definições de dados de referência Olá atualizada com base nesse padrão de caminho. Por exemplo, um padrão de `sample/{date}/{time}/products.csv` com um formato de data **"Aaaa-MM-DD"** e um formato de hora **"HH-mm"** instrui o Stream Analytics toopick o blob Olá atualizado `sample/2015-04-16/17-30/products.csv` em 5:30 PM em abril 16, fuso horário de UTC 2015.

> [!NOTE]
> No momento trabalhos do Stream Analytics procure atualização de blob Olá somente quando o tempo de máquina de saudação adianta a hora de toohello codificada em nome do blob hello. Por exemplo, o trabalho de saudação irá procurar `sample/2015-04-16/17-30/products.csv` assim que possível, mas não antes de 5:30 PM em 16 de abril de 2015 UTC fuso horário. Ele irá *nunca* procure um blob com um tempo codificado anteriores ao Olá um último que foi descoberto.
> 
> Por exemplo Depois que o trabalho Olá localiza blob Olá `sample/2015-04-16/17-30/products.csv` ele ignorará todos os arquivos com uma data codificado anterior 5:30 PM em 16 de abril de 2015 se um chegada tardia `sample/2015-04-16/17-25/products.csv` blob é criado no hello mesmo trabalho de saudação do contêiner não utilizá-lo.
> 
> Da mesma forma se `sample/2015-04-16/17-30/products.csv` só será produzido em 10:03 PM em 16 de abril de 2015, mas nenhum blob com uma data anterior está presente no contêiner hello, trabalho Olá usará esse arquivo começando em 10:03 PM em 16 de abril de 2015 e usar dados de referência anterior Olá até lá.
> 
> Toothis uma exceção é quando o trabalho Olá precisa toore processar dados de volta no tempo ou quando o trabalho de saudação é iniciado pela primeira vez. No início do trabalho de tempo de saudação está procurando blob mais recente do hello produzido antes que o trabalho de saudação hora de início especificada. Isso é feito tooensure que há um **não vazio** referência de conjunto de dados quando Olá trabalho é iniciado. Se não pode ser encontrado, o trabalho Olá exibe Olá diagnóstico a seguir: `Initializing input without a valid reference data blob for UTC time <start time>`.
> 
> 

[O Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) pode ser usado tooorchestrate Olá tarefa de criação de blobs Olá atualizado exigidos pelas definições de dados de referência do Stream Analytics tooupdate. Fábrica de dados é um serviço de integração de dados com base em nuvem que orquestra e automatiza a movimentação de saudação e transformação de dados. Fábrica de dados oferece suporte a [tooa grande número de baseado em nuvem e repositórios de dados em locais de conexão](../data-factory/data-factory-data-movement-activities.md) e movimentação de dados facilmente em um agendamento regular que você especificar. Para obter mais informações e instruções passo a passo sobre como tooset a uma fábrica de dados pipeline toogenerate dados de referência para análise de fluxo que é atualizada em um cronograma predefinido, confira este [GitHub exemplo](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs).

## <a name="tips-on-refreshing-your-reference-data"></a>Dicas sobre como atualizar seus dados de referência
1. Substituição blobs de dados de referência não causará Stream Analytics tooreload Olá blob e em alguns casos, isso poderá causar Olá toofail de trabalho. Olá recomendado dados de referência do modo toochange é tooadd um novo blob usando Olá mesmo padrão de contêiner e o caminho definido na entrada de trabalho hello e usam um valor de data/hora **maior** de Olá especificado pelo último blob de saudação na sequência de saudação.
2. Blobs de dados de referência são **não** ordenadas por hora da "Última modificação" hello blob, mas somente pelo tempo de saudação e a data especificada no nome do blob hello usando Olá {date} e substituições de {time}.
3. Em algumas ocasiões um trabalho deve voltar no tempo, portanto, blobs de dados de referência não devem ser alterados ou excluídos.

## <a name="get-help"></a>Obter ajuda
Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas
Foi introduzido tooStream Analytics, um serviço gerenciado para streaming de análise de dados de saudação Internet das coisas. toolearn mais informações sobre esse serviço, consulte:

* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.get.started]: stream-analytics-get-started.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
