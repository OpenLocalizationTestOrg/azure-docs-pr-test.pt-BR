---
title: "nível de compatibilidade de modelo aaaData no Azure Analysis Services | Microsoft Docs"
description: "Noções básicas sobre o nível de compatibilidade do modelo de dados de tabela."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/16/2017
ms.author: owend
ms.openlocfilehash: bfaf0c60666729d1e6e0baf082c046ea9faa4e86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a><span data-ttu-id="e30ca-103">Nível de compatibilidade para modelos de tabela do Analysis Services</span><span class="sxs-lookup"><span data-stu-id="e30ca-103">Compatibility level for Analysis Services tabular models</span></span>

<span data-ttu-id="e30ca-104">*Nível de compatibilidade* refere-se comportamentos específicos toorelease no mecanismo do Analysis Services hello.</span><span class="sxs-lookup"><span data-stu-id="e30ca-104">*Compatibility level* refers toorelease-specific behaviors in hello Analysis Services engine.</span></span> <span data-ttu-id="e30ca-105">Nível de compatibilidade de toohello alterações geralmente coincidam com as versões principais do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e30ca-105">Changes toohello compatibility level typically coincide with major releases of SQL Server.</span></span> <span data-ttu-id="e30ca-106">Essas alterações também são implementadas no paridade do Azure Analysis Services toomaintain entre as duas plataformas.</span><span class="sxs-lookup"><span data-stu-id="e30ca-106">These changes are also implemented in Azure Analysis Services toomaintain parity between both platforms.</span></span> <span data-ttu-id="e30ca-107">Alterações de nível de compatibilidade também afetam os recursos disponíveis em modelos de tabela.</span><span class="sxs-lookup"><span data-stu-id="e30ca-107">Compatibility level changes also affect features available in your tabular models.</span></span> <span data-ttu-id="e30ca-108">Por exemplo, o DirectQuery e os metadados de objeto de tabela têm implementações diferentes dependendo do nível de compatibilidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="e30ca-108">For example, DirectQuery and tabular object metadata have different implementations depending on hello compatibility level.</span></span> 

<span data-ttu-id="e30ca-109">Serviços de análise do Azure oferece suporte a modelos de tabela em níveis de compatibilidade Olá 1200 e 1400.</span><span class="sxs-lookup"><span data-stu-id="e30ca-109">Azure Analysis Services supports tabular models at hello 1200 and 1400 compatibility levels.</span></span>

<span data-ttu-id="e30ca-110">o nível de compatibilidade mais recente Olá é 1400.</span><span class="sxs-lookup"><span data-stu-id="e30ca-110">hello latest compatibility level is 1400.</span></span> <span data-ttu-id="e30ca-111">Esse nível coincide com o Analysis Services do SQL Server 2017.</span><span class="sxs-lookup"><span data-stu-id="e30ca-111">This level coincides with SQL Server 2017 Analysis Services.</span></span> <span data-ttu-id="e30ca-112">Os principais recursos no nível de compatibilidade de 1400 Olá incluem:</span><span class="sxs-lookup"><span data-stu-id="e30ca-112">Major features in hello 1400 compatibility level include:</span></span>

*  <span data-ttu-id="e30ca-113">Nova infraestrutura para conectividade de dados e importação para modelos de tabela com suporte para APIs de TOM e scripts de TMSL.</span><span class="sxs-lookup"><span data-stu-id="e30ca-113">New infrastructure for data connectivity and import into tabular models with support for TOM APIs and TMSL scripting.</span></span> <span data-ttu-id="e30ca-114">Esse novo recurso habilita o suporte para fontes de dados adicionais, como armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="e30ca-114">This new feature enables support for additional data sources such as Azure Blob storage.</span></span>
*  <span data-ttu-id="e30ca-115">Transformação de dados e recursos de mashup de dados usando expressões Obter dados e M.</span><span class="sxs-lookup"><span data-stu-id="e30ca-115">Data transformation and data mashup capabilities by using Get Data and M expressions.</span></span>
*  <span data-ttu-id="e30ca-116">Medidas que suportam uma propriedade de linhas de detalhes com uma expressão DAX.</span><span class="sxs-lookup"><span data-stu-id="e30ca-116">Measures support a Detail Rows property with a DAX expression.</span></span> <span data-ttu-id="e30ca-117">Essa propriedade permite que as ferramentas de cliente como o Microsoft Excel toodrill toodetailed dados de um relatório agregado.</span><span class="sxs-lookup"><span data-stu-id="e30ca-117">This property enables client tools like Microsoft Excel toodrill down toodetailed data from an aggregated report.</span></span> <span data-ttu-id="e30ca-118">Por exemplo, quando os usuários exibem o total de vendas de uma região e mês, eles podem exibir detalhes do pedido Olá associado.</span><span class="sxs-lookup"><span data-stu-id="e30ca-118">For example, when users view total sales for a region and month, they can view hello associated order details.</span></span> 
*  <span data-ttu-id="e30ca-119">Segurança em nível de objeto de tabela e coluna nomes, além de toohello dados dentro deles.</span><span class="sxs-lookup"><span data-stu-id="e30ca-119">Object-level security for table and column names, in addition toohello data within them.</span></span>
*  <span data-ttu-id="e30ca-120">Suporte aprimorado para hierarquias desbalanceadas.</span><span class="sxs-lookup"><span data-stu-id="e30ca-120">Enhanced support for ragged hierarchies.</span></span>
*  <span data-ttu-id="e30ca-121">Monitoramento de desempenho e melhorias.</span><span class="sxs-lookup"><span data-stu-id="e30ca-121">Performance and monitoring improvements.</span></span>
  
