---
<span data-ttu-id="ef5fa-101">título: aaa "lição do tutorial do Azure Analysis Services 9: criar hierarquias | Descrição de Microsoft Docs": serviços: documentationcenter do analysis services: ' autor: manager minewiskan: erikre editor: ' marcas: '</span><span class="sxs-lookup"><span data-stu-id="ef5fa-101">title: aaa"Azure Analysis Services tutorial lesson 9: Create hierarchies | Microsoft Docs" description: services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="ef5fa-102">MS. AssetID: MS. Service: MS. devlang do analysis services: NA MS. Topic: get-started-article tgt_pltfrm: NA Workload: MS. Date na: 26/05/2017 Author: owend</span><span class="sxs-lookup"><span data-stu-id="ef5fa-102">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-9-create-hierarchies"></a><span data-ttu-id="ef5fa-103">Lição 9: criar hierarquias</span><span class="sxs-lookup"><span data-stu-id="ef5fa-103">Lesson 9: Create hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="ef5fa-104">Nesta lição, você cria hierarquias.</span><span class="sxs-lookup"><span data-stu-id="ef5fa-104">In this lesson, you create hierarchies.</span></span> <span data-ttu-id="ef5fa-105">As hierarquias são grupos de colunas organizados em níveis. Por exemplo, uma hierarquia de Geografia pode ter subníveis para País, Estado, Região e Cidade.</span><span class="sxs-lookup"><span data-stu-id="ef5fa-105">Hierarchies are groups of columns arranged in levels; for example, a Geography hierarchy might have sublevels for Country, State, County, and City.</span></span> <span data-ttu-id="ef5fa-106">Hierarquias podem parecer separadas de outras colunas em uma lista de campos de aplicativo cliente relatório, tornando mais fácil para o cliente toonavigate usuários e incluir em um relatório.</span><span class="sxs-lookup"><span data-stu-id="ef5fa-106">Hierarchies can appear separate from other columns in a reporting client application field list, making them easier for client users toonavigate and include in a report.</span></span> <span data-ttu-id="ef5fa-107">toolearn mais, consulte [hierarquias](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span><span class="sxs-lookup"><span data-stu-id="ef5fa-107">toolearn more, see [Hierarchies](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span></span>
  
<span data-ttu-id="ef5fa-108">hierarquias toocreate, use o designer de modelo Olá no *exibição de diagrama*.</span><span class="sxs-lookup"><span data-stu-id="ef5fa-108">toocreate hierarchies, use hello model designer in *Diagram View*.</span></span> <span data-ttu-id="ef5fa-109">Não há suporte para criar e gerenciar hierarquias na Exibição de Dados.</span><span class="sxs-lookup"><span data-stu-id="ef5fa-109">Creating and managing hierarchies is not supported in Data View.</span></span>  
  
<span data-ttu-id="ef5fa-110">Estimado tempo toocomplete nesta lição: **20 minutos**</span><span class="sxs-lookup"><span data-stu-id="ef5fa-110">Estimated time toocomplete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="ef5fa-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ef5fa-111">Prerequisites</span></span>  
<span data-ttu-id="ef5fa-112">Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem.</span><span class="sxs-lookup"><span data-stu-id="ef5fa-112">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="ef5fa-113">Antes de executar tarefas de saudação nesta lição, você deverá ter completado lição anterior Olá: [lição 8: criar perspectivas](../tutorials/aas-lesson-8-create-perspectives.md).</span><span class="sxs-lookup"><span data-stu-id="ef5fa-113">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>  
  
## <a name="create-hierarchies"></a><span data-ttu-id="ef5fa-114">Criar hierarquias</span><span class="sxs-lookup"><span data-stu-id="ef5fa-114">Create hierarchies</span></span>  
  
#### <a name="toocreate-a-category-hierarchy-in-hello-dimproduct-table"></a><span data-ttu-id="ef5fa-115">uma hierarquia de categoria na tabela DimProduct de saudação do toocreate</span><span class="sxs-lookup"><span data-stu-id="ef5fa-115">toocreate a Category hierarchy in hello DimProduct table</span></span>  
  
