---
title: "recomendações do Advisor custo aaaAzure | Microsoft Docs"
description: "Use o custo de saudação do Azure Advisor toooptimize das implantações do Azure."
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
ms.openlocfilehash: 50f70c33a17f550c8753795435cdfddd51e409f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-cost-recommendations"></a>Recomendações de custo do Advisor

O Advisor ajuda você a otimizar e a reduzir seus gastos gerais com o Azure, identificando recursos ociosos e subutilizados. Você pode obter as recomendações de saudação custo **custo** guia no painel de Supervisor hello.

![Guia Custo do Assistente](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a>Otimizar o gasto da máquina virtual redimensionando instâncias subutilizadas 
Embora determinados cenários de aplicativo podem resultar em baixa utilização por design, você geralmente pode economizar dinheiro, gerenciando o tamanho de saudação e número de máquinas virtuais. O Assistente monitora o uso da máquina virtual durante 14 dias e, depois, identifica as máquinas virtuais com baixa utilização. As máquinas virtuais cuja utilização da CPU é de 5% ou menos e cujo uso de rede é de 7 MB ou menos durante quatro ou mais dias são consideradas máquinas virtuais de baixa utilização.

Mostra Advisor Olá custo estimado de continuar toorun sua máquina virtual, para que você possa escolher tooshut-para baixo ou redimensioná-la.  

![Recomendações de custo do Advisor para redimensionamento de máquinas virtuais](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-toomanage-performance-goals-of-multiple-sql-databases"></a>Use as metas de desempenho de toomanage uma solução econômica de vários bancos de dados SQL
O Advisor identifica as instâncias do SQL Server que podem se beneficiar da criação de pools de banco de dados elástico. Pools de banco de dados Elástico fornecem uma solução simples e econômica toomanage metas de desempenho de saudação de vários bancos de dados que têm vários padrões de uso. Para obter mais informações sobre os pools elásticos do Azure, consulte [O que é um pool elástico do Azure?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).

![Recomendações de custo do Advisor para pools de banco de dados elástico](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-tooaccess-cost-recommendations-in-azure-advisor"></a>Como tooaccess custo recomendações do Advisor do Azure

1. Entrar toohello [portal do Azure](https://portal.azure.com).

2. No painel esquerdo do hello, clique em **mais serviços**.

3. Em Olá serviço painel de menu em **monitoramento e gerenciamento**, clique em **Advisor Azure**.  
 Olá Advisor painel é exibido.

4. No painel do Advisor hello, clique em Olá **custo** guia.

5. Selecione a assinatura Olá para o qual você deseja tooreceive recomendações e, em seguida, clique em **obter recomendações**.

> [!NOTE]
> tooaccess as recomendações do Advisor, você deve primeiro *registrar sua assinatura* com o Supervisor. Uma assinatura é registrada quando um *assinatura proprietário* inicia Olá Olá de painel de controle e clica Advisor **obter recomendações** botão. Essa é uma *operação única*. Depois de Olá assinatura está registrada, você pode acessar as recomendações do Advisor como *proprietário*, *Colaborador*, ou *leitor* para uma assinatura de um grupo de recursos, ou um recurso específico.

## <a name="next-steps"></a>Próximas etapas

toolearn mais informações sobre recomendações do Advisor, consulte:
* [Introdução tooAdvisor](advisor-overview.md)
* [Introdução](advisor-get-started.md)
* [Recomendações de desempenho do Advisor](advisor-cost-recommendations.md)
* [Recomendações de alta disponibilidade do Advisor](advisor-cost-recommendations.md)
* [Recomendações de segurança do Advisor](advisor-cost-recommendations.md)