## <a name="set-compatibility-level"></a><span data-ttu-id="e30ca-122">Configuração de nível de compatibilidade</span><span class="sxs-lookup"><span data-stu-id="e30ca-122">Set compatibility level</span></span> 
 <span data-ttu-id="e30ca-123">Ao criar um novo projeto de modelo de tabela no SSDT, você pode especificar o nível de compatibilidade de saudação em Olá **designer de modelo Tabular** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e30ca-123">When creating a new tabular model project in SSDT, you can specify hello compatibility level on hello **Tabular model designer** dialog.</span></span> 
  
 ![ssas_tabularproject_compat1200](./media/analysis-services-compat-level/aas-tabularproject-compat.png)  
  
 <span data-ttu-id="e30ca-125">Se você selecionar Olá **não mostrar esta mensagem novamente** opção, todos os projetos subsequentes usam o nível de compatibilidade Olá especificado como o padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="e30ca-125">If you select hello **Do not show this message again** option, all subsequent projects use hello compatibility level you specified as hello default.</span></span> <span data-ttu-id="e30ca-126">Você pode alterar o nível de compatibilidade saudação padrão no SSDT em **ferramentas** > **opções**.</span><span class="sxs-lookup"><span data-stu-id="e30ca-126">You can change hello default compatibility level in SSDT in **Tools** > **Options**.</span></span>  
  
 <span data-ttu-id="e30ca-127">tooupgrade um projeto de modelo de tabela existente no SSDT, Olá conjunto **nível de compatibilidade** propriedade modelo Olá **propriedades** janela.</span><span class="sxs-lookup"><span data-stu-id="e30ca-127">tooupgrade an existing tabular model project in SSDT, set  hello **Compatibility Level** property in hello model **Properties** window.</span></span> <span data-ttu-id="e30ca-128">Tenha em mente, atualizar o nível de compatibilidade Olá é irreversível.</span><span class="sxs-lookup"><span data-stu-id="e30ca-128">Keep in-mind, upgrading hello compatibility level is irreversible.</span></span>
  
## <a name="check-compatibility-level-for-a-tabular-model-database-in-sql-server-management-studio"></a><span data-ttu-id="e30ca-129">Verifique o nível de compatibilidade de um banco de dados de modelo de tabela no SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="e30ca-129">Check compatibility level for a tabular model database in SQL Server Management Studio</span></span> 
 <span data-ttu-id="e30ca-130">No SSMS, clique no nome do banco de dados hello > **propriedades** > **nível de compatibilidade**.</span><span class="sxs-lookup"><span data-stu-id="e30ca-130">In SSMS, right-click hello database name > **Properties** > **Compatibility Level**.</span></span>  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a><span data-ttu-id="e30ca-131">Verifique o nível de compatibilidade com suporte para um servidor no SSMS</span><span class="sxs-lookup"><span data-stu-id="e30ca-131">Check supported compatibility level for a server in SSMS</span></span>  
 <span data-ttu-id="e30ca-132">No SSMS, clique no nome do servidor de saudação > **propriedades** > **nível de compatibilidade com suporte**.</span><span class="sxs-lookup"><span data-stu-id="e30ca-132">In SSMS, right-click hello server name>  **Properties** > **Supported Compatibility Level**.</span></span>  
  
 <span data-ttu-id="e30ca-133">Essa propriedade especifica hello mais alto nível de compatibilidade de um banco de dados que serão executados no servidor de saudação (excluindo a visualização).</span><span class="sxs-lookup"><span data-stu-id="e30ca-133">This property specifies hello highest compatibility level of a database that will run on hello server (excluding preview).</span></span> <span data-ttu-id="e30ca-134">Olá suporte para nível de compatibilidade não pode ser alterado.</span><span class="sxs-lookup"><span data-stu-id="e30ca-134">hello supported compatibility level cannot be changed.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="e30ca-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e30ca-135">Next steps</span></span>
  <span data-ttu-id="e30ca-136">[Como criar um modelo no portal do Azure](analysis-services-create-model-portal.md) </span><span class="sxs-lookup"><span data-stu-id="e30ca-136">[Create a model in Azure portal](analysis-services-create-model-portal.md) </span></span>  
  [<span data-ttu-id="e30ca-137">Gerenciar o Analysis Services</span><span class="sxs-lookup"><span data-stu-id="e30ca-137">Manage Analysis Services</span></span>](analysis-services-manage.md)  
