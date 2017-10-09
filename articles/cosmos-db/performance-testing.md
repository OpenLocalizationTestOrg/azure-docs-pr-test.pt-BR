---
title: aaaAzure Cosmos DB escala e o teste de desempenho | Microsoft Docs
description: Saiba como tooperform dimensionar e teste de desempenho com o banco de dados do Azure Cosmos
keywords: testes de desempenho
services: cosmos-db
author: arramac
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f4c96ebd-f53c-427d-a500-3f28fe7b11d0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: arramac
ms.openlocfilehash: 46d1217e11a39ee970a868de9a5c5dfcf52cedf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a>Teste de desempenho e escala com o Azure Cosmos DB
O teste de desempenho e escalabilidade é uma etapa importante no desenvolvimento de aplicativos. Para muitos aplicativos, a camada de banco de dados de saudação tem um impacto significativo hello desempenho e escalabilidade, e é, portanto, um componente crítico de desempenho de teste. O [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) foi desenvolvido para fins de escala elástica e desempenho previsível e, portanto, é uma excelente opção para aplicativos que precisam de uma camada de banco de dados de alto desempenho. 

Este artigo é uma referência para desenvolvedores que implementam conjuntos de testes de desempenho para suas cargas de trabalho do Cosmos DB ou que avaliam o Cosmos DB para cenários de aplicativos de alto desempenho. Ele se concentra principalmente nos testes de desempenho isolado do banco de dados hello, mas também inclui as práticas recomendadas para aplicativos de produção.

Depois de ler este artigo, você será capaz de tooanswer Olá perguntas a seguir:   

* Onde posso encontrar um aplicativo cliente do .NET de exemplo para testar o desempenho do Azure Cosmos DB? 
* Como fazer para obter altos níveis de produtividade com o Azure Cosmos DB em meu aplicativo cliente?

tooget iniciada com o código, baixe o projeto de saudação do [exemplo de teste de desempenho do Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark). 

> [!NOTE]
> meta de saudação do aplicativo é toodemonstrate práticas recomendadas para a extração de melhor desempenho do banco de dados do Cosmos com um pequeno número de computadores cliente. Isso não foi feito toodemonstrate capacidade de pico de saudação do serviço de saudação, que pode ser dimensionado limitlessly.
> 
> 

Se você estiver procurando por opções de configuração do cliente tooimprove Cosmos banco de dados de desempenho, consulte [dicas de desempenho do banco de dados do Azure Cosmos](performance-tips.md).

## <a name="run-hello-performance-testing-application"></a>Execute o aplicativo de teste de desempenho de saudação
Olá tooget de maneira mais rápida iniciado é toocompile e Olá execução de .NET de exemplo abaixo, conforme descrito nas etapas de saudação abaixo. Você pode também examinar código-fonte hello e implementar aplicativos de cliente próprio de tooyour configurações semelhantes.

**Etapa 1:** Download Olá Proje [exemplo de teste de desempenho do Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), ou o repositório do GitHub Olá bifurcação.

**Etapa 2:** modificar as configurações de saudação para EndpointUrl, AuthorizationKey, CollectionThroughput e DocumentTemplate (opcional) no App. config.

