---
title: "bancos de dados de nuvem escalonáveis aaaBuilding | Microsoft Docs"
description: "Compilar aplicativos de banco de dados .NET escalonáveis com biblioteca de cliente do banco de dados Elástico Olá"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 1f11c52d-13c1-4994-b9b1-5b1ae2f9255f
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: ca34eff2078c0700dee1bc587f264bbfca979eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="building-scalable-cloud-databases"></a>Criando bancos de dados de nuvem escalonáveis
A escala horizontal dos bancos de dados pode ser feita facilmente usando recursos e ferramentas escalonáveis do Banco de Dados SQL do Azure. Em particular, você pode usar o hello **biblioteca de cliente do banco de dados Elástico** toocreate e gerenciar bancos de dados expandido. Esse recurso permite que você desenvolva facilmente aplicativos fragmentados usando centenas — ou até mesmo milhares - de bancos de dados SQL do Azure. [Trabalhos Elásticos](sql-database-elastic-jobs-powershell.md) pode ser usado toohelp facilitar o gerenciamento desses bancos de dados.

biblioteca de saudação tooinstall, ir muito[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). 

## <a name="documentation"></a>Documentação
1. [Introdução às ferramentas do Banco de Dados Elástico](sql-database-elastic-scale-get-started.md)
2. [Recursos do Banco de Dados Elástico](sql-database-elastic-scale-introduction.md)
3. [Gerenciamento de mapa de fragmentos](sql-database-elastic-scale-shard-map-management.md)
4. [Migrar tooscale-out de bancos de dados existente](sql-database-elastic-convert-to-use-elastic-tools.md)
5. [Roteamento dependente de dados](sql-database-elastic-scale-data-dependent-routing.md)
6. [Consultas com vários fragmentos](sql-database-elastic-scale-multishard-querying.md)
7. [Adicionando um fragmento usando ferramentas do Banco de Dados Elástico](sql-database-elastic-scale-add-a-shard.md)
8. [Aplicativos multilocatários com ferramentas de banco de dados elástico e segurança em nível de linha](sql-database-elastic-tools-multi-tenant-row-level-security.md)
9. [Atualizar aplicativos de biblioteca de cliente](sql-database-elastic-scale-upgrade-client-library.md) 
10. [Visão geral de consultas elásticas](sql-database-elastic-query-overview.md)
11. [Glossário de ferramentas de banco de dados elástico](sql-database-elastic-scale-glossary.md)
12. [Biblioteca cliente do Banco de Dados Elástico com Entity Framework](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md)
13. [Biblioteca de cliente de banco de dados elástico com Dapper](sql-database-elastic-scale-working-with-dapper.md)
14. [Ferramenta de mesclagem/divisão](sql-database-elastic-scale-overview-split-and-merge.md)
15. [Contadores de desempenho do gerenciador de mapa de fragmentos](sql-database-elastic-database-client-library.md) 
16. [Perguntas frequentes sobre ferramentas de banco de dados elástico](sql-database-elastic-scale-faq.md)

## <a name="client-capabilities"></a>Recursos do cliente
Expansão de aplicativos usando *fragmentação* apresenta desafios para o desenvolvedor hello como administrador Olá. biblioteca de cliente Olá simplifica as tarefas de gerenciamento de saudação fornecendo ferramentas que permitem que desenvolvedores e administradores gerenciam bancos de dados expandido. Um exemplo típico, há muitos bancos de dados, conhecidos como "fragmentos" toomanage. Os clientes são co-localizados no hello mesmo banco de dados, e não há um banco de dados por cliente (um esquema de único Locatário). biblioteca de saudação do cliente inclui os seguintes recursos:

- **Gerenciamento de mapa do fragmento**: um banco de dados especial chamado hello "Gerenciador de mapa do fragmento" é criado. Gerenciamento de mapa do fragmento é a capacidade de saudação para metadados de toomanage um aplicativo sobre seus fragmentos. Os desenvolvedores podem usar bancos de dados de tooregister essa funcionalidade como fragmentos, descrevem os mapeamentos de chaves de fragmentação individuais ou bancos de dados de toothose de intervalos de chaves e manter esses metadados, como número de saudação e composição de bancos de dados evolui tooreflect alterações de capacidade. Sem a biblioteca de cliente do banco de dados Elástico hello, você precisaria toospend muito tempo para escrever o código de gerenciamento de saudação durante a implementação de fragmentação. Para obter mais detalhes, consulte [Gerenciamento de mapa do fragmento](sql-database-elastic-scale-shard-map-management.md).

- **Roteamento dependente de dados**: Imagine uma solicitação chega ao aplicativo hello. Com base no valor de chave de fragmentação Olá da solicitação hello, aplicativo hello precisa toodetermine Olá correto de banco de dados com base no valor de chave de saudação. Ele então abre uma solicitação de saudação de tooprocess do conexão toohello banco de dados. Roteamento dependente de dados fornece a capacidade de saudação conexões tooopen com uma única chamada fácil no mapa do fragmento de saudação do aplicativo hello. Roteamento dependente de dados foi outra área do código de infraestrutura que agora é coberto por funcionalidade na biblioteca de cliente do banco de dados Elástico hello. Para obter mais detalhes, consulte o [Roteamento dependente de dados](sql-database-elastic-scale-data-dependent-routing.md).
- **MSQ (Consulta de vários fragmentos)**: a consulta de vários fragmentos funciona quando uma solicitação envolve vários fragmentos, ou todos eles. Uma consulta de vários fragmento executa Olá mesmo código T-SQL em todos os fragmentos ou um conjunto de fragmentos. resultados de saudação do hello participantes fragmentos são mesclados em um resultado geral definido usando semântica UNION ALL. Conforme exposto pela biblioteca de cliente Olá Olá trata muitas tarefas, incluindo: gerenciamento de conexão, gerenciamento de threads, tratamento de falhas e processar os resultados intermediários. MSQ pode consultar toohundreds de fragmentos. Para obter detalhes, veja [Consulta de vários fragmentos](sql-database-elastic-scale-multishard-querying.md).

Em geral, os clientes usando as ferramentas de banco de dados Elástico podem esperar tooget funcionalidade de T-SQL completa ao enviar as operações de fragmento local como operações de fragmento de toocross contrário que têm suas próprias semânticas.

## <a name="next-steps"></a>Próximas etapas
Tente Olá [aplicativo de exemplo](sql-database-elastic-scale-get-started.md) que demonstra as funções de cliente de saudação. 

biblioteca de saudação tooinstall, ir muito[biblioteca de cliente de banco de dados Elástico](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).

Para obter instruções sobre como usar a ferramenta de mesclagem de divisão Olá, consulte Olá [visão geral da ferramenta de mesclagem de divisão](sql-database-elastic-scale-overview-split-and-merge.md).

[A biblioteca de cliente do banco de dados elástico agora é tem código aberto!](https://azure.microsoft.com/blog/elastic-database-client-library-is-now-open-sourced/)

Use as [Consultas elásticas](sql-database-elastic-query-overview.md).

Olá biblioteca está disponível como software livre em [GitHub](https://github.com/Azure/elastic-db-tools). 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-database-client-library/glossary.png

