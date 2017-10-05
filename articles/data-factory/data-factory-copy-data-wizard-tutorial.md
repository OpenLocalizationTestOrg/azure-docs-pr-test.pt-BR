---
title: "Tutorial: criar um pipeline usando o Assistente de Cópia | Microsoft Docs"
description: "Neste tutorial, você cria um pipeline do Azure Data Factory com uma Atividade de Cópia usando o Assistente de Cópia com suporte do Data Factory"
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
ms.openlocfilehash: 5922c050cc09236ba5fdec885a70d11da20135cd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-data-factory-copy-wizard"></a><span data-ttu-id="36b7f-103">Tutorial: Criar um pipeline com a Atividade de Cópia usando o Assistente de Cópia do Data Factory</span><span class="sxs-lookup"><span data-stu-id="36b7f-103">Tutorial: Create a pipeline with Copy Activity using Data Factory Copy Wizard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="36b7f-104">Visão geral e pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="36b7f-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="36b7f-105">Assistente de Cópia</span><span class="sxs-lookup"><span data-stu-id="36b7f-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="36b7f-106">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="36b7f-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="36b7f-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="36b7f-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="36b7f-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="36b7f-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="36b7f-109">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="36b7f-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="36b7f-110">API REST</span><span class="sxs-lookup"><span data-stu-id="36b7f-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="36b7f-111">API do .NET</span><span class="sxs-lookup"><span data-stu-id="36b7f-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="36b7f-112">Este tutorial mostra como usar o **assistente de cópia** para copiar dados de um armazenamento de blobs do Azure para um Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="36b7f-112">This tutorial shows you how to use the **Copy Wizard** to copy data from an Azure blob storage to an Azure SQL database.</span></span> 

