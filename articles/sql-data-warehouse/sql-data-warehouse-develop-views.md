---
title: "exibições de aaaUsing T-SQL no Azure SQL Data Warehouse | Microsoft Docs"
description: "Dicas para usar exibições Transact-SQL no Azure SQL Data Warehouse para desenvolvimento de soluções."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: b5208f32-8f4a-4056-8788-2adbb253d9fd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 3990b133946621691bdfa4b09523d21867470c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-sql-data-warehouse"></a>Modos de exibição no SQL Data Warehouse
Os modos de exibição são particularmente úteis no SQL Data Warehouse. Eles podem ser usados em um número de qualidade de saudação tooimprove maneiras diferentes de sua solução.  Este artigo destaca alguns exemplos de como tooenrich sua solução com modos de exibição, bem como limitações Olá que precisam toobe considerados.

> [!NOTE]
> A sintaxe para `CREATE VIEW` não é discutida neste artigo. Consulte toohello [CREATE VIEW] [ CREATE VIEW] artigo no MSDN para obter essas informações de referência.
> 
> 

## <a name="architectural-abstraction"></a>Abstração de arquitetura
Um padrão de aplicativo muito comum é toore-criar tabelas usando criar tabela como selecionar (CTAS) seguido por um objeto de renomeação padrão durante o carregamento de dados.

exemplo Hello abaixo adiciona uma dimensão de data de tooa data novos registros. Observe como uma nova tabble, DimDate_New, é criado pela primeira vez e em seguida renomeou versão original do hello tooreplace da tabela de saudação.

```sql
CREATE TABLE dbo.DimDate_New
WITH (DISTRIBUTION = ROUND_ROBIN
, CLUSTERED INDEX (DateKey ASC)
)
AS
SELECT *
FROM   dbo.DimDate  AS prod
UNION ALL
SELECT *
FROM   dbo.DimDate_stg AS stg
;

RENAME OBJECT DimDate tooDimDate_Old;
RENAME OBJECT DimDate_New tooDimDate;

```

No entanto, essa abordagem pode resultar em tabelas que aparecem e desaparecem da exibição do usuário, bem como nas mensagens de erro "a tabela não existe". Modos de exibição podem ser usado tooprovide usuários com uma camada de apresentação consistente enquanto objetos subjacentes Olá são renomeados. Fornecendo aos usuários acesso toohello dados por meio de modos de exibição, significa que os usuários não precisam toohave visibilidade de tabelas subjacentes hello. Isso fornece uma experiência de usuário consistente enquanto garante que os designers do data warehouse Olá podem desenvolver um modelo de dados de saudação e maximizar o desempenho usando CTAS durante o processo de carregamento de dados de saudação.    

## <a name="performance-optimization"></a>Otimização do desempenho
Modos de exibição também podem ser utilizadas tooenforce desempenho otimizado junções entre tabelas. Por exemplo, um modo de exibição pode incorporar uma chave de distribuição redundante como parte da saudação ingressar na movimentação de dados de toominimize critérios.  Outro benefício de um modo de exibição pode ser tooforce uma consulta específica ou dica de junção. Usando modos de exibição desta maneira garante que as junções sempre são executadas de maneira ideal, evitando a necessidade de saudação de construção da saudação correto do tooremember usuários para suas associações.

## <a name="limitations"></a>Limitações
Os modos de exibição no SQL Data Warehouse são somente metadados.  Consequentemente, Olá as opções a seguir não está disponível:

* Não há opção de associação de esquema
* Tabelas base não podem ser atualizadas por meio do modo de exibição de saudação
* Exibições não podem ser criadas em tabelas temporárias
* Não há suporte para Olá expandir / dicas NOEXPAND
* não há exibições indexadas no SQL Data Warehouse

## <a name="next-steps"></a>Próximas etapas
Para obter mais dicas de desenvolvimento, consulte [Visão geral de desenvolvimento do SQL Data Warehouse][SQL Data Warehouse development overview].
Para `CREATE VIEW` sintaxe, consulte muito[CREATE VIEW][CREATE VIEW].

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->
