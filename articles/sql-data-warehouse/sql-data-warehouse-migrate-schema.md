---
title: aaaMigrate tooSQL o esquema do Data Warehouse | Microsoft Docs
description: "Dicas para migrar seu tooAzure esquema SQL Data Warehouse para o desenvolvimento de soluções."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 538b60c9-a07f-49bf-9ea3-1082ed6699fb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 1309b743b78564575695038a4856d9d25a2b18d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-schemas-toosql-data-warehouse"></a>Migrar seu tooSQL esquemas do Data Warehouse
Diretrizes para migrar seu tooSQL de esquemas do SQL Data Warehouse. 

## <a name="plan-your-schema-migration"></a>Planejar a migração de esquema

Ao planejar uma migração, consulte Olá [visão geral da tabela] [ table overview] toobecome familiarizado com as considerações de design de tabela, como estatísticas, distribuição, particionamento e indexação.  Também lista alguns [recursos de tabela sem suporte][unsupported table features] e suas soluções alternativas.

## <a name="use-user-defined-schemas-tooconsolidate-databases"></a>Usar bancos de dados de tooconsolidate esquemas definidos pelo usuário

Provavelmente, a carga de trabalho tem mais de um banco de dados. Por exemplo, um data warehouse do SQL Server pode incluir um banco de dados de preparo, um banco de dados do data warehouse e alguns bancos de dados do data mart. Nessa topologia, cada banco de dados é executado como uma carga de trabalho separada, com políticas de segurança separadas.

Por outro lado, o SQL Data Warehouse é executado a carga de trabalho do hello todo o data warehouse em um banco de dados. Uniões cruzadas de banco de dados não são permitidas. Portanto, o SQL Data Warehouse espera que todas as tabelas usadas pelo Olá toobe de depósito de dados armazenado em um banco de dados de saudação.

É recomendável usar esquemas definidos pelo usuário tooconsolidate sua carga de trabalho existente em um banco de dados. Para obter exemplos, confira [Esquemas definidos pelo usuário](sql-data-warehouse-develop-user-defined-schemas.md)

## <a name="use-compatible-data-types"></a>Usar tipos de dados compatíveis
Modifique seu toobe de tipos de dados compatível com o SQL Data Warehouse. Para obter uma lista de tipos de dados com e sem suporte, confira [tipos de dados][data types]. Esse tópico fornece soluções alternativas para os tipos de saudação sem suporte. Ele também fornece uma consulta tooidentify tipos existentes que não têm suporte no SQL Data Warehouse.

## <a name="minimize-row-size"></a>Minimizar o tamanho de linha
Para melhor desempenho, minimiza o comprimento de linha de saudação de suas tabelas. Porque os comprimentos de linha menores levam toobetter desempenho, use Olá menor tipos de dados que funcionam para seus dados. 

Para a largura da linha de tabela, o PolyBase tem um limite de 1 MB.  Se você planejar dados tooload no SQL Data Warehouse com o PolyBase, atualize seu larguras de linha máximo tabelas toohave menos de 1 MB. 

<!--
- For example, this table uses variable length data but hello largest possible size of hello row is still less than 1 MB. PolyBase will load data into this table.

- This table uses variable length data and hello defined row width is less than one MB. When loading rows, PolyBase allocates hello full length of hello variable-length data. hello full length of this row is greater than one MB.  PolyBase will not load data into this table.  

-->

## <a name="specify-hello-distribution-option"></a>Especifique a opção de distribuição Olá
SQL Data Warehouse é um sistema de banco de dados distribuído. Cada tabela é distribuída ou replicada em nós de computação hello. Há uma opção de tabela que permite que você especifique como toodistribute Olá dados. Opções de saudação são round-robin replicado, ou distribuídos de hash. Cada um tem prós e contras. Se você não especificar a opção de distribuição hello, o SQL Data Warehouse usará round-robin como padrão de saudação.

- Round robin é o padrão de saudação. Ele é toouse mais simples de saudação e carrega dados de saudação tão rápidos quanto possível, mas junções exigirá a movimentação de dados que reduz o desempenho da consulta.
- Replicado armazena uma cópia da tabela de saudação em cada nó de computação. Tabelas replicadas são eficazes porque não exigem a movimentação de dados para junções e agregações. Isso exige armazenamento adicional e, assim, funciona melhor para tabelas menores.
- Hash distribuído distribui as linhas de saudação em todos os nós de saudação por meio de uma função de hash. Tabelas de hash distribuída são coração de saudação do SQL Data Warehouse porque eles são projetados tooprovide alto desempenho de consultas em tabelas grandes. Essa opção exige algum planejamento tooselect Olá melhor coluna onde os dados Olá toodistribute. No entanto, se você não escolher Olá Olá de coluna melhor a primeira vez, você pode facilmente novamente distribuir Olá dados em uma coluna diferente. 

toochoose Olá melhor opção de distribuição para cada tabela, consulte [distribuídas tabelas](sql-data-warehouse-tables-distribute.md).


## <a name="next-steps"></a>Próximas etapas
Depois que o tooSQL de esquema de banco de dados do Data Warehouse foi migrado com êxito, prossiga tooone de saudação artigos a seguir:

* [Migrar seus dados][Migrate your data]
* [Migrar seu código][Migrate your code]

Para obter mais informações sobre as práticas recomendadas do SQL Data Warehouse, consulte Olá [práticas recomendadas] [ best practices] artigo.

<!--Image references-->

<!--Article references-->
[Migrate your code]: ./sql-data-warehouse-migrate-code.md
[Migrate your data]: ./sql-data-warehouse-migrate-data.md
[best practices]: ./sql-data-warehouse-best-practices.md
[table overview]: ./sql-data-warehouse-tables-overview.md
[unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[data types]: ./sql-data-warehouse-tables-data-types.md
[unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types

<!--MSDN references-->


<!--Other Web references-->
