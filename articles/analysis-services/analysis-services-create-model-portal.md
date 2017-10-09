---
title: "aaaCreate um modelo de tabela usando o designer de Web do Azure Analysis Services Olá | Microsoft Docs"
description: "Saiba como toocreate um modelo de tabela do Azure Analysis Services usando Olá Web designer no portal do Azure."
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
ms.openlocfilehash: a37b326b76c84fc3a4300827bc1c8706b0584701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-model-in-azure-portal"></a><span data-ttu-id="435ee-103">Criar um modelo no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="435ee-103">Create a model in Azure portal</span></span>

<span data-ttu-id="435ee-104">recurso do Hello Azure Analysis Services na web designer (visualização) no portal do Azure fornece uma maneira rápida e fácil toocreate e editar modelos de tabela e consulta modelo dados diretamente no seu navegador.</span><span class="sxs-lookup"><span data-stu-id="435ee-104">hello Azure Analysis Services web designer (preview) feature in Azure portal provides a quick and easy way toocreate and edit tabular models and query model data right in your browser.</span></span> 

<span data-ttu-id="435ee-105">Tenha em mente, Olá web designer é **visualização**.</span><span class="sxs-lookup"><span data-stu-id="435ee-105">Keep in mind, hello web designer is **preview**.</span></span> <span data-ttu-id="435ee-106">Enquanto a nova funcionalidade está sendo adicionada tempo Olá todo, na visualização, a funcionalidade é limitada.</span><span class="sxs-lookup"><span data-stu-id="435ee-106">While new functionality is being added all hello time, in preview, functionality is limited.</span></span> <span data-ttu-id="435ee-107">Para mais avançados modelo teste e desenvolvimento, é melhor toouse Visual Studio (SSDT) e o SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="435ee-107">For more advanced model development and testing, it's best toouse Visual Studio (SSDT) and SQL Server Management Studio (SSMS).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="435ee-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="435ee-108">Prerequisites</span></span>

- <span data-ttu-id="435ee-109">Um servidor do Azure Analysis Services na camada Standard ou o desenvolvedor de saudação.</span><span class="sxs-lookup"><span data-stu-id="435ee-109">An Azure Analysis Services server at hello Standard or Developer tier.</span></span> <span data-ttu-id="435ee-110">Novos modelos criados usando o designer de Web hello são DirectQuery com suporte apenas essas camadas.</span><span class="sxs-lookup"><span data-stu-id="435ee-110">New models created by using hello Web designer are DirectQuery, supported only by these tiers.</span></span>
- <span data-ttu-id="435ee-111">Um Banco de Dados SQL Azure, Azure SQL Data Warehouse ou arquivo Power BI Desktop (.pbix) como fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="435ee-111">An Azure SQL Database, Azure SQL Data Warehouse, or Power BI Desktop (.pbix) file as a datasource.</span></span> <span data-ttu-id="435ee-112">Novos modelos criados por meio de arquivos Power BI Desktop dão suporte às fontes de dados de Banco de Dados SQL Azure, Azure SQL Data Warehouse, Oracle e Teradata.</span><span class="sxs-lookup"><span data-stu-id="435ee-112">New models created from Power BI Desktop files support Azure SQL Database, Azure SQL Data Warehouse, Oracle, and Teradata data sources.</span></span>
- <span data-ttu-id="435ee-113">Uma conta do SQL Server e a senha para se conectar a fontes de dados de banco de dados SQL ou do Azure SQL Data Warehouse tooAzure.</span><span class="sxs-lookup"><span data-stu-id="435ee-113">A SQL Server account and password for connecting tooAzure SQL Database or Azure SQL Data Warehouse data sources.</span></span>

## <a name="toocreate-a-new-tabular-model"></a><span data-ttu-id="435ee-114">toocreate um novo modelo de tabela</span><span class="sxs-lookup"><span data-stu-id="435ee-114">toocreate a new tabular model</span></span>

1. <span data-ttu-id="435ee-115">Na folha **Visão geral** > **Designer de Web** do seu servidor, clique em **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="435ee-115">In your server's **Overview** blade > **Web designer**, click **Open**.</span></span>

    ![Criar um modelo no portal do Azure](./media/analysis-services-create-model-portal/aas-create-portal-overview-wd.png)

