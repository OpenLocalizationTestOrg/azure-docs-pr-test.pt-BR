---
title: desempenho aaaTroubleshoot problemas e otimizar seu banco de dados | Microsoft Docs
description: "Aplicar as recomendações de desempenho tooyour banco de dados SQL, bem como limpar como toogain insights sobre Olá desempenho das consultas de saudação em execução no banco de dados"
metakeywords: azure sql database performance monitoring recommendation
services: sql-database
documentationcenter: 
manager: jhubbard
author: jan-eng
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,monitor & tune
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: janeng
ms.openlocfilehash: e948d30ac74eecf45420d5d77ef55e3c0b6f3f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-performance-issues-and-optimize-your-database"></a>Solucionar problemas de desempenho e otimizar seu banco de dados

Índices ausentes e consultas precárias são motivos comuns de um desempenho ruim do banco de dados. Neste tutorial, você aprenderá a:
> [!div class="checklist"]
> * Revisar, aplicar e reverter recomendações de melhoria de desempenho
> * Localizar consultas com alta utilização de recursos
> * Localizar consultas de longa execução

> Você precisa de uma carga de trabalho contínua no banco de dados com problemas de desempenho – um tooreceive por exemplo uma recomendação de índice ausente.
>

## <a name="log-in-toohello-azure-portal"></a>Faça logon no toohello portal do Azure

Faça logon no toohello [portal do Azure](https://portal.azure.com/).

## <a name="review-and-apply-a-recommendation"></a>Examinar e aplicar uma recomendação

Siga essas etapas tooapply uma recomendação do sistema de saudação do banco de dados:

1. Clique em Olá **recomendações de desempenho** menu na folha do banco de dados de saudação.

    ![recomendação de desempenho](./media/sql-database-performance-tutorial/perf_recommendations.png)

2. Na lista de saudação de recomendações, selecione uma recomendação de ativa. Neste exemplo, Create Index.

    ![selecionar recomendação](./media/sql-database-performance-tutorial/create_index.png)

3. Aplicar a recomendação de saudação clicando Olá **aplicar** botão. Opcionalmente, revise os detalhes de recomendação de saudação e consulte o script hello T-SQL muito a ser executado, basta clicar em **Exibir Script** botão.

    ![aplicar recomendação](./media/sql-database-performance-tutorial/apply.png)

4. [Opcional] Habilite o ajuste automático para recomendações toobe aplicada automaticamente.

    ![auto ajuste](./media/sql-database-performance-tutorial/auto_tuning.png)

## <a name="revert-a-recommendation"></a>Reverter uma recomendação

Olá Database Advisor monitora cada recomendação implementada. Se uma recomendação não melhorar a carga de trabalho hello, ele será revertido automaticamente. É possível reverter manualmente uma recomendação, mas isso não será necessário na maioria dos casos. toorevert uma recomendação:

1. Acesse o menu de recomendações de desempenho de toohello e selecione uma das recomendações de saudação aplicada.

    ![selecionar recomendação](./media/sql-database-performance-tutorial/select.png)

2. Na exibição de detalhes de saudação, clique em **Revert**.

    ![reverter recomendação](./media/sql-database-performance-tutorial/revert.png)

## <a name="find-hello-query-that-consumes-hello-most-resources"></a>Localizar a maioria dos recursos de consulta de saudação que consome Olá

Siga essas consultas de saudação etapas toofind consumindo Olá a maioria dos recursos:

1. Clique em Olá **Query Performance Insight** menu na folha do banco de dados de saudação.

    ![informações de consulta](./media/sql-database-performance-tutorial/query_perf_insights.png)

2. Selecionar um tipo de recurso.

    ![informações de consulta](./media/sql-database-performance-tutorial/select_resource_type.png)

3. Primeira consulta na tabela Olá Olá Select.

    ![informações de consulta](./media/sql-database-performance-tutorial/select_query.png)

4. Examine os detalhes da consulta de saudação.

    ![informações de consulta](./media/sql-database-performance-tutorial/query_details.png)

## <a name="find-hello-longest-running-query"></a>Localizar a consulta de execução mais longa Olá

1. Vá tooQuery Performance Insight e selecione Olá **consultas de longa execução** guia.

    ![informações de consulta](./media/sql-database-performance-tutorial/long_running.png)

3. Primeira consulta na tabela Olá Olá Select.

    ![informações de consulta](./media/sql-database-performance-tutorial/select_first_query.png)

4. Examine os detalhes da consulta de saudação.

    ![informações de consulta](./media/sql-database-performance-tutorial/review_query_details.png)



## <a name="next-steps"></a>Próximas etapas 
Índices ausentes e consultas precárias são motivos comuns de um desempenho ruim do banco de dados. Neste tutorial, você aprendeu a:
> [!div class="checklist"]
> * Revisar, aplicar e reverter recomendações de melhoria de desempenho
> * Localizar consultas com alta utilização de recursos
> * Localizar consultas de longa execução

[Dicas de ajuste de desempenho do Banco de Dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-performance)
