---
title: "AAA \"perspectivas do Azure Analysis Services tutorial lição 8 criar | Microsoft Docs\""
description: "Descreve como perspectivas toocreate em Olá projeto do tutorial do Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: 25391813e1969ecb22af4d6f9c1ccd8358d812fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="lesson-8-create-perspectives"></a>Lição 8: criar perspectivas

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Nesta lição, você criará uma perspectiva de Vendas pela Internet. Uma perspectiva define um subconjunto exibível de um modelo que fornece pontos de vista concentrados, específicos da empresa ou específicos do aplicativo. Quando um usuário se conecta a tooa modelo usando uma perspectiva, eles veem apenas os objetos de modelo (tabelas, colunas, medidas, hierarquias e KPIs) como campos definidos nessa perspectiva. mais, consulte toolearn [perspectivas](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).
  
Olá perspectiva de vendas pela Internet criado nesta lição exclui o objeto de tabela DimCustomer hello. Quando você cria uma perspectiva que exclui determinados objetos de exibição, esse objeto ainda existe no modelo de saudação. No entanto, não é visível em uma lista de campos de cliente de relatório. Colunas calculadas e medidas incluídas ou não em uma perspectiva ainda podem calcular com base em de dados do objeto excluído.  
  
Olá finalidade desta lição é toodescribe como toocreate perspectivas e se familiarizar com o modelo de tabela Olá ferramentas de criação. Se expandir este modelo tooinclude tabelas mais tarde, você pode criar perspectivas adicionais toodefine diferentes pontos de vista do modelo hello, por exemplo, inventário e vendas.  
  
Estimado tempo toocomplete nesta lição: **cinco minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem. Antes de executar tarefas de saudação nesta lição, você deverá ter completado lição anterior Olá: [lição 7: criar indicadores chave de desempenho](../tutorials/aas-lesson-7-create-key-performance-indicators.md).  
  
## <a name="create-perspectives"></a>Criar perspectivas  
  
#### <a name="toocreate-an-internet-sales-perspective"></a>toocreate uma perspectiva de vendas pela Internet  
  
1.  Clique em Olá **modelo** menu > **perspectivas** > **criar e gerenciar**.  
  
2.  Em Olá **perspectivas** caixa de diálogo, clique em **nova perspectiva**.  
  
3.  Clique duas vezes em Olá **nova perspectiva** título de coluna e, em seguida, renomeie **vendas pela Internet**.  
  
4.  Selecione Olá todas as tabelas de saudação *exceto* **DimCustomer**.  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    Em uma lição posterior, você usa Olá analisar no Excel recurso tootest essa perspectiva. Olá lista de campos de tabela dinâmica do Excel inclui cada tabela exceto tabela DimCustomer de saudação.  

## <a name="whats-next"></a>O que vem a seguir?
[Lição 9: criar hierarquias](../tutorials/aas-lesson-9-create-hierarchies.md).
  
  
  
  
