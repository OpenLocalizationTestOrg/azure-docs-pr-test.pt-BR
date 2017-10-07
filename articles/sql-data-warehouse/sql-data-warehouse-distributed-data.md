---
title: aaaHow distributed data funciona no Azure SQL Data Warehouse | Microsoft Docs
description: "Saiba como os dados são distribuídos para altamente paralela de processamento (MPP) e hello opções de distribuição das tabelas no Azure SQL Data Warehouse e o Parallel Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: bae494a6-7ac5-4c38-8ca3-ab2696c63a9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/12/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 9a712d8d5251e4391ede245105918283aaa4b193
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="distributed-data-and-distributed-tables-for-massively-parallel-processing-mpp"></a>Dados distribuídos e tabelas distribuídas para MPP (Processamento Paralelo Maciço)
Saiba como os dados do usuário são distribuídos no SQL Data Warehouse do Azure e Parallel Data Warehouse, que são os sistemas de MPP (Processamento Paralelo Maciço) da Microsoft. Projetando sua toouse de depósito de dados dados distribuídos efetivamente ajudam você tooachieve Olá processamento de consulta benefícios da saudação arquitetura MPP. Algumas opções de design de banco de dados podem ter um impacto significativo sobre como melhorar o desempenho da consulta.  

> [!NOTE]
> SQL Data Warehouse do Azure e hello de uso do Parallel Data Warehouse mesmo processamento paralelo em massa (MPP) de design, mas têm algumas diferenças devido a saudação plataforma de base. O SQL Data Warehouse é uma PaaS (plataforma como serviço) executada no Azure. Parallel Data Warehouse é executado no APS (sistema de Plataforma de Análise), que é um dispositivo local executado no Windows Server.
> 
> 

## <a name="what-is-distributed-data"></a>O que são dados distribuídos?
No SQL Data Warehouse e o Parallel Data Warehouse, dados distribuídos refere-se toouser dados armazenados em vários locais em Olá sistema MPP. Cada um desses locais funciona como um armazenamento independentes e a unidade de processamento que executa consultas na sua parte dos dados de saudação. Dados distribuídos são fundamental toorunning consultas paralelas tooachieve alto desempenho de consulta.

dados toodistribute, data warehouse de saudação atribui cada linha em uma tabela tooone distribuída de local do usuário.  Você pode distribuir tabelas com um método de distribuição de hash ou um método round robin. método de distribuição Hello é especificado na instrução CREATE TABLE de saudação. 

## <a name="hash-distributed-tables"></a>Tabelas distribuídas em hash
Olá diagrama a seguir ilustra como uma completa (tabela não distribuídos) é armazenada como uma tabela de hash distribuídos. Uma função determinística atribui cada distribuição de tooone toobelong linhas. Definição da tabela hello, uma das colunas de saudação é designada como coluna de distribuição de saudação. função de hash de saudação usa valor Olá Olá distribuição coluna tooassign distribuição de tooa cada linha.

Há considerações de desempenho para seleção de saudação de uma coluna de distribuição, como distinção, distorção de dados e tipos de saudação de consultas executadas no sistema de saudação.

![Tabela distribuída](media/sql-data-warehouse-distributed-data/hash-distributed-table.png "Tabela distribuída")  

* Cada linha pertence tooone distribuição.  
* Um algoritmo de hash determinística atribui cada distribuição tooone de linha.  
* número de Olá das linhas da tabela por distribuição varia conforme mostrado pelos tamanhos diferentes de saudação de tabelas.

## <a name="round-robin-distributed-tables"></a>Tabelas distribuídas round robin
Uma tabela de round-robin distribuída distribui as linhas de saudação atribuindo a distribuição de tooa cada linha de maneira sequencial. São dados tooload rápido em uma tabela de round-robin, mas o desempenho de consulta pode ser mais lento.  Ingressar em uma tabela de round-robin geralmente requer embaralhando Olá linhas tooenable Olá consulta tooproduce um resultado preciso, o que leva tempo.

