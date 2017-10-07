---
title: "aaaLearn sobre as operações do Azure SQL Data Warehouse | Microsoft Docs"
description: "A elasticidade do SQL Data Warehouse permite expandir, reduzir ou pausar o poder da computação usando uma escala deslizante de DWUs (Unidades de Data Warehouse). Este artigo explica as métricas de depósito de dados hello e como elas se relacionam tooDWUs. "
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: cadffa9c-589d-4db7-888a-1f202a753bc5
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 8be5ff6b14ab907e2b0a7eb55e0e2f4139aca8b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="data-warehouse-workload"></a>Carga de trabalho do data warehouse
Uma carga de trabalho do data warehouse refere-se tooall de operações de saudação que ocorrer em um data warehouse. carga de trabalho de depósito de dados Olá abrange todo o processo de carregar dados no warehouse Olá, realização de análises e relatórios no data warehouse de saudação, gerenciamento de dados no data warehouse de saudação e exportando dados do data warehouse de saudação hello. Olá profundidade e abrangência desses componentes são geralmente proporcionais com nível de maturidade da saudação do data warehouse de saudação.

## <a name="new-toodata-warehousing"></a>Novo toodata warehouse?
Um data warehouse é um conjunto de dados que são carregados de um ou mais dados fontes e é usado tooperform tarefas de business intelligence, como relatórios e análise de dados.

Data warehouse é caracterizado por consultas que examinam um número maior de linhas, grandes intervalos de dados e podem retornar resultados relativamente grandes para fins de saudação de análise e emissão de relatórios. Os data warehouses também são caracterizados pelos carregamentos de dados relativamente grandes, em oposição a inserções/atualizações/exclusões pequenas no nível de transação.

* Um data warehouse funciona melhor quando Olá dados são armazenados de forma que otimiza a consultas que precisam tooscan grandes números de linhas ou grandes intervalos de dados. Esse tipo de varredura funciona melhor quando dados saudação são armazenados e pesquisados por colunas, em vez de por linhas.

> [!NOTE]
> índice columnstore na memória, Olá, que usa o armazenamento de coluna, fornece ganhos de compactação too10x e 100 vezes ganhos de desempenho de consulta em árvores de binários tradicionais para consultas de relatórios e análises. Vamos considerar índices columnstore como saudação padrão para armazenar e verificação de dados grandes em um data warehouse.
> 
> 

* Os requisitos de um data warehouse são diferentes dos requisitos de um sistema que é otimizado para OLTP (processamento de transação online). Olá sistema OLTP tem muitas inserir, atualizar e excluir operações. Essas operações de busca toospecific linhas na tabela de saudação. Buscas de tabela têm melhor desempenho quando Olá dados são armazenados em uma maneira de linha por linha. dados de saudação podem ser classificados e rapidamente pesquisados com uma divisão e superar abordagem chamada uma pesquisa binária de árvore ou árvore b.

## <a name="data-loading"></a>Carregamento de dados
Carregamento de dados é uma grande parte da carga de trabalho do hello data warehouse. As empresas geralmente têm um sistema OLTP ocupado que rastreia as alterações ao longo do dia hello quando os clientes estão gerando transações comerciais. Periodicamente, geralmente à noite durante uma janela de manutenção, transações de saudação são movidas ou copiados toohello depósito de dados. Quando dados saudação são Olá data warehouse, analistas podem executar a análise e tomar decisões de negócios em dados de saudação.

* Tradicionalmente, o processo de saudação de carregamento é chamado ETL para extração, transformação e carga. Dados geralmente precisam toobe transformado é consistente com outros dados no data warehouse de saudação. Anteriormente, as empresas usado dedicadas transformações Olá servidores tooperform de ETL. Agora, com esse processamento paralelo rápida em massa, você pode carregar dados no SQL Data Warehouse primeiro e, em seguida, executar transformações de saudação. Esse processo é chamado de extração, carregar e transformar (ELT) e está se tornando um novo padrão de carga de trabalho do hello data warehouse.

