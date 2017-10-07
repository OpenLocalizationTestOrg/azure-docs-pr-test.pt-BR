---
title: "Introdução tooAzure Cosmos DB: API para o MongoDB | Microsoft Docs"
description: "Saiba como você pode usar o banco de dados do Azure Cosmos toostore e grandes volumes de consulta de documentos JSON com o uso de baixa latência Olá populares OSS MongoDB APIs."
keywords: "o que é o MongoDB"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 4afaf40d-c560-42e0-83b4-a64d94671f0a
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: anhoh
ms.openlocfilehash: 1eb88014cc4809332e3f5c109a44a55814194934
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-api-for-mongodb"></a>Introdução tooAzure Cosmos DB: API para o MongoDB

O [Azure Cosmos DB](../cosmos-db/introduction.md) é o serviço multimodelo de banco de dados da Microsoft, distribuído globalmente, para aplicativos críticos. Banco de dados do Azure Cosmos fornece [distribuição global turnkey](distribute-data-globally.md), [dimensionamento Elástico de taxa de transferência e armazenamento](partition-data.md) latências de milissegundo em todo o mundo, dígito no percentual de 99th hello, [cinco níveis de consistência bem definidos](consistency-levels.md)e a garantia de alta disponibilidade, apoiada por [SLAs do setor](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Banco de dados do Azure Cosmos [indexa automaticamente os dados](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) sem exigir que você toodeal com o gerenciamento de esquema e de índice. Ele tem vários modelos e suporta modelos de dados de colunas, gráficos, valores-chave e documentos. 

![Azure Cosmos DB: API do MongoDB](./media/mongodb-introduction/cosmosdb-mongodb.png) 

Bancos de dados do banco de dados do cosmos podem ser usados como repositório de dados Olá para aplicativos escritos para [MongoDB](https://docs.mongodb.com/manual/introduction/). Isso significa que, ao usar [drivers](https://docs.mongodb.org/ecosystem/drivers/) existentes, o aplicativo escrito para o MongoDB agora pode se comunicar com o Cosmos DB e usar bancos de dados do Cosmos DB, em vez de bancos de dados do MongoDB. Em muitos casos, você pode alternar usa o MongoDB tooCosmos DB simplesmente alterando uma cadeia de caracteres de conexão. Com essa funcionalidade, você pode facilmente criar e executar aplicativos de banco de dados do MongoDB no hello Azure nuvem com uma distribuição global do Azure Cosmos DB e [principais SLAs do setor abrangente](https://azure.microsoft.com/support/legal/sla/cosmos-db), enquanto continua toouse familiar habilidades e ferramentas para o MongoDB.


## <a name="what-is-hello-benefit-of-using-azure-cosmos-db-for-mongodb-applications"></a>O que é o benefício de saudação do banco de dados do Azure Cosmos para aplicativos do MongoDB?

**Taxa de transferência de forma escalonável e armazenamento:** facilmente dimensionar para cima ou para baixo o toomeet de banco de dados do MongoDB seu aplicativo precisa. Os dados são armazenados em SSD (discos de estado sólido) para fornecer latências baixas previsíveis. Cosmos banco de dados oferece suporte a coleções do MongoDB que podem ser dimensionado toovirtually tamanhos de armazenamento ilimitado e taxa de transferência fornecida. Você pode dimensionar o Cosmos DB de forma elástica com desempenho previsível à medida que o aplicativo cresce. 

**Replicação de várias regiões:** Cosmos DB transparentemente replica as que você associou com sua conta do MongoDB, permitindo que você toodevelop aplicativos que exigem acesso global toodata proporcionando o equilíbrio entre as regiões de dados tooall consistência, disponibilidade e desempenho, todos com garantias correspondentes. Cosmos DB fornece failover transparente de regional com APIs de hospedagem múltipla e a taxa de transferência da escala tooelastically Olá capacidade e armazenamento globo hello. Saiba mais em [Distribuir dados globalmente](distribute-data-globally.md).

**Compatibilidade com o MongoDB**: use os conhecimentos, o código do aplicativo e as ferramentas do MongoDB que você já tem. Você pode desenvolver aplicativos usando o MongoDB e implantá-las tooproduction usando Olá totalmente gerenciado globalmente distribuído serviço de banco de dados do Cosmos.

**Não há gerenciamento de servidor**: você não tem toomanage e dimensionar seus bancos de dados do MongoDB. Cosmos banco de dados é um serviço totalmente gerenciado, o que significa que você não tem toomanage qualquer infraestrutura ou máquinas virtuais por conta própria. O Cosmos DB está disponível em mais de 30 [Regiões do Azure](https://azure.microsoft.com/regions/services/).

**Níveis de consistência ajustáveis:** Select de cinco bem definidas compensação ideal de tooachieve do níveis de consistência entre a consistência e desempenho. Para operações de consulta e leitura, o Cosmos DB oferece cinco níveis de consistência distintos: forte, desatualização limitada, sessão, prefixo constante e eventual. Esses níveis de consistência bem definidos, granular permitem toomake som prós e contras latência, a disponibilidade e a consistência. Saiba mais em [usar consistência níveis de desempenho e disponibilidade de toomaximize](consistency-levels.md).

**A indexação automática**: por padrão, Cosmos DB automaticamente todas as propriedades de saudação dentro de documentos em seu banco de dados do MongoDB de índices e não esperar ou exigir qualquer esquema ou a criação de índices secundários.

**Pequeno porte** -Azure Cosmos DB dá suporte a várias réplicas locais toodeliver 99,99% disponibilidade e proteção de dados em face de saudação de falhas locais e regionais. O Azure Cosmos DB apresenta recursos de segurança e [certificações de conformidade](https://www.microsoft.com/trustcenter) de nível empresarial. 

Saiba mais neste vídeo do Azure Friday com Scott Hanselman e o Gerente Principal de Engenharia do Azure Cosmos DB, Kirill Gavrylyuk.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Introducing-Azure-Cosmos-DB/player]
> 

## <a name="how-tooget-started"></a>A inicialização de tooget

Siga Olá MongoDB inícios rápidos toocreate uma conta de banco de dados do Cosmos e migrar seu toouse de aplicativo de DB Mongo Cosmos DB existente ou criar um novo:

* [Migrar um aplicativo Web do MongoDB do Node.js existente](create-mongodb-nodejs.md).
* [Criar um aplicativo de web do MongoDB API com .NET e hello portal do Azure](create-mongodb-dotnet.md)
* [Criar um aplicativo de console do MongoDB API com o Java e Olá portal do Azure](create-mongodb-java.md)

## <a name="next-steps"></a>Próximas etapas

Informações sobre a API do Azure Cosmos banco de dados MongoDB são integradas ao Olá documentação de banco de dados do Cosmos geral do Azure, mas aqui estão alguns tooget ponteiros é iniciado:

* Siga Olá [conectar-se a conta do MongoDB tooa](connect-mongodb-account.md) toolearn tutorial como tooget as informações de cadeia de caracteres de conexão da conta.
* Siga Olá [MongoChef de uso com o banco de dados do Azure Cosmos](mongodb-mongochef.md) toolearn tutorial como toocreate uma conexão entre o banco de dados do banco de dados do Azure Cosmos e o aplicativo do MongoDB no MongoChef.
* Siga Olá [migrar dados tooAzure Cosmos DB com suporte de protocolo para o MongoDB](mongodb-migrate.md) tooimport tutorial tooan seus dados API de banco de dados do MongoDB.
* Conecte-se a API tooan para o MongoDB conta usando [Robomongo](mongodb-robomongo.md).
* Saber quantos RUs estiver usando as operações com hello [GetLastRequestStatistics de comando e Olá métricas portais do Azure](request-units.md#GetLastRequestStatistics).
* Saiba como muito[configurar preferências de leitura para aplicativos distribuídos globalmente](../cosmos-db/tutorial-global-distribution-mongodb.md).
