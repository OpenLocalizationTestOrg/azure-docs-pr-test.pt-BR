---
title: "Lição 8 do tutorial do Azure Analysis Services: criar perspectivas | Microsoft Docs"
description: Descreve como criar perspectivas no projeto de tutorial do Azure Analysis Services.
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
ms.openlocfilehash: 491500909b0de0360afae45e172e85999d764fe0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-8-create-perspectives"></a><span data-ttu-id="f9d4a-103">Lição 8: criar perspectivas</span><span class="sxs-lookup"><span data-stu-id="f9d4a-103">Lesson 8: Create perspectives</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="f9d4a-104">Nesta lição, você criará uma perspectiva de Vendas pela Internet.</span><span class="sxs-lookup"><span data-stu-id="f9d4a-104">In this lesson, you create an Internet Sales perspective.</span></span> <span data-ttu-id="f9d4a-105">Uma perspectiva define um subconjunto exibível de um modelo que fornece pontos de vista concentrados, específicos da empresa ou específicos do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f9d4a-105">A perspective defines a viewable subset of a model that provides focused, business-specific, or application-specific viewpoints.</span></span> <span data-ttu-id="f9d4a-106">Quando um usuário se conecta a um modelo usando uma perspectiva, ele vê apenas os objetos de modelo (tabelas, colunas, medidas, hierarquias e KPIs) como campos definidos nessa perspectiva.</span><span class="sxs-lookup"><span data-stu-id="f9d4a-106">When a user connects to a model by using a perspective, they see only those model objects (tables, columns, measures, hierarchies, and KPIs) as fields defined in that perspective.</span></span> <span data-ttu-id="f9d4a-107">Para saber mais, confira [Perspectivas](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="f9d4a-107">To learn more, see [Perspectives](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span></span>
  
<span data-ttu-id="f9d4a-108">A perspectiva de vendas pela Internet que você criou nesta lição excluirá o objeto de tabela DimCustomer.</span><span class="sxs-lookup"><span data-stu-id="f9d4a-108">The Internet Sales perspective you create in this lesson excludes the DimCustomer table object.</span></span> <span data-ttu-id="f9d4a-109">Quando você cria uma perspectiva que exclui determinados objetos de exibição, esse objeto ainda existe no modelo.</span><span class="sxs-lookup"><span data-stu-id="f9d4a-109">When you create a perspective that excludes certain objects from view, that object still exists in the model.</span></span> <span data-ttu-id="f9d4a-110">No entanto, não é visível em uma lista de campos de cliente de relatório.</span><span class="sxs-lookup"><span data-stu-id="f9d4a-110">However, it is not visible in a reporting client field list.</span></span> <span data-ttu-id="f9d4a-111">Colunas calculadas e medidas incluídas ou não em uma perspectiva ainda podem calcular com base em de dados do objeto excluído.</span><span class="sxs-lookup"><span data-stu-id="f9d4a-111">Calculated columns and measures either included in a perspective or not can still calculate from object data that is excluded.</span></span>  
  
<span data-ttu-id="f9d4a-112">O objetivo desta lição é descrever como criar perspectivas e se familiarizar com ferramentas de criação de modelo tabular.</span><span class="sxs-lookup"><span data-stu-id="f9d4a-112">The purpose of this lesson is to describe how to create perspectives and become familiar with the tabular model authoring tools.</span></span> <span data-ttu-id="f9d4a-113">Se você expandir este modelo para incluir tabelas adicionais posteriormente, você poderá criar perspectivas adicionais para definir diferentes pontos de vista do modelo, por exemplo, Vendas e Inventário.</span><span class="sxs-lookup"><span data-stu-id="f9d4a-113">If you later expand this model to include additional tables, you can create additional perspectives to define different viewpoints of the model, for example, Inventory and Sales.</span></span>  
  
<span data-ttu-id="f9d4a-114">Tempo estimado para a conclusão desta lição: **Cinco minutos**</span><span class="sxs-lookup"><span data-stu-id="f9d4a-114">Estimated time to complete this lesson: **Five minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="f9d4a-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f9d4a-115">Prerequisites</span></span>  
<span data-ttu-id="f9d4a-116">Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem.</span><span class="sxs-lookup"><span data-stu-id="f9d4a-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="f9d4a-117">Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [Lição 7: criar indicadores chave de desempenho](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span><span class="sxs-lookup"><span data-stu-id="f9d4a-117">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  
  
## <a name="create-perspectives"></a><span data-ttu-id="f9d4a-118">Criar perspectivas</span><span class="sxs-lookup"><span data-stu-id="f9d4a-118">Create perspectives</span></span>  
  
#### <a name="to-create-an-internet-sales-perspective"></a><span data-ttu-id="f9d4a-119">Para criar uma perspectiva de Vendas pela Internet</span><span class="sxs-lookup"><span data-stu-id="f9d4a-119">To create an Internet Sales perspective</span></span>  
  
1.  <span data-ttu-id="f9d4a-120">Clique no menu **Modelo** > **Perspectivas** > **Criar e Gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="f9d4a-120">Click the **Model** menu > **Perspectives** > **Create and Manage**.</span></span>  
  
2.  <span data-ttu-id="f9d4a-121">Na caixa de diálogo **Perspectivas**, clique em **Nova Perspectiva**.</span><span class="sxs-lookup"><span data-stu-id="f9d4a-121">In the **Perspectives** dialog box, click **New Perspective**.</span></span>  
  
3.  <span data-ttu-id="f9d4a-122">Clique duas vezes no título de coluna **Nova Perspectiva** e renomeie-o para **Vendas pela Internet**.</span><span class="sxs-lookup"><span data-stu-id="f9d4a-122">Double-click the **New Perspective** column heading, and then rename **Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="f9d4a-123">Selecione todas as tabelas, *exceto* **DimCustomer**.</span><span class="sxs-lookup"><span data-stu-id="f9d4a-123">Select the all the tables *except* **DimCustomer**.</span></span>  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    <span data-ttu-id="f9d4a-125">Em uma lição posterior, você usará o recurso Analisar no Excel para testar essa perspectiva.</span><span class="sxs-lookup"><span data-stu-id="f9d4a-125">In a later lesson, you use the Analyze in Excel feature to test this perspective.</span></span> <span data-ttu-id="f9d4a-126">A Lista de Campos de Tabela Dinâmica do Excel incluirá cada tabela, com exceção da tabela DimCustomer.</span><span class="sxs-lookup"><span data-stu-id="f9d4a-126">The Excel PivotTable Fields List includes each table except the DimCustomer table.</span></span>  

## <a name="whats-next"></a><span data-ttu-id="f9d4a-127">O que vem a seguir?</span><span class="sxs-lookup"><span data-stu-id="f9d4a-127">What's next?</span></span>
<span data-ttu-id="f9d4a-128">[Lição 9: criar hierarquias](../tutorials/aas-lesson-9-create-hierarchies.md).</span><span class="sxs-lookup"><span data-stu-id="f9d4a-128">[Lesson 9: Create hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>
  
  
  
  