1.  <span data-ttu-id="ef5fa-116">No designer de modelo da saudação (modo de exibição de diagrama), clique com botão direito Olá **DimProduct** tabela > **criar hierarquia**.</span><span class="sxs-lookup"><span data-stu-id="ef5fa-116">In hello model designer (diagram view), right-click hello **DimProduct** table > **Create Hierarchy**.</span></span> <span data-ttu-id="ef5fa-117">Uma nova hierarquia aparece na parte inferior da saudação da janela de tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="ef5fa-117">A new hierarchy appears at hello bottom of hello table window.</span></span> <span data-ttu-id="ef5fa-118">Renomear hierarquia Olá **categoria**.</span><span class="sxs-lookup"><span data-stu-id="ef5fa-118">Rename hello hierarchy **Category**.</span></span>  
  
2.  <span data-ttu-id="ef5fa-119">Clique e arraste Olá **ProductCategoryName** toohello de coluna nova **categoria** hierarquia.</span><span class="sxs-lookup"><span data-stu-id="ef5fa-119">Click and drag hello **ProductCategoryName** column toohello new **Category** hierarchy.</span></span>  
  
3.  <span data-ttu-id="ef5fa-120">Em Olá **categoria** hierarquia, Olá atalho **ProductCategoryName** > **Renomear**e, em seguida, digite **categoria**.</span><span class="sxs-lookup"><span data-stu-id="ef5fa-120">In hello **Category** hierarchy, right-click hello **ProductCategoryName** > **Rename**, and then type **Category**.</span></span>  
  
    > [!NOTE]  
    > <span data-ttu-id="ef5fa-121">Renomear uma coluna em uma hierarquia não renomeia essa coluna na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="ef5fa-121">Renaming a column in a hierarchy does not rename that column in hello table.</span></span> <span data-ttu-id="ef5fa-122">Uma coluna em uma hierarquia é apenas uma representação de coluna Olá na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="ef5fa-122">A column in a hierarchy is just a representation of hello column in hello table.</span></span>  
  
4.  <span data-ttu-id="ef5fa-123">Clique e arraste Olá **ProductSubcategoryName** coluna toohello **categoria** hierarquia.</span><span class="sxs-lookup"><span data-stu-id="ef5fa-123">Click and drag hello **ProductSubcategoryName** column toohello **Category** hierarchy.</span></span> <span data-ttu-id="ef5fa-124">Renomeie-a como **Subcategoria**.</span><span class="sxs-lookup"><span data-stu-id="ef5fa-124">Rename it **Subcategory**.</span></span> 
  
5.  <span data-ttu-id="ef5fa-125">Saudação de atalho **ModelName** coluna > **adicionar toohierarchy**e, em seguida, selecione **categoria**.</span><span class="sxs-lookup"><span data-stu-id="ef5fa-125">Right-click hello **ModelName** column > **Add toohierarchy**, and then select **Category**.</span></span> <span data-ttu-id="ef5fa-126">Renomeie-a como **Modelo**.</span><span class="sxs-lookup"><span data-stu-id="ef5fa-126">Rename it **Model**.</span></span>

6.  <span data-ttu-id="ef5fa-127">Finalmente, adicione **EnglishProductName** toohello a hierarquia de categoria.</span><span class="sxs-lookup"><span data-stu-id="ef5fa-127">Finally, add **EnglishProductName** toohello Category hierarchy.</span></span> <span data-ttu-id="ef5fa-128">Renomeie-a como **Produto**.</span><span class="sxs-lookup"><span data-stu-id="ef5fa-128">Rename it **Product**.</span></span>  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="toocreate-hierarchies-in-hello-dimdate-table"></a><span data-ttu-id="ef5fa-130">hierarquias de toocreate na tabela DimDate de saudação</span><span class="sxs-lookup"><span data-stu-id="ef5fa-130">toocreate hierarchies in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="ef5fa-131">Em Olá **DimDate** de tabela, crie uma hierarquia chamada **calendário**.</span><span class="sxs-lookup"><span data-stu-id="ef5fa-131">In hello **DimDate** table, create a hierarchy named **Calendar**.</span></span>  
  
