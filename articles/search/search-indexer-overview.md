---
title: Indexadores na Azure Search | Microsoft Docs
description: "Rastrear um banco de dados SQL do Azure, Azure Cosmos DB ou Armazenamento do Azure para extrair dados pesquisáveis e preencher um índice do Azure Search."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 10/17/2017
ms.author: heidist
ms.openlocfilehash: a51aa48a9a2c3c062c374885d45f08ae0b397ce1
ms.sourcegitcommit: 176c575aea7602682afd6214880aad0be6167c52
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="indexers-in-azure-search"></a>Indexadores no Azure Search
> [!div class="op_single_selector"]
>
> * [Visão geral](search-indexer-overview.md)
> * [Portal](search-import-data-portal.md)
> * [SQL Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
> * [Banco de dados do Azure Cosmos](search-howto-index-cosmosdb.md)
> * [Armazenamento de Blobs do Azure](search-howto-indexing-azure-blob-storage.md)
> * [Armazenamento de Tabelas do Azure](search-howto-indexing-azure-tables.md)
>

Um *indexador* no Azure Search é um rastreador que extrai dados pesquisáveis e metadados de uma fonte de dados externa e popula um índice com base nos mapeamentos de campo a campo entre o índice e a fonte de dados. Essa abordagem às vezes é chamada de 'modelo de pull' porque o serviço obtém os dados sem que você precise escrever código que envia dados por push a um índice.

Os indexadores se baseiam em tipos de fonte de dados ou plataformas com indexadores individuais para SQL Server no Azure, Cosmos DB, Armazenamento de Tabelas do Azure e Armazenamento de Blobs e assim por diante.

Você pode usar um indexador como o único meio para ingestão de dados ou usar uma combinação de técnicas que incluam o uso de um indexador para carregar apenas alguns dos campos no índice.

Você pode executar os indexadores sob demanda ou em uma agenda de atualização de dados recorrente que é executada a cada quinze minutos. Atualizações mais frequentes exigem um modelo de push que atualiza simultaneamente os dados no Azure Search e na fonte de dados externa.

## <a name="approaches-for-creating-and-managing-indexers"></a>Abordagens para criar e gerenciar indexadores

Você pode criar e gerenciar indexadores usando estas abordagens:

* [Portal > Assistente de Dados de Importação ](search-get-started-portal.md)
* [API REST do Serviço](https://msdn.microsoft.com/library/azure/dn946891.aspx)
* [SDK .NET](https://msdn.microsoft.com/library/azure/microsoft.azure.search.iindexersoperations.aspx)

Inicialmente, um novo indexador é anunciado como uma versão prévia do recurso. As versões prévias do recurso são introduzidas em APIs (REST e .NET) e então integradas ao portal após a graduação para a disponibilidade geral. Se você estiver avaliando um novo indexador, deverá planejar escrever código.

## <a name="basic-configuration-steps"></a>Etapas da configuração básica
Os indexadores podem oferecer recursos que são exclusivos da fonte de dados. Nesse sentido, alguns aspectos de configuração da fonte de dados ou do indexador variam de acordo com o tipo de indexador. No entanto, todos os indexadores compartilham a mesma composição básica e os mesmos requisitos. As etapas que são comuns a todos os indexadores são abordadas a seguir.

### <a name="step-1-create-a-data-source"></a>Etapa 1: Criar uma fonte de dados
Um indexador extrai dados de uma *fonte de dados* que contém informações como uma cadeia de conexão e, possivelmente, credenciais. Atualmente, há suporte às seguintes fontes de dados:

* [Banco de Dados SQL do Azure ou SQL Server em uma máquina virtual do Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Banco de dados do Azure Cosmos](search-howto-index-cosmosdb.md)
* [Armazenamento de Blobs do Azure](search-howto-indexing-azure-blob-storage.md) para tipos de conteúdo selecionados
* [Armazenamento de Tabelas do Azure](search-howto-indexing-azure-tables.md)

As fontes de dados são configuradas e gerenciadas independentemente dos indexadores que as utilizam, o que significa que uma fonte de dados pode ser usada por vários indexadores para carregar mais de um índice por vez.

### <a name="step-2-create-an-index"></a>Etapa 2: Criar um índice
Um indexador automatizará algumas tarefas relacionadas à ingestão de dados, mas a criação de um índice não é uma delas. Como pré-requisito, você deve ter um índice predefinido com campos iguais aos da sua fonte de dados externa. Para saber mais sobre como estruturar um índice, confira [Criar um índice (API REST do Azure Search)](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Para obter ajuda com associações de campo, veja [Mapeamento de campos em indexadores do Azure Search](search-indexer-field-mappings.md).

> [!Tip]
> Embora indexadores não consigam gerar um índice para você, o assistente de **Importar dados** no portal pode ajudar. Na maioria dos casos, o assistente pode inferir um esquema de índice a partir de metadados existentes na fonte, apresentando um esquema de índice preliminar que você pode editar em linha enquanto o assistente estiver ativo. Assim que o índice é criado no serviço, outras edições no portal são, na sua maior parte, limitadas a adicionar novos campos. Leve o assistente em consideração para criar, mas não para revisar um índice. Para o aprendizado prático, percorra o [passo a passo portal](search-get-started-portal.md).

### <a name="step-3-create-and-schedule-the-indexer"></a>Etapa 3: Criar e agendar o indexador
A definição do indexador é uma construção que especifica o índice, a fonte de dados e uma agenda. Um indexador pode referenciar uma fonte de dados de outro serviço, desde que a fonte de dados seja da mesma assinatura. Para saber maissobre como estruturar um indexador, confira [Criar indexador (API REST do Azure Search)](https://docs.microsoft.com/rest/api/searchservice/Create-Indexer).

## <a name="next-steps"></a>Próximas etapas
Agora que você tem as noções básicas, a próxima etapa é examinar os requisitos e as tarefas específicas para cada tipo de fonte de dados.

* [Banco de Dados SQL do Azure ou SQL Server em uma máquina virtual do Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Banco de dados do Azure Cosmos](search-howto-index-cosmosdb.md)
* [Armazenamento de Blobs do Azure](search-howto-indexing-azure-blob-storage.md)
* [Armazenamento de Tabelas do Azure](search-howto-indexing-azure-tables.md)
* [Indexação de blobs CSV usando o indexador de Blobs do Azure Search](search-howto-index-csv-blobs.md)
* [Indexação de blobs JSON com o indexador de blobs do Azure Search](search-howto-index-json-blobs.md)
