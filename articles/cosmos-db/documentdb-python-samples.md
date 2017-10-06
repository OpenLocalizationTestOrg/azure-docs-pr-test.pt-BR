---
title: exemplos de Python aaaDocumentDB API para o banco de dados do Azure Cosmos | Microsoft Docs
description: "Encontre exemplos do Python no GitHub para tarefas comuns no Azure Cosmos DB, incluindo operações CRUD."
keywords: Exemplos do Python
services: cosmos-db
author: moderakh
manager: jhubbard
editor: monicar
documentationcenter: python
ms.assetid: 7f4f8db3-e9db-4645-92ef-7819d486a349
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2016
ms.author: moderakh
ms.openlocfilehash: d8f240782b0997f2d32b68d310dc6f4ff6cb36d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-examples"></a>Exemplos do Python no Azure Cosmos DB
> [!div class="op_single_selector"]
> * [Exemplos do .NET](documentdb-dotnet-samples.md)
> * [Exemplos do Node.js](documentdb-nodejs-samples.md)
> * [Exemplos do Python](documentdb-python-samples.md)
> * [Galeria de Exemplos de Código do Azure](https://azure.microsoft.com/documentation/samples/?service=documentdb)
> 
> 

Soluções de exemplo que executam operações CRUD e outras operações comuns no banco de dados do Azure Cosmos recursos estão incluídas no hello [azure-documentdb-python](https://github.com/Azure/azure-documentdb-python/tree/master/samples) repositório GitHub. Esse artigo fornece:

* Tarefas de toohello links em cada um dos arquivos de projeto de exemplo hello Python. 
* Toohello links relacionados ao conteúdo de referência de API.

**Pré-requisitos**

1. É necessário uma conta do Azure toouse esses exemplos de Python:
   * Você pode [abrir uma conta do Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/): você obtém créditos você pode usar tootry out paga serviços do Azure e mesmo depois que eles são usados até você pode manter a conta de saudação e usar serviços do Azure, como sites de livre. Seu cartão de crédito nunca será cobrado a menos que você explicitamente alterar suas configurações e pergunte toobe cobrado.
     * É possível [ativar os benefícios para assinantes do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/): todos os meses, sua assinatura do Visual Studio concede créditos que podem ser usados para experimentar serviços pagos do Azure.
2. Você também precisa Olá [SDK de Python](documentdb-sdk-python.md). 
   
   > [!NOTE]
   > Cada exemplo é independente, eles se configuram e fazem a limpeza sozinhos. Como tal, exemplos de saudação emitem várias chamadas muito[document_client. CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html). Cada vez que isso é feito sua assinatura será cobrada por 1 hora de uso de cada nível de desempenho de saudação da coleção hello está sendo criada. 
   > 
   > 

## <a name="database-examples"></a>Exemplos de banco de dados
Olá [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement/Program.py) arquivo hello [DatabaseManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement) projeto mostra como as tarefas de saudação tooperform a seguir.

| Tarefa | Referência de API |
| --- | --- |
| [Criar um banco de dados](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L65-L76) |[document_client.CreateDatabase](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [Consultar uma conta para um banco de dados](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L49-L62) |[document_client.QueryDatabases](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [Ler um banco de dados por ID](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L79-L96) |[document_client.ReadDatabase](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [Listar bancos de dados para uma conta](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L99-L110) |[document_client.ReadDatabases](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [Excluir um banco de dados](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L113-L126) |[document_client.DeleteDatabase](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |

## <a name="collection-examples"></a>Exemplos de coleção
Olá [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement/Program.py) arquivo hello [CollectionManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement) projeto mostra como as tarefas de saudação tooperform a seguir.

| Tarefa | Referência de API |
| --- | --- |
| [Criar uma coleção](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L84-L135) |[document_client.CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Ler uma lista de todas as coleções em um banco de dados](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L198-L225) |[document_client.ListCollections](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Obter uma coleção por ID](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L178-L195) |[document_client.ReadCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Obter o nível de desempenho de uma coleção](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L139-L161) |[DocumentQueryable.QueryOffers](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Alterar o nível de desempenho de uma coleção](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L163-L175) |[document_client.ReplaceOffer](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Excluir uma coleção](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L212-L225) |[document_client.DeleteCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |

