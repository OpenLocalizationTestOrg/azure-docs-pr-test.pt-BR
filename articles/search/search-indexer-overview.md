---
title: aaaIndexers na pesquisa do Azure | Microsoft Docs
description: "Rastreamento de banco de dados SQL do Azure, o banco de dados do Azure Cosmos ou dados pesquisável do armazenamento do Azure tooextract e popular um índice de pesquisa do Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 34a7694c-8fd9-46b1-8900-cefdd7236323
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: 6a816252ec5d6032491a12651c05cb1fe77d3d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="indexers-in-azure-search"></a>Indexadores na Pesquisa do Azure
> [!div class="op_single_selector"]
>
> * [Visão geral](search-indexer-overview.md)
> * [Portal](search-import-data-portal.md)
> * [SQL Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
> * [Azure Cosmos DB](search-howto-index-documentdb.md)
> * [Armazenamento de Blobs do Azure](search-howto-indexing-azure-blob-storage.md)
> * [Armazenamento de Tabelas do Azure](search-howto-indexing-azure-tables.md)
>
>

Um **indexador** na pesquisa do Azure é um rastreador que extrai dados pesquisáveis e metadados de uma fonte de dados externa e popula um índice com base nos mapeamentos de campo para entre o índice de saudação e sua fonte de dados. Essa abordagem é às vezes chamado tooas 'modelo de pull' porque o serviço de saudação extrai dados em sem a necessidade de toowrite qualquer código que envia dados tooan índice.

Você pode usar um indexador como Olá único significa para a ingestão de dados ou usar uma combinação de técnicas que incluem o uso de saudação de um indexador para carregar apenas alguns dos campos de saudação no índice.

Você pode executar os indexadores sob demanda ou em uma agenda de atualização de dados recorrente que é executada a cada quinze minutos. Atualizações mais frequentes exigem um modelo de push que atualiza simultaneamente os dados na Pesquisa do Azure e na fonte de dados externa.

## <a name="approaches-for-creating-and-managing-indexers"></a>Abordagens para criar e gerenciar indexadores
Para indexadores disponíveis, como o Azure SQL ou o Azure Cosmos DB, você pode criar e gerenciar índices usando estas abordagens:

* [Portal > Assistente de Dados de Importação ](search-get-started-portal.md)
* [API REST do Serviço](https://msdn.microsoft.com/library/azure/dn946891.aspx)
* [SDK .NET](https://msdn.microsoft.com/library/azure/microsoft.azure.search.iindexersoperations.aspx)

## <a name="basic-configuration-steps"></a>Etapas da configuração básica
Indexadores podem oferecer recursos de fonte de dados toohello exclusivo. Nesse sentido, alguns aspectos de configuração da fonte de dados ou do indexador variam de acordo com o tipo de indexador. No entanto, todos os indexadores compartilham Olá mesmo composição básica e requisitos. Etapas que são comuns tooall indexadores são abordados a seguir.

### <a name="step-1-create-an-index"></a>Etapa 1: criar um índice
Um indexador automatizará a inclusão de toodata relacionados algumas tarefas, mas a criação de um índice não é um deles. Como pré-requisito, você deve ter um índice predefinido com campos iguais aos da sua fonte de dados externa. Para saber mais sobre como estruturar um índice, confira [Criar um índice (API REST da Pesquisa do Azure)](https://msdn.microsoft.com/library/azure/dn798941.aspx).

### <a name="step-2-create-a-data-source"></a>Etapa 2: criar uma fonte de dados
Um indexador extrai dados de uma **fonte de dados** que contém informações como uma cadeia de conexão. Atualmente, Olá fontes de dados a seguir têm suporte:

* [Banco de Dados SQL do Azure ou SQL Server em uma máquina virtual do Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Banco de dados do Azure Cosmos](search-howto-index-documentdb.md)
* [Armazenamento de BLOBs do Azure](search-howto-indexing-azure-blob-storage.md), usado tooextract texto de PDF, documentos do Office, HTML ou XML
* [Armazenamento de Tabelas do Azure](search-howto-indexing-azure-tables.md)

Fontes de dados são configuradas e gerenciadas independentemente de indexadores Olá que usá-los, que significa que uma fonte de dados pode ser usada por vários tooload de indexadores de mais de um índice por vez.

### <a name="step-3create-and-schedule-hello-indexer"></a>Etapa 3: criar e agendar indexador Olá
definição do indexador Olá é uma construção especificando índice hello, fonte de dados e uma agenda. Um indexador pode fazer referência a uma fonte de dados de outro serviço, como fonte de dados é de saudação mesma assinatura. Para saber maissobre como estruturar um indexador, confira [Criar indexador (API REST da Pesquisa do Azure)](https://msdn.microsoft.com/library/azure/dn946899.aspx).

## <a name="next-steps"></a>Próximas etapas
Agora que você tem a ideia básica hello, o hello próxima etapa é tooreview requisitos e o tipo de fonte de dados de tooeach específico de tarefas.

* [Banco de Dados SQL do Azure ou SQL Server em uma máquina virtual do Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Banco de dados do Azure Cosmos](search-howto-index-documentdb.md)
* [Armazenamento de BLOBs do Azure](search-howto-indexing-azure-blob-storage.md), usado tooextract texto de PDF, documentos do Office, HTML ou XML
* [Armazenamento de Tabelas do Azure](search-howto-indexing-azure-tables.md)
* [A indexação de blobs CSV usando o indexador de BLOBs do Azure pesquisa Olá](search-howto-index-csv-blobs.md)
* [Indexação de blobs JSON com o indexador de blobs do Azure Search](search-howto-index-json-blobs.md)
