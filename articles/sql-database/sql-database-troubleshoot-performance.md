---
title: aaaMonitoring & ajuste de desempenho - banco de dados do SQL Azure | Microsoft Docs
description: "Dicas de ajuste de desempenho no Banco de Dados SQL por meio de avaliação e melhoria."
services: sql-database
documentationcenter: 
author: v-shysun
manager: felixwu
editor: 
keywords: ajuste de desempenho de sql, ajuste de desempenho de banco de dados, dicas de ajuste de desempenho do sql, ajuste de desempenho de banco de dados sql
ms.assetid: eb7b3f66-3b33-4e1b-84fb-424a928a6672
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: v-shysun
ms.openlocfilehash: 9e196831902aa6ea841ef14caf5713e82ebfc62d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-performance-tuning"></a>Monitoramento e ajuste de desempenho

Banco de dados do SQL Azure é gerenciado automaticamente e recomendações que podem melhorar o desempenho do banco de dados, ou permitir que o banco de dados se adaptar a carga de trabalho tooyour de localização do serviço de dados flexível, onde você pode facilmente monitorar o uso, adicionar ou remover recursos (CPU, memória, e/s), e Otimize o desempenho automaticamente.

Este artigo fornece uma visão geral das opções de monitoramento e ajuste de desempenho disponíveis no Banco de Dados SQL do Azure.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="monitoring-and-troubleshooting-database-performance"></a>Monitorando e solucionando problemas de desempenho do banco de dados

Habilita banco de dados SQL do Azure tooeasily você monitorar o uso do banco de dados e identificar as consultas que podem causar problemas de desempenho de saudação. Monitore o desempenho do banco de dados usando o portal do Azure ou exibições do sistema. Você tem Olá opções para monitorar e solucionar problemas de desempenho do banco de dados a seguir:

1. Em Olá [portal do Azure](https://portal.azure.com), clique em **bancos de dados SQL**, selecione o banco de dados de saudação e, em seguida, usar Olá toolook de gráfico de monitoramento de recursos se aproximando o máximo. O consumo de DTU é exibido por padrão. Clique em **editar** toochange Olá intervalo de tempo e os valores mostrados.
2. Use [Query Performance Insight](sql-database-query-performance.md) consultas Olá tooidentify gastam hello mais recursos.
3. Você pode usar exibições de gerenciamento dinâmico (DMVs), eventos estendidos (`XEvents`), e Olá repositório de consultas em parâmetros de desempenho do SSMS tooget em tempo real.

Consulte Olá [tópico do guia de desempenho](sql-database-performance-guidance.md) toofind técnicas que você pode usar tooimprove o desempenho do banco de dados do SQL Azure se identificar algum problema ao usar esses relatórios ou modos de exibição.

> [!IMPORTANT] 
> É recomendável que você sempre use Olá versão mais recente do Management Studio tooremain sincronizado com atualizações tooMicrosoft Azure e banco de dados SQL. [Atualizar o SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
>

## <a name="optimize-database-tooimprove-performance"></a>Otimizar o desempenho do banco de dados tooimprove

Banco de dados SQL do Azure permite que você tooidentify oportunidades tooimprove e otimizar o desempenho de consulta sem alterar recursos revisando [recomendações de ajuste de desempenho](sql-database-advisor.md). Índices ausentes e consultas precárias são motivos comuns de um desempenho ruim do banco de dados. Você pode aplicar essas ajuste recomendações tooimprove de desempenho da carga de trabalho.
Você também pode permitir que banco de dados do SQL Azure muito[automaticamente otimizar o desempenho de suas consultas](sql-database-automatic-tuning.md) aplicando todas identificadas recomendações e verificar que melhoram o desempenho do banco de dados. Você pode usar o hello desempenho de tooimprove de opções do banco de dados a seguir:

1. Use [orientador de banco de dados SQL](sql-database-advisor-portal.md) tooview recomendações para criar e descartar índices, parametrizando consultas e corrigir problemas de esquema.
2. [Habilite o ajuste automático](sql-database-automatic-tuning-enable.md) e permita que o banco de dados SQL do Azure corrija os problemas de desempenho identificados automaticamente.

## <a name="improving-database-performance-with-more-resources"></a>Melhorando o desempenho do banco de dados com mais recursos

Por fim, se não houver nenhum item acionáveis que pode melhorar o desempenho do banco de dados, você pode alterar a quantidade Olá dos recursos disponíveis no banco de dados do SQL Azure. Você pode atribuir mais recursos alterando Olá [camada de serviço](sql-database-service-tiers.md) de independente do banco de dados ou aumentar o eDTUs de saudação de um pool Elástico a qualquer momento.
1. Para bancos de dados independentes, você pode [alterar as camadas de serviço](sql-database-service-tiers.md) sob demanda tooimprove desempenho de banco de dados.
2. Vários bancos de dados, considere o uso de [pools Elásticos](sql-database-elastic-pool-guidance.md) tooscale recursos automaticamente.

## <a name="tune-and-refactor-application-or-database-code"></a>Ajustar e refatorar o código do aplicativo ou do banco de dados

Você pode alterar toomore de código do aplicativo de maneira ideal usar Olá banco de dados, alterar índices, impor planos ou usar dicas de toomanually se adaptar a carga de trabalho de tooyour de banco de dados hello. Localizar algumas diretrizes e dicas para o ajuste manual e reescrever código Olá Olá [tópico do guia de desempenho](sql-database-performance-guidance.md) artigo.


## <a name="next-steps"></a>Próximas etapas

- tooenable automático de ajuste no banco de dados do SQL Azure e permita automática totalmente o recurso de ajuste gerenciar sua carga de trabalho, consulte [Ativar ajuste automático](sql-database-automatic-tuning-enable.md).
- ajuste manual toouse, você pode examinar [recomendações no portal do Azure de ajuste](sql-database-advisor-portal.md) e aplicar manualmente Olá aqueles que melhoram o desempenho de suas consultas.
- Altere os recursos que estão disponíveis no banco de dados alterando as [camadas de serviço do Banco de Dados SQL do Azure](sql-database-performance-guidance.md)