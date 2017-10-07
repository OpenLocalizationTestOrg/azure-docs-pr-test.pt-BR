---
title: aaaIntroduction tooAzure Cosmos DB | Microsoft Docs
description: "Saiba mais sobre o Azure Cosmos DB. Este multimodelo de banco de dados distribuído globalmente foi criado para alta disponibilidade, escalabilidade elástica e baixa latência."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: a855183f-34d4-49cc-9609-1478e465c3b7
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/14/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: f2acbe99f425b2f07a62bbbb4324aa48f1037481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="welcome-tooazure-cosmos-db"></a>Bem-vindo tooAzure Cosmos DB

O BD Cosmos do Azure é o multimodelo de banco de dados distribuído globalmente da Microsoft. Olá clicando em um botão, o banco de dados do Azure Cosmos lhe permite tooelastically e independentemente taxa de transferência de escala e o armazenamento em qualquer número de regiões geográficas do Azure. Ele oferece garantias de taxa de transferência, disponibilidade, latência e consistência com [SLAs](https://aka.ms/acdbsla) (contratos de nível de serviço) abrangentes, algo que nenhum outro serviço de banco de dados pode oferecer.

![O Azure Cosmos DB é um serviço de banco de dados distribuído globalmente pela Microsoft com escala horizontal elástica, baixa latência garantida, cinco modelos de consistência e SLAs de garantia abrangente](./media/introduction/azure-cosmos-db.png)

## <a name="solutions-that-benefit-from-azure-cosmos-db"></a>Soluções que se beneficiam do Azure Cosmos DB

Qualquer [web, móveis, jogos e aplicativos de IoT](use-cases.md) que precisam de toohandle grandes quantidades de leituras e gravações em um [global](distribute-data-globally.md) dimensionar com baixo tempo de resposta para uma variedade de dados se beneficiarão do Azure Cosmos DB [garantia](https://azure.microsoft.com/support/legal/sla/cosmos-db/) disponibilidade, alta taxa de transferência, baixa latência e consistência ajustável.

## <a name="key-capabilities"></a>Principais recursos
Como um serviço de banco de dados globalmente distribuído, o banco de dados do Azure Cosmos fornece Olá toohelp recursos criar aplicativos escalonáveis e altamente responsivos a seguir:

* **Distribuição global turnkey**
    * Você pode [distribuir os dados](distribute-data-globally.md) tooany o número de [regiões do Azure](https://azure.microsoft.com/regions/), com hello [clique de um botão](tutorial-global-distribution-documentdb.md). Isso permite que você tooput seus dados em que os usuários, garantindo a menor latência possível de saudação tooyour clientes. 
    * APIs de hospedagem múltipla, Olá aplicativo sempre usando o Azure Cosmos DB sabe onde hello mais próximo da região é e enviará solicitações toohello mais próximo do Centro de dados. Tudo isso é possível sem alterações de configuração, defina sua região de gravação e como muitos leiam regiões conforme desejar e Olá resto é feito para você.

* **Vários modelos de dados e APIs populares para acessar e consultar dados**
    * modelo de dados com base em do atom--sequência de registro (ARS) Hello Azure Cosmos DB é criado no modo nativo oferece suporte a vários modelos de dados, incluindo, mas não limitado toodocument, gráfico, chave-valor, tabela e modelos de dados de colunas.
    * APIs de saudação modelos de dados a seguir têm suporte com SDKs disponíveis em vários idiomas:
        * [API do DocumentDB](documentdb-introduction.md)
        * [API do MongoDB](mongodb-introduction.md)
        * [API de Tabela](table-introduction.md)
        * [API do Graph (Gremlin)](graph-introduction.md)
        * Modelos de dados adicionais em breve 

* **Dimensionar elasticamente a taxa de transferência e o armazenamento sob demanda, em todo o mundo**
    * Dimensione facilmente a taxa de transferência do banco de dados em uma granularidade [por segundo](request-units.md) e altere-a sempre que desejar. 
    * Dimensionar o tamanho do armazenamento [transparente e automática](partition-data.md) toohandle seus requisitos de tamanho agora e para sempre.

* **Criar aplicativos altamente responsivos e críticos**
    * Banco de dados do Azure Cosmos garante a baixa latência de ponta a ponta em Olá 99th clientes de tooits percentual. 
    * Para um item KB 1 típico, Cosmos DB garante latência de ponta a ponta de leituras em 10 ms e indexadas gravações em 15 ms no percentual de 99th hello, Olá no mesmo região do Azure. latências mediano Olá são significativamente menores (menos de 5 ms).

* **Garantir disponibilidade "sempre ativa"**
    * Disponibilidade de 99,99% em uma única região.
    * Implantar o número de tooany de [regiões do Azure](https://azure.microsoft.com/regions) para maior disponibilidade.
    * [Simule uma falha](regional-failover.md) de uma ou mais regiões com a garantia de nenhuma perda de dados. 

* **Gravar aplicativos distribuídos globalmente, hello diretas**
    * Cinco [modelos de consistência](consistency-levels.md) modelos oferecem uma gama de consistência forte do tipo SQL todos Olá consistência eventual tooNoSQL maneira semelhante e cada coisa entre. 
  
* **Garantia do dinheiro de volta**
    * Agilidade nos seus dados ou o seu dinheiro de volta. 
    * [Contratos de nível de serviço](https://aka.ms/acdbsla) para disponibilidade, latência, taxa de transferência e consistência. 

* **Sem gerenciamento de esquema/índice de banco de dados**
    * Pare de se preocupar sobre como manter o esquema e os índices do seu banco de dados em sincronia com o esquema do seu aplicativo. Somos livres de esquema. 
    * Mecanismo de banco de dados do Azure Cosmos DB é completamente independente de esquema – ele indexa automaticamente todos os dados de saudação que consome sem a necessidade de qualquer esquema ou índices e serve consultas rápidas impressionante. 

* **Baixo custo de propriedade**
    * Cinco vezes tooten [mais econômica](https://aka.ms/cosmos-db-tco-paper) que uma solução não gerenciada.
    * Três vezes mais barato do que o DynamoDB.

## <a name="capability-comparison"></a>Comparação de funcionalidade

Banco de dados Cosmos do Azure fornece recursos de melhor Olá de bancos de dados relacionais e não relacionais.

| Funcionalidades | Bancos de dados relacionais   | Bancos de dados não relacionais (NoSQL) |    Azure Cosmos DB |
| --- | --- | --- | --- |
| Distribuição global | Não | Não | Sim, a distribuição turnkey em 30 + regiões, com as APIs de hospedagem múltipla|
| Escala horizontal | Não | Sim | Sim, você pode dimensionar de maneira independente o armazenamento e a taxa de transferência | 
| Garantias de latência | Não | Sim | Sim, 99% de leituras em < 10 ms e gravações em < 15 ms | 
| Alta disponibilidade | Não | Sim | Sim, o Cosmos DB está sempre ativo, tem vantagens e desvantagens PACELC e fornece opções de failover automático e manual|
| Modelo de dados + API | Relacional + SQL | Multimodelo + API OSS | Multimodelo + SQL + API OSS (e mais em breve) |
| SLAs | Sim | Não | Sim, SLAs abrangentes de latência, taxa de transferência, consistência e disponibilidade |


## <a name="next-steps"></a>Próximas etapas
Comece no Azure Cosmos DB com um dos nossos guias de início rápido:

* [Introdução à API DocumentDB do Azure Cosmos DB](create-documentdb-dotnet.md)
* [Introdução à API MongoDB do Azure Cosmos DB](create-mongodb-nodejs.md)
* [Introdução à API do Graph do Azure Cosmos DB](create-graph-dotnet.md)
* [Introdução à API de Tabela do Azure Cosmos DB](create-table-dotnet.md)
