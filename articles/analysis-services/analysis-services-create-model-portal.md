---
title: Criar um modelo de tabela usando o designer de Web do Azure Analysis Services | Microsoft Docs
description: Saiba como criar um modelo de tabela do Azure Analysis Services usando o designer de Web no portal do Azure.
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
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: bd58f1845dabf6afb47ce27236d14479677a8808
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-model-in-azure-portal"></a><span data-ttu-id="d5139-103">Criar um modelo no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d5139-103">Create a model in Azure portal</span></span>

<span data-ttu-id="d5139-104">O recurso de Web designer do Azure Analysis Services (Versão Prévia) no portal do Azure fornece uma maneira rápida e fácil de criar e editar modelos de tabela e consultar dados de modelo diretamente em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="d5139-104">The Azure Analysis Services web designer (preview) feature in Azure portal provides a quick and easy way to create and edit tabular models and query model data right in your browser.</span></span> 

<span data-ttu-id="d5139-105">Tenha em mente que o Web designer é uma **versão prévia**.</span><span class="sxs-lookup"><span data-stu-id="d5139-105">Keep in mind, the web designer is **preview**.</span></span> <span data-ttu-id="d5139-106">Embora novas funcionalidades estão sendo adicionadas o tempo todo, na versão prévia, a funcionalidade é limitada.</span><span class="sxs-lookup"><span data-stu-id="d5139-106">While new functionality is being added all the time, in preview, functionality is limited.</span></span> <span data-ttu-id="d5139-107">Para desenvolvimento e teste de modelos mais avançados, é melhor usar o Visual Studio (SSDT) e SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="d5139-107">For more advanced model development and testing, it's best to use Visual Studio (SSDT) and SQL Server Management Studio (SSMS).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5139-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d5139-108">Prerequisites</span></span>

- <span data-ttu-id="d5139-109">Um servidor do Azure Analysis Services na camada Padrão ou Desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="d5139-109">An Azure Analysis Services server at the Standard or Developer tier.</span></span> <span data-ttu-id="d5139-110">Novos modelos criados usando o designer de Web são DirectQuery com suporte apenas dessas camadas.</span><span class="sxs-lookup"><span data-stu-id="d5139-110">New models created by using the Web designer are DirectQuery, supported only by these tiers.</span></span>
- <span data-ttu-id="d5139-111">Um Banco de Dados SQL Azure, Azure SQL Data Warehouse ou arquivo Power BI Desktop (.pbix) como fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="d5139-111">An Azure SQL Database, Azure SQL Data Warehouse, or Power BI Desktop (.pbix) file as a datasource.</span></span> <span data-ttu-id="d5139-112">Novos modelos criados por meio de arquivos Power BI Desktop dão suporte às fontes de dados de Banco de Dados SQL Azure, Azure SQL Data Warehouse, Oracle e Teradata.</span><span class="sxs-lookup"><span data-stu-id="d5139-112">New models created from Power BI Desktop files support Azure SQL Database, Azure SQL Data Warehouse, Oracle, and Teradata data sources.</span></span>
- <span data-ttu-id="d5139-113">Uma conta e senha do SQL Server para se conectar a fontes de dados do Banco de Dados SQL Azure ou Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d5139-113">A SQL Server account and password for connecting to Azure SQL Database or Azure SQL Data Warehouse data sources.</span></span>

## <a name="to-create-a-new-tabular-model"></a><span data-ttu-id="d5139-114">Para criar um novo modelo de tabela</span><span class="sxs-lookup"><span data-stu-id="d5139-114">To create a new tabular model</span></span>

1. <span data-ttu-id="d5139-115">Na folha **Visão geral** > **Designer de Web** do seu servidor, clique em **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="d5139-115">In your server's **Overview** blade > **Web designer**, click **Open**.</span></span>

    ![Criar um modelo no portal do Azure](./media/analysis-services-create-model-portal/aas-create-portal-overview-wd.png)

2. <span data-ttu-id="d5139-117">Em **Designer de Web** > **Modelos**, clique em **+ Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d5139-117">In **Web designer** > **Models**, click **+ Add**.</span></span>

    ![Criar um modelo no portal do Azure](./media/analysis-services-create-model-portal/aas-create-portal-models.png)