> [!NOTE]
> Antes de provisionar coleções com alta taxa de transferência, consulte toohello [página de preços](https://azure.microsoft.com/pricing/details/cosmos-db/) custos de saudação tooestimate por coleção. Banco de dados do Azure Cosmos cobra armazenamento e a taxa de transferência de forma independente em uma base por hora, então você pode salvar os custos excluindo ou diminuir a taxa de transferência de saudação de suas coleções de banco de dados do Azure Cosmos após o teste.
> 
> 

**Etapa 3:** compilar e executar o aplicativo de console Olá da linha de comando hello. Você deve ver a saída como Olá seguinte:

    Summary:
    ---------------------------------------------------------------------
    Endpoint: https://docdb-scale-demo.documents.azure.com:443/
    Collection : db.testdata at 50000 request units per second
    Document Template*: Player.json
    Degree of parallelism*: 500
    ---------------------------------------------------------------------

    DocumentDBBenchmark starting...
    Creating database db
    Creating collection testdata
    Creating metric collection metrics
    Retrying after sleeping for 00:03:34.1720000
    Starting Inserts with 500 tasks
    Inserted 661 docs @ 656 writes/s, 6860 RU/s (18B max monthly 1KB reads)
    Inserted 6505 docs @ 2668 writes/s, 27962 RU/s (72B max monthly 1KB reads)
    Inserted 11756 docs @ 3240 writes/s, 33957 RU/s (88B max monthly 1KB reads)
    Inserted 17076 docs @ 3590 writes/s, 37627 RU/s (98B max monthly 1KB reads)
    Inserted 22106 docs @ 3748 writes/s, 39281 RU/s (102B max monthly 1KB reads)
    Inserted 28430 docs @ 3902 writes/s, 40897 RU/s (106B max monthly 1KB reads)
    Inserted 33492 docs @ 3928 writes/s, 41168 RU/s (107B max monthly 1KB reads)
    Inserted 38392 docs @ 3963 writes/s, 41528 RU/s (108B max monthly 1KB reads)
    Inserted 43371 docs @ 4012 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 48477 docs @ 4035 writes/s, 42282 RU/s (110B max monthly 1KB reads)
    Inserted 53845 docs @ 4088 writes/s, 42845 RU/s (111B max monthly 1KB reads)
    Inserted 59267 docs @ 4138 writes/s, 43364 RU/s (112B max monthly 1KB reads)
    Inserted 64703 docs @ 4197 writes/s, 43981 RU/s (114B max monthly 1KB reads)
    Inserted 70428 docs @ 4216 writes/s, 44181 RU/s (115B max monthly 1KB reads)
    Inserted 75868 docs @ 4247 writes/s, 44505 RU/s (115B max monthly 1KB reads)
    Inserted 81571 docs @ 4280 writes/s, 44852 RU/s (116B max monthly 1KB reads)
    Inserted 86271 docs @ 4273 writes/s, 44783 RU/s (116B max monthly 1KB reads)
    Inserted 91993 docs @ 4299 writes/s, 45056 RU/s (117B max monthly 1KB reads)
    Inserted 97469 docs @ 4292 writes/s, 44984 RU/s (117B max monthly 1KB reads)
    Inserted 99736 docs @ 4192 writes/s, 43930 RU/s (114B max monthly 1KB reads)
    Inserted 99997 docs @ 4013 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 100000 docs @ 3846 writes/s, 40304 RU/s (104B max monthly 1KB reads)

    Summary:
    ---------------------------------------------------------------------
    Inserted 100000 docs @ 3834 writes/s, 40180 RU/s (104B max monthly 1KB reads)
    ---------------------------------------------------------------------
    DocumentDBBenchmark completed successfully.


**Etapa 4 (se necessário):** Olá taxa de transferência relatada (RU/s) da ferramenta Olá deve ser Olá mesmo ou maior que a taxa de transferência fornecida da coleção Olá Olá. Caso contrário, aumentando Olá DegreeOfParallelism em pequenos incrementos pode ajudá-lo a atingir o limite de saudação. Se plateaus a taxa de transferência de saudação do seu aplicativo cliente, iniciar várias instâncias do aplicativo hello em Olá mesmo ou computadores diferentes, ajudará você a atingir o limite de saudação provisionada em Olá instâncias diferentes. Se você precisar de ajuda com essa etapa, escreva um email tooaskcosmosdb@microsoft.com ou emitir um ticket de suporte de saudação [Portal do Azure](https://portal.azure.com).

Uma vez que o aplicativo hello em execução, você pode tentar diferentes [políticas de indexação](indexing-policies.md) e [níveis de consistência](consistency-levels.md) toounderstand seu impacto na taxa de transferência e latência. Também pode examinar o código-fonte hello e implementar aplicativos de produção ou de conjuntos de testes próprio de tooyour de configurações semelhantes.

## <a name="next-steps"></a>Próximas etapas
Neste artigo, analisamos como você pode realizar testes de desempenho e escala com o Cosmos DB usando um aplicativo de console .NET. Consulte toohello links abaixo para obter informações adicionais sobre como trabalhar com o banco de dados do Azure Cosmos.

* [Amostra de teste de desempenho do Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [Tooimprove de opções de configuração do cliente desempenho de banco de dados do Azure Cosmos](performance-tips.md)
* [Particionamento do lado do servidor no Azure Cosmos DB](partition-data.md)