> [!NOTE]
> Com o SQL Server 2016, agora você pode realizar a análise em tempo real em uma tabela OLTP. Isso não substitui a necessidade Olá para um toostore de depósito de dados e analisar dados, mas ele fornece uma análise de tooperform de maneira em tempo real.
> 
> 

### <a name="reporting-and-analysis-queries"></a>Consultas de análise e relatórios
As consultas de análise e relatórios muitas vezes são classificadas em pequenas, médias e grandes com base em vários critérios, mas normalmente se baseiam no tempo. Na maioria dos data warehouses, há uma carga de trabalho mista de consultas de execução rápida e execução longa. Em cada caso, é importante toodetermine essa combinação e toodetermine sua frequência (por hora, diariamente, final do mês, trimestre-end e assim por diante). É importante toounderstand que Olá a carga de trabalho de consultas mistas, juntamente com simultaneidade, lead tooproper planejamento de capacidade para um data warehouse.

* Planejamento de capacidade pode ser uma tarefa complexa para uma carga de trabalho de consultas mistas, especialmente quando precisar de um cliente potencial longo tempo tooadd capacidade toohello data warehouse. SQL Data Warehouse remove urgência saudação do planejamento de capacidade, desde que você pode aumentar ou reduzir a capacidade de computação a qualquer momento e, como armazenamento e a capacidade de computação são dimensionados de forma independente.

### <a name="data-management"></a>Gerenciamento de dados
Gerenciamento de dados é importante, especialmente quando você souber a que você poderá ficar sem espaço em disco no hello futuro próximo. Data warehouse geralmente divide dados saudação em intervalos significativos, que são armazenados como partições em uma tabela. Todos os produtos com base em SQL Server permitem mover partições dentro e fora da tabela de saudação. Essa partição alternância permite que você move antigo armazenamento mais econômico tooless de dados e manter dados mais recentes de saudação disponíveis no armazenamento online.

* Os índices columnstore oferecem suporte a tabelas particionadas. Em índices columnstore, as tabelas particionadas são usadas para gerenciamento de dados e arquivamento. Em tabelas armazenadas linha por linha, as partições têm uma função mais importante no desempenho da consulta.  
* O PolyBase desempenha um papel importante no gerenciamento de dados. Usando o PolyBase, você tem tooHadoop tooarchive dados mais antigo opção hello ou armazenamento de BLOBs do Azure.  Isso fornece muitas opções como dados saudação ainda esteja online.  Pode levar mais tempo dados de tooretrieve do Hadoop, mas a compensação de saudação do tempo de recuperação pode sobrecarregar o custo de armazenamento de saudação.

### <a name="exporting-data"></a>Exportando dados
Uma maneira toomake disponíveis para análise e relatórios são toosend dados de Olá tooservers de depósito de dados dedicado para execução de relatórios e análise. Esses servidores são chamados de data marts. Por exemplo, você poderia pré-processar dados de relatório e, em seguida, exportá-lo do servidores Olá data warehouse toomany mundo hello, toomake amplamente disponível para clientes e analistas.

* Para gerar relatórios, todas as noites você pode preencher servidores de relatório somente leitura com um instantâneo dos dados diários hello. Isso fornece maior largura de banda para clientes reduzir as necessidades de recursos de computação Olá no data warehouse de saudação. De um aspecto de segurança, armazéns de dados permitem você tooreduce Olá número de usuários que têm acesso toohello data warehouse do.
* Para análise, você pode criar um cubo de análise no data warehouse do hello e executar a análise no data warehouse do hello, ou pré-processar dados e exportá-lo toohello o servidor de análise para análise adicional.

## <a name="next-steps"></a>Próximas etapas
Agora que você conheça um pouco sobre o SQL Data Warehouse, saiba como tooquickly [criar um SQL Data Warehouse] [ create a SQL Data Warehouse] e [carregar dados de amostra][load sample data].

<!--Image references-->

<!--Article references-->
[load sample data]: ./sql-data-warehouse-load-sample-databases.md
[create a SQL Data Warehouse]: ./sql-data-warehouse-get-started-provision.md

<!--MSDN references-->

<!--Other web references-->