3. <span data-ttu-id="d5139-119">Em **Novo modelo**, digite um nome de modelo e, em seguida, selecione uma fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="d5139-119">In **New model**, type a model name, and then select a data source.</span></span>

    ![Caixa de diálogo Novo modelo no portal do Azure](./media/analysis-services-create-model-portal/aas-create-portal-new-model.png)

4. <span data-ttu-id="d5139-121">Em **Conectar**, insira as propriedades de conexão.</span><span class="sxs-lookup"><span data-stu-id="d5139-121">In **Connect**, enter the connection properties.</span></span> <span data-ttu-id="d5139-122">Nome de usuário e senha devem ser uma conta do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d5139-122">Username and password must be a SQL Server account.</span></span>

     ![Caixa de diálogo Conectar no portal do Azure](./media/analysis-services-create-model-portal/aas-create-portal-connect.png)

5. <span data-ttu-id="d5139-124">Em **Tabelas e exibições**, selecione as tabelas para incluir em seu modelo e, em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d5139-124">In **Tables and views**, select the tables to include in your model, and then click **Create**.</span></span> <span data-ttu-id="d5139-125">São criadas automaticamente relações entre tabelas com um par de chaves.</span><span class="sxs-lookup"><span data-stu-id="d5139-125">Relationships are created automatically between tables with a key pair.</span></span>

     ![Selecionar tabelas e exibições](./media/analysis-services-create-model-portal/aas-create-portal-tables.png)

<span data-ttu-id="d5139-127">O novo modelo é exibido no navegador.</span><span class="sxs-lookup"><span data-stu-id="d5139-127">Your new model appears in your browser.</span></span> <span data-ttu-id="d5139-128">A partir daqui, você pode:</span><span class="sxs-lookup"><span data-stu-id="d5139-128">From here, you can:</span></span>   

- <span data-ttu-id="d5139-129">Consultar dados de modelo arrastando campos para o designer de consulta e adicionando filtros.</span><span class="sxs-lookup"><span data-stu-id="d5139-129">Query model data by dragging fields to the query designer and adding filters.</span></span>
- <span data-ttu-id="d5139-130">Crie novas medidas nas tabelas.</span><span class="sxs-lookup"><span data-stu-id="d5139-130">Create new measures in tables.</span></span>
- <span data-ttu-id="d5139-131">Edite metadados do modelo usando o editor json.</span><span class="sxs-lookup"><span data-stu-id="d5139-131">Edit model metadata by using the json editor.</span></span>
- <span data-ttu-id="d5139-132">Abra o modelo no Visual Studio (SSDT), Power BI Desktop ou Excel.</span><span class="sxs-lookup"><span data-stu-id="d5139-132">Open the model in Visual Studio (SSDT), Power BI Desktop, or Excel.</span></span>

![Selecionar tabelas e exibições](./media/analysis-services-create-model-portal/aas-create-portal-query.png)

> [!NOTE]
> <span data-ttu-id="d5139-134">Quando você edita os metadados de modelo ou cria novas medidas em seu navegador, você está salvando as alterações em seu modelo no Azure.</span><span class="sxs-lookup"><span data-stu-id="d5139-134">When you edit model metadata or create new measures in your browser, you're saving those changes to your model in Azure.</span></span> <span data-ttu-id="d5139-135">Se você também estiver trabalhando em seu modelo no SSDT, Power BI Desktop ou Excel, o modelo pode ficar fora de sincronia.</span><span class="sxs-lookup"><span data-stu-id="d5139-135">If you're also working on your model in SSDT, Power BI Desktop, or Excel, your model can get out of sync.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d5139-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d5139-136">Next steps</span></span> 
[<span data-ttu-id="d5139-137">Gerenciar usuários e funções de banco de dados</span><span class="sxs-lookup"><span data-stu-id="d5139-137">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="d5139-138">Conectar com o Excel</span><span class="sxs-lookup"><span data-stu-id="d5139-138">Connect with Excel</span></span>](analysis-services-connect-excel.md)  


