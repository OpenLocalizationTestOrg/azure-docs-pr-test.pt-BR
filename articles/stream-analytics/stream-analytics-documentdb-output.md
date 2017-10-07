---
title: "saída de aaaJSON para análise de fluxo | Microsoft Docs"
description: "Saiba como o Stream Analytics pode direcionar o Azure Cosmos DB para uma saída em JSON, para arquivamento de dados e consultas de baixa latência em dados JSON não estruturados."
keywords: "Saída em JSON"
documentationcenter: 
services: stream-analytics,documentdb
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 5d2a61a6-0dbf-4f1b-80af-60a80eb25dd1
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: fa717818c839ecd7a60fcee33d22011990fd5878
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="target-azure-cosmos-db-for-json-output-from-stream-analytics"></a>Direcionar o Azure Cosmos DB para uma saída em JSON no Stream Analytics
O Stream Analytics pode direcionar o [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) para uma saída em JSON, possibilitando o arquivamento de dados e consultas de baixa latência em dados JSON não estruturados. Este documento aborda algumas práticas recomendadas para implementar essa configuração.

Para aqueles que não estão familiarizados com o banco de dados do Cosmos, dê uma olhada [de aprendizado do Azure Cosmos DB](https://azure.microsoft.com/documentation/learning-paths/documentdb/) tooget iniciado. 

Observação: atualmente, não há suporte para coleções do Cosmos DB baseados na API do Mongo DB. 

## <a name="basics-of-cosmos-db-as-an-output-target"></a>Conceitos básicos do Cosmos DB como um destino de saída
Hello Azure Cosmos DB saída no Stream Analytics permite gravar seu fluxo de processamento de resultados como saída JSON em seu banco de dados do Cosmos collection(s). Análise de fluxo não criar coleções no banco de dados, em vez disso, exigindo que você toocreate-los antecipadamente. Isso é para que os custos de cobrança de saudação de coleções de banco de dados do Cosmos são tooyou transparente e para que você pode ajustar o desempenho de hello, consistência e a capacidade de suas coleções diretamente usando Olá [Cosmos DB APIs](https://msdn.microsoft.com/library/azure/dn781481.aspx). É recomendável usar um banco de dados DB Cosmos por fluxo de trabalho separado de toologically suas coleções para um trabalho de streaming.

Algumas das opções de coleção de banco de dados do Cosmos Olá são detalhadas abaixo.

## <a name="tune-consistency-availability-and-latency"></a>Ajustar a consistência, a disponibilidade e a latência
toomatch seus requisitos de aplicativo, banco de dados do Cosmos permite banco de dados do toofine ajustar hello e coleções e verifique prós e contras latência, a disponibilidade e a consistência. Dependendo dos níveis de consistência de leitura exigidos pelo seu cenário em relação à latência de leitura e de gravação, você poderá escolher um nível de consistência em sua conta de banco de dados. Também por padrão, DB Cosmos permite a indexação síncrona em cada coleção de tooyour operações CRUD. Isso é Olá toocontrol de outra opção útil desempenho no banco de dados do Cosmos de leitura/gravação. Para obter mais informações sobre este tópico, revise Olá [alterar os níveis de consistência do banco de dados e consulta](../documentdb/documentdb-consistency-levels.md) artigo.

## <a name="upserts-from-stream-analytics"></a>Inserções e atualizações a partir do Stream Analytics
Integração de análise de fluxo com o banco de dados do Cosmos permite tooinsert ou atualizar registros na sua coleção de banco de dados do Cosmos com base em uma determinada coluna de ID do documento. Isso também é chamado de tooas um *Upsert*.

Análise de fluxo utiliza uma abordagem Upsert otimista, onde as atualizações são realizadas somente quando insert falha devido a conflito de ID do documento tooa. Essa atualização é executada pela análise de fluxo como um PATCH, para que ele permite que o documento de toohello atualizações parciais, ou seja, a adição de novas propriedades ou substituindo que uma propriedade existente é executada de forma incremental. Observe que as alterações nos valores de saudação de propriedades de matriz no documento JSON resultarem em todo o array Olá obtendo substituído, ou seja, a matriz Olá não será mesclada.

## <a name="data-partitioning-in-cosmos-db"></a>Particionamento de dados no Cosmos DB
Cosmos DB [particionada coleções](../cosmos-db/partition-data.md) são Olá recomendado abordagem para particionar seus dados. 

Para coleções de banco de dados do Cosmos único, análise de fluxo ainda permite que você toopartition seus dados com base em padrões de consulta hello e necessidades de desempenho do seu aplicativo. Cada uma coleção pode conter o too10GB de dados (máximo) e atualmente que não há nenhuma maneira tooscale backup (ou estouro). Para dimensionar, o Stream Analytics permite toowrite toomultiple coleções com um prefixo especificado (consulte os detalhes de uso abaixo). Olá consistente o Stream Analytics usa [Hash partição resolvedor](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.partitioning.hashpartitionresolver.aspx) estratégia baseada em usuário Olá fornecido PartitionKey coluna toopartition seus registros de saída. Olá número de coleções com hello fornecido prefixo na hora de início do trabalho de streaming de saudação é usado como contagem de partições de saída de hello, trabalho de saudação toowhich grava tooin paralelo (coleções de banco de dados do Cosmos = partições de saída). Para uma coleção individual com indexação lenta que realiza apenas inserções, é possível esperar uma produtividade de gravação de cerca de 0,4 MB/s. Usando várias coleções pode permitir que você tooachieve maior taxa de transferência e o aumento da capacidade.

Se você pretende tooincrease Olá a contagem de partição no hello futuras, talvez seja necessário toostop seu trabalho, reparticionar Olá dados de suas coleções existentes novas coleções e, em seguida, trabalho de análise de fluxo de saudação reinicialização. Incluiremos mais detalhes sobre como usar PartitionResolver e o novo particionamento, junto com um exemplo de código, em uma próxima postagem. artigo Olá [particionamento e escala no banco de dados do Cosmos](../documentdb/documentdb-partition-data.md) também fornece detalhes sobre isso.

## <a name="cosmos-db-settings-for-json-output"></a>Configurações do Cosmos DB para saída em JSON
A criação do Cosmos DB como uma saída no Stream Analytics gera uma solicitação de informações, conforme mostrado abaixo. Esta seção fornece uma explicação da definição de propriedades de saudação.

Coleção particionada | Várias coleções de “partição única”
---|---
![tela de saída do stream analytics do banco de dados de documentos](media/stream-analytics-documentdb-output/stream-analytics-documentdb-output-1.png) |  ![tela de saída do stream analytics do banco de dados de documentos](media/stream-analytics-documentdb-output/stream-analytics-documentdb-output-2.png)


  
> [!NOTE]
> Olá **várias coleções de "Única partição"** cenário requer uma chave de partição e é uma configuração com suporte. 

* **Alias de saída** – um toorefer alias esta saída em sua consulta ASA  
* **O nome da conta** – nome hello ou ponto de extremidade URI da saudação conta de banco de dados do Cosmos.  
* **Chave de conta** – chave de acesso compartilhado Olá para Olá conta de banco de dados do Cosmos.  
* **Banco de dados** – nome de banco de dados do banco de dados do Cosmos hello.  
* **Padrão de nome** – nome da coleção hello ou seu padrão para Olá coleções toobe usado. formato de nome de coleção Olá pode ser construído usando o token {partition} opcional de hello, onde as partições começam do 0. A seguir estão as entradas válidas de exemplo:  
  1\) MyCollection – uma coleção denominada “MyCollection” deve existir.  
  2\) MyCollection{partition} – estas coleções devem existir – "MyCollection0”, “MyCollection1”, “MyCollection2” e assim por diante.  
* **Chave de Partição** — opcional. Isso só será necessário se você estiver usando um token {partition} no seu padrão de nome de coleção. nome de saudação do campo de saudação na saída eventos usados toospecify Olá chave para particionamento de saída por coleções. Para uma saída de coleção única, nenhuma coluna de saída arbitrária pode ser usada, por exemplo, PartitionId.  
* **ID do Documento** : opcional. nome de saudação do campo Olá em eventos de saída usado chave primária de saudação toospecify nas quais insert ou update operações são baseadas.  
