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
# <a name="lesson-8-create-perspectives"></a><span data-ttu-id="12a00-103">Lição 8: criar perspectivas</span><span class="sxs-lookup"><span data-stu-id="12a00-103">Lesson 8: Create perspectives</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="12a00-104">Nesta lição, você criará uma perspectiva de Vendas pela Internet.</span><span class="sxs-lookup"><span data-stu-id="12a00-104">In this lesson, you create an Internet Sales perspective.</span></span> <span data-ttu-id="12a00-105">Uma perspectiva define um subconjunto exibível de um modelo que fornece pontos de vista concentrados, específicos da empresa ou específicos do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="12a00-105">A perspective defines a viewable subset of a model that provides focused, business-specific, or application-specific viewpoints.</span></span> <span data-ttu-id="12a00-106">Quando um usuário se conecta a tooa modelo usando uma perspectiva, eles veem apenas os objetos de modelo (tabelas, colunas, medidas, hierarquias e KPIs) como campos definidos nessa perspectiva.</span><span class="sxs-lookup"><span data-stu-id="12a00-106">When a user connects tooa model by using a perspective, they see only those model objects (tables, columns, measures, hierarchies, and KPIs) as fields defined in that perspective.</span></span> <span data-ttu-id="12a00-107">mais, consulte toolearn [perspectivas](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="12a00-107">toolearn more, see [Perspectives](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span></span>
  
<span data-ttu-id="12a00-108">Olá perspectiva de vendas pela Internet criado nesta lição exclui o objeto de tabela DimCustomer hello.</span><span class="sxs-lookup"><span data-stu-id="12a00-108">hello Internet Sales perspective you create in this lesson excludes hello DimCustomer table object.</span></span> <span data-ttu-id="12a00-109">Quando você cria uma perspectiva que exclui determinados objetos de exibição, esse objeto ainda existe no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="12a00-109">When you create a perspective that excludes certain objects from view, that object still exists in hello model.</span></span> <span data-ttu-id="12a00-110">No entanto, não é visível em uma lista de campos de cliente de relatório.</span><span class="sxs-lookup"><span data-stu-id="12a00-110">However, it is not visible in a reporting client field list.</span></span> <span data-ttu-id="12a00-111">Colunas calculadas e medidas incluídas ou não em uma perspectiva ainda podem calcular com base em de dados do objeto excluído.</span><span class="sxs-lookup"><span data-stu-id="12a00-111">Calculated columns and measures either included in a perspective or not can still calculate from object data that is excluded.</span></span>  
  
<span data-ttu-id="12a00-112">Olá finalidade desta lição é toodescribe como toocreate perspectivas e se familiarizar com o modelo de tabela Olá ferramentas de criação.</span><span class="sxs-lookup"><span data-stu-id="12a00-112">hello purpose of this lesson is toodescribe how toocreate perspectives and become familiar with hello tabular model authoring tools.</span></span> <span data-ttu-id="12a00-113">Se expandir este modelo tooinclude tabelas mais tarde, você pode criar perspectivas adicionais toodefine diferentes pontos de vista do modelo hello, por exemplo, inventário e vendas.</span><span class="sxs-lookup"><span data-stu-id="12a00-113">If you later expand this model tooinclude additional tables, you can create additional perspectives toodefine different viewpoints of hello model, for example, Inventory and Sales.</span></span>  
  
<span data-ttu-id="12a00-114">Estimado tempo toocomplete nesta lição: **cinco minutos**</span><span class="sxs-lookup"><span data-stu-id="12a00-114">Estimated time toocomplete this lesson: **Five minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="12a00-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="12a00-115">Prerequisites</span></span>  
<span data-ttu-id="12a00-116">Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem.</span><span class="sxs-lookup"><span data-stu-id="12a00-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="12a00-117">Antes de executar tarefas de saudação nesta lição, você deverá ter completado lição anterior Olá: [lição 7: criar indicadores chave de desempenho](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span><span class="sxs-lookup"><span data-stu-id="12a00-117">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  
  
## <a name="create-perspectives"></a><span data-ttu-id="12a00-118">Criar perspectivas</span><span class="sxs-lookup"><span data-stu-id="12a00-118">Create perspectives</span></span>  
  
#### <a name="toocreate-an-internet-sales-perspective"></a><span data-ttu-id="12a00-119">toocreate uma perspectiva de vendas pela Internet</span><span class="sxs-lookup"><span data-stu-id="12a00-119">toocreate an Internet Sales perspective</span></span>  
  
1.  <span data-ttu-id="12a00-120">Clique em Olá **modelo** menu > **perspectivas** > **criar e gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="12a00-120">Click hello **Model** menu > **Perspectives** > **Create and Manage**.</span></span>  
  
2.  <span data-ttu-id="12a00-121">Em Olá **perspectivas** caixa de diálogo, clique em **nova perspectiva**.</span><span class="sxs-lookup"><span data-stu-id="12a00-121">In hello **Perspectives** dialog box, click **New Perspective**.</span></span>  
  
3.  <span data-ttu-id="12a00-122">Clique duas vezes em Olá **nova perspectiva** título de coluna e, em seguida, renomeie **vendas pela Internet**.</span><span class="sxs-lookup"><span data-stu-id="12a00-122">Double-click hello **New Perspective** column heading, and then rename **Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="12a00-123">Selecione Olá todas as tabelas de saudação *exceto* **DimCustomer**.</span><span class="sxs-lookup"><span data-stu-id="12a00-123">Select hello all hello tables *except* **DimCustomer**.</span></span>  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    <span data-ttu-id="12a00-125">Em uma lição posterior, você usa Olá analisar no Excel recurso tootest essa perspectiva.</span><span class="sxs-lookup"><span data-stu-id="12a00-125">In a later lesson, you use hello Analyze in Excel feature tootest this perspective.</span></span> <span data-ttu-id="12a00-126">Olá lista de campos de tabela dinâmica do Excel inclui cada tabela exceto tabela DimCustomer de saudação.</span><span class="sxs-lookup"><span data-stu-id="12a00-126">hello Excel PivotTable Fields List includes each table except hello DimCustomer table.</span></span>  

## <a name="whats-next"></a><span data-ttu-id="12a00-127">O que vem a seguir?</span><span class="sxs-lookup"><span data-stu-id="12a00-127">What's next?</span></span>
<span data-ttu-id="12a00-128">[Lição 9: criar hierarquias](../tutorials/aas-lesson-9-create-hierarchies.md).</span><span class="sxs-lookup"><span data-stu-id="12a00-128">[Lesson 9: Create hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>
  
  
  
  