3.  <span data-ttu-id="ef5fa-132">Adicione Olá colunas na ordem a seguir:</span><span class="sxs-lookup"><span data-stu-id="ef5fa-132">Add hello following columns in-order:</span></span>

    *  <span data-ttu-id="ef5fa-133">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="ef5fa-133">CalendarYear</span></span>
    *  <span data-ttu-id="ef5fa-134">CalendarSemester</span><span class="sxs-lookup"><span data-stu-id="ef5fa-134">CalendarSemester</span></span>
    *  <span data-ttu-id="ef5fa-135">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="ef5fa-135">CalendarQuarter</span></span>
    *  <span data-ttu-id="ef5fa-136">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="ef5fa-136">MonthCalendar</span></span>
    *  <span data-ttu-id="ef5fa-137">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="ef5fa-137">DayNumberOfMonth</span></span>
    
4.  <span data-ttu-id="ef5fa-138">Em Olá **DimDate** de tabela, crie um **Fiscal** hierarquia.</span><span class="sxs-lookup"><span data-stu-id="ef5fa-138">In hello **DimDate** table, create a **Fiscal** hierarchy.</span></span> <span data-ttu-id="ef5fa-139">Inclua Olá colunas na ordem a seguir:</span><span class="sxs-lookup"><span data-stu-id="ef5fa-139">Include hello following columns in-order:</span></span>  
  
    *  <span data-ttu-id="ef5fa-140">FiscalYear</span><span class="sxs-lookup"><span data-stu-id="ef5fa-140">FiscalYear</span></span>
    *  <span data-ttu-id="ef5fa-141">FiscalSemester</span><span class="sxs-lookup"><span data-stu-id="ef5fa-141">FiscalSemester</span></span>
    *  <span data-ttu-id="ef5fa-142">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="ef5fa-142">FiscalQuarter</span></span>
    *  <span data-ttu-id="ef5fa-143">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="ef5fa-143">MonthCalendar</span></span>
    *  <span data-ttu-id="ef5fa-144">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="ef5fa-144">DayNumberOfMonth</span></span>
  
5.  <span data-ttu-id="ef5fa-145">Por fim, na Olá **DimDate** de tabela, crie um **ProductionCalendar** hierarquia.</span><span class="sxs-lookup"><span data-stu-id="ef5fa-145">Finally, in hello **DimDate** table, create a **ProductionCalendar** hierarchy.</span></span> <span data-ttu-id="ef5fa-146">Inclua Olá colunas na ordem a seguir:</span><span class="sxs-lookup"><span data-stu-id="ef5fa-146">Include hello following columns in-order:</span></span>  
    *  <span data-ttu-id="ef5fa-147">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="ef5fa-147">CalendarYear</span></span>
    *  <span data-ttu-id="ef5fa-148">WeekNumberOfYear</span><span class="sxs-lookup"><span data-stu-id="ef5fa-148">WeekNumberOfYear</span></span>
    *  <span data-ttu-id="ef5fa-149">DayNumberOfWeek</span><span class="sxs-lookup"><span data-stu-id="ef5fa-149">DayNumberOfWeek</span></span>
  
 ## <a name="whats-next"></a><span data-ttu-id="ef5fa-150">O que vem a seguir?</span><span class="sxs-lookup"><span data-stu-id="ef5fa-150">What's next?</span></span>
<span data-ttu-id="ef5fa-151">[Lição 10: criar partições](../tutorials/aas-lesson-10-create-partitions.md).</span><span class="sxs-lookup"><span data-stu-id="ef5fa-151">[Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span> 
  
  
