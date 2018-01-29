---
title: Exemplos da CLI do Azure para o Azure Cosmos DB | Microsoft Docs
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
ms.date: 11/29/2017
ms.author: mimig
ms.openlocfilehash: 432ffc80d602a9e4eaf83fba15f0e6ebabd13603
ms.sourcegitcommit: a5f16c1e2e0573204581c072cf7d237745ff98dc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2017
---
# <a name="azure-cli-samples-for-azure-cosmos-db"></a>Exemplos da CLI do Azure para o Azure Cosmos DB

[!INCLUDE [cosmos-db-sql-api](../../includes/cosmos-db-sql-api.md)] 

A tabela a seguir inclui links para exemplos de scripts de CLI do Azure para o Azure Cosmos DB. Páginas de referência para todos os comandos de CLI do Azure Cosmos DB estão disponíveis na [referência da CLI 2.0 do Azure](https://docs.microsoft.com/cli/azure/cosmosdb).

| |  |
|---|---|
|**Criar uma conta, banco de dados e contêineres do Azure Cosmos DB**||
|[Criar uma conta da API do SQL](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| Cria uma única conta, banco de dados e contêiner da API do Azure Cosmos DB para usar com a API do SQL. |
| [Criar uma conta da API do MongoDB](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Cria uma única conta, banco de dados e coleção da API de MongoDB do Azure Cosmos DB. |
|**Dimensionar o Azure Cosmos DB**||
| [Escalar a taxa de transferência de contêiner](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Altera a taxa de transferência provisionada em um contêiner.|
|[Replicar uma conta de banco de dados do Azure Cosmos DB em várias regiões e configurar as prioridades de failover](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|Replica globalmente os dados da conta em várias regiões com uma prioridade de failover especificada.|
|**Proteger o Azure Cosmos DB**||
| [Obter chaves da conta](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Obtém a chaves de gravação mestre primária e secundária e as chaves somente leitura primária e secundária da conta.|
| [Obter cadeia de conexão do MongoDB](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Obtém a cadeia de conexão para conectar seu aplicativo MongoDB à sua conta do Azure Cosmos DB.|
|[Regenerar chaves da conta](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|Regenera a chave mestre ou somente leitura da conta.|
|[Criar um firewall](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| Cria uma política de controle de acesso IP de entrada para limitar o acesso à conta por um conjunto aprovado de máquinas e/ou serviços de nuvem.|
|**Alta disponibilidade, recuperação de desastre, backup e restauração**||
|[Configurar política de failover](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|Define a prioridade de failover para cada região em que a conta é replicada.|
|**Conectar o Azure Cosmos DB aos recursos**||
|[Conectar um aplicativo Web ao Azure Cosmos DB](../app-service/scripts/app-service-cli-app-service-documentdb.md?toc=%2fcli%2fazure%2ftoc.json)|Criar e conectar um banco de dados do Azure Cosmos DB e um aplicativo Web.|
|||