2. <span data-ttu-id="435ee-117">Em **Designer de Web** > **Modelos**, clique em **+ Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="435ee-117">In **Web designer** > **Models**, click **+ Add**.</span></span>

    ![Criar um modelo no portal do Azure](./media/analysis-services-create-model-portal/aas-create-portal-models.png)

3. <span data-ttu-id="435ee-119">Em **Novo modelo**, digite um nome de modelo e, em seguida, selecione uma fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="435ee-119">In **New model**, type a model name, and then select a data source.</span></span>

    ![Caixa de diálogo Novo modelo no portal do Azure](./media/analysis-services-create-model-portal/aas-create-portal-new-model.png)

4. <span data-ttu-id="435ee-121">Em **conectar**, insira as propriedades de conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="435ee-121">In **Connect**, enter hello connection properties.</span></span> <span data-ttu-id="435ee-122">Nome de usuário e senha devem ser uma conta do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="435ee-122">Username and password must be a SQL Server account.</span></span>

     ![Caixa de diálogo Conectar no portal do Azure](./media/analysis-services-create-model-portal/aas-create-portal-connect.png)

5. <span data-ttu-id="435ee-124">Em **tabelas e exibições**, selecione Olá tooinclude de tabelas em seu modelo e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="435ee-124">In **Tables and views**, select hello tables tooinclude in your model, and then click **Create**.</span></span> <span data-ttu-id="435ee-125">São criadas automaticamente relações entre tabelas com um par de chaves.</span><span class="sxs-lookup"><span data-stu-id="435ee-125">Relationships are created automatically between tables with a key pair.</span></span>

     ![Selecionar tabelas e exibições](./media/analysis-services-create-model-portal/aas-create-portal-tables.png)

<span data-ttu-id="435ee-127">O novo modelo é exibido no navegador.</span><span class="sxs-lookup"><span data-stu-id="435ee-127">Your new model appears in your browser.</span></span> <span data-ttu-id="435ee-128">A partir daqui, você pode:</span><span class="sxs-lookup"><span data-stu-id="435ee-128">From here, you can:</span></span>   

- <span data-ttu-id="435ee-129">Dados de modelo de consulta arrastando o designer de consulta toohello campos e adicionar filtros.</span><span class="sxs-lookup"><span data-stu-id="435ee-129">Query model data by dragging fields toohello query designer and adding filters.</span></span>
- <span data-ttu-id="435ee-130">Crie novas medidas nas tabelas.</span><span class="sxs-lookup"><span data-stu-id="435ee-130">Create new measures in tables.</span></span>
- <span data-ttu-id="435ee-131">Edite metadados do modelo usando o editor de json hello.</span><span class="sxs-lookup"><span data-stu-id="435ee-131">Edit model metadata by using hello json editor.</span></span>
- <span data-ttu-id="435ee-132">Abra o modelo de saudação no Visual Studio (SSDT), o Power BI Desktop ou o Excel.</span><span class="sxs-lookup"><span data-stu-id="435ee-132">Open hello model in Visual Studio (SSDT), Power BI Desktop, or Excel.</span></span>

![Selecionar tabelas e exibições](./media/analysis-services-create-model-portal/aas-create-portal-query.png)

> [!NOTE]
> <span data-ttu-id="435ee-134">Quando você editar os metadados de modelo ou cria novas medidas em seu navegador, você está salvando modelo de tooyour essas alterações no Azure.</span><span class="sxs-lookup"><span data-stu-id="435ee-134">When you edit model metadata or create new measures in your browser, you're saving those changes tooyour model in Azure.</span></span> <span data-ttu-id="435ee-135">Se você também estiver trabalhando em seu modelo no SSDT, Power BI Desktop ou Excel, o modelo pode ficar fora de sincronia.</span><span class="sxs-lookup"><span data-stu-id="435ee-135">If you're also working on your model in SSDT, Power BI Desktop, or Excel, your model can get out of sync.</span></span>


## <a name="next-steps"></a><span data-ttu-id="435ee-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="435ee-136">Next steps</span></span> 
[<span data-ttu-id="435ee-137">Gerenciar usuários e funções de banco de dados</span><span class="sxs-lookup"><span data-stu-id="435ee-137">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="435ee-138">Conectar com o Excel</span><span class="sxs-lookup"><span data-stu-id="435ee-138">Connect with Excel</span></span>](analysis-services-connect-excel.md)  