<span data-ttu-id="36b7f-113">O **assistente de cópia** permite que você crie rapidamente um pipeline de dados que copia dados de um armazenamento de dados de origem com suporte para um armazenamento de dados de destino com suporte.</span><span class="sxs-lookup"><span data-stu-id="36b7f-113">The Azure Data Factory **Copy Wizard** allows you to quickly create a data pipeline that copies data from a supported source data store to a supported destination data store.</span></span> <span data-ttu-id="36b7f-114">Portanto, recomendamos que você use o assistente como uma primeira etapa para criar um pipeline de exemplo no cenário de movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="36b7f-114">Therefore, we recommend that you use the wizard as a first step to create a sample pipeline for your data movement scenario.</span></span> <span data-ttu-id="36b7f-115">Para obter uma lista de armazenamentos de dados com suporte como origens e destinos, consulte [Armazenamentos de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="36b7f-115">For a list of data stores supported as sources and as destinations, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>  

<span data-ttu-id="36b7f-116">Este tutorial mostra como criar um Azure Data Factory, iniciar o Assistente de Cópia, seguir uma série de etapas para fornecer detalhes sobre seu cenário de ingestão/movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="36b7f-116">This tutorial shows you how to create an Azure data factory, launch the Copy Wizard, go through a series of steps to provide details about your data ingestion/movement scenario.</span></span> <span data-ttu-id="36b7f-117">Quando você concluir as etapas no assistente, ele criará um pipeline com Atividade de Cópia a fim de copiar dados de um armazenamento de blobs do Azure para um banco de dados SQL do Azure automaticamente.</span><span class="sxs-lookup"><span data-stu-id="36b7f-117">When you finish steps in the wizard, the wizard automatically creates a pipeline with a Copy Activity to copy data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="36b7f-118">Para saber mais sobre a atividade de cópia, confira [Atividades de movimentação de dados](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="36b7f-118">For more information about Copy Activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36b7f-119">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="36b7f-119">Prerequisites</span></span>
<span data-ttu-id="36b7f-120">Conclua os pré-requisitos listados no artigo [Visão geral do tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) antes de executar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="36b7f-120">Complete prerequisites listed in the [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article before performing this tutorial.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="36b7f-121">Criar um data factory</span><span class="sxs-lookup"><span data-stu-id="36b7f-121">Create data factory</span></span>
<span data-ttu-id="36b7f-122">Nesta etapa, você usa o Portal do Azure para criar um data factory do Azure denominado **ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="36b7f-122">In this step, you use the Azure portal to create an Azure data factory named **ADFTutorialDataFactory**.</span></span>

1. <span data-ttu-id="36b7f-123">Faça logon no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="36b7f-123">Log in to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="36b7f-124">Clique em **+NOVO** no canto superior esquerdo, clique em **Dados + análise** e clique em **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="36b7f-124">Click **+ NEW** from the top-left corner, click **Data + analytics**, and click **Data Factory**.</span></span> 
   
   ![Novo -> DataFactory](./media/data-factory-copy-data-wizard-tutorial/new-data-factory-menu.png)
2. <span data-ttu-id="36b7f-126">Na folha **Nova data factory** :</span><span class="sxs-lookup"><span data-stu-id="36b7f-126">In the **New data factory** blade:</span></span>
   
   1. <span data-ttu-id="36b7f-127">Digite **ADFTutorialDataFactory** como **nome**.</span><span class="sxs-lookup"><span data-stu-id="36b7f-127">Enter **ADFTutorialDataFactory** for the **name**.</span></span>
       <span data-ttu-id="36b7f-128">O nome da data factory do Azure deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="36b7f-128">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="36b7f-129">Se você receber o seguinte erro, `Data factory name “ADFTutorialDataFactory” is not available`, altere o nome do data factory (por exemplo, seunomeADFTutorialDataFactoryDDMMAAAA) e tente criá-lo novamente.</span><span class="sxs-lookup"><span data-stu-id="36b7f-129">If you receive the error: `Data factory name “ADFTutorialDataFactory” is not available`, change the name of the data factory (for example, yournameADFTutorialDataFactoryYYYYMMDD) and try creating again.</span></span> <span data-ttu-id="36b7f-130">Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="36b7f-130">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
      
       ![Nome da data factory indisponível](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-not-available.png)    
   2. <span data-ttu-id="36b7f-132">Selecione sua **assinatura**do Azure.</span><span class="sxs-lookup"><span data-stu-id="36b7f-132">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="36b7f-133">Em relação ao Grupo de Recursos, execute uma das seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="36b7f-133">For Resource Group, do one of the following steps:</span></span> 
      
      - <span data-ttu-id="36b7f-134">Selecione **Usar existente** para selecionar um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="36b7f-134">Select **Use existing** to select an existing resource group.</span></span>
      - <span data-ttu-id="36b7f-135">Selecione **Criar novo** e insira um nome para um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="36b7f-135">Select **Create new** to enter a name for a resource group.</span></span>
          
        <span data-ttu-id="36b7f-136">Algumas das etapas neste tutorial supõem que você usa o nome: **ADFTutorialResourceGroup** para o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="36b7f-136">Some of the steps in this tutorial assume that you use the name: **ADFTutorialResourceGroup** for the resource group.</span></span> <span data-ttu-id="36b7f-137">Para saber mais sobre grupos de recursos, consulte [Usando grupos de recursos para gerenciar recursos do Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="36b7f-137">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>
   4. <span data-ttu-id="36b7f-138">Selecione um **local** para o data factory.</span><span class="sxs-lookup"><span data-stu-id="36b7f-138">Select a **location** for the data factory.</span></span>
   5. <span data-ttu-id="36b7f-139">Marque a caixa de seleção **Fixar no painel** na parte inferior da folha.</span><span class="sxs-lookup"><span data-stu-id="36b7f-139">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>  
   6. <span data-ttu-id="36b7f-140">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="36b7f-140">Click **Create**.</span></span>
      
       ![Folha Nova data factory](media/data-factory-copy-data-wizard-tutorial/new-data-factory-blade.png)            
3. <span data-ttu-id="36b7f-142">Depois que a criação for concluída, você verá a folha **Data Factory**, conforme mostrado na seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="36b7f-142">After the creation is complete, you see the **Data Factory** blade as shown in the following image:</span></span>
   
   ![Página inicial da data factory](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-home-page.png)

## <a name="launch-copy-wizard"></a><span data-ttu-id="36b7f-144">Iniciar o Assistente de cópia</span><span class="sxs-lookup"><span data-stu-id="36b7f-144">Launch Copy Wizard</span></span>
1. <span data-ttu-id="36b7f-145">Na folha Data Factory, clique em **Copiar dados [VERSÃO PRÉVIA]** para iniciar o **Assistente de cópia**.</span><span class="sxs-lookup"><span data-stu-id="36b7f-145">On the Data Factory blade, click **Copy data [PREVIEW]** to launch the **Copy Wizard**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="36b7f-146">Se você vir que o navegador da Web está bloqueado em "Autorizando...", desmarque a configuração **Bloquear cookies de terceiros e dados de site** nas configurações do navegador (ou) mantenha-a habilitada, crie uma exceção para **login.microsoftonline.com** e tente iniciar o assistente novamente.</span><span class="sxs-lookup"><span data-stu-id="36b7f-146">If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting in the browser settings (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.</span></span>
2. <span data-ttu-id="36b7f-147">Na página **Propriedades** :</span><span class="sxs-lookup"><span data-stu-id="36b7f-147">In the **Properties** page:</span></span>
   
   1. <span data-ttu-id="36b7f-148">Insira **CopyFromBlobToAzureSql** para o **Nome da tarefa**</span><span class="sxs-lookup"><span data-stu-id="36b7f-148">Enter **CopyFromBlobToAzureSql** for **Task name**</span></span>
   2. <span data-ttu-id="36b7f-149">Insira uma **descrição** (opcional).</span><span class="sxs-lookup"><span data-stu-id="36b7f-149">Enter **description** (optional).</span></span>
   3. <span data-ttu-id="36b7f-150">Altere a **data/hora de início** e a **data/hora de término** para que a data de término seja definida como a data de hoje e a de início, cinco dias antes.</span><span class="sxs-lookup"><span data-stu-id="36b7f-150">Change the **Start date time** and the **End date time** so that the end date is set to today and start date to five days earlier.</span></span>  
   4. <span data-ttu-id="36b7f-151">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="36b7f-151">Click **Next**.</span></span>  
      
      ![Ferramenta de Cópia - página Propriedades](./media/data-factory-copy-data-wizard-tutorial/copy-tool-properties-page.png) 
3. <span data-ttu-id="36b7f-153">Na página **Repositório de dados de origem**, clique no bloco **Armazenamento de Blobs do Azure**.</span><span class="sxs-lookup"><span data-stu-id="36b7f-153">On the **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="36b7f-154">Use essa página para especificar o repositório de dados de origem para a tarefa de cópia.</span><span class="sxs-lookup"><span data-stu-id="36b7f-154">You use this page to specify the source data store for the copy task.</span></span> 
   
    ![Ferramenta de Cópia - página de repositório de dados de origem](./media/data-factory-copy-data-wizard-tutorial/copy-tool-source-data-store-page.png)
4. <span data-ttu-id="36b7f-156">Na página **Especificar a conta de armazenamento de Blobs do Azure** :</span><span class="sxs-lookup"><span data-stu-id="36b7f-156">On the **Specify the Azure Blob storage account** page:</span></span>
   
   1. <span data-ttu-id="36b7f-157">Insira **AzureStorageLinkedService** para o **Nome do serviço vinculado**.</span><span class="sxs-lookup"><span data-stu-id="36b7f-157">Enter **AzureStorageLinkedService** for **Linked service name**.</span></span>
   2. <span data-ttu-id="36b7f-158">Confirme se a opção **De assinaturas do Azure** foi selecionada em **Método de seleção de conta**.</span><span class="sxs-lookup"><span data-stu-id="36b7f-158">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="36b7f-159">Selecione sua **assinatura**do Azure.</span><span class="sxs-lookup"><span data-stu-id="36b7f-159">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="36b7f-160">Selecione uma **Conta de armazenamento do Azure** na lista de contas de armazenamento do Azure disponíveis na assinatura selecionada.</span><span class="sxs-lookup"><span data-stu-id="36b7f-160">Select an **Azure storage account** from the list of Azure storage accounts available in the selected subscription.</span></span> <span data-ttu-id="36b7f-161">Você também pode inserir as configurações de conta de armazenamento manualmente selecionando a opção **Inserir manualmente** para o **Método de seleção de conta** e clicando em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="36b7f-161">You can also choose to enter storage account settings manually by selecting **Enter manually** option for the **Account selection method**, and then click **Next**.</span></span> 
      
      ![Ferramenta de Cópia - especifique a conta de armazenamento de Blobs do Azure](./media/data-factory-copy-data-wizard-tutorial/copy-tool-specify-azure-blob-storage-account.png)
5. <span data-ttu-id="36b7f-163">Na página **Escolher o arquivo de entrada ou a pasta** :</span><span class="sxs-lookup"><span data-stu-id="36b7f-163">On **Choose the input file or folder** page:</span></span>
   
   1. <span data-ttu-id="36b7f-164">Clique duas vezes em **adftutorial** (pasta).</span><span class="sxs-lookup"><span data-stu-id="36b7f-164">Double-click **adftutorial** (folder).</span></span>
   2. <span data-ttu-id="36b7f-165">Selecione **emp.txt** e clique em **Escolher**</span><span class="sxs-lookup"><span data-stu-id="36b7f-165">Select **emp.txt**, and click **Choose**</span></span>
      
      ![Ferramenta de Cópia - escolha a pasta ou o arquivo de entrada](./media/data-factory-copy-data-wizard-tutorial/copy-tool-choose-input-file-or-folder.png)
6. <span data-ttu-id="36b7f-167">Na página **Escolha o arquivo ou a pasta de entrada**, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="36b7f-167">On the **Choose the input file or folder** page, click **Next**.</span></span> <span data-ttu-id="36b7f-168">Não selecione **Cópia binária**.</span><span class="sxs-lookup"><span data-stu-id="36b7f-168">Do not select **Binary copy**.</span></span> 
   
    ![Ferramenta de Cópia - escolha a pasta ou o arquivo de entrada](./media/data-factory-copy-data-wizard-tutorial/chose-input-file-folder.png) 
7. <span data-ttu-id="36b7f-170">Na página **Configurações de formato de arquivo**, você vê os delimitadores e o esquema é detectado automaticamente pelo assistente na análise do arquivo.</span><span class="sxs-lookup"><span data-stu-id="36b7f-170">On the **File format settings** page, you see the delimiters and the schema that is auto-detected by the wizard by parsing the file.</span></span> <span data-ttu-id="36b7f-171">Você também pode inserir os delimitadores manualmente para que o assistente de cópia pare de detectar automaticamente ou substitua.</span><span class="sxs-lookup"><span data-stu-id="36b7f-171">You can also enter the delimiters manually for the copy wizard to stop auto-detecting or to override.</span></span> <span data-ttu-id="36b7f-172">Clique em **Avançar** depois de revisar os delimitadores e visualizar os dados.</span><span class="sxs-lookup"><span data-stu-id="36b7f-172">Click **Next** after you review the delimiters and preview data.</span></span> 
   
    ![Ferramenta de Cópia - configurações de formato de arquivo](./media/data-factory-copy-data-wizard-tutorial/copy-tool-file-format-settings.png)  
8. <span data-ttu-id="36b7f-174">Na página Repositório de dados de destino, selecione **Banco de Dados SQL do Azure** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="36b7f-174">On the Destination data store page, select **Azure SQL Database**, and click **Next**.</span></span>
   
    ![Ferramenta de Cópia - escolha o repositório de destino](./media/data-factory-copy-data-wizard-tutorial/choose-destination-store.png)
9. <span data-ttu-id="36b7f-176">Na página **Especificar o banco de dados SQL do Azure** :</span><span class="sxs-lookup"><span data-stu-id="36b7f-176">On **Specify the Azure SQL database** page:</span></span>
   
   1. <span data-ttu-id="36b7f-177">Digite **AzureSqlLinkedService** no campo **Nome da conexão**.</span><span class="sxs-lookup"><span data-stu-id="36b7f-177">Enter **AzureSqlLinkedService** for the **Connection name** field.</span></span>
   2. <span data-ttu-id="36b7f-178">Confirme se a opção **De assinaturas do Azure** foi selecionada em **Método de seleção de servidor/banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="36b7f-178">Confirm that **From Azure subscriptions** option is selected for **Server / database selection method**.</span></span>
   3. <span data-ttu-id="36b7f-179">Selecione sua **assinatura**do Azure.</span><span class="sxs-lookup"><span data-stu-id="36b7f-179">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="36b7f-180">Selecione **Nome do servidor** e **Banco de Dados**.</span><span class="sxs-lookup"><span data-stu-id="36b7f-180">Select **Server name** and **Database**.</span></span>
   5. <span data-ttu-id="36b7f-181">Insira o **Nome de usuário** e a **Senha**.</span><span class="sxs-lookup"><span data-stu-id="36b7f-181">Enter **User name** and **Password**.</span></span>
   6. <span data-ttu-id="36b7f-182">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="36b7f-182">Click **Next**.</span></span>  
      
      ![Ferramenta de Cópia - especifique o banco de dados SQL do Azure](./media/data-factory-copy-data-wizard-tutorial/specify-azure-sql-database.png)
10. <span data-ttu-id="36b7f-184">Na página **Mapeamento de tabela**, selecione **emp** para o campo **Destino** na lista suspensa e clique em **seta para baixo** (opcional) para ver o esquema e visualizar os dados.</span><span class="sxs-lookup"><span data-stu-id="36b7f-184">On the **Table mapping** page, select **emp** for the **Destination** field from the drop-down list, click **down arrow** (optional) to see the schema and to preview the data.</span></span>
    
     ![Ferramenta de Cópia - mapeamento de tabela](./media/data-factory-copy-data-wizard-tutorial/copy-tool-table-mapping-page.png) 
11. <span data-ttu-id="36b7f-186">Na página **Mapeamento de esquema**, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="36b7f-186">On the **Schema mapping** page, click **Next**.</span></span>
    
    ![Ferramenta de Cópia - mapeamento de esquema](./media/data-factory-copy-data-wizard-tutorial/schema-mapping-page.png)
12. <span data-ttu-id="36b7f-188">Na página **Configurações de desempenho**, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="36b7f-188">On the **Performance settings** page, click **Next**.</span></span> 
    
    ![Ferramenta de cópia - configurações de desempenho](./media/data-factory-copy-data-wizard-tutorial/performance-settings.png)
13. <span data-ttu-id="36b7f-190">Examine as informações na página **Resumo** e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="36b7f-190">Review information in the **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="36b7f-191">Esse assistente cria dois serviços vinculados, dois conjuntos de dados (entrada e saída) e um pipeline no data factory (de onde você iniciou o Assistente de Cópia).</span><span class="sxs-lookup"><span data-stu-id="36b7f-191">The wizard creates two linked services, two datasets (input and output), and one pipeline in the data factory (from where you launched the Copy Wizard).</span></span> 
    
    ![Ferramenta de cópia - configurações de desempenho](./media/data-factory-copy-data-wizard-tutorial/summary-page.png)

## <a name="launch-monitor-and-manage-application"></a><span data-ttu-id="36b7f-193">Iniciar o monitor e gerenciar aplicativo</span><span class="sxs-lookup"><span data-stu-id="36b7f-193">Launch Monitor and Manage application</span></span>
1. <span data-ttu-id="36b7f-194">Na página **Implantação**, clique no link: `Click here to monitor copy pipeline`.</span><span class="sxs-lookup"><span data-stu-id="36b7f-194">On the **Deployment** page, click the link: `Click here to monitor copy pipeline`.</span></span>
   
   ![Ferramenta de Cópia - implantação bem-sucedida](./media/data-factory-copy-data-wizard-tutorial/copy-tool-deployment-succeeded.png)  
2. <span data-ttu-id="36b7f-196">O aplicativo de monitoramento é iniciado em uma guia separada no navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="36b7f-196">The monitoring application is launched in a separate tab in your web browser.</span></span>   
   
   ![Aplicativo de Monitoramento](./media/data-factory-copy-data-wizard-tutorial/monitoring-app.png)   
3. <span data-ttu-id="36b7f-198">Para ver o status mais recente das fatias de cada hora, clique no botão **Atualizar** da lista **JANELAS DE ATIVIDADE** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="36b7f-198">To see the latest status of hourly slices, click **Refresh** button in the **ACTIVITY WINDOWS** list at the bottom.</span></span> <span data-ttu-id="36b7f-199">Você vê cinco janelas de atividade para cinco dias entre as horas de início e de término do pipeline.</span><span class="sxs-lookup"><span data-stu-id="36b7f-199">You see five activity windows for five days between start and end times for the pipeline.</span></span> <span data-ttu-id="36b7f-200">A lista não é atualizada automaticamente e, portanto, talvez seja necessário clicar em Atualizar algumas vezes para poder ver todas as janelas de atividade com status Pronto.</span><span class="sxs-lookup"><span data-stu-id="36b7f-200">The list is not automatically refreshed, so you may need to click Refresh a couple of times before you see all the activity windows in the Ready state.</span></span> 
4. <span data-ttu-id="36b7f-201">Selecione uma janela de atividade na lista.</span><span class="sxs-lookup"><span data-stu-id="36b7f-201">Select an activity window in the list.</span></span> <span data-ttu-id="36b7f-202">Consulte os detalhes sobre ela no **Gerenciador da janela de atividade** à direita.</span><span class="sxs-lookup"><span data-stu-id="36b7f-202">See the details about it in the **Activity Window Explorer** on the right.</span></span>

    ![Detalhes da janela Atividade](media/data-factory-copy-data-wizard-tutorial/activity-window-details.png)    

    <span data-ttu-id="36b7f-204">Observe que as datas 11, 12, 13, 14 e 15 estão na cor verde, que significa que as fatias de saída diária para essas datas já foram produzidas.</span><span class="sxs-lookup"><span data-stu-id="36b7f-204">Notice that the dates 11, 12, 13, 14, and 15 are in green color, which means that the daily output slices for these dates have already been produced.</span></span> <span data-ttu-id="36b7f-205">Você também verá essa codificação de cor no pipeline e o conjunto de dados de saída na exibição de diagrama.</span><span class="sxs-lookup"><span data-stu-id="36b7f-205">You also see this color coding on the pipeline and the output dataset in the diagram view.</span></span> <span data-ttu-id="36b7f-206">Na etapa anterior, observe que duas fatias já foram produzidas, uma está sendo processada e os outras duas estão aguardando processamento (com base na codificação de cores).</span><span class="sxs-lookup"><span data-stu-id="36b7f-206">In the previous step, notice that two slices have already been produced, one slice is currently being processed, and the other two are waiting to be processed (based on the color coding).</span></span> 

    <span data-ttu-id="36b7f-207">Para saber mais sobre como usar o aplicativo, confira [Monitorar e gerenciar o pipeline usando o aplicativo de monitoramento](data-factory-monitor-manage-app.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="36b7f-207">For more information on using this application, see [Monitor and manage pipeline using Monitoring App](data-factory-monitor-manage-app.md) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36b7f-208">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="36b7f-208">Next steps</span></span>
<span data-ttu-id="36b7f-209">Neste tutorial, você usou o armazenamento de blobs do Azure como um armazenamento de dados de origem e um banco de dados SQL do Azure como um armazenamento de dados de destino em uma operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="36b7f-209">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="36b7f-210">A tabela a seguir fornece uma lista de armazenamentos de dados com suporte como origens ou destinos na atividade de cópia:</span><span class="sxs-lookup"><span data-stu-id="36b7f-210">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="36b7f-211">Para obter detalhes sobre campos/propriedades que você vê no assistente de cópia de um armazenamento de dados, clique no link para o armazenamento de dados na tabela.</span><span class="sxs-lookup"><span data-stu-id="36b7f-211">For details about fields/properties that you see in the copy wizard for a data store, click the link for the data store in the table.</span></span> 