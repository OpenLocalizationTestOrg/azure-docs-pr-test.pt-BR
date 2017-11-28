---
title: "Tutorial: criar um pipeline usando o Assistente de Cópia | Microsoft Docs"
description: "Neste tutorial, você criar um pipeline da fábrica de dados do Azure com uma atividade de cópia usando Olá Assistente para cópia de suporte pela fábrica de dados"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b87afb8e-53b7-4e1b-905b-0343dd096198
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 567b89e7a54c245c134cd0674690e6f3499b46d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-data-factory-copy-wizard"></a><span data-ttu-id="36ee4-103">Tutorial: Criar um pipeline com a Atividade de Cópia usando o Assistente de Cópia do Data Factory</span><span class="sxs-lookup"><span data-stu-id="36ee4-103">Tutorial: Create a pipeline with Copy Activity using Data Factory Copy Wizard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="36ee4-104">Visão geral e pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="36ee4-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="36ee4-105">Assistente de Cópia</span><span class="sxs-lookup"><span data-stu-id="36ee4-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="36ee4-106">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="36ee4-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="36ee4-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="36ee4-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="36ee4-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="36ee4-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="36ee4-109">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="36ee4-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="36ee4-110">API REST</span><span class="sxs-lookup"><span data-stu-id="36ee4-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="36ee4-111">API do .NET</span><span class="sxs-lookup"><span data-stu-id="36ee4-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="36ee4-112">Este tutorial mostra como Olá toouse **Assistente para cópia de** toocopy dados de um banco de dados de SQL do Azure de tooan do armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="36ee4-112">This tutorial shows you how toouse hello **Copy Wizard** toocopy data from an Azure blob storage tooan Azure SQL database.</span></span> 

