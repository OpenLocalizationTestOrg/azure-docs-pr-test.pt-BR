---
title: aaaAzure exemplos de CLI para o banco de dados do Azure Cosmos | Microsoft Docs
description: "Exemplos da CLI do Azure - Criar e gerenciar contas, , bancos de dados, contêineres, regiões e firewalls do Azure Cosmos DB."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: database
ms.date: 06/07/2017
ms.author: mimig
ms.openlocfilehash: d6eefc3274e0b66eec4e69166bb7d4ddd58a522e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-azure-cosmos-db"></a>Exemplos da CLI do Azure para o Azure Cosmos DB

Olá tabela a seguir inclui links toosample CLI do Azure scripts para o banco de dados do Azure Cosmos. Páginas de referência para todos os comandos de CLI do Azure Cosmos banco de dados estão disponíveis em Olá [referência da CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/cosmosdb).

| |  |
|---|---|
|**Criar uma conta, banco de dados e contêineres do Azure Cosmos DB**||
|[Criar uma conta da API de DocumentDB, Graph ou Tabela](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| Cria uma conta da API de banco de dados do Azure Cosmos único, o banco de dados e o contêiner para uso com hello documentos, gráfico ou APIs de tabela. |
| [Criar uma conta da API do MongoDB](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Cria uma única conta, banco de dados e coleção da API de MongoDB do Azure Cosmos DB. |
|**Dimensionar o Azure Cosmos DB**||
| [Escalar a taxa de transferência de contêiner](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Olá alterações provisionados througput em um contêiner.|
|[Replicar uma conta de banco de dados do Azure Cosmos DB em várias regiões e configurar as prioridades de failover](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|Replica globalmente os dados da conta em várias regiões com uma prioridade de failover especificada.|
|**Proteger o Azure Cosmos DB**||
| [Obter chaves da conta](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Obtém as chaves de gravação mestre primário e secundário hello e chaves somente leitura primária e secundária para a conta de saudação.|
| [Obter cadeia de conexão do MongoDB](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Obtém o tooconnect de cadeia de caracteres de conexão de saudação seu aplicativo de MongoDB tooyour conta de banco de dados do Azure Cosmos.|
|[Regenerar chaves da conta](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|Regenera mestre hello ou chave de somente leitura para a conta de saudação.|
|[Criar um firewall](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| Cria uma entrada IP acesso controle política toolimit toohello conta de acesso de um conjunto aprovado de máquinas e/ou serviços de nuvem.|
|**Alta disponibilidade, recuperação de desastre, backup e restauração**||
|[Configurar política de failover](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|Conjuntos de Olá prioridade de failover de cada região em que a conta de saudação é replicada.|
|**Conectar o Azure Cosmos DB aos recursos**||
|[Conecte-se um aplicativo de web tooAzure Cosmos DB](https://docs.microsoft.com/azure/app-service-web/scripts/app-service-cli-app-service-documentdb?toc=%2fcli%2fazure%2ftoc.json)|Criar e conectar um banco de dados do Azure Cosmos DB e um aplicativo Web.|
|||
