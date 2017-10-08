---
title: "recomendações de desempenho de Supervisor aaaAzure | Microsoft Docs"
description: "Use o Supervisor de desempenho de saudação toooptimize das implantações do Azure."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: eb3d928664717f6f322132ac740f42015f56b76e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-performance-recommendations"></a>Recomendações de desempenho do Advisor

Recomendações de desempenho de Supervisor do Azure ajudam a melhorar a velocidade de saudação e capacidade de resposta de seus aplicativos essenciais aos negócios. Você pode obter recomendações de desempenho do Advisor em Olá **desempenho** Olá Advisor painel.

![guia Desempenho do Advisor](./media/advisor-performance-recommendations/advisor-performance-tab.png)

## <a name="improve-database-performance-with-sql-db-advisor"></a>Melhorar o desempenho do banco de dados com o Assistente do BD SQL

O Advisor fornece uma exibição consistente e consolidada de recomendações para todos os seus recursos do Azure. Ele se integra ao Supervisor de banco de dados do SQL toobring você recomendações para melhorar o desempenho de saudação do banco de dados do SQL Azure. Orientador de banco de dados do SQL avalia o desempenho de saudação de seus bancos de dados do SQL Azure analisando seu histórico de uso. Em seguida, oferece recomendações mais adequados para executar a carga de trabalho normal do banco de dados da saudação. 

> [!NOTE]
> recomendações de tooget, um banco de dados deve ter aproximadamente uma semana de uso e dentro dessa semana deve haver alguma atividade consistente. O Assistente do Banco de Dados SQL pode ser otimizado com mais facilidade para padrões de consulta consistentes do que para intermitências irregulares de atividade.

Para obter mais informações sobre o Assistente do Banco de Dados SQL, consulte [Assistente do Banco de Dados SQL](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).

![Recomendações do banco de dados SQL](./media/advisor-performance-recommendations/advisor-performance-sql.png)

## <a name="improve-redis-cache-performance-and-reliability"></a>Melhorar o desempenho e a confiabilidade do Cache Redis

O Assistente identifica as instâncias do Cache Redis nas quais o desempenho pode ser prejudicado por alto uso de memória, carga do servidor, largura de banda da rede ou grande número de conexões de cliente. O Advisor também fornece melhores práticas recomendações toohelp evitar possíveis problemas. Para saber mais sobre recomendações do Cache Redis, veja [Advisor do Cache Redis](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).


## <a name="improve-app-service-performance-and-reliability"></a>Melhorar o desempenho e a confiabilidade do Serviço de Aplicativo

O Azure Advisor integra as práticas recomendadas para melhorar sua experiência com os Serviços de Aplicativos e descobrir recursos relevantes de plataforma. Os exemplos de recomendações dos Serviços de Aplicativos são:
* Detecção de instâncias nas quais os recursos de memória ou de CPU são esgotados por tempos de execução de aplicativo com opções de mitigação.
* Detecção de instâncias nas quais a disposição de recursos como aplicativos Web e bancos de dados pode melhorar o desempenho e reduzir custos. 

Para saber mais sobre recomendações de Serviços de Aplicativos, veja [Práticas recomendadas para o Serviço de Aplicativo do Azure](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).
![Recomendações dos Serviços de Aplicativos](./media/advisor-performance-recommendations/advisor-performance-app-service.png)

## <a name="how-tooaccess-performance-recommendations-in-advisor"></a>Como tooaccess recomendações de desempenho Advisor

1. Entrar toohello [portal do Azure](https://portal.azure.com).

2. No painel esquerdo do hello, clique em **mais serviços**.

3. Em Olá serviço painel de menu em **monitoramento e gerenciamento**, clique em **Advisor Azure**.  
 Olá Advisor painel é exibido.

4. No painel do Advisor hello, clique em Olá **desempenho** guia.

5. Selecione a assinatura Olá para o qual você deseja tooreceive recomendações e, em seguida, clique em **obter recomendações**.

> [!NOTE]
> tooaccess as recomendações do Advisor, você deve primeiro *registrar sua assinatura* com o Supervisor. Uma assinatura é registrada quando um *assinatura proprietário* inicia Olá Olá de painel de controle e clica Advisor **obter recomendações** botão. Essa é uma *operação única*. Depois de Olá assinatura está registrada, você pode acessar as recomendações do Advisor como *proprietário*, *Colaborador*, ou *leitor* para uma assinatura de um grupo de recursos, ou um recurso específico.

## <a name="next-steps"></a>Próximas etapas

toolearn mais informações sobre recomendações do Advisor, consulte:

* [Introdução tooAdvisor](advisor-overview.md)
* [Introdução ao Advisor](advisor-get-started.md)
* [Recomendações de custo do Advisor](advisor-performance-recommendations.md)
* [Recomendações de alta disponibilidade do Advisor](advisor-high-availability-recommendations.md)
* [Recomendações de segurança do Advisor](advisor-security-recommendations.md)

