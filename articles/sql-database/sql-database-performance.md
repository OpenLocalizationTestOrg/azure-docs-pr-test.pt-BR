---
title: aaaMonitor e melhorar o desempenho - banco de dados do SQL Azure | Microsoft Docs
description: "saudação de que banco de dados SQL do Azure fornece desempenho ferramentas toohelp identificar áreas que podem melhorar o desempenho da consulta atual."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: a60b75ac-cf27-4d73-8322-ee4d4c448aa2
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2016
ms.author: sstein
ms.openlocfilehash: 84b8a1bc62698a29deb49e765f208bd7e14d0870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-improve-performance"></a>Monitorar e melhorar o desempenho
O Banco de Dados SQL do Azure identifica possíveis problemas em seu banco de dados e recomenda ações que podem melhorar o desempenho de sua carga de trabalho, fornecendo ações de ajuste inteligente e recomendações.

tooreview o desempenho do banco de dados, use Olá **desempenho** lado a lado na página de visão geral de saudação ou navegue para baixo demais "Suporte + solução de problemas" seção:

   ![Exibir Desempenho](./media/sql-database-performance/entries.png)

Na seção hello "Suporte + solução de problemas", você pode usar o hello páginas a seguir:


1. [Visão geral do desempenho](#performance-overview) toomonitor o desempenho do banco de dados. 
2. [Recomendações de desempenho](#performance-recommendations) toofind recomendações de desempenho que podem melhorar o desempenho da carga de trabalho.
3. [Análise de desempenho de consulta](#query-performance-insight) toofind principais consultas de consumo.
4. [Ajuste automático](#automatic-tuning) toolet banco de dados do SQL Azure automaticamente otimizar seu banco de dados.

## <a name="performance-overview"></a>Visão geral do desempenho
Essa exibição fornece um resumo do desempenho de seu banco de dados e lhe ajudará com ajustes e solução de problemas de desempenho. 

![Desempenho](./media/sql-database-performance/performance.png)

* Olá **recomendações** lado a lado fornece uma análise de ajuste recomendações para seu banco de dados (a três principais recomendações são mostradas se há mais). Ao clicar nesse bloco você irá muito**[recomendações de desempenho](#performance-recommendations)**. 
* Olá **ajuste atividade** lado a lado fornece um resumo da saudação em andamento e concluída ajuste ações para o banco de dados, dando a você uma exibição rápida no histórico de saudação do ajuste de atividade. Clicar nesse bloco leva você toohello completo ajuste o modo de exibição de histórico para seu banco de dados.
* Olá **auto-ajuste** bloco mostra Olá [autoajuste da configuração](sql-database-automatic-tuning-enable.md) para seu banco de dados (ajuste opções tooyour aplicadas automaticamente no banco de dados). Clicar neste bloco abre a caixa de diálogo de configuração de automação hello.
* Olá **consultas de banco de dados** bloco mostra Olá resumo de desempenho de consulta de saudação do banco de dados (geral DTU uso e principais consultas de consumo). Ao clicar nesse bloco você irá muito**[Query Performance Insight](#query-performance-insight)**.

## <a name="performance-recommendations"></a>Recomendações do desempenho
Esta página fornece [recomendações de ajuste](sql-database-advisor.md) inteligente que podem melhorar o desempenho do banco de dados. Olá tipos das recomendações a seguir é mostrado nesta página:

* Recomendações sobre quais índices toocreate ou drop.
* Recomendações quando problemas de esquema são identificados no banco de dados de saudação.
* Recomendações quando consultas podem se beneficiar de consultas parametrizadas.

![Desempenho](./media/sql-database-performance/recommendations.png)

Você também pode encontrar o histórico completo de ajuste de ações que foram aplicadas no hello anterior.

Saiba como toofind um aplicar recomendações de desempenho [localizar e aplicar recomendações de desempenho](sql-database-advisor-portal.md) artigo.

## <a name="automatic-tuning"></a>Ajuste automático
O Bancos de Dados SQL do Azure pode ajustar o desempenho do banco de dados automaticamente, aplicando as [recomendações de desempenho](sql-database-advisor.md). mais, leia toolearn [artigo ajuste automático](sql-database-automatic-tuning.md). tooenable, ler [como o ajuste automático tooenable](sql-database-automatic-tuning-enable.md).

## <a name="query-performance-insight"></a>Análise de desempenho de consultas
[Análise de desempenho de consulta](sql-database-query-performance.md) permite que você toospend menos tempo Solucionando problemas de desempenho de banco de dados, fornecendo:

* Mais informações sobre o consumo de recursos de bancos de dados (DTU). 
* Olá principais consumidores de CPU consultas, que potencialmente podem ser ajustadas para melhorar o desempenho. 
* Olá toodrill de capacidade para baixo em detalhes de saudação de uma consulta. 

  ![painel de desempenho](./media/sql-database-query-performance/performance.png)

Encontre mais informações sobre esta página no artigo Olá  **[como toouse Query Performance Insight](sql-database-query-performance.md)**.

## <a name="additional-resources"></a>Recursos adicionais
* [Diretrizes de desempenho do Banco de Dados SQL do Azure para bancos de dados únicos](sql-database-performance-guidance.md)
* [Quando um pool elástico deve ser usado?](sql-database-elastic-pool-guidance.md)

