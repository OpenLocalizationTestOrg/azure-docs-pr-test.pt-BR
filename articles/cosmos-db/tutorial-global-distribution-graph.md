---
title: "tutorial de distribuição global de banco de dados do Cosmos aaaAzure API do Graph | Microsoft Docs"
description: "Saiba como distribuição global usando o banco de dados do Azure Cosmos toosetup Olá API do Graph."
services: cosmos-db
keywords: "distribuição global, graph, gremlin"
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: 1629a31e12a18079f63e07c4909862b36b5f4c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-graph-api"></a>Como a distribuição global usando o banco de dados do Azure Cosmos toosetup Olá API do Graph

Neste artigo, mostramos como toouse Olá distribuição global do banco de dados do Azure Cosmos toosetup portal do Azure e, em seguida, conecte-se usando Olá Graph API (visualização).

Este artigo aborda Olá tarefas a seguir: 

> [!div class="checklist"]
> * Configurar a distribuição global usando Olá portal do Azure
> * Configurar a distribuição global usando Olá [Graph APIs](graph-introduction.md) (visualização)

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-graph-api-using-hello-net-sdk"></a>Conectar-se a região preferida tooa usando a API do Graph do hello usando Olá SDK .NET

Olá Graph API é exposta como uma biblioteca de extensões sobre Olá SDK do DocumentDB.

Em ordem tootake aproveitar [distribuição global](distribute-data-globally.md), aplicativos cliente podem especificar Olá ordenados lista de preferência de regiões toobe usada tooperform operações de documento. Isso pode ser feito definindo a diretiva de conexão hello. Com base na configuração de conta do banco de dados do Azure Cosmos hello, disponibilidade regional atual e a lista de preferência de saudação especificado, Olá ponto de extremidade mais ideal será escolhido por gravação de tooperform SDK hello e operações de leitura.

Esta lista de preferência é especificada durante a inicialização de uma conexão usando Olá SDKs. Olá SDKs aceitar um parâmetro opcional "PreferredLocations" que é uma lista ordenada de regiões do Azure.

* **Grava**: Olá SDK enviará automaticamente todas as gravações toohello região de gravação atual.
* **Lê**: todas as leituras serão enviadas toohello primeira região disponível na lista de PreferredLocations hello. Se Olá solicitação falhar, o cliente Olá falhar para baixo próxima região do hello lista toohello e assim por diante. Olá SDKs somente tentará tooread de regiões de saudação especificado em PreferredLocations. Assim, por exemplo, se Olá conta Cosmos DB está disponível em três regiões, mas somente cliente Olá especifica duas regiões de gravação não Olá para PreferredLocations, em seguida, nenhuma leitura será servida fora da região de gravação hello, mesmo no caso de saudação de failover.

aplicativo Hello pode verificar o ponto de extremidade de gravação atual Olá e ler escolhido pelo Olá SDK pela verificação duas propriedades, WriteEndpoint e ReadEndpoint, disponível no SDK versão 1.8 e acima do ponto de extremidade. Se Olá PreferredLocations propriedade não for definida, todas as solicitações serão atendidas a partir de região de gravação atual hello.

### <a name="using-hello-sdk"></a>Usando Olá SDK

Por exemplo, Olá .NET SDK, Olá `ConnectionPolicy` parâmetro hello `DocumentClient` construtor tem uma propriedade chamada `PreferredLocations`. Essa propriedade pode ser definida tooa lista de nomes de região. nomes de exibição Olá para [regiões do Azure] [ regions] pode ser especificado como parte de `PreferredLocations`.

> [!NOTE]
> Olá URLs para pontos de extremidade de saudação não devem ser consideradas como constantes e longa duração. serviço de saudação pode atualizar essas a qualquer momento. Olá SDK manipula essa alteração automaticamente.
>
>

```cs
// Getting endpoints from application settings or other configuration location
Uri accountEndPoint = new Uri(Properties.Settings.Default.GlobalDatabaseUri);
string accountKey = Properties.Settings.Default.GlobalDatabaseKey;

ConnectionPolicy connectionPolicy = new ConnectionPolicy();

//Setting read region selection preference
connectionPolicy.PreferredLocations.Add(LocationNames.WestUS); // first preference
connectionPolicy.PreferredLocations.Add(LocationNames.EastUS); // second preference
connectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope); // third preference

// initialize connection
DocumentClient docClient = new DocumentClient(
    accountEndPoint,
    accountKey,
    connectionPolicy);

// connect tooAzure Cosmos DB
await docClient.OpenAsync().ConfigureAwait(false);
```

Assim, concluímos este tutorial. Você pode aprender como toomanage Olá consistência da sua conta global replicada lendo [níveis de consistência no banco de dados do Azure Cosmos](consistency-levels.md). E para saber mais sobre como a replicação de banco de dados global funciona no Azure Cosmos DB, veja [Distribuir dados globalmente com o Azure Cosmos DB](distribute-data-globally.md).

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você fez a seguir hello:

> [!div class="checklist"]
> * Configurar a distribuição global usando Olá portal do Azure
> * Configurar a distribuição global usando Olá APIs do DocumentDB

Você pode continuar toolearn tutorial do próximo toohello como toodevelop localmente usando Olá emulador local do banco de dados do Azure Cosmos.

> [!div class="nextstepaction"]
> [Desenvolva localmente com o emulador de saudação](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