## <a name="distributed-storage-locations-are-called-distributions"></a>Locais de armazenamento distribuído são chamados de distribuições
Cada local distribuído é chamado de distribuição. Quando uma consulta é executada em paralelo, cada distribuição executa uma consulta SQL em sua parte dos dados de saudação. SQL Data Warehouse usa uma consulta do banco de dados SQL toorun hello. Parallel Data Warehouse usa uma consulta do SQL Server toorun hello. Esse design de arquitetura nada compartilhado é fundamental tooachieving expansão computação paralela.

### <a name="can-i-view-hello-distributions"></a>Exibir distribuições Olá?
Cada distribuição tem uma ID de distribuição e fica visível nas exibições do sistema que pertencem a tooSQL do Data Warehouse e o Parallel Data Warehouse. Você pode usar o desempenho da consulta Olá distribuição ID tootroubleshoot e outros problemas. Para obter uma lista de exibições do sistema hello, consulte Olá [exibição do sistema MPP](sql-data-warehouse-reference-tsql-statements.md).

## <a name="difference-between-a-distribution-and-a-compute-node"></a>Diferença entre uma distribuição e um nó de Computação
Uma distribuição é a unidade básica de saudação para armazenar dados distribuídos e processamento de consultas paralelas. Distribuições são agrupadas em nós de Computação. Cada nó de Computação rastreia uma ou mais distribuições.  

* Analytics Platform System usa nós de computação como um componente central de recursos de hardware Olá arquitetura e expansão. Ele sempre usa oito distribuições por nó de computação, conforme mostrado no diagrama de saudação para tabelas de hash distribuídos. Olá número de nós de computação e hello, portanto, o número de distribuições, é determinado pelo número de saudação de nós de computação de que compra para o dispositivo de saudação. Por exemplo, se você comprar oito nós de Computação, obterá 64 distribuições (oito nós de computação x oito distribuições/nó). 
* O SQL Data Warehouse tem um número fixo de 60 distribuições e um número flexível de nós de Computação. nós de computação Olá são implementadas com recursos de computação e armazenamento do Azure. número de saudação de nós de computação pode alterar cargas de trabalho serviço back-end de acordo toohello e Olá capacidade de computação (DWUs) especificado para o data warehouse de saudação. Quando o número de saudação de nós de computação é alterado, o número de saudação de Distribuições por nó de computação alterações também. 

### <a name="can-i-view-hello-compute-nodes"></a>Exibir nós de computação Olá?
Cada nó de computação tem uma ID de nó e é visível nas exibições do sistema que pertencem a tooSQL do Data Warehouse e o Parallel Data Warehouse.  Você pode ver o nó de computação Olá olhando para a coluna de node_id Olá nas exibições do sistema cujos nomes começam com sys.pdw_nodes. Para obter uma lista de exibições do sistema hello, consulte Olá [exibição do sistema MPP](sql-data-warehouse-reference-tsql-statements.md).

## <a name="Replicated"></a>Tabelas Replicadas
Uma tabela replicada tem um totalmente a cópia da tabela de saudação armazenados em cada nó de computação. Duplicar uma tabela remove os dados de tootransfer de necessidade Olá entre nós de computação antes de uma junção ou agregação. Tabelas replicadas só são viáveis com tabelas pequenas devido a saudação tabela completa do armazenamento extra necessário toostore Olá em cada nó de computação.  

Olá diagrama a seguir mostra uma tabela replicada é armazenada em cada nó de computação. Para o SQL Data Warehouse, tabela replicada Olá é tooa totalmente copiados o banco de dados de distribuição em cada nó de computação. Parallel Data Warehouse, tabela replicada Olá é armazenada em todos os discos atribuídos toohello do nó de computação.  Essa estratégia de disco é implementada usando grupos de arquivos do SQL Server.  

![Tabela replicada](media/sql-data-warehouse-distributed-data/replicated-table.png "Tabela replicada") 

## <a name="next-steps"></a>Próximas etapas
tabelas de toouse distribuído com eficiência, consulte [distribuir tabelas no SQL Data Warehouse](sql-data-warehouse-tables-distribute.md)  