<span data-ttu-id="36ee4-113">saudação do Azure Data Factory **Assistente para cópia** permite que você tooquickly criar um pipeline de dados que copia dados de um repositório de dados de destino origem com suporte dados repositório tooa com suporte.</span><span class="sxs-lookup"><span data-stu-id="36ee4-113">hello Azure Data Factory **Copy Wizard** allows you tooquickly create a data pipeline that copies data from a supported source data store tooa supported destination data store.</span></span> <span data-ttu-id="36ee4-114">Portanto, recomendamos que você use o Assistente de saudação como uma primeira toocreate da etapa um pipeline de exemplo para seu cenário de movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="36ee4-114">Therefore, we recommend that you use hello wizard as a first step toocreate a sample pipeline for your data movement scenario.</span></span> <span data-ttu-id="36ee4-115">Para obter uma lista de armazenamentos de dados com suporte como origens e destinos, consulte [Armazenamentos de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="36ee4-115">For a list of data stores supported as sources and as destinations, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>  

<span data-ttu-id="36ee4-116">Este tutorial mostra como toocreate uma fábrica de dados do Azure, Olá Iniciar Assistente para cópia, passar por uma série de detalhes de tooprovide etapas sobre seu cenário de inclusão/movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="36ee4-116">This tutorial shows you how toocreate an Azure data factory, launch hello Copy Wizard, go through a series of steps tooprovide details about your data ingestion/movement scenario.</span></span> <span data-ttu-id="36ee4-117">Quando você concluir as etapas no Assistente de saudação, o Assistente de saudação cria automaticamente um pipeline com dados de toocopy uma atividade de cópia de um banco de dados de SQL do Azure de tooan do armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="36ee4-117">When you finish steps in hello wizard, hello wizard automatically creates a pipeline with a Copy Activity toocopy data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="36ee4-118">Para saber mais sobre a atividade de cópia, confira [Atividades de movimentação de dados](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="36ee4-118">For more information about Copy Activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36ee4-119">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="36ee4-119">Prerequisites</span></span>
<span data-ttu-id="36ee4-120">Conclua os pré-requisitos listados em Olá [visão geral do Tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) artigo antes de executar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="36ee4-120">Complete prerequisites listed in hello [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article before performing this tutorial.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="36ee4-121">Criar um data factory</span><span class="sxs-lookup"><span data-stu-id="36ee4-121">Create data factory</span></span>
<span data-ttu-id="36ee4-122">Nesta etapa, você usa Olá toocreate portal do Azure uma fábrica de dados do Azure denominada **ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="36ee4-122">In this step, you use hello Azure portal toocreate an Azure data factory named **ADFTutorialDataFactory**.</span></span>

1. <span data-ttu-id="36ee4-123">Faça logon no muito[portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="36ee4-123">Log in too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="36ee4-124">Clique em **+ novo** no canto superior esquerdo de saudação, clique em **dados + análise**e clique em **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="36ee4-124">Click **+ NEW** from hello top-left corner, click **Data + analytics**, and click **Data Factory**.</span></span> 
   
   ![Novo -> DataFactory](./media/data-factory-copy-data-wizard-tutorial/new-data-factory-menu.png)
2. <span data-ttu-id="36ee4-126">Em Olá **nova fábrica de dados** folha:</span><span class="sxs-lookup"><span data-stu-id="36ee4-126">In hello **New data factory** blade:</span></span>
   
   1. <span data-ttu-id="36ee4-127">Digite **ADFTutorialDataFactory** para Olá **nome**.</span><span class="sxs-lookup"><span data-stu-id="36ee4-127">Enter **ADFTutorialDataFactory** for hello **name**.</span></span>
       <span data-ttu-id="36ee4-128">nome de Olá Olá do Azure da fábrica de dados deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="36ee4-128">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="36ee4-129">Se você receber o erro Olá: `Data factory name “ADFTutorialDataFactory” is not available`, altere o nome de Olá Olá da fábrica de dados (por exemplo, yournameADFTutorialDataFactoryYYYYMMDD) e tente criar novamente.</span><span class="sxs-lookup"><span data-stu-id="36ee4-129">If you receive hello error: `Data factory name “ADFTutorialDataFactory” is not available`, change hello name of hello data factory (for example, yournameADFTutorialDataFactoryYYYYMMDD) and try creating again.</span></span> <span data-ttu-id="36ee4-130">Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="36ee4-130">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
      
       ![Nome da data factory indisponível](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-not-available.png)    
   2. <span data-ttu-id="36ee4-132">Selecione sua **assinatura**do Azure.</span><span class="sxs-lookup"><span data-stu-id="36ee4-132">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="36ee4-133">Para o grupo de recursos, siga um destes Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="36ee4-133">For Resource Group, do one of hello following steps:</span></span> 
      
      - <span data-ttu-id="36ee4-134">Selecione **usar existente** tooselect um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="36ee4-134">Select **Use existing** tooselect an existing resource group.</span></span>
      - <span data-ttu-id="36ee4-135">Selecione **criar novo** tooenter um nome para um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="36ee4-135">Select **Create new** tooenter a name for a resource group.</span></span>
          
        <span data-ttu-id="36ee4-136">Algumas das etapas neste tutorial Olá pressupõem que você use o nome da saudação: **ADFTutorialResourceGroup** Olá para grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="36ee4-136">Some of hello steps in this tutorial assume that you use hello name: **ADFTutorialResourceGroup** for hello resource group.</span></span> <span data-ttu-id="36ee4-137">toolearn sobre grupos de recursos, consulte [usando o recurso de grupos de toomanage os recursos do Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="36ee4-137">toolearn about resource groups, see [Using resource groups toomanage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>
   4. <span data-ttu-id="36ee4-138">Selecione um **local** Olá fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="36ee4-138">Select a **location** for hello data factory.</span></span>
   5. <span data-ttu-id="36ee4-139">Selecione **toodashboard Pin** caixa de seleção na parte inferior da saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="36ee4-139">Select **Pin toodashboard** check box at hello bottom of hello blade.</span></span>  
   6. <span data-ttu-id="36ee4-140">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="36ee4-140">Click **Create**.</span></span>
      
       ![Folha Nova data factory](media/data-factory-copy-data-wizard-tutorial/new-data-factory-blade.png)            
3. <span data-ttu-id="36ee4-142">Após a conclusão da criação de saudação, você ver Olá **Data Factory** folha conforme Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="36ee4-142">After hello creation is complete, you see hello **Data Factory** blade as shown in hello following image:</span></span>
   
   ![Página inicial da data factory](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-home-page.png)

## <a name="launch-copy-wizard"></a><span data-ttu-id="36ee4-144">Iniciar o Assistente de cópia</span><span class="sxs-lookup"><span data-stu-id="36ee4-144">Launch Copy Wizard</span></span>
1. <span data-ttu-id="36ee4-145">Na folha de fábrica de dados hello, clique em **copiar dados [visualização]** toolaunch Olá **Assistente para cópia de**.</span><span class="sxs-lookup"><span data-stu-id="36ee4-145">On hello Data Factory blade, click **Copy data [PREVIEW]** toolaunch hello **Copy Wizard**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="36ee4-146">Se você vir esse navegador da web hello está preso em "Autorizar...", desabilitar/desmarque **bloquear cookies de terceiros e dados do site** definindo as configurações do navegador hello (ou) manter ele habilitado e criar uma exceção para  **login.microsoftonline.com** e tente iniciar o Assistente de saudação novamente.</span><span class="sxs-lookup"><span data-stu-id="36ee4-146">If you see that hello web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting in hello browser settings (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching hello wizard again.</span></span>
2. <span data-ttu-id="36ee4-147">Em Olá **propriedades** página:</span><span class="sxs-lookup"><span data-stu-id="36ee4-147">In hello **Properties** page:</span></span>
   
   1. <span data-ttu-id="36ee4-148">Insira **CopyFromBlobToAzureSql** para o **Nome da tarefa**</span><span class="sxs-lookup"><span data-stu-id="36ee4-148">Enter **CopyFromBlobToAzureSql** for **Task name**</span></span>
   2. <span data-ttu-id="36ee4-149">Insira uma **descrição** (opcional).</span><span class="sxs-lookup"><span data-stu-id="36ee4-149">Enter **description** (optional).</span></span>
   3. <span data-ttu-id="36ee4-150">Saudação de alteração **data/hora inicial** e hello **data hora de término** para que a data de término hello é definir tootoday e iniciar data toofive dias.</span><span class="sxs-lookup"><span data-stu-id="36ee4-150">Change hello **Start date time** and hello **End date time** so that hello end date is set tootoday and start date toofive days earlier.</span></span>  
   4. <span data-ttu-id="36ee4-151">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="36ee4-151">Click **Next**.</span></span>  
      
      ![Ferramenta de Cópia - página Propriedades](./media/data-factory-copy-data-wizard-tutorial/copy-tool-properties-page.png) 
3. <span data-ttu-id="36ee4-153">Em Olá **repositório de dados de origem** , clique em **armazenamento de BLOBs do Azure** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="36ee4-153">On hello **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="36ee4-154">Você pode usar esse repositório de dados de origem do página toospecify Olá para tarefas de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="36ee4-154">You use this page toospecify hello source data store for hello copy task.</span></span> 
   
    ![Ferramenta de Cópia - página de repositório de dados de origem](./media/data-factory-copy-data-wizard-tutorial/copy-tool-source-data-store-page.png)
4. <span data-ttu-id="36ee4-156">Em Olá **especificar conta de armazenamento de BLOBs do Azure Olá** página:</span><span class="sxs-lookup"><span data-stu-id="36ee4-156">On hello **Specify hello Azure Blob storage account** page:</span></span>
   
   1. <span data-ttu-id="36ee4-157">Insira **AzureStorageLinkedService** para o **Nome do serviço vinculado**.</span><span class="sxs-lookup"><span data-stu-id="36ee4-157">Enter **AzureStorageLinkedService** for **Linked service name**.</span></span>
   2. <span data-ttu-id="36ee4-158">Confirme se a opção **De assinaturas do Azure** foi selecionada em **Método de seleção de conta**.</span><span class="sxs-lookup"><span data-stu-id="36ee4-158">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="36ee4-159">Selecione sua **assinatura**do Azure.</span><span class="sxs-lookup"><span data-stu-id="36ee4-159">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="36ee4-160">Selecione um **conta de armazenamento do Azure** de saudação lista de armazenamento do Azure contas disponível na assinatura de saudação selecionada.</span><span class="sxs-lookup"><span data-stu-id="36ee4-160">Select an **Azure storage account** from hello list of Azure storage accounts available in hello selected subscription.</span></span> <span data-ttu-id="36ee4-161">Você também pode escolher tooenter configurações de conta de armazenamento manualmente selecionando **inserir manualmente** opção Olá **método de seleção de conta**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="36ee4-161">You can also choose tooenter storage account settings manually by selecting **Enter manually** option for hello **Account selection method**, and then click **Next**.</span></span> 
      
      ![Copie a ferramenta - especificar conta de armazenamento de BLOBs do Azure Olá](./media/data-factory-copy-data-wizard-tutorial/copy-tool-specify-azure-blob-storage-account.png)
5. <span data-ttu-id="36ee4-163">Em **pasta ou escolha o arquivo de entrada hello** página:</span><span class="sxs-lookup"><span data-stu-id="36ee4-163">On **Choose hello input file or folder** page:</span></span>
   
   1. <span data-ttu-id="36ee4-164">Clique duas vezes em **adftutorial** (pasta).</span><span class="sxs-lookup"><span data-stu-id="36ee4-164">Double-click **adftutorial** (folder).</span></span>
   2. <span data-ttu-id="36ee4-165">Selecione **emp.txt** e clique em **Escolher**</span><span class="sxs-lookup"><span data-stu-id="36ee4-165">Select **emp.txt**, and click **Choose**</span></span>
      
      ![Copie a ferramenta - escolha a pasta ou arquivo de entrada hello](./media/data-factory-copy-data-wizard-tutorial/copy-tool-choose-input-file-or-folder.png)
6. <span data-ttu-id="36ee4-167">Em Olá **pasta ou escolha o arquivo de entrada hello** , clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="36ee4-167">On hello **Choose hello input file or folder** page, click **Next**.</span></span> <span data-ttu-id="36ee4-168">Não selecione **Cópia binária**.</span><span class="sxs-lookup"><span data-stu-id="36ee4-168">Do not select **Binary copy**.</span></span> 
   
    ![Copie a ferramenta - escolha a pasta ou arquivo de entrada hello](./media/data-factory-copy-data-wizard-tutorial/chose-input-file-folder.png) 
7. <span data-ttu-id="36ee4-170">Em Olá **as configurações de formato de arquivo** página, consulte delimitadores hello e esquema de saudação que é detectada automaticamente pelo Assistente de saudação Analisando arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="36ee4-170">On hello **File format settings** page, you see hello delimiters and hello schema that is auto-detected by hello wizard by parsing hello file.</span></span> <span data-ttu-id="36ee4-171">Você também pode inserir delimitadores Olá manualmente para Olá cópia Assistente toostop detectar automaticamente ou toooverride.</span><span class="sxs-lookup"><span data-stu-id="36ee4-171">You can also enter hello delimiters manually for hello copy wizard toostop auto-detecting or toooverride.</span></span> <span data-ttu-id="36ee4-172">Clique em **próximo** Após examinar delimitadores hello e visualizar dados.</span><span class="sxs-lookup"><span data-stu-id="36ee4-172">Click **Next** after you review hello delimiters and preview data.</span></span> 
   
    ![Ferramenta de Cópia - configurações de formato de arquivo](./media/data-factory-copy-data-wizard-tutorial/copy-tool-file-format-settings.png)  
8. <span data-ttu-id="36ee4-174">Em dados de destino de saudação repositório de página, selecione **banco de dados do SQL Azure**e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="36ee4-174">On hello Destination data store page, select **Azure SQL Database**, and click **Next**.</span></span>
   
    ![Ferramenta de Cópia - escolha o repositório de destino](./media/data-factory-copy-data-wizard-tutorial/choose-destination-store.png)
9. <span data-ttu-id="36ee4-176">Em **banco de dados do SQL Azure especifique Olá** página:</span><span class="sxs-lookup"><span data-stu-id="36ee4-176">On **Specify hello Azure SQL database** page:</span></span>
   
   1. <span data-ttu-id="36ee4-177">Digite **AzureSqlLinkedService** para Olá **nome de Conexão** campo.</span><span class="sxs-lookup"><span data-stu-id="36ee4-177">Enter **AzureSqlLinkedService** for hello **Connection name** field.</span></span>
   2. <span data-ttu-id="36ee4-178">Confirme se a opção **De assinaturas do Azure** foi selecionada em **Método de seleção de servidor/banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="36ee4-178">Confirm that **From Azure subscriptions** option is selected for **Server / database selection method**.</span></span>
   3. <span data-ttu-id="36ee4-179">Selecione sua **assinatura**do Azure.</span><span class="sxs-lookup"><span data-stu-id="36ee4-179">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="36ee4-180">Selecione **Nome do servidor** e **Banco de Dados**.</span><span class="sxs-lookup"><span data-stu-id="36ee4-180">Select **Server name** and **Database**.</span></span>
   5. <span data-ttu-id="36ee4-181">Insira o **Nome de usuário** e a **Senha**.</span><span class="sxs-lookup"><span data-stu-id="36ee4-181">Enter **User name** and **Password**.</span></span>
   6. <span data-ttu-id="36ee4-182">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="36ee4-182">Click **Next**.</span></span>  
      
      ![Ferramenta de Cópia - especifique o banco de dados SQL do Azure](./media/data-factory-copy-data-wizard-tutorial/specify-azure-sql-database.png)
10. <span data-ttu-id="36ee4-184">Em Olá **mapeamento de tabela** página, selecione **emp** para Olá **destino** campo da lista suspensa de saudação, clique em **a seta para baixo** (opcional) toosee Olá esquema e toopreview Olá dados.</span><span class="sxs-lookup"><span data-stu-id="36ee4-184">On hello **Table mapping** page, select **emp** for hello **Destination** field from hello drop-down list, click **down arrow** (optional) toosee hello schema and toopreview hello data.</span></span>
    
     ![Ferramenta de Cópia - mapeamento de tabela](./media/data-factory-copy-data-wizard-tutorial/copy-tool-table-mapping-page.png) 
11. <span data-ttu-id="36ee4-186">Em Olá **mapeamento de esquema** , clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="36ee4-186">On hello **Schema mapping** page, click **Next**.</span></span>
    
    ![Ferramenta de Cópia - mapeamento de esquema](./media/data-factory-copy-data-wizard-tutorial/schema-mapping-page.png)
12. <span data-ttu-id="36ee4-188">Em Olá **as configurações de desempenho** , clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="36ee4-188">On hello **Performance settings** page, click **Next**.</span></span> 
    
    ![Ferramenta de cópia - configurações de desempenho](./media/data-factory-copy-data-wizard-tutorial/performance-settings.png)
13. <span data-ttu-id="36ee4-190">Revise informações Olá **resumo** página e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="36ee4-190">Review information in hello **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="36ee4-191">Assistente de saudação cria um pipeline, dois conjuntos de dados (de entrada e saída) e dois serviços vinculados na fábrica de dados de saudação (a partir de onde você iniciou Olá Assistente para copiar).</span><span class="sxs-lookup"><span data-stu-id="36ee4-191">hello wizard creates two linked services, two datasets (input and output), and one pipeline in hello data factory (from where you launched hello Copy Wizard).</span></span> 
    
    ![Ferramenta de cópia - configurações de desempenho](./media/data-factory-copy-data-wizard-tutorial/summary-page.png)

## <a name="launch-monitor-and-manage-application"></a><span data-ttu-id="36ee4-193">Iniciar o monitor e gerenciar aplicativo</span><span class="sxs-lookup"><span data-stu-id="36ee4-193">Launch Monitor and Manage application</span></span>
1. <span data-ttu-id="36ee4-194">Em Olá **implantação** página, clique no link de saudação: `Click here toomonitor copy pipeline`.</span><span class="sxs-lookup"><span data-stu-id="36ee4-194">On hello **Deployment** page, click hello link: `Click here toomonitor copy pipeline`.</span></span>
   
   ![Ferramenta de Cópia - implantação bem-sucedida](./media/data-factory-copy-data-wizard-tutorial/copy-tool-deployment-succeeded.png)  
2. <span data-ttu-id="36ee4-196">saudação de monitoramento do aplicativo é iniciada em uma guia separada em seu navegador da web.</span><span class="sxs-lookup"><span data-stu-id="36ee4-196">hello monitoring application is launched in a separate tab in your web browser.</span></span>   
   
   ![Aplicativo de Monitoramento](./media/data-factory-copy-data-wizard-tutorial/monitoring-app.png)   
3. <span data-ttu-id="36ee4-198">toosee hello mais recente status de fatias de hora em hora, clique em **atualizar** botão Olá **atividade WINDOWS** lista na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="36ee4-198">toosee hello latest status of hourly slices, click **Refresh** button in hello **ACTIVITY WINDOWS** list at hello bottom.</span></span> <span data-ttu-id="36ee4-199">Você vê cinco janelas de atividade de cinco dias entre horários de início e término para o pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="36ee4-199">You see five activity windows for five days between start and end times for hello pipeline.</span></span> <span data-ttu-id="36ee4-200">lista de saudação não será atualizada automaticamente, para que você pode precisar tooclick atualizar algumas vezes antes de ver todas as janelas de atividade de saudação em estado pronto do hello.</span><span class="sxs-lookup"><span data-stu-id="36ee4-200">hello list is not automatically refreshed, so you may need tooclick Refresh a couple of times before you see all hello activity windows in hello Ready state.</span></span> 
4. <span data-ttu-id="36ee4-201">Selecione uma janela de atividade na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="36ee4-201">Select an activity window in hello list.</span></span> <span data-ttu-id="36ee4-202">Consulte os detalhes Olá sobre ele Olá **Pesquisador de objetos de janela de atividade** em saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="36ee4-202">See hello details about it in hello **Activity Window Explorer** on hello right.</span></span>

    ![Detalhes da janela Atividade](media/data-factory-copy-data-wizard-tutorial/activity-window-details.png)    

    <span data-ttu-id="36ee4-204">Observe que as datas de saudação 11, 12, 13, 14 e 15 na cor verde, o que significa que já foram produzidas Olá diário fatias de saída para essas datas.</span><span class="sxs-lookup"><span data-stu-id="36ee4-204">Notice that hello dates 11, 12, 13, 14, and 15 are in green color, which means that hello daily output slices for these dates have already been produced.</span></span> <span data-ttu-id="36ee4-205">Também consulte essa codificação por cores no pipeline hello e Olá conjunto de dados de saída no modo de exibição de diagrama de saudação.</span><span class="sxs-lookup"><span data-stu-id="36ee4-205">You also see this color coding on hello pipeline and hello output dataset in hello diagram view.</span></span> <span data-ttu-id="36ee4-206">Na etapa anterior de Olá, observe que duas fatias já foram produzidas, uma fatia está sendo processada no momento e hello outros dois estão esperando toobe processada (com base em Olá codificação por cores).</span><span class="sxs-lookup"><span data-stu-id="36ee4-206">In hello previous step, notice that two slices have already been produced, one slice is currently being processed, and hello other two are waiting toobe processed (based on hello color coding).</span></span> 

    <span data-ttu-id="36ee4-207">Para saber mais sobre como usar o aplicativo, confira [Monitorar e gerenciar o pipeline usando o aplicativo de monitoramento](data-factory-monitor-manage-app.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="36ee4-207">For more information on using this application, see [Monitor and manage pipeline using Monitoring App](data-factory-monitor-manage-app.md) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36ee4-208">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="36ee4-208">Next steps</span></span>
<span data-ttu-id="36ee4-209">Neste tutorial, você usou o armazenamento de blobs do Azure como um armazenamento de dados de origem e um banco de dados SQL do Azure como um armazenamento de dados de destino em uma operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="36ee4-209">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="36ee4-210">Olá tabela a seguir fornece uma lista de repositórios de dados com suporte como origens e destinos de atividade de cópia de saudação:</span><span class="sxs-lookup"><span data-stu-id="36ee4-210">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="36ee4-211">Para obter detalhes sobre campos/propriedades que você vê no Assistente para cópia de saudação para um repositório de dados, clique o link Olá Olá repositório de dados na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="36ee4-211">For details about fields/properties that you see in hello copy wizard for a data store, click hello link for hello data store in hello table.</span></span> 
