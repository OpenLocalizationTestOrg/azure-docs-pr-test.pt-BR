---
title: "tutorial de distribuição global aaaAzure Cosmos DB para a tabela de API | Microsoft Docs"
description: "Saiba como distribuição global usando o banco de dados do Azure Cosmos toosetup Olá API de tabela."
services: cosmos-db
keywords: "distribuição global, Tabela"
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: d2a995e09c37f9449856aef2ab707e95eb8a540c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-table-api"></a>Como a distribuição global usando o banco de dados do Azure Cosmos toosetup Olá API de tabela

Neste artigo, mostramos como toouse Olá distribuição global do banco de dados do Azure Cosmos toosetup portal do Azure e, em seguida, conecte-se usando Olá API de tabela (visualização).

Este artigo aborda Olá tarefas a seguir: 

> [!div class="checklist"]
> * Configurar a distribuição global usando Olá portal do Azure
> * Configurar a distribuição global usando Olá [API de tabela](table-introduction.md)

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-table-api"></a>Conectar-se a região preferida tooa usando Olá API de tabela

Em ordem tootake aproveitar [distribuição global](distribute-data-globally.md), aplicativos cliente podem especificar Olá ordenados lista de preferência de regiões toobe usada tooperform operações de documento. Isso pode ser feito por configuração Olá `TablePreferredLocations` valor de configuração na configuração de aplicativo hello para visualização Olá SDK de armazenamento do Azure. Com base na configuração de conta do banco de dados do Azure Cosmos hello, disponibilidade regional atual e a lista de preferência de saudação especificado, Olá ponto de extremidade mais ideal será escolhido por hello Azure Storage SDK tooperform gravam e operações de leitura.

Olá `TablePreferredLocations` deve conter uma lista separada por vírgulas de locais (múltipla) preferenciais para leituras. Cada instância de cliente pode especificar um subconjunto dessas regiões Olá preferido para leituras de baixa latência. regiões de saudação devem ser nomeados usando seus [exibir nomes](https://msdn.microsoft.com/library/azure/gg441293.aspx), por exemplo, `West US`.

Todas as leituras serão enviadas toohello primeira região disponível em Olá `TablePreferredLocations` lista. Se Olá solicitação falhar, o cliente Olá falhar para baixo próxima região do hello lista toohello e assim por diante.

Olá SDK somente tentará tooread de regiões de saudação especificado em `TablePreferredLocations`. Portanto, por exemplo, se Olá conta de banco de dados está disponível em três regiões, mas o cliente Olá especifica apenas duas das Olá regiões não-gravação para `TablePreferredLocations`, e nenhuma leitura será servida fora da região de gravação hello, mesmo no caso de saudação de failover.

Olá SDK enviará automaticamente todas as gravações toohello gravação região atual.

Se hello `TablePreferredLocations` propriedade não for definida, todas as solicitações serão atendidas a partir de região de gravação atual hello.

```xml
    <appSettings>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>           
    </appSettings>
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
